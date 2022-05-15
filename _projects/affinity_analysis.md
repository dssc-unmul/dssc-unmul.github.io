---
layout: page
title: Afinity Analysis Sederhana
description: Membangun afinity analysis sederhana untuk product recommendation
img: /assets/img/affinity_thumbnail.png
importance: 1
category: belajar
---

## Chapter 1 Memulai Data Mining

Saat ini kita mengumpulkan informasi pada skala yang tidak pernah dicapai sebelumnya pada sejarah umat manusia dan menerapkan kepentingan penggunaan informasi ini di kehidupan sehari-hari kita. Kita mengharapkan komputer bisa melakukan apapun mulai dari terjemahin halaman web sampai merekomendasikan barang yang kita beli.

Data mining adalah metodologi yang bisa kita terapkan untuk melatih komputer agar dapat membuat keputusan dari data dan sebagai kekuatan pada banyak sistem teknologi saat ini.

Bahasa pemrograman Python sudah berkembang dalam popularitasnya. Sintaks nya mudah dibaca dan yang paling jelas dibanding bahasa pemrograman lain. Ada banyak komunitas peneliti, praktisi, dan pemula yang menggunakan Python untuk data mining.

### Intro to Data Mining

Data mining is part of algorithms, statistics, engineering, optimization, and computer science. We also use concepts and knowledge from other fields such as linguistics, neuroscience, or town planning. Applying it effectively usually requires this domain-specific knowledge to be integrated with the algorithms.

Untuk memulai proses data mining, kita buat sebuah dataset. Dataset mengandung dua aspek berikut:

- Sampel, adalah objek pada dunia nyata. Contohnya buku, hewan, orang, dll.
- Fitur, adalah deskripsi dari sampel dalam dataset. Contohnya panjang, jumlah kaki, tanggal dibuat, dll.

| Orang | Tinggi | Tinggi atau pendek |
| ----- | ------ | ------------------ |
| 1     | 155 cm | pendek             |
| 2     | 165 cm | pendek             |
| 3     | 175 cm | tinggi             |
| 4     | 185 cm | tinggi             |

>sebagai contoh, kita mau komputer bisa menyebutkan orang ini pendek atau tinggi. Kita mulai dengan mengumpulkan data yang isinya ukuran tinggi dari orang-orang yang berbeda dan apakah dia dianggap tinggi atau pendek

Langkah selanjutnya adalah tuning algoritma. Anggaplah ini adalah algoritma yang simpel; jika tinggi lebih dari $$x$$, orang nya tinggi, jika tidak orangnya rendah.

>anggaplah x nya adalah 170. Yang lebih dari 170 dianggap tinggi, sisanya pendek. Di praktek nanti ada dataset asli untuk mengetahui orang pendek atau tinggi.

## Persiapan Environment

- Install python
- Install jupyter notebook
- Install pandas
	```console
	conda install pandas
	```

### Affinity Analysis Sederhana

[Notebook project](https://github.com/dssc-unmul/affinity-analysis/blob/main/Affinity.ipynb) atau [![Buka di Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/dssc-unmul/affinity-analysis/blob/main/Affinity.ipynb)

---

## Summary

---

## Resource

- [buku pdf](https://newoutlook.it/download/python/learning-data-mining-with-python.pdf)
- [github repo dari buku](https://github.com/PacktPublishing/Learning-Data-Mining-with-Python)
