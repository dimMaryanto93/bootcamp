---
layout: post
title: "Servlet Event Listeners"
date: 2020-09-05T20:06:46+07:00
lang: java-web
categories:
- java
- web
- war
refs: 
- https://docs.oracle.com/cd/B14099_19/web.1012/b14017/filters.htm#i1000654
youtube: 
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-018
---

Servlet Event Listeners yaitu pendeteksi perubahan terhadap suatu kejadian contohnya event selesai deploy, request-response pada web, perubahan data pada session dan lain-lain.

Sebuah Event teridiri dari 2 level category yaitu 

1. Servlet Context level
    - Lifecyle changes
    - Attribute changes
2. Session Level
    - Lifecyle changes
    - Attribute changes

Kita bisa menjalankan task ketika event tersebut terjadi contohnya kita bisa membuat connection ke database, jalankan script migration database ketika aplikasi terdeploy dengan menggunakan servlet context level, atau kita juga bisa membuat session tracker (brapa banyak user yang login) dengan menggunakan event session level. 


Berikut adalah contoh penggunaan Event Servlet Context Level:

{% gist page.gist "DatabaseService.java" %}

Berikut adalah event servlet context listener untuk connection database:

{% gist page.gist "DatabaseConnectionListener.java" %}

Berikut adalah contoh memanggil servlet context listner dari servlet:

{% gist page.gist "ServletListenerRequest.java" %}