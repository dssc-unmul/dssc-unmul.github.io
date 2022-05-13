---
layout: distill
title: Data Science 101

bibliography: intro-to-data.bib
---

## Apa itu Data

Data adalah kumpulan informasi yang diperoleh dari suatu pengamatan, dapat berupa angka, lambang atau sifat. Atau dapat didefinisikan juga sebagai kumpulan nilai dari suatu obyek. Data dapat diperoleh dari sampel atau populasi. **Data Science** menggunakan serangkaian metode untuk menganalisis sejumlah besar data dan mengekstrak insight didalamnya <d-cite key=cielen_introducing_2016></d-cite>.

## Kategori Data

Dalam data science berikut adalah kategori utama data <d-cite key=cielen_introducing_2016></d-cite>:

- Terstruktur (*Structured*)
- Tidak terstruktur (*Unstructured*)
- Bahasa natural (*Natural language*)
- Dihasilkan mesin (*Machine-generated*)
- Berbasis graf (*Graph-based*)
- Audio, video, dan gambar
- Streaming

### Structured

Data terstruktur adalah data yang bergantung pada model data dan terdapat dalam catatan dengan bidang (*field*) yang tetap <d-cite key=cielen_introducing_2016></d-cite>. Makanya lebih mudah untuk menyimpan file dalam database atau spreadsheet yang terdiri dari kolom dan baris.

![](https://www.michael-gramlich.com/wp-content/uploads/2020/09/structured-data-example.jpg)

Namun di dunia ini tidak hanya berisi data terstruktur, lebih sering data yang ada tidak terstruktur.

### Unstructured

Data tidak terstruktur adalah data yang tidak mudah dimasukkan ke dalam model data karena kontennya spesifik terhadap konteks atau bervariasi<d-cite key=cielen_introducing_2016></d-cite>. Salah satu contoh data tidak terstruktur adalah cuitan twitter.

![](/assets/img/2022-05-13-17-20-27.png)

Teks yang ditulis oleh kita, manusia, juga merupakan contoh Natural Language

### Natural Language

Natural language adalah kasus spesial dari data tidak tersturktur; membutuhkan teknik khusus dan ilmu linguistik untuk bisa memprosesnya<d-cite key=cielen_introducing_2016></d-cite>.

### Machine-generated

Data yang dihasilkan mesin adalah informasi yang dibuat secara otomatis oleh komputer, proses, aplikasi, atau mesin lain tanpa campur tangan manusia. Contohnya perangkat IOT yang mengumpulkan data sensor secara terus menerus.

### Graph-based

“Graf” dalam hal ini menunjuk pada [teori graf](https://id.wikipedia.org/wiki/Teori_graf) . Dalam teori graf, graf adalah struktur untuk memodelkan hubungan antara objek. Graf menggambarkan kedekatan atau hubungan objek. Struktur graf menggunakan node, tepi, dan properti untuk mewakili dan menyimpan data graf<d-cite key=cielen_introducing_2016></d-cite>. Data berbasis graf adalah cara alami untuk menggambarkan jaringan pertemanan di sosmed atau pilihan jalur dari suatu titik ke titik lain.

![travelling salesman problem](https://upload.wikimedia.org/wikipedia/commons/thumb/1/11/GLPK_solution_of_a_travelling_salesman_problem.svg/220px-GLPK_solution_of_a_travelling_salesman_problem.svg.png)

### Audio, image, and video

Data multimedia sudah banyak menjadi perhatian data scientist. Pemrosesan data video sudah diterapkan pada banyak industri misalnya mobil Tesla dengan autopilotnya. Kemudian salah satu *task* untuk data gambar adalah [object detection](https://en.wikipedia.org/wiki/Object_detection)

### Streaming

Meskipun streaming data dapat menjadi hampir semua bentuk-bentuk data diatas, data streaming memiliki properti tambahan. Data mengalir (*stream*) ke sistem ketika suatu peristiwa (*event*) terjadi daripada dimuat ke penyimpanan data dalam batch. Contohnya data pasar saham.

## Data Collection

Proses data collection adalah proses yang tidak dapat dihindari. Data collection berarti mengumpulkan data dari satu atau lebih sumber.

Dua metode data collection antara lain<d-cite key=noauthor_what_2021></d-cite>:

- **Primer**. Data dikumpulkan langsung oleh peneliti. Datanya sangat akurat namun butuh waktu dan biaya yang tidak sedikit
- **Sekunder**. Data sekunder adalah data yang dikumpulkan oleh pihak lain dan telah melalui analisis statistik. Sederhananya, ini adalah informasi pihak keuda. Meskipun lebih mudah dan lebih murah untuk diperoleh daripada informasi primer, informasi sekunder menimbulkan kekhawatiran mengenai akurasi dan keaslian. Data kuantitatif merupakan mayoritas data sekunder.

### Teknik Data Collection

#### Data Collection Primer

- Interview
- Focus group
- Kuisioner

#### Data Collection Sekunder

Tidak ada teknik khusus untuk data sekunder. Jadi peneliti mengandalkan data source untuk mendapatkan data antara lain:

- Laporan finansial
- Laporan sales
- Jurnal bisnis
- Sensus
- [Catatan pemerintah](data.gov)
- Internet
- [Awesome Public Dataset](https://github.com/awesomedata/awesome-public-datasets)
- [Kaggle](https://kaggle.com)
- [Google Dataset Search](https://datasetsearch.research.google.com/)
