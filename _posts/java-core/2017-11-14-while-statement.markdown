---
layout: post
title: "Looping menggunakan WHILE dan DO-WHILE statement"
date: 2017-11-14T13:09:15+07:00
lang: java-core
categories:
- Java
- Core
gist: 
youtube: 
comments: true
---

Tidak jauh berbeda dengan perulangan dengan `for` statement di [materi sebelumnya]({% post_url java-core/2017-11-14-for-statement-2 %}). Sekarang kita lihat cara bekerja untuk perulangan menggunakan `do-while` terlebih dahulu. berikut contohnya:

{% highlight java linenos %}
package com.maryanto.dimas.tdi.training.java.core;

public class DoWhileStatement{

    public static void main(String[] args){
        Integer i = 0;
        do {
            System.out.println("Sekarang ada di index ke " + i++);
        } while (i < 10);
    }
}
{% endhighlight %}

Jadi penjelasnya seperti berikut:

1. di baris ke `6` kita membuat variable `i = 0`
2. Untuk perulangan dengan `do-while` jadi perintahnya di kerjakan dulu baru di cek kondisinya, seperti berikut berarti kita tau sekarang `i = 0` maka akan menampilkan ke layar
```sh
Sekarang ada di index ke 0
```
3. Maka setelah itu di cek apakah `i < 10`, terus nilai variable `i` sekarang jadi nilainya `1` loh kenapa `i = 1` bukannya barusan nilainya `0`, ya karena ada operator `i++` jika kita menggunakan `++i` maka yang tampil di layar adalah `sekarang ada di index ke 1`
4. Setelah itu masuk ke iterasi selanjutnya yaitu `i = 1`, menjalakan lagi dan menampilkan kelayar 
```sh
Sekarang ada di index ke 1
```
5. Sama seperti tadi dicek lagi di condisi perlualngan apakah `2 < 10` jawabanya benar ya jadi masuk ke iterasi selanjutnya terus seperti itu hingga iterasi ke 9 (saya skip ya supaya gak kepanjangan nulisnya)
6. Di iterasi ke 9 ini brati log di consolenya 
```sh
Sekarang ada di index ke 8
```
7. baru di cek apakan `i < 10`, nilai i sekarang adalah `9` karena benar jadi balik lagi ke iterasi selanjutnya.
8. Sekarang ada di iterasi terakhir, `i = 10` jadi tanpil ke console 
```sh
Sekarang ada di index ke 9
```
9. Cek lagi ke kondisi `i < 10`, nilai i sekarang addalah `10` karena `i < 10` tidak terpenuhi maka sekarang keluar dari perulangan.

Setelah menggunakan yang `do-while` statement, sekarang kita menggunakan yang `while`.

{% highlight java linenos %}
package com.maryanto.dimas.tdi.training.java.core;

public class WhileStatement{

    public static void main(String[] args){
        Integer i = 0;
        while (i < 10){
            System.out.println("Sekarang ada di index ke " + (i++));
        }        
    }
}
{% endhighlight %}

Penjelasannya, kurang lebih sama dengan perulangan dengan `do-while` tapi bedanya adalah kalau menggunakan `while` itu di seleksi dulu.