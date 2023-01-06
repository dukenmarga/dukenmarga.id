---
# Common-Defined
title: "Software Kurvatur Momen"
date: 2015-11-26T08:00:00+07:00
lastmod: 2015-11-26T08:00:00+07:00
menu: "main"
weight: 50
author: "Duken Marga"

# you can close something for this content if you open it in config.toml.
comment: false
mathjax: false
contentCopyright: '<img src="https://mirrors.creativecommons.org/presskit/buttons/88x31/png/by.png" style="height:40px" /><br><a rel="license noopener" href="https://creativecommons.org/licenses/by/4.0/" target="_blank">CC BY 4.0 license.</a>'
---

### Pengantar

Halaman ini diperuntukkan sebagai cadangan (backup) halaman software Kurvatur Momen yang pernah saya buat ketika bekerja di Lab Rekayasa Struktur, Institut Teknologi Bandung. Dokumen versi lawas tidak akan saya upload ulang. Halaman asli bisa dilihat di http://lab-struktur.si.itb.ac.id/software-kurvatur-momen/

Versi 1.5.1 adalah versi terakhir yang saya kerjakan di Lab. Rekayasa Struktur ITB. Versi 1.6 hingga yang terakhir adalah program terbaru yang saya buat di waktu senggang saya. Saya kembali mengembangkan software ini karena saya sendiri cukup sering menggunakan software ini dalam pekerjaan saya. Beberapa bug yang saya anggap mengganggu akan saya patch di versi berikutnya, termasuk menambah dan menyempurnakan beberapa fitur dari aplikasi ini. Untuk nilai momen nominal untuk analisis tulangan beton, jika kondisi under-reinforcement terjadi, nilai yang dihasilkan software ini lebih kecil 5-15% dari nilai kalkulasi tangan (manual) bergantung dari banyak tulangan, jadi cukup konservatif.

### Fungsi

Daktilitas suatu struktur paling tidak dibagi bisa ke dalam 4 kelompok:
1) Material, biasa diuji dengan menggunakan tes lab (uji tarik, tekan, dsb)
2) Penampang strukturcontohnya bisa dicek dari sifat under-reinforced atau over-reinforced suatu penampang balok beton,
3) Elemen struktur, bisa dicek dengan analisis plastis, dan
4) Struktur secara keseluruhan, bisa dicek menggunakan pushover analysis (static) atau uji analisis nonlinear lainnya

Untuk poin 1, 3, dan 4, mungkin teman-teman yang spesialisasi struktur sudah pernah melakukannya. Untuk poin nomor 2, salah satu cara untuk mengetahui apakah penampang beton, terutama beam, bersifat daktail atau tidak bisa dicek menggunakan analisis kurvatur momen.

Terakhir aku baca buku MacGregor edisi 6, analisis kurvatur momen ini dibahas lebih awal (bab 4 Behaviour of Flexural Member). Sebenarnya apa sih kurvatur momen itu? Kurvatur momen adalah sudut yang dibentuk ketika beam diberi beban (sederhananya gitu).

Lalu apa saja yang bisa diperoleh dari kurva momen?
1) Overview grafik bisa menunjukkan apakah elemen daktail atau tidak
2) Bisa menunjukkan apakah penampang beton bersifat overreinforced atau under-reinforced.
3) Bisa menentukan kapan bagian beton yang mengalami tarik retak untuk pertama kalinya
4) Bisa menentukan kapan beton tekan mengalami crush (hancur) untuk pertama kalinya (mencapai fc’)
5) Bisa menentukan kapan baja leleh untuk pertama kalinya, sekaligus sebagai nilai momen nominal (jika under reinforced)
6) Mengetahui kapan penampang beton mengalami fail (plastis)
7) Kalo lagi senggang, mungkin kalian bisa mempelajari sifat-sifat dari kombinasi variabel di beton

Software yang saya buat ini bisa memodelkan penampang beton tidak terkekang (tanpa sengkang) dan terkekang (dengan sengkang) dikombinasikan dengan penampang berbentuk lingkaran atau persegi panjang beserta tulangannya.

Kekurangannya: 1) panduan manualnya ga lengkap; 2) pembacaan kurva momen cenderung harus disertai dengan engineering judgment dari yang menganalisis;

Saya upload di blog ini karena saya tidak lagi mempunyai akses ke website resminya.

### Download

Versi 1.6 ([Download](https://storage.googleapis.com/dukenmarga.id/zip/Kurvatur-Momen-1.5.1.zip)) – 26 November 2015

* Fixed: Perbaikan aplikasi untuk sistem operasi yang mempunyai fungsi tanda koma dan titik saling bergantian sehingga tidak bisa menghasilkan solusi
* Added: Icon software

Versi 1.5.1 ([Download](https://storage.googleapis.com/dukenmarga.id/zip/Kurvatur-Momen-1.5.1.zip)) – 30 September 2013

* Fixed: Nilai kurvatur-momen pada saat beton retak atau baja leleh tidak ditampilkan pada penampang lingkaran

Versi 1.5 (Download) – 30 September 2013

* Added: Model beton terkekang untuk penampang lingkaran: Mander, dkk

Versi 1.4.1 (Download) – 27 September 2013

* Minor fixed: Program crash ketika menganalisis tanpa ada input

Versi 1.4 (Download) – 27 September 2013

* Added: Model beton terkekang untuk penampang persegi panjang: Kent & Park
* Fixed: Momden dan Kurvatur pada saat beton retak atau baja leleh

Versi 1.3 (Download) – 23 September 2013

* Added: Kontrol untuk menampilkan kurva tegangan regangan material beton dan baja
* Added: Momen dan Kurvatur pada saat beton retak atau baja leleh
* Fixed: Fungsi tegangan-regangan baja metode Trilinear
* Added: Regangan di semua titik di sepanjang penampang

Versi 1.2 (Download) (Dasar Teori PDF) (Manual) – 20 September 2013

* Added: Gambar penampang lingkaran dan persegi beserta letak tulangannya
* Added: Angka akhir analisis perhitungan: Momen, kurvatur, sumbu netral, balance force, regangan
* Added: Kurva regangan untuk semua step

Versi 1.1 (Download ZIP) (Dasar Teori PDF) (Manual) – 18 September 2013

* Bentuk penampang lingkaran
* Added: Menampilkan hasil kurvatur momen dalam bentuk angka
* Added: Model tegangan-regangan baja: Trilinear
* Fixed: Penentuan kuat tarik beton

Versi 1.0 (Download ZIP) (Dasar Teori PDF) – 26 Juli 2013

* Bentuk penampang persegi panjang
* Plot grafik 2kurvatur vs momen
* Model tegangan-regangan beton: Popovics; Hognestad
* Model tegangan-regangan baja: Ramberg-Osgood; Elasto-Plastis
* Model regangan ultimit Baja: Raphael; Oluokun; British Code (BS 8807:1897)
* Penyimpanan kurva dalam bentuk gambar
