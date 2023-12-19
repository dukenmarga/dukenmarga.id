---
# Common-Defined
title: "Lokasi 1 Layer Tulangan Susut dan Rangkak pada Beton Slab on grade"
date: 2022-01-09T00:00:00+07:00
lastmod: 2023-05-10T00:00:00+07:00
draft: false
tags: ["concrete", "slab", "reinforcement"]
categories: ["Structural Design", "index"]
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

## Definisi

*Slab on grade* atau *slab on ground* adalah jenis struktur beton yang dipasang bersentuhan langsung di atas permukaan tanah.
Disebut slab karena memiliki permukaan yang cukup luas. Pada umumnya *slab on grade* memiliki beban merata (*uniform load*) dan sejumlah beban titik (*point load*)
jika nilainya cukup signifikan.

*Slab on grade* berbeda dengan pondasi dangkal yang pada umumnya memiliki kolom pendek atau pedestal di atasnya yang bisa dimodelkan sebagai beban titik.

## Jenis Slab-on-Grade dan Fungsi Tulangan

1. ***Plain concrete slab***: Slab beton polos tanpa adanya tulangan, kawat, serat, kabel post-tension, atau bentuk tulangan lainnya. Slab dianggap tidak crack akibat beban yang diberikan.
   Untuk mengurangi efek retak susut pada saat *curing* beton (drying-shrinkage crack), PCA menyarankan spacing atau jarak contruction joint diambil 600-900mm setiap 25mm kebetalan beton.
   Misalkan ketebalan beton 50mm, maka setiap 1200mm slab harus dibuatkan *contruction joint*. 
2. ***Slab reinforced for shrinkage and temperature only***: Slab dengan tulangan suhu dan tulangan susut. Penambahan tulangan ditujukan untuk menangkap dan mengendalikan retak yang mungkin terbentuk antar sambungan.
   Yang perlu diperhatikan, fungsi utama tulangan bukanlah untuk mencegah retak, karena retak sudah pasti terbentuk. Tulangan juga tidak berfungsi untuk meningkatkan nilai beban yang bisa diterima *slab-on-ground* (tidak seperti pada balok beton pada gedung).
   Justru uniknya, cara terbaik untuk meningkatkan kapasitas lentur *slab-on-ground* adalah dengan menambah tebal slab itu sendiri, bukan dengan menambah tulangan.
3. ***Shrinkage-compensating concrete with shrinkage reinforcement***: Slab dengan tulangan kompensasi susut. Jumlah tulangan susut biasanya berkisar 0.15-0.20 persen dari luas potongan (*cross section*) slab
   dan biasanya diletakkan di sisi atas untuk membatasi *initial expansion* dan mengurangi laju susut pada saat curing (drying shrinkage).
4. ***Slab post-tensioned to offset shrinkage***: Slab dengan tambahan kabel post-tensioned. Adanya post-tensioned akan meminimalkan jumlah crack, sehingga spacing antar join bisa lebih panjang dibandingkan
   tanpa tulangan.
5. ***Slab post-tensioned and/or reinforced, with active prestress***: Slab dengan kabel prestres aktif. Adanya tegangan aktif bisa mengurangi tebal slab. 
6. ***Slab reinforced for structural action***: Slab dengan tulangan yang berfungsi struktural. Crack mungkin terjadi akibat beban yang ada. Desain dan posisi tulangan pada tipe ini harus
   didesain dengan metode konvensional yang kita ketahui atau bisa menggunakan metode numerik (misal dengan software *Finite Element Method*). Tipsnya: jika ternyata stress/tegangan pada beton akibat kombinasi
   beban sudah mendekati atau lebih besar dari tegangan crack beton (kurang lebih 10% fc'), maka slab sebaiknya didesain sebagai slab struktural.

Slab nomor 1-5 didesain dengan asumsi bahwa slab tidak mengalami retak akibat beban yang diberikan, sedangkan slab nomor 6 didesain dengan mengantisipasi adanya retak akibat beban yang diberikan.

## Lokasi Tulangan 2 Layer
Untuk *slab on grade* yang memiliki fungsi struktural ataupun yang perilakunya didominasi oleh beban static/dinamik (tipe nomor 6 di atas), kita perlu menghitung berapa kebutuhan jumlah tulangan. Umumnya, diperlukan 2 lapis tulangan: sisi atas dan bawah.

Beberapa contoh:
- Slab dengan beban titik seperti pedestal/kolom pendek kemungkinan besar akan memiliki momen negatif dan positif akibat gaya dari pedestal, biasanya akibat beban lateral. Posisi perletakan tulangan ditentukan dengan memerhatikan
*minimum slab cover* yang merupakan fungsi dari lingkungan tempat slab akan dipasang.
- Slab yang berfungsi menahan air juga biasanya memiliki persyaratan khusus untuk mencegah retak berlebih.

Semua elemen dalam perancangan harus menjadi pertimbangan dalam menentukan jumlah dan posisi tulangan. Saya rasa semua engineer yang berpengalaman sudah cukup familiar dengan skema ini.

## Lokasi Tulangan 1 Layer
Lalu bagaimana jika *slab on ground* yang direncanakan tidak masuk dalam kategori slab struktural atau justru memiliki fungsi arsitektural saja? Fungsi arsitektural berarti: tidak ada beban statik/dinamis yang memberikan momen berarti pada slab.
Jika dicek kembali, justru persyaratan tulangan minimumlah yang menjadi batasan dalam penentuan jumlah tulangan. Seperti yang kita tahu, jumlah tulangan minimum harus terpenuhi untuk mengantisipasi
tidak berfungsinya slab akibat retak berlebih dari beban lingkungan seperti suhu (*temperature*) dan susut (*shrinkage*) pada kasus slab atau untuk menghindari kegagalan getas (*brittle*) pada kasus balok.

Pada *slab on grade*, jumlah tulangan susut dan suhu bisa dihitung dengan menggunakan persamaan berikut yang diambil dari ACI 360R-92 pasal 6.3:

{{< figure src="https://storage.googleapis.com/dukenmarga.id/images/2023/temperature-and-shrinkage-reinforcement-slab-on-grade.png" caption="Nominal tulangan suhu dan susut slab on grade ACI 360R-92 pasal 6.3" >}}

Bisa dilihat bahwa fungsi tulangan susut dan suhu pada *slab on grade* merupakan fungsi dari tebal slab, *drag friction* antara slab dan permukaan tanah di bawahnya, jarak antar *slab joint*
(umumnya *contraction joint* atau *expansion joint*), dan mutu tulangan yang dipasang.

Jika dihitung, tulangan susut dan suhu cukup bisa dipasang dengan menggunakan 1 lapis tulangan.

Di manakah posisi tulangan jika hanya diperlukan 1 lapis tulangan? Cukup banyak praktisi dan gambar kerja yang meletakkan tulangannya di sisi setengah bawah dari ketebalan slab.
Hal ini lumrah terjadi karena terbawa penulangan slab *multi-storey* yang duduk di atas beam yang bukan di atas tanah. Padahal kedua perilaku slabnya berbeda.

Slab pada *multi-storey* akan melendut ke arah bawah akibat gravitasi, sehingga diperlukan tulangan di sisi bawah.

Sedangkan pada *slab-on-ground*, ada  tahanan tanah yang merata (*uniform*) pada semua permukaan
dan menopang langsung penyaluran beban dari slab. Friksi antara tanah dan slab juga harus dianggap sebagai *constraint* yang mengakibatkan slab *cenderung* melengkung ke atas, bukan ke bawah, terutama saat panas siang hari
akan membuat sisi atas slab lebih panas dibandingkan sisi bawah slab.

{{< figure src="https://storage.googleapis.com/dukenmarga.id/images/2023/concrete-curling-during-day.png" caption="Concrete curling. Source: https://concretesouth.com/tech-center/tech-topics-ready-mix/concrete-curling" >}}

Pertimbangan lainnya ditinjau dari sisi estetika adalah kita lebih membutuhkan *crack control* pada sisi atas slab
dibandingkan *crack control* pada sisi bawah slab yang belum tentu akan kita lihat lagi setelah pengecoran selesai.

Sehingga untuk kebanyakan kasus, kebutuhan tulangan di sisi bawah slab menjadi tidak signifikan.

ACI 360R-92 pasal 6.4 menyarankan untuk meletakkan tulangan susut dan tulangan suhu di tengah atau di atasnya (setengah bagian atas), namun tidak di sisi bawah (setengah bagian bawah).

{{< figure src="https://storage.googleapis.com/dukenmarga.id/images/2023/location-1-layer-reinforcement.png" caption="Tulangan 1 lapis ACI 360R-92 pasal 6.4" >}}

Tulangan bisa diletakkan di 38mm-50mm di bawah sisi atas permukaan beton atau 1/3 tebal slab di bawah permukaan beton. Dari persyaratan guideline ini, kita bisa membuat beberapa simulasi:
- Jika tebal beton 75mm, maka posisi tulangan 1 lapis diletakkan di tengah-tengah.
- Tebal beton yang lebih kecil dari 75mm menjadi kurang ideal dengan 1 lapis tulangan karena
  posisinya sudah berada di setengah sisi bawah (kurang dari 1/2 x 75mm). Kurang ideal berarti fungsi tulangan tidak maksimal. Jika tebal kurang dari 75mm, sebaiknya jenis *slab-on-grade*
  diubah menjadi plain-slab tanpa tulangan dengan memperkecil jarak antar *construction joint*, sehingga meminimalisir jumlah retak tidak terencana. 
- Jika tebal beton 150mm, posisi tulangan ada di 1/3 tebal slab atau 50mm di bawah sisi atas beton.
- Jika lebih tebal dari 150mm, contohnya 210mm, posisi bisa diambil di 50mm atau hingga di 70mm (1/3 x 210mm) di bawah sisi atas permukaan beton. 

Tulangan 1 lapis lebih mungkin terjadi pada jenis slab 2, 3, dan 4 di atas. Slab tipe 5 dan 6 lebih cocok dikategorikan sebagai beton struktural yang jumlah tulangan dan posisinya
harus disesuaikan dengan berapa gaya dan tegangan yang terjadi.