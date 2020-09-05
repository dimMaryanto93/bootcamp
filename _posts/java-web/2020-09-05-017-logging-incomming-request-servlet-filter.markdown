---
layout: post
title: "Logging incomming request dengan Servlet Filter"
date: 2020-09-05T18:02:26+07:00
lang: java-web
categories:
- java
- web
- war
refs: 
- https://docs.oracle.com/cd/B14099_19/web.1012/b14017/filters.htm
youtube: 
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-019
---

Servlet Filter yaitu sebuah object yang di trigger ketika sebelum atau sesudah suatu proces dari sebuah request ke web aplikasi.

Filter biasanya digunakan untuk:

1. Recording semua request yang masuk,
2. Logging, 
3. Data compression,
4. Encription dan Dencryption, 
5. Input validation.

Untuk menggunakan filter di dalam servlet, kita harus mengimplement interface `javax.servlet.Filter` yang terdiri dari 3 method yaitu:

1. `init()` method, yaitu method yang biasanya digunakan untuk menginisialisasi data dan juga biasanya di panggil satu kali saat di awal web app di deploy
2. `doFilter(HttpServlerRequest, HttpServletResponse, FilterChain)` method, yaitu method yang digunakan untuk melakukan logging, data compression, encription dan dencryption, input validation dan lain-lain.
3. `destroy()` method, yaitu method yang biasanya digunakan untuk melakukan cleanup data setelah di un-deploy

Berikut adalah contoh penggunaan logging menggunakan Servlet Filter:

{% gist page.gist "PreLoggingFilter.java" %}