---
layout: post
title: "Pengenalan JavaServer Page (JSP)"
lang: java-web
categories:
- java
- web
- war
refs: []
youtube: 
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-020
---

JavaServer Page atau JSP yaitu Server-Side Programing Technology yang digunakan untuk membuat Web Aplikasi berupa content HTML menjadi dynamis. 

JSP ini berextensi ```.jsp``` bukan ```.html``` dan media internet typenya yaitu ```application/jsp```.

{% highlight jsp %}
<html>
<head><title>Belajar Web Pages dengan JSP</title></head>
<body>
<!-- ini code java dalam html -->
  <%  out.println("Ini sintax JSP"); %>
</body>
</html>
{% endhighlight %}

atau anda juga bisa menggunakan gaya bahasa XML seperti berikut:

{% highlight jsp %}
<html>
<head><title>Belajar Web Pages dengan JSP</title></head>
<body>
<!-- ini syntax JSP dengan xml format -->
  <jsp:scriptlet>
    out.println("Ini sintax JSP lagi");
  </jsp:scriptlet>
</body>
</html>
{% endhighlight %}

JSP component adalah sejenis dengan [Java Servlet](http://www.oracle.com/technetwork/java/index-jsp-135475.html) yang khusus di design supaya user membangun user interface dengan mudah untuk aplikasi java web. Dengan JSP kita bisa membuat halaman yang dinamis seperti input data, ngambil data dari database dan lain-lain.

tag JSP dapat digunakan seperti mengambil data dari database, meng-akses komponent JavaBeans, bertukar informasi yang berbeda halaman, request dan lain-lain.

Keuntungan menggunakan JSP adalah

* JSP selalu melakukan kompilasi terlebih dahulu sebelum diproses, ini memang konsep java sejak dulu supaya menghasilkan koding yang mengurangi erorr yang disebabkan oleh sintax erorr.
* JSP bisa mengakses semua fitur JavaEE seperti EJB, JavaBeans, JDBC, Persistance dan lain-lain.
* JSP bisa dikombinasikan dengan Servlet untuk menghandle proses bisnis.

Finally, JSP is an integral part of Java EE, a complete platform for enterprise class applications. This means that JSP can play a part in the simplest applications to the most complex and demanding.