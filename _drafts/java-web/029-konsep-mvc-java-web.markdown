---
layout: post
title: "Konsep Model View Controller (MVC) design pattern"
lang: java-web
categories:
- java
- web
- war
refs: []
youtube: 
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-029
---

Ada beberapa konsep design pattern yang popular dan membawa atau memberikan effect besar pada pengembangan aplikasi contohnya MVC (Model View Controller). MVC yaitu mecahkan masalah dengan membagi menjadi 2 kompenent yaitu 

1. Model
2. View
3. Controller

## Model

Model merupakan representasi dari data dan bisnis logic yang mengatur akses dan memodifkias data. contoh realnya kita bisa ibaratkan seperti select data from database.

## View

View merupakan presenter dari Model yang telah di proses secara bisnis logic.

## Controller

Controller merupakan mengendalikan request dan respose dari HTTP. 

View dan Model saling berkomunikasi dengan Controller, jika saya gambarkan kedalam diagram sequance maka jadi seperti berikut flow interaksinya:

![flow mvc using jsp/servlet]({{site.baseurl}}{{page.image_path}}/flow-mvc-servlet-jsp.png)


## Keuntungan MVC Design Pattern

Keuntungan menggunakan design pattern MVC (Model View Controller) diantaranya sebagai berikut:

1. Decoupling (Pemisahan), dengan memisahkan untuk fitur presenter, control, dan data ini akan menghasilkan aplikasi yang fleksible, reuseable, dan easy to maintanace
2. Jika melakukan development dapat di kerjakan bersama team, karena secara task pekerjaan berbeda layer.
3. Jika melakukan perubahan terhada 1 layer ini tidak akan berimbas pada layer lainnya dengan syarat sesuai dengan persetujuan atau spesifikasi.

