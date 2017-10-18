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
Sebelum kita koding dengan bahasa pemograman berorientasi object ini (Java), kita harus install dulu Software Development Kit atau SDK yaitu JDK kependekan dari _Java Development Kit_. JDK bertujuan untuk menyediakan sekumpulan tools handal yang disediakan oleh para insyinyur Java (gelar) contoh diantarnya sebagai berikut

![JDK vs JRE](/resources/downloads/java-arc.png)

### Level Tools & Tools APIs
1. `javac` untuk melakukan compilasi
2. `java` untuk menjalankan hasil compilasi atau bytecode
3. `javadoc` untuk membuat Dokumentasi di dalam koding Java
4. `jar`, `war`, `ejb` dan `ear` hasil akhir project Java, defaultnya `jar` untuk aplikasi desktop dan `war` untuk aplikasi web atau Java EE.

### Level Development

1. `Java Web`, web development di Java biasanya menggunakan teknologi `Servlet` & `JSP`
2. `Applet`, Aplikasi desktop yang bisa berjalan di Browser
3. `JavaFX`, Aplikasi desktop yang modern sebelumya sebagai pengganti `Java Swing`
4. `Java Swing`, Aplikasi desktop yang berfokus pada component

### Level Base Libraries

1. `JDBC`, API yang digunakan untuk mengakses Database Relational seperti MySQL, Oracle, PostgreSQL dan lain-lain.
2. `RMI`, Remote Method Invocation untuk mengakses resourse server (Client-Server Application)
3. `Networking`, Java API untuk Jaringan.
4. `Date & Time`, Java API untuk mengakses waktu dan date di system (Operation System)
5. `Internationalization`, digunakan untuk membuat aplikasi multi bahasa contohnya ingin membuat aplikasi yang menggunakan bahasa indonesia, bahasa arab dll.
6. `Math`, Java API untuk melakukan perhitungan matematika, fisika dll
7. `Collections`, Java API untuk menyimpan nilai yang multi value (Array)
8. dll masih banyak lagi ya... gak bisa disebutin satu-satu karena kebanyakan wkwkw

Nah semua teknologi diatas mulai dari level tools & tools API, development, dan base libraries itu berjalan di atas Java Virtual Machine atau yang bisa disebut JVM. OK nah mungkin dari temen-temen agak pusing kok banyak banget ya... ya teknologi Java itu memang luas banget blum lagi klo integrasi sama teknologi lain atau frameworknya Java seperti `Spring Framework`, `Play Framework`, `ZKoss`, `Vaadin` dll.

Udah mulai penasaran khan bagaimana Teknologi Java ini... ok baiklah `#showMeTheCode`

Contohnya saya punya file dengan nama `HaloWorld.java` di dalam folder `~/Blogs/java-core/src/main/java/com/maryanto/dimas/` isinya seperti berikut:

{% highlight java linenos %}
package com.maryanto.dimas;

public class HaloWorld{
    public static void main(String[] args){
        System.out.println("Halo World");
    }
}
{% endhighlight %}

Kemudian saya akan compile menggunakan tools `javac` dan menjalankannya dengan perintah `java` tapi sebelum itu saya mau buat folder dulu namanya `out`

 {% highlight sh %}
 # dimmaryanto93@Aspire-E5-473G:~/Blogs/java-core$
 mkdir out
 {% endhighlight %}

setelah folder terbuat jadi hasil compilenya saya mau di buat di folder `out/` seperti berikut:

## Perintah `javac`

{% highlight sh %}
# dimmaryanto93@Aspire-E5-473G:~/Blogs/java-core$
javac src/main/java/com/maryanto/dimas/HaloWorld.java -d out/
{% endhighlight %}

*penjelasanya jadi dengan perintah `javac namafile.java` kita melakukan compile terhadap `namafile.java` sedangkan parameter `-d out/` artinya hasil compilenya diarahkan ke folder `out`

Setelah dijalankan akan menghasilkan bytecode `.class` seperti berikut:

{% highlight sh %}
# dimmaryanto93@Aspire-E5-473G:~/Blogs/java-core$
# works only on linux if you windows user `tree` (without dot)
tree .
# will show like this
.
├── out
│   └── com
│       └── maryanto
│           └── dimas
│               └── HaloWorld.class # <<< that's bytecode
└── src
    └── main
        └── java
            └── com
                └── maryanto
                    └── dimas
                        └── HaloWorld.java # <<< java source code
{% endhighlight %}

## Perintah `java`

Setelah berhasil seperti diatas file `.class` terbuat maka tahap selanjutnya kita bisa running the application with command `java`

{% highlight sh %}
# dimmaryanto93@Aspire-E5-473G:~/Blogs/java-core$
java -cp out/ com.maryanto.dimas.HaloWorld
Halo World # <<< the result printed to the console
{% endhighlight %}

*penjelasananya dengan menggunakan perintah `java` kita bisa menjalankan aplikasi Java. tapi yang perlu diingat adalah perintah `java` hanya bisa bekerja jika di dalam filenya ada method atau fungsi seperti berikut:

```java
public static void main(String[] args){
    // statements
}
```
kalo gak ada method atau fungsi seperti diatas makan akan muncul pesan error di console seperti berikut:

```bash
# dimmaryanto93@Aspire-E5-473G:~/Blogs/java-core$
java -cp src/main/java/ com.maryanto.dimas.HaloWorld
Error: Could not find or load main class com.maryanto.dimas.HaloWorld #<<< error logs
```





