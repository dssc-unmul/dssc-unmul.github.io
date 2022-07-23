---
title: Exploratory Data Analysis
layout: page
---

# Introduction

## Sebuah Analogi

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/aleksandra-boguslawska-MS7KD9Ti7FQ-unsplash.jpg" title="beach image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Photo by <a href="https://unsplash.com/@aleksandraboguslawska?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Aleksandra Boguslawska</a> on <a href="https://unsplash.com/s/photos/beach?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
 </div>

Bayangkan kamu dan circle mu rencana mau trip ke pantai. Tapi masih bingung mau pantai mana. Jadi kamu mulai riset sendiri.

Mungkin awalnya kamu nyari "pantai di kalimantan timur". Kamu hitung biaya perjalanan, apa aja wahananya, bersih atau nggak, dsb. Data-data ini kamu masukin ke spreadsheet.

Temanmu juga mulai nanya-nanya orang pantai ini bagus gak, pantai itu worth ga, dan akhirnya kalian dapat pantai tujuan kalian.

Tindakan apapun yang dilakukan untuk menentukan/menginvestigasi lokasi pantai tujuan adalah apa yang disebut oleh data scientist sebagai __Analisis Data Eksploratif__ (bahasa inggrisnya Exploratory Data Analysis atau EDA).

## Apa Itu EDA

Exploratory Data Analysis (EDA), seperti namanya, adalah pendekatan untuk menganalisis/mengeksplorasi kumpulan data untuk merangkum karakteristik kumpulan data dan temuan menarik. Seringkali, karakteristik ini ditampilkan secara visual. Dalam konteks teknis data science, ini mengacu pada proses kritis dalam melakukan penyelidikan awal pada data untuk:
- Temukan pola
- Anomali spot
- Uji hipotesis
- Periksa asumsi (jika ada) dengan bantuan statistik ringkasan dan representasi grafis.

## Mengapa EDA

Alasan utama kita melakukan EDA adalah:

- Untuk melihat bentuk awal data.
- Untuk menampilkan data sehingga fitur yang paling menarik akan terlihat. Kita kemudian dapat menggunakan fitur ini untuk tujuan machine learning.
- Untuk mendeteksi kesalahan
- Untuk memeriksa asumsi
- Untuk pemilihan awal model yang sesuai
- Untuk menentukan hubungan antara variabel input, dan
- Untuk menilai arah dan ukuran kasar hubungan antara variabel input dan target.

## Letak Proses EDA Dalam Data Science

<img src="https://dphi-live.s3.amazonaws.com/media_uploads/image_827e51adcd4e478fb28e34b488432f75.png" height=320>

Data scientist menghabiskan sekitar 60–70% waktu mereka dalam proyek pada fase data cleaning hingga feature engineering. Dan kira-kira 40–50% dari waktu itu dihabiskan di EDA.

# Hands-On Lab

Notebook hands-on dapat diakses di [github](https://github.com/dssc-unmul/eda/blob/main/Exploratory-Data-Analysis.ipynb) atau langsung buka di colab [![Buka di Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/dssc-unmul/eda/blob/main/Exploratory-Data-Analysis.ipynb)

# Sumber

- [DPhi Course Introduction to Exploratory Data Analysis](https://dphi.tech/learn/introduction-to-exploratory-data-analysis)
- [IBM Coursera Data Analysis with Python](https://www.coursera.org/learn/data-analysis-with-python)