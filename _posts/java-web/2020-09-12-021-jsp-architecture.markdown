---
layout: post
title: "JSP Architecture"
date: 2020-09-12T21:15:36+07:00
lang: java-web
categories:
- java
- web
- war
refs: 
- http://tomcat.apache.org/whichversion.html
youtube: https://www.youtube.com/watch?v=442-W6LvC-8&list=PLV1-tdmPblvyaCTcYR9u7k4G24uVDZT0v&index=20
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-021
---

JSP membutuhkan Web Server dengan spesifikasi JSP Proccessing tertentu, Contohnya seperti Apache Tomcat 7 yang kita gunakan yaitu memiliki spesifikasi servlet version `3.0`, JSP version `2.2` dan JDK yang disupport yaitu `7 or later`.

Berikut adalah diagram dimana posisi JavaServer Page dalam container Web Server dalam Web Aplikasi

![jsp inside container]({{site.baseurl}}{{page.image_path}}/java-web-deployment-env.jpg)

## JavaServer Pages Processing

Bagaimana JSP di proses dalam web server, berikut diagram untuk menjelaskan flow proses JSP di proses oleh web server:

![jsp processing]({{site.baseurl}}{{page.image_path}}/jsp-processing.jpg)