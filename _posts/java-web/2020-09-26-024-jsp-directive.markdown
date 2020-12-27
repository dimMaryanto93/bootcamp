---
layout: post
title: "JSP Directive"
date: 2020-09-26T20:31:52+07:00
lang: java-web
categories:
- java
- web
- war
refs: 
- https://docs.oracle.com/cd/B14099_19/web.1012/b14014/genlovw.htm#directives
- https://docs.oracle.com/cd/B14099_19/web.1012/b14014/jspnls.htm
youtube: https://www.youtube.com/watch?v=XceBjKui3xQ&list=PLV1-tdmPblvyaCTcYR9u7k4G24uVDZT0v&index=23
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-022
---

JSP Directive biasanya digunakan untuk merubah struktural pada servlet class yang akan di generate setelah di render. JSP Directive terdiri dari beberapa tag diantaranya `page`, `include` dan `taglib`.

### 4.1. Page Directive

JSP Page Directive biasanya digunakan untuk menentukan behavior atau prilaku pada suatu jsp/servlet contohnya biasanya digunakan untuk import class, apakah kita mau mengaktifkan expression languge dan lain-lain. Contohnya seperti berikut

{% gist page.gist "scriptlet-directive-page.jsp" %}

### 4.2. Include Directive

JSP Include Directive, untuk tag ini sesuai dengan namanya jadi kita bisa include file jsp lainnya dari jsp yang kita gunakan contoh penggunananya seperti berikut:

{% gist page.gist "scriplet-directive-include.jsp" %}

### 4.3. Taglib Directive

JSP Taglib Directive, untuk tag ini kita akan bahas di materi selanjutnya ya... jadi kita skip dulu.