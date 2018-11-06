---
layout: post
title: "Time is your for practice part 3"
date: 2017-11-15T10:52:22+07:00
lang: java-core
categories:
- Java
- Core
gist: 
youtube: 
comments: true
---

1. Buatlah file `LatihanNo1`, `LatihanNo2` dan `LatihanNo3` dengan struktur directory dan tempat menyipan _source code_ seperti berikut
{% highlight bash %}
├── out
└── src
    └── tdi
        └── training
            └── java
                └── core
                    ├── data
                    │   └── LatihanNo3.java
                    ├── LatihanNo1.java
                    └── service
                        └── LatihanNo2.java
{% endhighlight %}

2. Untuk file `LatihanNo3.java` didalam folder `src/tdi/training/java/core/data` buatlah method dengan nama `getNamaLengkap()` untuk mengeluarkan nilai dengan tipe `java.lang.String` yang diisi dengan nilai 'nama anda' contoh `Dimas Maryanto`.

3. Kemudian untuk file `LatihanNo2.java` didalam folder `src/tdi/training/java/core/service` buatlah method dengan nama `setNamaLengkap` untuk menerima data nama lengkap anda yang diisi dari method `getNamaLengkap()` dalam _class_ `LatihanNo3` dalam package `tdi.training.java.core.data`, kemudian tampilkan ke layar console menggunakan `System.out.println()`

4. Untuk file `LatihanNo1.java` dalam folder `src/tdi/training/java/core` buatlah method `main(String[] args)` kemudian panggil method `setNamaLengkap` dari _class_ `LatihanNo2` dalam package `tdi.training.java.core.service` maka klo dijalankan akan menghasilkan output seperti berikut:
```sh
Nama lengkap saya adalah Dimas Maryanto
```

## My Solution

Seperti biasa berikut solusi dari soal diatas, [download di sini]({{ site.baseurl }}/resources/downloads/file/java-core.quis-3.zip)