---
# Common-Defined
title: "Menghitung Beban Dinamis pada Crane pada saat Lifting"
date: 2023-05-10T00:00:00+07:00
lastmod: 2023-05-10T00:00:00+07:00
draft: false
tags: ["crane", "dynamic", "load"]
categories: ["Analysis"]
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

## Hukum Newton dan Perubahan Momentum

Bagaimana cara sederhana menghitung total beban crane akibat tambahan beban dinamis?

Mengacu pada Hukum Newton, gaya terjadi akibat adanya percepatan pada suatu massa. Namun, jika di-*extend* ke level selanjutnya, gaya terjadi akibat adanya perubahan momentum terhadap waktu.

$$
F = \dfrac{d(mv)}{dt}
$$

$$
F = m\dfrac{dv}{dt} + v\dfrac{dm}{dt}
$$

**m** = massa dalam kg dan
**v** = kecepatan dalam m/s

Aplikasinya pada bidang struktur, beban statik dan dinamik hanya menggunakan bagian yang pertama saja (sisi kiri). Ini bisa kita artikan sebagai massa dengan perubahan kecepatan terhadap waktu.

$$
F = m\dfrac{dv}{dt}
$$

$$
F = m.a
$$

dengan **a** = percepatan dalam m/s2

Untuk persamaan bagian kedua (sisi kanan), umumnya digunakan dalam analisis pada massa yang berubah terhadap waktu, misalnya pada aliran air dalam pipa dengan kecepatan tetap. Jadi misalkan kita ingin menghitung berapa gaya yang dihasilkan oleh aliran air pada pipa, bisa menggunakan persamaan di bawah ini. Unit satuan **dm/dt** bisa menggunakan kg/detik, yaitu perubahan massa setiap detiknya.

$$
F = v\dfrac{dm}{dt}
$$

## Beban Dinamik Crane

Beban crane bisa dikategorikan sebagai beban dengan massa tetap, sehingga menghitungnya cukup menggunakan persamaan sisi kiri pada penjelasan di atas.

$$
F = m\dfrac{dv}{dt}
$$

Kita sudah mengetahui nilai massa pada crane, yaitu beban yang akan diangkat oleh crane.
Sebelum mulai menghitung, kita perlu mengetahui fase dalam pengangkatan crane.

Pada semua fase atau kondisi di bawah, gaya gravitasi selalu aktif dengan nilai g = 9.8 m/s2.

* Fase 1: Beban ada di bawah dalam kondisi diam diletakkan di tanah (*rest*). Crane belum menerima beban apapun. Kecepatan pengangkatan v = 0 m/s
* Fase 2: Crane mulai mengangkat beban. Pada fase ini, ada perubahan kecepatan beban dimulai dari kecepatan v = 0 m/s hingga kecepatan tertentu dan konstan
* Fase 3: Crane melakukan pengangkatan dengan kecepatan tetap
* Fase 4: Crane menurunkan kecepatan pengangkatan dari sebelumnya konstan hingga kondisi berhenti atau kecepatan v = 0 m/s
* Fase 5: Crane berhenti menjadi kecepatan v = 0 m/s dan posisi beban diangkat sepenuhnya oleh crane.

Dari 5 fase di atas, crane akan menerima beban statik dan kombinasi statik dan dinamik.
Selanjutnya, notasi **t** dan **Δt** melambangkan waktu pada saat perubahan kecepatan terjadi.

### Fase 1
Tidak ada beban pada crane. Gaya yang terjadi pada kabel crane T = 0.

$$
T = 0
$$

### Fase 2
Pada fase 2, terjadi perubahan kecepatan, yang awalnya berhenti (fase 1) menuju kecepatan tetap (fase 3).

$$
T = m\dfrac{dv}{dt}
$$

$$
T = m.g + m \dfrac{(v_{22} - v_{21})} {(t_2-t_1)}
$$

Kita bisa menyederhanakan percepatan pengangkatan sebagai **ad**:
$$
a_d = \dfrac{(v_{22} - v_{21})} {(t_2-t_1)} = \dfrac{\Delta{v_2}}{\Delta{t}}
$$

Karena fase 2 diawali dari kecepatan 0, maka percepatan ad akan bernilai positif (searah gravitasi).

$$
a_d > 0
$$

Dengan demikian total beban statik dan beban dinamis pada fase ini:
$$
T = m.g + m.a_d
$$

$$
T = m (g+a_d)
$$

### Fase 3
Karena kecepatan pengangkatan beban tetap pada fase ini, maka tidak ada perubahan kecepatan. Penjabaran di bawah menunjukkan, tidak ada beban dinamis yang terjadi pada saat terjadi pengangkatan dengan kecepatan tetap.

$$
T = m\dfrac{dv}{dt}
$$

$$
T = m.g + m \dfrac{(v_{32} - v_{31})} {t}
$$

$$
v_{32} = v_{31}
$$

$$
T = m.g + m \dfrac{0} {t}
$$

$$
T = m.g
$$

### Fase 4
Fase 4 hampir mirip kondisinya dengan fase 2, terjadi perubahan kecepatan yang sebaliknya, dari kecepatan tetap (fase 3) ke posisi berhenti (fase 5).

$$
T = m\dfrac{dv}{dt}
$$

$$
T = m.g + m \dfrac{(v_{42} - v_{41})} {(t_2-t_1)}
$$

Kita bisa menyederhanakan percepatan pengangkatan sebagai **ad**:
$$
a_d = \dfrac{(v_{42} - v_{41})} {(t_2-t_1)} = \dfrac{\Delta{v_4}}{\Delta{t}}
$$

Karena fase 4 ini diawali dari kecepatan tertentu hingga berhenti di kecepatan 0, maka percepatan **ad** akan bernilai negatif (berlawanan arah gravitasi).

$$
a_d < 0
$$

Total beban statik dan beban dinamis pada fase ini:
$$
T = m.g + m.a_d
$$

$$
T = m (g+a_d)
$$


### Fase 5
Crane mengangkat sepenuhnya beban, namun karena posisi beban diam, maka perubahan kecepatan adalah 0.

$$
T = m\dfrac{dv}{dt}
$$

$$
T = m.g + m\dfrac{(v_{52} - v_{51})}{dt}
$$

$$
v_{52} = v_{51} = 0
$$


$$
T = m.g
$$

## Kondisi Kritis Akibat Beban Dinamik
Dari penjabaran di atas, beban statik akibat gravitasi terjadi pada semua fase (fase 1-5).
Sedangkan tambahan beban dinamik terjadi hanya pada fase:
- Fase 2: Pengangkatan dimulai dari kecepatan 0 hingga kecepatan tertentu
- Fase 4: Pengangkatan akan berhenti dari kecepatan tertentu

Tentu fase di atas adalah simplifikasi dari kompleksitas *lifting* yang sesungguhnya. Ada banyak faktor yang kita tidak perhitungkan seperti beban angin, friksi dan tahanan massa dengan udara sekitar, friksi kabel, dan lain sebagainya.

Ada beberapa kesimpulan yang bisa diambil:
- Perubahan kecepatan pengangkatan crane terhadap waktu **Δt** akan memengaruhi beban dinamik yang dihasilkan. Semakin cepat perubahan kecepatannya (**Δt** semakin kecil) , maka semakin besar pula beban dinamiknya.
- Berlandaskan poin 1 di atas, produsen crane biasanya akan membatasi kecepatan maximum. Hal ini bertujuan untuk membatasi percepatan yang terjadi.

Kondisi di atas berlaku untuk pengangkatan, belum termasuk pada pada penurunan massa dari ketinggian ke tanah (*rest*). Namun jika menggunakan formula di atas untuk kedua kasus pengangkatan dan menurunkan massa dari/ke crane, beban-beban kritis bisa dikelompokkan menjadi:

* Kasus Pengangkatan Massa
  - Kondisi dari diam ke bergerak (fase 2) adalah fase paling kritis karena pengangkatan ke arah atas mengakibatkan adanya tambahan percepatan.

$$
T = m (g+a_d)
$$

$$
a_d = \dfrac{(v_{22} - v_{21})} {(t_2-t_1)} = \dfrac{\Delta{v_2}}{\Delta{t}} > 0
$$

* Kasus Penurunan Massa
  - Kondisi dari bergerak ke diam (pada saat massa hendak menyentuh tanah) adalah fase paling kritis pada kabel crane. Perlu diperhatikan, pada saat penurunan, nilai kecepatan adalah bernilai negatif, berkebalikan dari pengangkatan. Formula di bawah menggunakan notasi 4 yang berarti fase 4 pada saat penurunan, yaitu sesaat sebelum massa menyentuh tanah.

$$
T = m (g+a_d)
$$

$$
a_d = \dfrac{(v_{42} - v_{41})} {(t_2-t_1)} = \dfrac{\Delta{v_4}}{\Delta{t}} > 0
$$

$$
v_{42} = 0; v_{41} < 0
$$


## Simplifikasi Beban Dinamik Berdasarkan ASCE-7

Beban crane dikategorikan sebagai beban hidup (*Live Load*) pada sub-chapter 4.9 ASCE-7. Tidak terbatas pada beban dinamik akibat pengangkatan vertikal, ASCE 7 juga mengcover beban dinamik akibat pemindahan horizontal, terutam akibat friksi pada *runway beam*.

{{< figure src="https://storage.googleapis.com/dukenmarga.id/images/2023/crane-load-asce-7-16.png" caption="Tambahan beban impact crane ASCE 7-16 sub-chapter 4.9" >}}

Desain praktis lebih disarankan untuk mengacu pada code seperti ASCE 7 yang merupakan penyederhanaan beban dinamik sebagai beban statik.