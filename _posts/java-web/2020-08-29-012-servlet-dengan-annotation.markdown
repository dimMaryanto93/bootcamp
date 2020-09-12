---
layout: post
title: "Pemograman Servlet dengan Annotation"
date: 2020-08-29T19:28:33+07:00
lang: java-web
categories:
- java
- web
- war
refs: []
youtube: https://www.youtube.com/watch?v=HjMOCEqbx8Q&list=PLV1-tdmPblvyaCTcYR9u7k4G24uVDZT0v&index=11
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-012
---

Sebelumnya kita telah membuat servlet dengan menggunakan **xml-mapping**, jaman sekarang configurasi di xml udah usang atau jarang dipake. Sekarang udah **Zamannya Annotation** maka dari itu saya bakalan membahas tentang servlet dengan annotation.

Buat kelas baru dengan nama `ServletAnnotation` seperti berikut:


{% gist page.gist "ServletAnnotation.java" %}

klo anda perhatikan, di beris ke  terdapat sepenggalan koding seperti berikut:

{% highlight java %}
@WebServlet(urlPatterns = {"/servlet-annotation"}, name = "configAnnotation")
{% endhighlight %}

nah klo ini sama seperti configurasi di xmlnya seperti berikut:

{% highlight xml %}
<servlet>
    <servlet-name>configAnnotation</servlet-name>
    <servlet-class>belajar.java.web.controller.ServletAnnotation</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>configAnnotation</servlet-name>
    <url-pattern>/servlet-annotation</url-pattern>
</servlet-mapping>
{% endhighlight %}

Gimana perbandingannya cukup praktiskan untuk configurasi menggunakan Annotation. Nah jadi mulai saat ini kita akan terus menggunakan Annotation karena supaya lebih memudahkan dan mempercepat proses mapping url.