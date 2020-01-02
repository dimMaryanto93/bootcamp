---
layout: post
title: "Tipe data untuk menyimpan Tanggal"
date: 2017-11-07T23:36:01+07:00
lang: java-core
categories:
- Java
- Core
refs: []
youtube: 
comments: true
---

Tipe data yang tidak terlupakan adalah untuk mengimpan tanggal dan waktu, di Java tipe data Tanggal ini ada beberapa macem mulai dari bawaan JDK Java bahkan library atau dependency.

## Date primitif

Untuk tipe data tanggal dengan sudah ada sejak dulu yaitu `java.util.Date`, Tipe data ini merepresentasikan tahun, bulan, hari, jam, menit dan second yang bisa diformat ke pattern tertentu dengan menggunakan object `SimpleDateFormat` yang di import dari `java.text.SimpleDateFormat`. Untuk tipe data ini udah ada sejak JDK 1.0. cara Penggunaannya adalah sebagai berikut:

{% highlight java linenos %}
import java.util.Date;

public class TipeDataDatePrimitif{
    public static void main(String[] args){
        Date tanggalSekarang = new Date();
        System.out.println("Tanggal Sekarang adalah " + tanggalSekarang);
    }
}
{% endhighlight %}

Nah dari perintah tersebut outputnya seperti berikut:

```sh
Tanggal Sekarang adalah Tue Nov 07 23:12:40 WIB 2017
```

Ok misalnya saya mau tanggal yang di output tersebut di format dengan menggunakan format indonesia seperti `07 Nov 2017 23:12:40 WIB` contohnya seperti berikut:

{% highlight java linenos %}
import java.util.Date;
import java.text.SimpleDateFormat;

public class TipeDataDatePrimitif {

    public static void main(String[] args) throws Exception {
        Date tanggalSekarang = new Date();
        // tanggalnya di format sesuai yang kita inginkan
	SimpleDateFormat sdf = new SimpleDateFormat("dd MMM yyyy hh:mm:ss z");
        System.out.println("Tanggal Sekarang adalah " + sdf.format(tanggalSekarang));
    }
}
{% endhighlight %}

Untuk lebih lanjutnya mengenai formating tanggal boleh di baca di dokumentasi 

- [SimpleDateFormat](https://docs.oracle.com/javase/7/docs/api/java/text/SimpleDateFormat.html)
- [DateFormat](https://docs.oracle.com/javase/7/docs/api/java/text/DateFormat.html)

## Date in JDK 1.8

Saat ini menggunakan operasi tanggal biasa menggunakan yang ada dalam package `java.time.*` diantaranya 

1. `java.time.LocalDate` untuk menyimpan tanggal dengan value tanggal, tahun, dan bulan
2. `java.time.LocalDateTime` untuk menyimpan tanggal yang mirip dengan `java.util.Date` dia menyimpan informasi tanggal, bulan, tahun, jam, menit, second dan time zone
3. `java.time.LocalTime` untuk menyimpan waktu tanpa tanggal dan time zone contohnya jam, menit dan second.
4. `java.time.Year` untuk menyimpan berupa tahun saja.
5. `java.time.YearMonth` untuk menyimpan informasi tentang tahun dan bulan saja
6. Masih banyak lagi ya, boleh dibaca [di sini](https://docs.oracle.com/javase/8/docs/api/java/time/package-summary.html)

Untuk implementasinya seperti berikut:

{% highlight java linenos %}
import java.time.LocalDate;

public class TipeDataJava8Date{

    public static void main(String[] args){
        LocalDate tanggalSekarang = LocalDate.now();
        System.out.println(
            "Tanggal sekarang adalah " + 
            tanggalSekarang
        );
        LocalDate kemarin = LocalDate.of(2017, 10, 2);
        System.out.println(
            "Tanggal kemarin adalah " + 
            kemarin
        );
    }
}
{% endhighlight %}

Untuk lebih lengkapnya menggunakan `java.time.LocalDate` bisa di baca [di sini](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html)