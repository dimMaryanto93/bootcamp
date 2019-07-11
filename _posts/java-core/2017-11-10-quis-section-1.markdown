---
layout: post
title: "Time is your practice"
date: 2017-11-10T14:31:35+07:00
lang: java-core
categories:
- Java
- Core
gist: 
youtube: 
comments: true
---

1. Buat project Java dengan nama `java-core.quis-1`, yang didalamnya terdapat folder `src` dan `out`. Kemudian didalam folder `src` buat folder lagi `com/tabledata/bootcamp/java/core`

2. buat kelas dengan nama `Persegi` dalam package `com.tabeldata.bootcamp.java.core` Program menghitung persegi
    1. Buatlah variable dengan nama `sisi` dengan tipe data `java.lang.Double` kemudian berikan nilai `50`
    2. Berdasarkan variable tersebut buatlah untuk menghitung luas persegi tersebut
    3. Dan tampilkan ke layar console seperti berikut `Dengan sisi 50cm maka luas persegi tersebut adalah 25m`

3. Buat **kelas baru** dengan nama `PersegiPanjang` masih dalam **package yang sama dengan soal no 2**, Program menghitung persegi panjang
    1. Buatlah variable dengan nama `panjang` dan `tinggi` dengan tipe data `java.lang.Integer` sebagai global variable
    2. Di dalam method `main(String[] args)` berikan nilai untuk kedua variable tersebut, untuk variable `panjang` berinilai `10` sedangkan untuk variable `tinggi` berinilai `5`
    3. Buatlah untuk cara menghitung luas persegi panjang, kemudian tampilkan ke layar console seperti berikut `Tinggi {tinggi}cm, dan Panjang {panjang}cm. Maka luas persegi panjang adalah {luas}cm`

4. Buat **kelas baru** dengan nama `Lingkaran` **gunakan package yang sama dengan no 2**, Program menghitung lingkaran.
    1. Buatlah variable dengan nama `jariJari` dan beri nilai `15`
    2. Buat variable dengan nama `diameter` kemudian berinilai dari hasil perkalian variable `jariJari` x `2`
    3. Untuk nilai Phi (\pi) gunakan kelas `java.math`
    4. Hitunglah keliling lingkaran tersebut. Tampilkan di console seperti berikut `Nilai PI {nilai}, maka kelilingnya adalah {keliling}`
  
**keterangan** ==> `{ ket }` ubah menjadi nilai sebenarnya contohnya `Tinggi {tinggi}cm` ==> `Tinggi 30cm`