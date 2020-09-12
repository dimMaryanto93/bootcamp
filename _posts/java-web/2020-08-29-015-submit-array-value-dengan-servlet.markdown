---
layout: post
title: "Submit Array value menggunakan Servlet"
date: 2020-08-29T19:28:54+07:00
lang: java-web
categories:
- java
- web
- war
refs: []
youtube: https://www.youtube.com/watch?v=VvApkFldl4w&list=PLV1-tdmPblvyaCTcYR9u7k4G24uVDZT0v&index=14
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-015
---

Kita sudah memahami perbedaan tentang HTTP Method GET dan POST, sekarang saya mau membahas tentang mengirim multiple parameter ke sebuah servlet dengan method GET, kenapa menggunakan GET? jawabanya supaya kita tau apa yang dikirim ditampilkan di URL ya tapi klo digunakan untuk aplikasi sesunggunya disarankan menggunakan POST ya!!!.

Jadi saya punya form seperti berikut:

![multiple select]({{ site.baseurl }}{{ page.image_path }}/multiselect.png)

Dan jika di submit maka URLnya paramenternya akan menampilkan seperti berikut:

`atribut?values=bola&values=basket&values=touring`

Nah jadi bagaimana menangkap value tersebut kalo menggunakan `getParameter` itu hanya akan mengambil value yang terahhir muncul saya yaitu `touring` terus bagimana?

Ok sekarang anda buat dulu form HTMLnya dengan nama `multiplevalues.html` seperti berikut:

{% gist page.gist "multiplevalues.html" %}

Kemudian anda buat servletnya di dengan nama `MultipleValuesController.java` dalam package `belajar.java.web.controller` seperti berikut:

{% gist page.gist "MultipleValuesController.java" %}

sekarang klo form tersebut di submit maka akan tampil seperti berikut:

![hasil submit]({{ site.baseurl }}{{ page.image_path }}/getParamenterValues.png)

Nah jadi solusinya menggunakan method

{% highlight java %}
String[] values = response.getParameterValues("name-atribute");
{% endhighlight %}

setelah itu kita bisa loop datanya dari variable `values` tersebut.