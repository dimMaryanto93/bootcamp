---
layout: post
title: "Tipe data logika (true of false)"
date: 2017-11-07T22:05:46+07:00
lang: java-core
categories:
- Java
- Core
refs: 
- https://docs.oracle.com/javase/7/docs/api/java/lang/Boolean.html
youtube: https://www.youtube.com/watch?v=YiVCDgStS_Q&list=PLV1-tdmPblvz0NCFYgVQaQEOTWJCjjucO&index=14
comments: true
---

Tipe data logika ini pada dasarnya adalah yang mengembalikan nilai boolean. Boolean hanya bernilai `true` or `false`. contohnya basicnya 

{% highlight java linenos %}
public class TipeDataLogika {
    public static void main(String[] x){
        Boolean isValid = true;
        System.out.println(
            "Nilai dari variable isValid adalah " + 
            isValid ? "Benar" : "Salah"
        );
    }
}
{% endhighlight %}

Selain itu kita juga bisa menggunakan operator `==` sebagai perbadingan seperti berikut contohnya: 

{% highlight java linenos %}
public class PerbandinganDenganOperator {
    publis static void main(String[] args){
        Integer bilanganBulat = 10;
        Boolean isZero = (bilanganBulat == 10);
        System.out.println(
            "Variable bilangan apakah sama dengan 10 : "+ 
            isZero ? "Ya benar" : "Anda salah"
        );
    }
}
{% endhighlight %}