---
layout: post
title: "Tipe data yang bernilai Number"
date: 2017-11-07T19:03:01+07:00
lang: java-core
categories:
- Java
- Core
refs: 
- https://docs.oracle.com/javase/8/docs/api/java/lang/Byte.html
- https://docs.oracle.com/javase/8/docs/api/java/lang/Short.html
- https://docs.oracle.com/javase/8/docs/api/java/math/BigDecimal.html
- https://docs.oracle.com/javase/8/docs/api/java/lang/Float.html
- https://docs.oracle.com/javase/8/docs/api/java/lang/Integer.html
- https://docs.oracle.com/javase/8/docs/api/java/lang/Long.html
youtube: https://www.youtube.com/watch?v=weZ5N5Aq1M4&list=PLV1-tdmPblvz0NCFYgVQaQEOTWJCjjucO&index=13
comments: true
---

Tipe data untuk yang bernilai number di bahasa pemograman Java pada dasarnya dibagi jadi 2 kategori yitu bilangan bulat dan bilangan pecahan baik positif dan negatif. Bilangan bulat dibagi lagi menjadi beberapa range yaitu kecil, sedang dan besar.

## Bilangan Bulat

Bilangan bulat baik itu negatif maupun positif dibagi lagi menjadi 4 yaitu 

### `java.lang.Byte` 

Digunakan untuk yang memiliki nilai tidak kurang dari `-128` hinga `127` atau sama dengan `1 btye` contohnya:
{% highlight java linenos %}
public class BilanganBulatKecil{

    public static void main(String[] args){
        Byte nilaiMin = -128;
        Byte nilaiMax = 127;
        System.out.println(
            "Nilai minimum dari tipe data java.lang.Byte adalah " 
            + nilaiMin + 
            ", Sedangkan nilai maximumnya adalah "
            + nilaiMax 
        );    
    }
} 
{% endhighlight %}

### `java.lang.Short` 

Digunakan untuk yang memiliki nilai tidak kurang dari `-32,768` hinga `32,767` atau `2 byte` contohnya seperti berikut:
{% highlight java linenos %}
public class BilanganBulatMenengah {
    public static void main(String[] args){
        Short nilaiMin = -32_768;
        Short nilaiMax = 32_767;
        System.out.println(
            "Nilai minimum dari tipe data java.lang.Short adalah " 
            + nilaiMin + 
            ", Sedangkan nilai maximumnya adalah " 
            + nilaiMax 
        );    
    }
}
{% endhighlight %}

### `java.lang.Integer`

Digunakan untuk memiliki nilai tidak kurang dari `-2,147,483,648` hinga `2,147,483,647` atau `4 byte` contohnya seperti berikut:

{% highlight java linenos %}
publi class BilanganBulatBesar {
    public static void main(String[] a){
        Integer nilaiMin = -2_147_483_648;
        Integer nilaiMax = 2_147_483_647;
        System.out.println(
            "Nilai minimum dari tipe data java.lang.Integer adalah " 
            + nilaiMin + 
            ", Sedangkan nilai maximumnya adalah " 
            + nilaiMax 
        );    
    }
}
{% endhighlight %}

### `java.lang.Long`

Digunakan untuk memiliki nilai tidak kurang dari `-9,223,372,036,854,775,808` hinga `9,223,372,036,854,775,807` atau `8 byte` contohnya seperti berikut:

{% highlight java linenos %}
publi class BilanganBulatSangatBesar {
    public static void main(String[] a){
        Long nilaiMin = -9_223_372_036_854_775_808;
        Long nilaiMax = 9_223_372_036_854_775_807;
        System.out.println(
            "Nilai minimum dari tipe data java.lang.Long adalah " 
            + nilaiMin + 
            ", Sedangkan nilai maximumnya adalah " 
            + nilaiMax 
        );    
    }
}
{% endhighlight %}

## Bilangan pecahan

Bilangan pecahan pada dasarnya ada 2 yaitu `java.lang.Float` dan `java.lang.Double`, jadi intinya tipe data `java.lang.Double` lebih besar dari `java.lang.Float`

### `java.lang.Float`

Tipe data float ini lebih besar dari tipe data yang ada di atasnya yaitu `byte`, `short`, `int`, dan `long` karena dia bisa menerima bilangan pecahanan contohnya `0.50123` dst. contohnya:

{% highlight java linenos %}
publi class BilanganBulatSangatBesar {
    public static void main(String[] a){
        Float nilaiMin = -9_223_372_036_854_775_808f;
        Float nilaiMax = 9_223_372_036_854_775_807f;
        System.out.println(
            "Nilai minimum dari tipe data java.lang.Float adalah " 
            + nilaiMin + 
            ", Sedangkan nilai maximumnya adalah " 
            + nilaiMax 
        );    
    }
}
{% endhighlight %}

### `java.lang.Double`

Tipe data yang terakhir dari yang paling besar dari semua tipe data untuk number adalah `java.lang.Double` contohnya seperti berikut:

{% highlight java linenos %}
publi class BilanganBulatSangatBesar {
    public static void main(String[] a){
        Double nilaiMin = -9_223_372_036_854_775_808d;
        Double nilaiMax = 9_223_372_036_854_775_807d;
        System.out.println(
            "Nilai minimum dari tipe data java.lang.Float adalah " 
            + nilaiMin + 
            ", Sedangkan nilai maximumnya adalah " 
            + nilaiMax 
        );    
    }
}
{% endhighlight %}

