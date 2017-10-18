---
layout: post
title: "Software Development for Java Users"
lang: java-core
categories:
- java
- core
gist: 
youtube:
---

Halo nah sesuai topik yang di Judul, jadi kali ini saya akan membuat atau membahas hal-hal apa aja yang harus di _setup_ untuk ngoding dengan bahasa pemograman Java berikut ulasannya tetang bagaimana cara setup Java Development Environtment pada Sistem Operasi Windows 10, UBuntu dan Fedora.

Di bahasa pemograman Java kita harus melakukan setup JDK atau kependekan dari _Java Development Kit_. JDK bertujuan untuk menyediakan sekumpulan tools handal yang disediakan oleh para insyinyur Java (gelar) contoh diantarnya sebagai berikut

- `javac` (untuk melakukan compilasi)

{% highlight sh %}
javac lokasi.package.namakelas.MainMethod.java
{% endhighlight %}

- `java` (untuk menjalankan hasil compilasi atau bytecode)

{% highlight sh %}
java lokasi.package.namakelas.MainMethod
{% endhighlight %}

- dan lain-lain, karena masih banyak tools yang gak bisa disebutin satu persatu. seperti arsitektur JDK pada gambar dibawah ini:

![JDK vs JRE](/resources/downloads/java-arc.png)


