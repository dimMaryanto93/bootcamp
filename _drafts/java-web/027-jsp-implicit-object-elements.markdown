---
layout: post
title: "JSP Implicit Object"
lang: java-web
categories:
- java
- web
- war
refs: 
- https://docs.oracle.com/cd/B14099_19/web.1012/b14014/genlovw.htm#directives
- https://docs.oracle.com/cd/B14099_19/web.1012/b14014/jspnls.htm
youtube: 
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-022
---

JSP Implicit Object adalah pre-defined atau reseved variable atau variable yang sudah dibuatkan oleh JSP / Servlet untuk mengakses object seperti `session`, `parameter`, `servlet context`, dan `exception handling`. Contohnya seperti berikut:

{% gist page.gist "scriptlet-implicit.jsp" %}

Sekarang coba request dengan url seperti berikut [host:port/context-path/jsp/scriplet-implicit.jsp?nim=1051148&namaLengkap=Dimas%20Maryanto&tanggalLahir=1991-01-01](http://localhost:8080/bootcamp-java-webapp/jsp/scriplet-implicit.jsp?nim=1051148&namaLengkap=Dimas%20Maryanto&tanggalLahir=1991-01-01)
