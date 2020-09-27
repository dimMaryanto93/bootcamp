---
layout: post
title: "Implementasi MVC menggunakan JSP dan Servlet"
date: 2020-09-27T15:31:42+07:00
lang: java-web
categories:
- java
- web
- war
refs: []
youtube: 
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-030
---

Berikut adalah implementasi konsep MVC dengan Java Web, 

## Model 

Untuk model kita masih menggunakan class `Mahasiswa` yang telah dibuat di materi sebelumnya seperti berikut:

{% gist page.gist "Mahasiswa.java" %}

Kemudian kita siapkan data dengan membuat interface terlebih dahulu yang di letakan di package `com/maryanto/dimas/bootcamp/service` seperti berikut:

{% gist page.gist "MahasiswaService.java" %}

Dan untuk merepresentasi data dari database kita buat data dummy seperti berikut:

{% gist page.gist "MahasiswaServiceImpl.java" %}

## View 

Sekarang kita akan membuat presenternya dari data yang telah kita buat yaitu dengan membuat file `jsp` yang di letakan dalam folder `src/main/webapp/WEB-INF` dengan folder `mahasiswa` dan nama filenya `list.jsp` seperti berikut:

{% gist page.gist "mahasiswa-list.jsp" %}

## Controller

Dan yang terakhir kita buat controllernya dengan menggunakan servlet seperti berikut:

{% gist page.gist "MahasiswaListController.java" %}

Dan sekarang coba jalankan kemudian akses url [http://localhost:8080/bootcamp-java-webapp/mahasiswa/list](http://localhost:8080/bootcamp-java-webapp/mahasiswa/list)

Hasilnya maka akan menampilkan seperti berikut:

![mvc-jsp-servlet]({{site.baseurl}}{{page.image_path}}/servlet-jsp-mvc-impl.png)