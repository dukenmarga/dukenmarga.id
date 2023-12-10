---
# Common-Defined
title: "Beberapa Tips Uji Tekan Beton"
date: 2023-12-10T00:00:00+07:00
lastmod: 2023-12-10T00:00:00+07:00
draft: false
tags: ["concrete", "test", "crush"]
categories: ["Structural"]
author: "Duken Marga"

# User-Defined
# You can close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: true
toc: true
# You can also define another contentCopyright
contentCopyright: '<a rel="license noopener" href="https://creativecommons.org/licenses/by-nc-nd/4.0/" target="_blank">CC BY-NC-ND 4.0</a>'
reward: false
mathjax: true
---

## Pengantar

Apakah kalian sudah melakukan uji tekan beton dengan benar? Ada beberapa hal teknis terkait uji tekan beton yang kadang luput dari pengawasan kita.
Beberapa hal di bawah ini semoga bisa menambah pengetahuan kita ketika hendak melakukan uji tekan beton, sesuai ASTM C39/C39M (***Standard Test Method for Compressive Strength of Cylindrical Concrete Specimens***).

Artikel ini merujuk pada [ASTM C39/C39M 17B](https://www.astm.org/c0039_c0039m-17b.html), namun versi terakhirnya adalah [C39/C39M 21](https://www.astm.org/c0039_c0039m-21.html). Hal teknis lainnya yang lebih detail bisa merujuk langsung pada dokumen tersebut.

## Tips

1. **Rate of Loading - Uji dengan menggunakan laju beban yang sesuai**

   Beban dari alat uji tekan beton harus diberikan secara menerus dan tanpa beban kejut. Mesin uji dengan sistem hidraulik (umumnya banyak digunakan saat ini) harus menerapkan beban dengan kecepatan **0.25 +- 0.05 MPa/s** atau kurang lebih **15 MPa/menit**. Anggap saja mutu beton saat ini banyak menggunakan fc' = 30 Mpa, maka uji tekan beton pada umur 28 hari hingga beton hancur akan memakan waktu kurang lebih 2 menit.

   Bagaimana jika laju beban tidak sesuai? ASTM tidak menjelaskan perlu tidaknya koreksi pada nilai akhir mutu beton.

   Namun yang paling penting, laju beban ini harus dipertahankan pada setengah fase terakhir pembebanan menuju nilai fc' yang ditargetkan. Contohnya, untuk sampel
beton silinder 15cm dengan fc' = 30 Mpa, yang estimasi keruntuhannya ada pada beban 530 KN, maka laju pembebanan pada 265-530 KN haruslah pada rentang 0.25 +- 0.05 MPa/s, sedangkan pada fase awal 0-265 KN, bisa menggunakan laju beban yang lebih tinggi.

   {{< figure src="https://storage.googleapis.com/dukenmarga.id/images/2023/rate-loading-concrete-compressive-test.png" caption="Concrete compressive test rate loading. Source: ASTM C39/C39M 17" >}}

2. **Fail and Pattern - Uji hingga benar-benar runtuh dan mendapatkan pola keruntuhan yang sudah didefinisikan dengan baik**

   Pastikan bahwa beban yang diberikan benar-benar sudah turun dari beban puncak (***ultimate***) dan terbentuk pola keruntuhan yang sudah didefinisikan. Ada kalanya, beton
   hancur pada tepi/sudut sampel, namun sebenarnya belum mencapai beban puncak. Untuk mesin uji yang memiliki fitur mati otomatis saat mendeteksi beton hancur, sebaiknya fitur ini
   dimatikan dan pemberian beban tetap dilakukan hingga beban benar-benar sudah turun hingga 95% dari  beban puncak. Misalnya beban puncak ada di 500 KN, maka
   penghentian bisa dilakukan jika beban kurang dari 475 KN (95% dari 500 KN).


   {{< figure src="https://storage.googleapis.com/dukenmarga.id/images/2023/apply-concrete-test-until-failure.png" caption="Stop test until it is fail. Source: ASTM C39/C39M 17" >}}

   Jangan lupa untuk mencantumkan pola keruntuhan sampel beton. Saya rasa, tidak banyak lab yang memberikan informasi terkait ini. Jika pola keruntuhan tidak ada
   pada pola yang sudah didefinisikan di bawah ini, maka polanya harus dicantumkan pada hasil test.

   {{< figure src="https://storage.googleapis.com/dukenmarga.id/images/2023/typical-concrete-failure-pattern.png" caption="Concrete fracture pattern. Source: ASTM C39/C39M 17" >}}

3. **L/D correction factors - Koreksi nilai akhir jika L/D tidak normal** 

   Uji tekan beton dilakukan pada sampel dengan rasio tinggi dan diameter beton sama dengan 2 (L/D = 2), pada umumnya menggunakan sampel dengan tinggi 30cm dan diameter 15cm. Jika L/D kurang dari 1.75, maka nilai akhir harus dikoreksi dengan nilai pada tabel 9.2. Jika tidak tercantum pada tabel, bisa menggunakan nilai interpolasi.

   {{< figure src="https://storage.googleapis.com/dukenmarga.id/images/2023/ld-correction-concrete-sample.png" caption="L/D correction factor for concrete sampel. Source: ASTM C39/C39M 17" >}}


4. **Testing Machine - Gunakan mesin uji yang dipersyaratkan dengan baik dan dikalibrasi secara teratur**

   Untuk mendapatkan hasil uji yang baik, tentu mesin yang digunakan juga harus baik juga. Beberapa persyaratan yang dicantumkan dalam ASTM C39M antara lain: 
   memiliki kapasitas yang cukup untuk beban yang diuji, bisa menampilkan laju beban (load rate), dikalibrasi dalam 13 bulan terakhir, dioperasikan dengan mesin
   listrik (bukan manual dengan orang), dan bisa memberikan beban kontinu tanpa adanya beban kejut/tiba-tiba.

   {{< figure src="https://storage.googleapis.com/dukenmarga.id/images/2023/good-testing-machine.png" caption="Testing machine requirement. Source: ASTM C39/C39M 17" >}}

Kelihatannya belum semua tips dan persyaratan di atas kita lakukan dan lab lakukan. Namun, dengan rekomendasi dari ASTM C39/C39M 17 atau bahkan yang terbaru,
kita semua sebagai pelaku konstruksi bisa meningkatkan kapasitas kita untuk menghasilkan uji tekan yang berkualitas.