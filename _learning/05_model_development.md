---
layout: distill
title: Model Development and Evaluation
toc:
    - name: Model Development
      subsections:
        - name: Simple dan Multiple Linear Regression
        - name: R-Squared dan MSE untuk In-Sample Evaluation
        - name: Model Evaluation dengan Visualisasi
        - name: Prediction dan Decision Making
    - name: Model Evaluation
---

# Model Development

Kita telah menentukan variabel mana yang bagus mana yang jelek. Kita juga sudah membersihkan data sehingga akhirnya siap untuk digunakan dalam pengembangan model. Sekarang saatnya kita memprediksi harga mobil berdasarkan data yang ada.

Buka hands-on di [github](https://github.com/dssc-unmul/data-analysis/blob/main/Model-Development.ipynb) atau langsung buka di colab [![Buka di Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/dssc-unmul/data-analysis/blob/main/Model-Development.ipynb)

## Simple dan Multiple Linear Regression

- (Simple) Linear regression mengacu pada satu variabel independen untuk membuat prediksi
- Multiple linear regression mengacu pada __lebih dari satu__ variabel independen untuk membuat prediksi

### Simple Linear Regression

Ini hanya untuk dua variabel saja, satu prediktor satu target.

$$Y=a+bX$$

Dimana:

- $$a$$: intersep (nilai ketika x=0)
- $$b$$: slope (kemiringan garis/gradien)

#### Prediction

Anggaplah `highway-mpg` punya relasi linear dengan `price`.

![](/assets/img/prediction.png)

Jika `highway`-nya 20 maka pricenya sekian.

#### Fitting

Nah untuk membuat garisnya. Diambil titik data untuk di latih (_fit_).

![](/assets/img/fit.png)

Hasil dari fitting adalah parameter $$(a,b)$$.

Titik data disimpan dalam numpy array. Array `y` untuk target, array `x` untuk predictor.

Banyak faktor yang dapat mempengaruhi prediksi. Ketidakpastian ini disertakan dengan mengasumsikan nilai acak kecil ditambahkan pada titik data di garis regresi. Inilah yang disebut _noise_.

![](/assets/img/distribution-of-noise.png)

Gambar di atas adalah distribusi noisenya

- Sumbu vertikal menunjukkan value yang ditambahkan
- Sumbu horizontal mengilustrasikan kemungkinan value tersebut akan ditambahkan

#### Wrap Up

- Kita punya training point (titik data untuk dilatih)
- Kemudian di train
- Menghasilkan parameter $$(a,b)$$
- Gunakan parameternya untuk model $$\hat{Y}=a+bX$$

Jika masih penasaran dengan cara kerja linear regression, video dibawah mungkin bisa membantu

<iframe width="560" height="315" src="https://www.youtube.com/embed/nk2CQITm_eo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

#### Fitting a Simple Linear Model Estimator

```python
from sklearn.linear_model import LinearRegression
```

Kemudian bikin objek

```python
lm = LinearRegression
```

Tentukan variabel prediktor dan target nya

```python
X = df[['highway-mpg']]
Y = df['price']
```

Kemudian _fit the model_
```python
lm.fit(X,Y)
```

Sekarang kita bisa memperoleh prediksi
```python
Yhat = lm.predict(new_predictor)
```

$$a$$ dan $$b$$ dapat diakses sebagai atribut.

### Multiple Linear Regression

```python
Z = df[['horsepower', 'curb-weight', 'engine-size', 'highway-mpg']]
lm.fit(Z, df['price'])

Yhat = lm.predict(new_predictor)
```

## Model Evaluation dengan Visualisasi

### Regression Plot

Kenapa pakai regression plot?. Karena bisa memberi estimasi yang bagus pada:
- Relasi antara dua variabel
- Tingkat korelasi
- Arah relasi (positif atau negatif)

Regression plot dapat menampilkan kombinasi dari scatter plot dan garis regresi linear yang sudah dilatih. Garis regresi linear merepresentasikan nilai yang diprediksi.

Cara menggunakannya

```python
import seaborn as sns
sns.regplot(x="highway-mpg", y="price", data=df)
```

![](/assets/img/2022-08-03-23-59-21.png)

### Residual Plot

Residual plot merepresentasikan error antara nilai aktualnya.

Kurangkan nilai actualnya dengan nilai predicted-nya sehingga dapat nilai error. Kemudian plot kembali hasilnya.

![](/assets/img/how-residual-plot-work.png)

Hasil yang diinginkan adalah plot nya (titik-titiknya) tersebar secara random disekitar sumbu x.

![](/assets/img/good-residual-plot.png)

Ini berarti linear modelnya bagus.

![](/assets/img/residual-plot-curvature.png)

Disini plotnya membentuk kurva, tidak tersebar secara random. Mungkin lebih baik menggunakan nonlinear model.

![](/assets/img/residual-plot-increasing-variance.png)

Disini variance dari residualnya meningkat dengan x. Maka model nya salah

```python
import seaborn as sns

sns.residplot(df['highway-mpg'], df['price'])
```

### Distribution plot

Distribution plot menghitung nilai actual versus nilai predicted.

```python
import seaborn as sns

ax1 = sns.distplot(df['price'], hist=False, color="r", label='Actual value')
sns.distplot(Yhat, hist=False, color='b', label='Fitted Values', ax=ax1)
```
![](/assets/img/distribution-plot.png)

## Polynomial Regression dan Pipelines

### Polynomial regression

Bagaimana jika linear regression bukan model yang tepat. Kita ubah data kita menjadi [polinomial](https://id.wikipedia.org/wiki/Polinomial) (suku banyak) kemudian gunakan linear regression untuk melatih parameter

<a title="Gisling, CC BY-SA 4.0 &lt;https://creativecommons.org/licenses/by-sa/4.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:Chebyshev_polynomial.gif"><img width="300" alt="Chebyshev polynomial" src="https://upload.wikimedia.org/wikipedia/commons/5/56/Chebyshev_polynomial.gif"></a>

Polynomial regression berguna untuk relasi yang berbentuk kurva (_curvilinier relationship_). Curvilinier relationship didapat dari mengkuadratkan atau menetapkan derajat suku tinggi ke variabel prediktor. Berarti harus transforming data.

Walaupun variabel prediktor dari Polynomial Regression tidak linear, hubungan antara parameter atau koefisien nya tetap linear.

#### Macam-macam polynomial regression

- Quadratic - derajat 2
  - $$\hat{Y}=b_0+b_1x_1+b_2(x_1)^2$$

    <a title="Original hand-drawn version: N.MoriUpdated hand-drawn version: Rubber Duck (☮ • ✍), Public domain, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:Polynomialdeg2.svg"><img width="256" alt="Polynomialdeg2" src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/f8/Polynomialdeg2.svg/256px-Polynomialdeg2.svg.png"></a>

- Cubic - derajat 3
  - $$\hat{Y}=b_0+b_1x_1+b_2(x_1)^2+b_3(x_1)^3$$

    <a title="N.Mori, Public domain, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:Polynomialdeg3.svg"><img width="256" alt="Polynomialdeg3" src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a3/Polynomialdeg3.svg/256px-Polynomialdeg3.svg.png"></a>

- Derajat tinggi
  - $$\hat{Y}=b_0+b_1x_1+b_2(x_1)^2+b_3(x_1)^3+...$$

    <a title="Geek3, CC BY-SA 3.0 &lt;https://creativecommons.org/licenses/by-sa/3.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:Polynomialdeg5.svg"><img width="256" alt="Polynomialdeg5" src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/55/Polynomialdeg5.svg/128px-Polynomialdeg5.svg.png"></a>

#### Implementasi di Python

Menghitung polynomial derajat 3

```python
f = np.polyfit(x,y,3)
p = np.polyfit(f)
```

$$-1.557(x_1)^3+204.8(x_1)^+8965x_1+1.37\times{10^5}$$

Dimensi banyak

$$\hat{Y} = b_0 + b_1 X_1 + b_2 X_2 + b_3 X_1 X_2 + b_4 (X_1)^2 + b_5(X_2)^2 + \dots$$

```python
from sklearn.preprocessing import PolynomialFeatures

pr = PolynomialFeatures(degree=2, include_bias=False)

x_polly = pr.fit_transform(x[['horsepower', 'curb-weight']])
```

#### Pre-processing

Semakin besar dimensinya (variabel yang digunakan), kita mungkin mau menormalisasikan fitur-fitur (variabel) nya sekaligus.

```python
from sklearn.preprocessing import StandardScaler

scale = StandardScaler()
scale.fit(x_data[['horsepower', 'highway-mpg']])

x_scale = scale.transform(x_data[['horsepower', 'highway-mpg']])
```

### Pipeline

Pipeline digunakan untuk menyederhanakan proses

```python
from sklearn.preprocessing import PolynomialFeatures, StandardScaler
from sklearn.linear_model import LinearRegression
from sklearn.pipeline import Pipeline

# buat list of tuple
# elemen pertama adalah namanya
# elemen kedua adalah constructornya
input = [('scale', StandardScaler()), ('polynomial', PolynomialFeatures(degree=2)), ..., ('model', LinearRegression())]

#pipline constructor
pipe = Pipeline(input)

# we can train the pipeline object
pipe.train(x[['horsepower', 'highway-mpg', 'curb-weight', 'engine-size']], y)
yhat = pipe.predict(X[['horsepower', 'highway-mpg', 'curb-weight', 'engine-size']])
```

Metode ini menormalisasi data, transformasi polinomial, dan menghasilkan prediksi.

## R-Squared dan MSE untuk In-Sample Evaluation

Pengukuran ini adalah salah satu cara untuk mengukur secara numerik seberapa bagus modelnya untuk dataset. Ada dua metrik pengukur penting:

- [Mean Squared Error (MSE)](https://id.wikipedia.org/wiki/Rata-rata_kuadrat_galat)
- [R-Squared](https://en.wikipedia.org/wiki/Coefficient_of_determination)

### Mean Squared Error (MSE)

Langkahnya:

1. Selisihkan nilai asli dan predicted nya
2. Pangkatkan 2
3. Tambahkan dengan nilai-nilai yang lain
4. Bagi sejumlah banyak nilai-nilainya

```python
from sklearn.metrics import mean_squared_error

mean_squared_error(df['price'], Y_predict_simple_fit)
```

### R-Squared

Disebut juga _Coefficient of Determination_ adalah pengukuran untuk menentukan seberapa dekat data dengan garis regresi.

$$R^2=1-\frac{MSE\ of\ regression\ line}{MSE\ of\ the\ average\ of\ the\ data}$$

1 artinya bagus, 0 jelek

![](/assets/img/r_squared_graphs.png)

- Garis biru merepresentasikan garis regresi
- Kotak biru menunjukkan MSE dari garis regresi
- garis merah menunjukkan rata-rata nilai dari titik data
- Kotak merah menunjukkan MSE dari garis merah
- Bisa dilihat kotak biru lebih kecil daripada kotak merah

R-Squared di python dapat diakses dari atribut `score` model object setelah di `fit`

## Prediction dan Decision Making

### Prediction

Prediksi bisa dilakukan dengan memasukkan nilai X yang mau diprediksi ke dalam method `predict`

```python
yhat=lm.predict(new_input)
```

### Menentukan Model yang Bagus

Supaya tau model ini adalah best fit, lihat:

- Nilai yang diprediksi makes sense, misalnya nilai nya tidak negatif
- [Visualisasinya](#model-evaluation-dengan-visualisasi)
- [Pengukuran numerik untuk evaluasi](#r-squared-dan-mse-untuk-in-sample-evaluation)
- Membandingkan antara model yang berbeda
  - Apakah [MSE](#mean-squared-error-mse) yang lebih rendah selalu mengindikasikan model lebih baik? Belum tentu
  - MSE untuk model [Multiple Linear Regression](#multiple-linear-regression) akan selalu lebih kecil daripada MSE untuk [Simple Linear Regression](#simple-linear-regression). Karena error pada data akan berkurang ketika lebih banyak variabel yang dimasukkan ke dalam model
  - [Polynomial Regression](#polynomial-regression) juga akan punya MSE yang rendah daripada linear regression biasa
  - Hubungan kebalikannya yang serupa juga berlaku untuk R-Squared

<<<<<<< HEAD
# Model Evaluation
=======
# Model Evaluation and Refinement
>>>>>>> 25c98ef (Model development and evaluation material)

Evaluasi model dibutuhkan untuk mengukur akurasi. Akurasi model dapat ditingkatkan dengan banyak metode.

Buka hands-on model evaluation di [github](https://github.com/dssc-unmul/data-analysis/blob/main/Model-Evaluation.ipynb) atau langsung buka di colab [![Buka di Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/dssc-unmul/data-analysis/blob/main/Model-Evaluation.ipynb)