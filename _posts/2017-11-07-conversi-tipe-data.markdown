---
layout: post
title: "Conversi Tipe data Otomatis di Java"
date: 2017-11-07T23:40:58+07:00
lang: java-core
categories:
- Java
- Core
gist: 
youtube: 
comments: true
---

Untuk konversi tipe data di Java, pada dasarnya otomatis tpi ada beberapa syarat seperti berikut:

1. Sesuai dengan hirarki tipe data tersebut
2. Sesuai dengan tipe data, contohnya jika tipe data `Byte` tidak bisa di konversi ke `boolean` jadi harus ke tipe data yang sifatnya number dan hirarcki yang lebih tinggi seperti gambar berikut:

![Flow conversi otomatis](/resources/downloads/java-core-convert-data/flow.jpg)

Implementasinya seperti berikut:

{% highlight java linenos %}
package com.maryanto.dimas.tdi.training.java.core;

public class KonversiTipeDataOtomatis{

    public static void main(String[] args){
        Integer intVal = 10;
        Float floatVal = 0f;
        Double doubleVal = (double) intVal * floatVal;
        System.out.println("Nilai " + intVal + " * " + floatVal + " = " + doubleVal); 
    }
}
{% endhighlight %}