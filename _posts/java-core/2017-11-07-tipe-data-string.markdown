---
layout: post
title: "Tipe data untuk bernilai Karakter"
date: 2017-11-07T22:29:55+07:00
lang: java-core
categories:
- Java
- Core
gist: 
youtube: 
comments: true
---

Tipe data untuk karakter diaktegorikan ada 2 jenis yaitu single karakter dan multiple karakter (String).

## Tipe data single karakter

Tipe data ini pada dasarnya sama seperti pendahulunya `C/C++` yaitu menggunakan `char` atau `Character` kharakter ini merepresentasikan huruf, angka dan simbol. Biasanya tipe data ini hanya dapat menyimpan single word, yang di simpan diatara `'` (single quotes) contohnya seperti berikut:

{% highlight java linenos %}
package com.maryanto.dimas.tdi.training.java.core;

public class TipeDataCharacter{
    public static void main(String[] args){
        Character var = 'A';
        System.out.println("Nilai dari variable var adalah " + var);
    }
}
{% endhighlight %}

## Tipe data multiple karakter

Kalo dulu jika belajar bahasa pemograman `C/C++` atau `pascal` tipe data string ini pasti menggunakan `char[]` character tetapi menggunakan sistem array. Nah di Java tidak seperti itu ya. tipe data multiple karater ini di Java dinamakan dengan `java.lang.String`. Tipe data `String` ini bisa digunakan untuk menyimpan karakter yang sangat besar atau banyak, dengan menggunkan `"` (double quotes) contohnya seperti berikut:

{% highlight java linenos %}
package com.maryanto.dimas.tdi.training.java.core;

public class TipeDataString{

    publis static void main(String[] args){
        String namaSaya = "Dimas Maryanto";
        System.out.println(
            "Variable dengan nama namaSaya berisi karakter " + namaSaya
        );
    }
}
{% endhighlight %}

Untuk tipe data String kita bisa konversi menjadi `char`, karena tipe data String memiliki banyak karakter sedangkan di char hanya boleh menyimpan satu karakter saja jadi contohnya saya mau mengambil huruf `D` dari kalimat `Dimas Maryanto` jadi seperti berikut:

{% highlight java linenos %}
package com.maryanto.dimas.tdi.training.java.core;

public class AmbilKaracterDariString{

    public static void main(String[] a){
        String namaAnda = "Dimas Maryanto";
        char hurufPertama = namaAnda.charAt(0);
        System.out.println(
            "Karakter pertama dari variable namaAnda adalah " + hurufPertama
        );
    }
}
{% endhighlight %} 

Selain itu juga masih banyak fungsi-fungsi di dalam fungsi String contohnya seperti berikut:

1. Membandingkan kedua string dengan menggunakan method `equals("param")`
2. Membandingkan kedua string tanpa melihat huruf besar dan kecilnya `equalsIgnoreCase("param")`
3. Menambahkan karakter berikutnya dengan menggunakan method `concat("param")`
4. Memecah string menjadi bagian tertentu, dengan menggunakan method `substring(1, 10)`
5. Masih banyak lagi ya!!! silahkan [baca di sini](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html)