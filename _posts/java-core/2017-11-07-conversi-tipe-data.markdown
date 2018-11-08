---
layout: post
title: "Konversi tipe data otomatis di Java"
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

![Flow conversi otomatis]({{ site.baseurl}}/resources/posts/java-convert-data/flow.jpg)

Implementasinya seperti berikut:

{% highlight java linenos %}
public class KonversiTipeDataOtomatis{

    public static void main(String[] args){
        Integer intVal = 10;
        Float floatVal = 0f;
        Double doubleVal = (double) intVal * floatVal;
        System.out.println("Nilai " + intVal + " * " + floatVal + " = " + doubleVal); 
    }
}
{% endhighlight %}

Contoh lebih detailnya lagi berdasarkan gambar diatas:

{% highlight java linenos %}
public class TipeDataKonversiFlow {

	public static void main(String[] args){
		byte varByte = 100;
		System.out.println("var byte adalah " + varByte);
		short varShort = varByte;
		System.out.println("var byte ke short adalah " + varShort);
		int varInt = varShort;
		System.out.println("var short ke int adalah " + varInt);
		long varLong = varInt;
		System.out.println("var int ke long adalah " + varLong);
		float varIntToFloat = varInt;		
		System.out.println("var int ke float adalah " + varIntToFloat);
		float varLongToFloat = varLong;
		System.out.println("var long ke float adalah " + varLongToFloat);
		double varFloatToDouble = varLongToFloat;
		System.out.println("var float ke double adalah " + varFloatToDouble);
		double varIntToDouble = varInt;
		System.out.println("var int ke double adalah " + varIntToDouble);
		double varLongToDouble = varLong;
		System.out.println("var long ke double adalah " + varLongToDouble);		
	}
}
{% endhighlight %}

Jika di jalankan hasilnya seperti berikut:

```sh
var byte adalah 100
var byte ke short adalah 100
var short ke int adalah 100
var int ke long adalah 100
var int ke float adalah 100.0
var long ke float adalah 100.0
var float ke double adalah 100.0
var int ke double adalah 100.0
var long ke double adalah 100.0
```