---
layout: post
title: "Variabel dan Tipe Data"
date: 2017-11-07T16:40:18+07:00
lang: java-core
categories:
- Java
- Core
gist: 
youtube: 
comments: true
---

Ok pembahasan selanjutnya adalah variable dan tipe data di bahasa pemograman Java. Pembahasan pertama yaitu variable.

## Variable

_Variable_ pada dasarnya perintah untuk komputer menyimpan suatu nilai di _memory_ (RAM atau _Random Access Memory_), untuk di proses oleh procesor di ALU (_Arithmetic Logic Unit_). 

Pemberian nilai ke variable tertentu disebut, instilahnya inisialisasi sedangkan membuat variable dinamakan deklarasi. Mungkin dari temen-temen masih agak bingung dengan istilah tersebut supaya lebih paham berikut contohnya:

### Deklarasi variable

Dekarasi variable di Java sangat ketat, magsugnya ketat apa nih? ambigu ya!!!. nah jadi karena Java adalah _strong typing_ jadi setiap variable harus memiliki tipe data. Untuk tipe data akan saya bahas di bawah ya. jadi tipe data yang sama mau pakai yaitu `Integer` kemudian membuat variable dengan nama `serverPort` seperti berikut:

{% highlight java %}
public class DataTypeDeclaration {

    // inilah yang disebut deklarasi
    public java.lang.Integer serverPort;
}
{% endhighlight %}

### Inisialiasi variable

Inisialisasi seperti yang dikatakan diatas tadi, jadi inisialisasi adalah pemberian nilai terhadap suatu variable seperti berikut:

{% highlight java %}
public class DataTypeDeclaration {

    // inilah yang disebut deklarasi
    public java.lang.Integer serverPort;

    public void setServerPort(){
        // ini lah yang disebut inisialisasi terhadap variable
        this.serverPort = 10;
    }
}
{% endhighlight %}

Jadi dari contoh di atas kita memberikan nilai `10` terhadap variable dengan nama `serverPort` dengan tipe datanya yang harus number dan bilangan bulat posif atau negatif. Atau cara mudahnya di posisi sebelah kanan diatara operator `=` adalah `10` dan di sebelah kirinya adalah variable `serverPort` jadi gambarannya dari kanan dialirkan ke sebelah kiri.

## Tipe data

Nah sakarang saya mau bahas tentang tipe data, jadi tipe data di bahasa pemograman Java ada 2 macem yaitu
1. Primitif
2. Sederhana

Nah magsud dari tipe data primitif adalah tipe data yang dari dulu nenek monyang pencipta bahasa pemograman Java dibuat sudah ada. contohnya 

1. `int`, 
2. `short`, 
3. `char`, 
4. `boolean`,
5. `long` dan
6. `byte`. 

Sedangkan yang sederhana atau bisa disebut **kekinian bangetz** klo kata anak jaman sekarang itu ada 

1. `java.lang.Integer`,
2. `java.lang.Double`,
3. `java.lang.Float`,
4. `java.lang.String`,
5. `java.math.BigDecimal` 
6. dll maaf klo disebuti atu-atu blenger nulisnya soalnya banyak banget ya... klo mau lebih dalam lagi tentang tipe data ini boleh baca dokumentasi atau javadoc [berikut](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html)

