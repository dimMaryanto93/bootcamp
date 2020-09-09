---
layout: post
title: "Event Listeners using Servlet Context Level"
date: 2020-09-18T09:30:11+07:00
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

Servlet Context Event Listener yaitu melakukan notifikasi terhadap suatu event web application procces dimulai (deployed) atau di shutdown (un-deployed). Contohnya biasanya digunakan untuk melakukan init database ketika web application startup kemudian objectnya disimpan di serlet context setelah berakhir kita bisa destroy connection-nya. Berikut adalah implementasinya:

{% gist page.gist "DatabaseService.java" %}

Berikut adalah event servlet context listener untuk connection database:

{% gist page.gist "DatabaseConnectionListener.java" %}

Berikut adalah contoh memanggil servlet context listner dari servlet:

{% gist page.gist "ServletListenerRequest.java" %}

Selain contoh di atas, kita juga bisa menggunakan beberapa fitur lainnya seperti:

| Event Category        | Event Description | Java Interface    |
| :---                  | :---              | :---              |
| Lifecycle Change      | Servlet Context creation (deploy started), Imminent shutdown of the servlet context | `javax.servlet.ServletContextListner` |
| Attribute Changes     | Addition, Removal, Replacement of servlet context attributes |  `javax.servlet.ServletContextAttributeListener` |