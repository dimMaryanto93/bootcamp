---
layout: post
title: "Time is your practice part 4"
date: 2017-11-17T21:02:41+07:00
lang: java-core
categories:
- Java
- Core
gist: 
youtube: 
comments: true
---

![Class diagram]({{ site.baseurl }}/resources/downloads/imgs/java-core/quis-4/classes.jpg)

1. Buatlah _class_ sesuai dengan perancangan _class diagram_ diatas, Untuk _class_ `Nasabah`, `NasabahPerorangan` dan `NasabahBadanUsaha` simpan dalam package `tdi.training.java.core.model.nasabah`, Sedangkan untuk _class_ `Tabungan` simpan dalam package `tdi.training.java.core.model.aplikasi`

2. Dalam _class_ `NasabahPerorangan` buat sebuah _contructor_ untuk menset data `nomorIdentitas`, `namaLengkap`, `alamat`, `nomorHp`, serta berikan nilai _default_ untuk `active = false`, `saldo = BigDecimal.ZERO`.

3. Masih dalam method _constructor_ pada _class_ `NasabahPerorangan`, buat _instance object_ untuk variable `tabungan` setelah itu berikan nilai _default_ untuk `sukuBunga = 0.1`, `kriteria = "Tabungan Mapan"`, dan `saldo = BigDecimal.ZERO`.

4. Masih dalam _class_ `NasabahPerorangan` buatlah method `toString()` yang mengembalikan tipe data `String` kemudian berikan annotation `@Override` diatas method tersebut, setelah itu buatlah untuk mengembalikan text seperti berikut: `nasabah [noIdentitas: 62213424, status: false, namaLengkap: Dimas Maryanto, saldo tabungan: 0]`.

5. Buat _class_ baru dengan nama `MainApplication` dalam package `tdi.training.java.core`, setelah itu buat _method_ `main(String[])`. Kemudian buat instance object dari _class_ `NasabahPerorangan` dengan parameter sebagai berikut `nomorIdentitas = "621234"`, `namaLengkap = "Muhamad Yusuf"`, `alamat = "Jl. Ujung berung no 123"`, `nomorHp = "08123423434"`.

6. Masih dalam _class_ `MainApplication`, setelah membuat _instance object_ untuk _class_ `NasabahPerorangan` panggil method `toString()` untuk menghasilkan seperti berikut:
```sh
nasabah [noIdentitas: 621234, status: false, namaLengkap: Muhamad Yusuf, saldo tabungan: 0]
``` 

## My Solution

Seperti biasa, [download disini]({{ site.baseurl }}/resources/downloads/file/java-core.quis-4.zip) untuk melihat solusi dari pertanyaan diatas.