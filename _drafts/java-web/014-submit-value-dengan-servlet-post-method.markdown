---
layout: post
title: "Submit value dengan Servlet menggunakan Http POST Method"
lang: java-web
categories:
- java
- web
- war
refs: []
youtube: 
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-014
---

Sebelumnya kita udah meng-submit request dengan menggunakan `HTTP Method GET` nah sekarang kita akan menggunakan `HTTP Method POST` dan sekalian kita akan membaningkan perbedaan kedua HTTP Method tersebut.

Padasarnya saya akan membuat hal yang sama yaitu menginputkan `nim` dan `nama` kemudian di submit dengan menggunakan method `POST`, sekarang coba anda buat halaman html dengan nama `submitpost.html` seperti berikut:

{% gist page.gist "submitpost.html" %}

Kemudian untuk menghandle mappingnya, kita seperti biasa membuat servlet dengan nama `SubmitPostController.java` seperti berikut:

{% gist page.gist "SubmitPostController.java" %}

Nah klo anda jalankan url `http://localhost:8084/tutorial-javawebapp/submitpost.html` pada dasarnya akan mempilkan form yang sama dengan pembahasan sebelumnya yaitu submit dengan method GET, tpi coba anda perhatikan lagi setelah anda melakukan submit lalu lihat pada path urlnya??? yang terlihat hanya `http://localhost:8084/tutorial-javawebapp/kirim-post` dan di halaman browsernya terdapat outputnya sama dengan submit menggunakan method GET.

Jadi kesimpulannya adalah klo menggunakan method GET maka valuenya akan ditambahkan di URL klo menggunakan POST maka akan disembunyikan.