---
layout: page
title: Data Wrangling
---
Data wrangling, biasa juga disebut data cleaning, data preprocessing, dll. Semua jatuh pada maksud yang sama yaitu proses transformasi dan mapping data dari satu format ke format lain. Tujuannya adalah untuk membuat format data lebih mudah digunakan untuk hal-hal seperti analisis bisnis atau machine learning.

Mari mulai dengan import library yang dibutuhkan yaitu `matplotlib.pyplot` dan `pandas`.

```python
import pandas as pd
import matplotlib.pyplot as plt
```

Kemudian muat data dari URL berikut: https://archive.ics.uci.edu/ml/machine-learning-databases/autos/imports-85.data . Tidak perlu bingung, file data ini jika dibuka dengan teks editor akan berformat seperti file csv, jadi kita bisa menggunakan fungsi `read_csv` dari pandas.

Perlu diperhatikan data ini tidak memiliki _header_ atau nama kolom sehingga pandas akan membuat baris pertama pada data sebagai headernya secara default. Karena itu kita membutuhkan nama header yang sesuai dengan kolom-kolomnya. Nama-nama kolom ini bisa kita dapatkan dari sumber yang sama yaitu di https://archive.ics.uci.edu/ml/machine-learning-databases/autos/imports-85.names.

```python
filename = "https://archive.ics.uci.edu/ml/machine-learning-databases/autos/imports-85.data"
headers = ["symboling","normalized-losses","make","fuel-type","aspiration", "num-of-doors","body-style",
         "drive-wheels","engine-location","wheel-base", "length","width","height","curb-weight","engine-type",
         "num-of-cylinders", "engine-size","fuel-system","bore","stroke","compression-ratio","horsepower",
         "peak-rpm","city-mpg","highway-mpg","price"]
```

Maka untuk memuat datanya gunakan fungsi `read_csv` dengan argumen pertama file datanya dan argumen berikutnya tambahkan `names` bernilai list nama header yang sudah kita buat kemudian masukkan ke dalam variabel. Variabel ini yang selanjutnya akan kita gunakan untuk mengakses data hingga akhir notebook.

```python
df = pd.read_csv(filename, names=headers)
```

Berikut langkah-langkah untuk melakukan proses data wrangling.

## Missing Value

### Bagaimana cara mengatasi missing value

- Cek lagi sumbernya
- Hapus (_drop_) missing valuenya dengan impact paling minimum
         - Hapus kolomnya
         - Hapus baris data nya, datanya memang banyak
- Ganti missing value
         - Ganti dengan rata-rata
         - Ganti dengan modus (yang paling banyak), untuk data non-numerik
         - Ganti menggunakan fungsi custom. Biasanya kalau udah tau apa yang harus masuk ke situ
         - Tinggalkan aja sebagai missing data

### Gimana cara menghapus missing value

Gunakan `df.dropna()`. Tambahkan parameter `axis=0` untuk menghapus baris (default), `axis=1` untuk menghapus kolom.

```python
df.dropna(subset=["price"], axis=0, inplace=True)
```

Nilai pada parameter `subset` adalah untuk kolom yang punya missing value, `inplace=True` untuk membuat perubahan langsung di dataframenya.

Kode diatas sama dengan

```python
df = df.dropna(subset=["price"], axis=0)
```

### Cara mengganti missing value

Gunakan `df.replace(missing_value, new_value)`

```python
mean = df["normalized-losses"].mean()

df["normalized-losses"].replace(np.nan, mean)
```

## Data Formatting

Data formatting adalah mengubah data menjadi <mark>standar umum</mark> sehingga kita bisa membuat perbandingan yang bermakna.

### Mengaplikasikan perhitungan ke kolom

Misalnya mau mengubah "mpg" (_miles per galon_) ke "L/100km"

```python
df["city-mpg"]=235/df["city-mpg"]
```
kemudian ganti nama kolomnya

```python
df.rename(columns={"city-mpg": "city-L/100km"}, inplace=True)
```

### Tipe data yang salah

Untuk mengubah tipe data yang salah, convert dengan `df.astype()`

contoh:

```python
df["price"] = df["price"].astype("int")
```

## Data Normalization

Kenapa data harus dinormalisasi. Kalau misalnya mau dilakukan regresi linier, fitur dengan nilai yang tinggi bakal dapat influence yang lebih tinggi padahal seharusnya tidak.

Bayangkan ada kolom pada data punya range yang berbeda, misal `umur` yang mana range nya sekitar 17-65 dan `pendapatan` dengan range 500000-12000000, kemudian dua kolom ini akan dijadikan variabel prediktor untuk model prediksi misal regresi linear, fitur/kolom/variabel `pendapatan` bakal punya pengaruh yang lebih tinggi karena nilai jauh lebih tinggi dari umur padahal seharusnya tidak demikian dan akhirnya akurasi model menurun. Makanya perlu dilakukan normalisasi terlebih dahulu. 

### Metode Normalisasi Data

1. Simple feature scaling

   $$x_{new} = \frac{x_{old}}{x_{max}}$$

2. Min-Max

   $$x_{new} = \frac{x_{old} - x_{min}}{x_{max} - x_{min}}$$

3. Z-score

   $$x_{new} = \frac{x_{old} - \mu}{\sigma}$$

## Binning

Binning adalah membuat group value kedalam bin. Misalnya mem-bin "age" ke 0-5, 6-10, 11-15,...

Biasanya binning digunakan untuk mengelompokkan beberapa nilai numerik ke dalam bin dengan nilai yang lebih sedikit supaya dapat memahami distribusi data lebih baik.

Dalam dataset, jika ingin mengelompokkan price menjadi low, medium high, gunakan

```python
bins = np.linspace(min(df["price"]), max(df["price"]), 4)
```
- untuk membagi nilai menjadi 3 kategori kita butuh 4 angka
- 4 angka dengan jarak yang *equally distributed*. Gunakan `np.linspace`.
- dimulai dari nilai paling rendah `min(df["price"])` ke nilai paling tinggi `max(df["price"])`

kemudian buat nama kategorinya

```python
group_names = ["low", "medium", "high"]
```
lalu gunakan function `pd.cut()`

```python
df["price-binned"] = pd.cut(df["price"], bins, labels=group_names, include_lowest=True)
```

Kemudian hasil bin ini bisa divisualisasikan dengan histogram.

## Mengubah variabel kategorik menjadi variabel kuantitatif

Statistical model (mis. regresi linear) biasanya tidak bisa menggunakan string/object sebagai inputnya.

Jadi solusinya adalah mengubahnya menjadi 0 dan 1. Teknik ini biasa disebut [One-Hot Encoding](https://www.educative.io/blog/one-hot-encoding):

- bikin dummy variables untuk setiap kategori
- masukkan 0 atau 1 dalam setiap kategori
         - masukkan 1 untuk setiap kategori yang dijadikan dummy yang sesuai

### Dummy variables di pandas

Gunakan function `pd.get_dummies()`

```python
pd.get_dummies(df["fuel"])
```
Akan menghasilkan dummy variabel dengan nilai 0 dan 1 yang bersesuaian dengan kolom fuel.

# Hands-on Lab

Sekarang coba praktikan dengan akses notebook hands-on di [github](https://github.com/dssc-unmul/data-analysis/blob/main/Data-Wrangling.ipynb) atau buka di google colab [![Buka di Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/dssc-unmul/data-analysis/blob/main/Data-Wrangling.ipynb)

# Sumber

- [IBM Coursera Data Analysis with Python](https://www.coursera.org/learn/data-analysis-with-python)
