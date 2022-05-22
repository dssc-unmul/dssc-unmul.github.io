---
layout: page
title: Web Scraping
description: Scraping data dari IMDB <a href="https://colab.research.google.com/github/dssc-unmul/web-scrape/blob/main/webscrape.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg"></a>
img: /assets/img/webscrape_thumbnail.png
# importance: 1
category: belajar
---

## Overview

Ada banyak data yang sudah siap diolah dari berbagai sumber. Ada saatnya kita membutuhkan data yang tersedia dalam sebuah website. Untuk website tertentu biasanya mereka menyediakan API yang bisa dipakai programmer untuk meminta data mereka. Tidak jarang juga yang tidak menyediakan API tersebut, solusinya adalah dengan *web scraping*.

Web Scraping memungkinkan kita untuk mengambil data dari sebuah website secara terprogram. Untuk dapat melakukan web scraping sebaiknya kita juga mengetahui struktur dasar HTML. [Petani kode](https://www.petanikode.com/tutorial/html/) punya bahan bacaan bagus untuk memahami struktur dasar HTML.

## Web Scraping IMDB Most Popular Movie

Project bisa dibuka di google colab [![Buka di Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/dssc-unmul/web-scrape/blob/main/webscrape.ipynb)
, atau buka di [github](https://github.com/dssc-unmul/web-scrape/blob/main/webscrape.ipynb).

### Library yang dibutuhkan

Library yang dibutuhkan adalah [beautifulsoup](https://pypi.org/project/beautifulsoup4/)

Jika membuat project di Colab, beautifulsoup sudah terinstall secara default. Jika menggunakan jupyter notebook di komputer sendiri, beautifulsoup harus diinstall dulu.

Jika menggunakan conda, install dengan command berikut

```console
conda install -c anaconda beautifulsoup4
```
Jika tidak, install dengan command berikut

```console
pip install beautifulsoup4
```
#### Beautiful Soup

Beautiful soup adalah library yang dapat parsing struktur HTML menjadi struktur object-oriented dalam python. Berikut cheat sheet untuk membantu menggunakan beautiful soup.

<script src="https://gist.github.com/yoki/b7f2fcef64c893e307c4c59303ead19a.js"></script>
