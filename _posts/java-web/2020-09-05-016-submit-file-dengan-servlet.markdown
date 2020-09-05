---
layout: post
title: "Submit file menggunakan Servlet"
date: 2020-09-05T16:00:53+07:00
lang: java-web
categories:
- java
- web
- war
refs: 
- http://tomcat.apache.org/whichversion.html
- https://stackoverflow.com/a/2424824/6685789
- https://stackoverflow.com/a/18664715/6685789
- https://stackoverflow.com/a/1812356/6685789
youtube: 
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-016
---

Setelah kita belajar mengirimkan data berupa text, sekarang kita akan membahas mengirimkan file menggunakan servlet dan attribute `enctype="multipart/form-data"`. Untuk menggunakan **attribute enctype hanya bisa digunakan dengan menggunakan `HTTP Method POST`** selain itu juga untuk meng-upload file ada beberapa kondisi yaitu 

1. Servlet spec 3.1 or newer, bisa menggunakan native API
2. Servlet spec < 3.1, ada issue untuk method `getSubmittedFileName()` karena method tersebut baru di perkenalkan di web server seperti `Tomcat8`, `Jetty 9`, `WildFly 8`, `GlassFish 4`
3. Menggunakan Thirdparty lib seperty `Apache Commons FileUpload`.

Karena servlet spec yang kita gunakan masih menggunakan `Tomcat7` sebagai development jadi kita akan menggunakan flow no 2.

Ok sekarang kita akan buat form seperti berikut:

![design form]({{site.baseurl}}{{page.image_path}}/form-input-file.PNG)

Berikut adalah file html nya, save di `/src/main/webapp/example/request-file.html`:

{% gist page.gist "request-file.html" %}

Untuk memproses file upload berikut adalah servlet nya:

{% gist page.gist "ServletHandlerFileRequest.java" %}

dan hasilnya seperti berikut:

![result]({{site.baseurl}}{{page.image_path}}/result-file-upload.PNG)

Dan berikut adalah lokasi filenya setelah di pindahkan:

![file-saved]({{site.baseurl}}{{page.image_path}}/file-save-system.PNG)