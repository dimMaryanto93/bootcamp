---
layout: post
title: "JSP Scriptlet"
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

## 1. JSP Scriptlet

Scriptlet yaitu sintax yang memungkinkan statement Java seperti variables, method declaration atau expresion yang ditulis di web pages (HTML). Contohnya seperti berikut:

{% gist page.gist "simple-scriptlet.jsp" %}

## 2. JSP Declaration

Declaration, sama seperti namanya declaration yaitu kita bisa mendeklarikan variable atau method dalam JSP dengan menggunakan contoh

{% gist page.gist "scriplet-declaration.jsp" %}

## 3. JSP Expration

JSP Expration yaitu scription language yang biasanya digunakan untuk melakukan perhitungan, conversi ke `java.lang.String`, dan lain-lain. Contoh penggunaannya seperti berikut:

{% gist page.gist "scriptlet-expration.jsp" %}
