---
layout: post
title: "Event Listeners using Session Level"
date: 2020-09-09T09:30:11+07:00
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
image_path: /resources/posts/java-web-019
---

Event Listeners using Session Level yaitu Event atau kejadian yang biasanya di catch ketika session dibuat atau di destroy. Biasanya penggunaanya untuk authentication, mendapatkan user/session yang active.

Berikut adalah contoh Event Listener using Session Level yang digunakan untuk menghitung jumlah user yang mengunjugi webapp.

Pertama membuat halaman utama terlebih dahalu dengan URI seperti berikut dengan servlet `/listener/home`

{% gist page.gist "HomeSessionListenerController.java" %}

Setelah itu kita buat package baru dengan nama `listener` dengan function untuk menghitung jumlah yang pengunjung yang login dan logout berdasarkan session yang dibuat dan di destroy. seperti berikut:

{% gist page.gist "UserLogonCountingListener.java" %}

Dan kemudian kita buat halaman login dan untuk memproses login nya dengan servlet berikut:

{% gist page.gist "LoginSessionListenerController.java" %}

Dan yang terakhir kita buat untuk handler logout nya dengan servlet berikut:

{% gist page.gist "LogoutSessionListenerController.java" %}

Dan berikut adalah hasilnya:

jika temen-temen arahkan ke url [host:port/context-path/listener/home](http://localhost:8080/bootcamp-java-webapp/listener/home)

Maka akan terlihat seperti berikut:

![home]({{site.baseurl}}{{page.image_path}}/01-home.png)

Setelah itu coba arahkan ke [host:port/context-path/listener/login](http://localhost:8080/bootcamp-java-webapp/listener/login)

Input username dan password kemudian submit maka hasilnya seperti berikut:

![home increment]({{site.baseurl}}{{page.image_path}}/02-home-result.png)

nilai `total user = 1` dan `current user = 1` 

setelah itu coba arahkan [host:port/context-path/listener/logout](http://localhost:8080/bootcamp-java-webapp/listener/logout)

Maka nilai `total user = 1` dan `current user = 0` 