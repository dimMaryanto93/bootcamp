---
layout: post
title: "Submit value dengan Servlet menggunakan Http GET Method"
date: 2020-08-29T19:28:39+07:00
lang: java-web
categories:
- java
- web
- war
refs: []
youtube: https://www.youtube.com/watch?v=cK0mhNaJfsM&list=PLV1-tdmPblvyaCTcYR9u7k4G24uVDZT0v&index=12
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-013
---

Sekarang kita akan membuat untuk menerima request dari Form dari HTML menggunakan Servlet. Berikut adalah implementasinya:

Pertama kita buat dulu file `html` dalam folder `src/main/webapp` misalnya dengan nama `submitget.html` berikut isi filenya:

{% gist page.gist "submitget.html" %}

Setelah itu, kita buat _action handler_ untuk url `kirim-get` yaitu dengan menggunakan servlet yaitu seperti berikut dengan nama kelas `SubmitGetController.java` yaitu isinya seperti berikut:

{% gist page.gist "SubmitGetController.java" %}

Nah sekarang anda coba perhatikan url berikut:

`http://localhost:8084/tutorial-javawebapp/kirim-get?nim=10511148&nama=Dimas+Maryanto`

Klo menggunakan submit dengan method GET maka parameter itu muncul semua seperti link diatas ketika di submit.