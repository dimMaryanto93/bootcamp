---
layout: post
title: "Pengenalan Pemograman Servlet"
lang: java-web
categories:
- java
- web
- war
refs: []
youtube: 
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-011
---

Sekarang saya mau membahas tentang basic pemograman Java Web yaitu Servlet. Apa itu Servlet?

Pemograman Servlet, hal yang pertama yang anda harus ketahui jika kita ingin menggunakan teknologi Java Web karena sebelum kita menggunakan framework seperti JSP, SpringMVC, Struct2 dan lain-lain. Basic dari pemograman Java Web adalah Servlet. Nah sekarang kita masuk ke materi apa itu Servlet?

> Servlet adalah bahasa pemograman java yang khusus dibuat untuk Web, servlet ini akan menghasilkan request dan response dari Web Server. Web Server akan me-request dinamic web page dengan tujuan (response) mengenerate page static berupa html ke client (browser).

Ok nah sekarang kita akan memulai membuat Servlet, untuk membuat servlet itu sebenarnya sangatlah mudah, kita buat kelas baru dengan nama ```HaloController``` dalam package ```com.hotmail.dimmaryanto.software.controller``` isinya seperti berikut:

{% gist page.gist HaloController.java %}

Nah setelah kita membuat servlet, apa yang harus kita lakukan??? mungkin di benak anda mana urlnya untuk mengakses?? yak tepat sekali, kita perlu mapping urlnya untuk servlet tersebut. berikut adalah caranya:

1. Ubah file ```src/main/webapp/WEB-INF/web.xml```
2. Menggunakan annotation atau ```@WebServlet```

Jadi ada 2 cara yaitu dengan menggunakan web descriptor (xml) atau biasa menggunakan annotation ```@WebServlet```, nah sekarang kita coba dulu menggunakan yang XML dulu supaya tau gimana jaman dulu klo bikin Java Web itu seperti apa OK.

nah coba buka file ```web.xml``` seperti yang saya sebutkan tadi lokasinya. kemudian tambahkan tag ```<servlet></servlet>``` seperti berikut:

{% highlight xml %}
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app>
  <display-name>Archetype Created Web Application</display-name>
  <servlet>
    <servlet-name>Halo</servlet-name>
    <servlet-class>belajar.java.web.controller.HaloController</servlet-class>
  </servlet>

  <servlet-mapping>
    <servlet-name>Halo</servlet-name>
    <url-pattern>/selamat/datang</url-pattern>
  </servlet-mapping>

</web-app>
{% endhighlight %}

Nah sekarang coba running aplikasinya menggunakan maven plugin tomcat7 seperti beritku:

{% highlight bash %}
mvn clean package tomcat7:run
{% endhighlight %}

kemudian coba akses alamat berikut:

{% highlight bash %}
http://localhost:8080/tutorial-javawebapp/selamat/datang
{% endhighlight %}

maka hasilnya akan seperti berikut:

![servelt pertama]({{ site.baseurl }}{{ page.image_path }}/selamat-datang.png)

Jadi penjelasanya adalah kita membuat ketika browser me-request alamat ```http://localhost:8080/tutorial-javawebapp/selamat/datang``` maka akan ditambkan oleh servlet dengan nama ```Halo``` yang mereferensi ke klass servlet yaitu ```belajar.java.web.controller.HaloController```. Ada pertanyaan silakan komentar.
