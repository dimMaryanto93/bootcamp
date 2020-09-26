---
layout: post
title: "Static Resources with WebJars"
date: 2020-09-26T20:32:24+07:00
lang: java-web
categories:
- java
- web
- war
refs: 
- https://www.webjars.org/
youtube: 
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-026
---

Update your `pom.xml` dengan menambahkan [webjars](https://www.webjars.org/) library contohnya seperti [jQuery](https://jquery.com/), [Bootstrap](https://getbootstrap.com/), [DataTables](https://datatables.net/) seperti berikut:

{% highlight xml %}
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <!-- project properties -->

    <properties>
    <!-- properties value -->
    </properties>

    <dependencies>
        <!-- other libs -->

        <!--webjars -->
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>bootstrap</artifactId>
            <version>4.5.2</version>
        </dependency>
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>jquery</artifactId>
            <version>3.5.1</version>
        </dependency>
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>jquery-validation</artifactId>
            <version>1.19.0</version>
        </dependency>
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>datatables</artifactId>
            <version>1.10.21</version>
        </dependency>
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>datatables-buttons</artifactId>
            <version>1.6.1</version>
        </dependency>
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>datatables-bootstrap</artifactId>
            <version>2-20120202-2</version>
        </dependency>
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>datatables-colreorder</artifactId>
            <version>1.5.1-1</version>
        </dependency>
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>datatables-responsive</artifactId>
            <version>2.2.3</version>
        </dependency>
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>datatables-rowreorder</artifactId>
            <version>1.2.4</version>
        </dependency>
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>datatables-fixedheader</artifactId>
            <version>3.1.7</version>
        </dependency>
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>datatables-fixedcolumns</artifactId>
            <version>3.2.2</version>
        </dependency>
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>datatables-colvis</artifactId>
            <version>1.1.1</version>
        </dependency>
    </dependencies>
</project>
{% endhighlight %}

Sekarang kita akan coba untuk test, apakah resources yang kita tambahkan sudah bisa di access melalui web contohnya seperti resource `bootstrap:4.5.2` yang kita tambahkan sebagai dependency coba access dengan url [http://localhost:8080/bootcamp-java-webapp/webjars/bootstrap/4.5.2/css/bootstrap.min.js](http://localhost:8080/bootcamp-java-webapp/webjars/bootstrap/4.5.2/css/bootstrap.min.js) jika berhasil maka outputnya seperti berikut:

![bootstrap loaded]({{site.baseurl}}{{page.image_path}}/bootstrap-css-resources.png)

Setelah itu, kita bisa menggunakan di halaman html atau jsp contohnya seperti berikut:

{% gist page.gist "style-webjars-jstl.jsp" %}

Hasilnya seperti berikut:

![hasil]({{site.baseurl}}{{page.image_path}}/jsp-webjars-resources-jstl.png)

Mungkin dari temen-temen bertanya? bang itu kok tau lokasi file css atau js. itu di ambil dari mana ya?

jawabanya: nih lokasinya ada di lib/dependency seperti berikut:

![location lib]({{site.baseurl}}{{page.image_path}}/location-resource.png)

dan coba [baca ini](https://www.webjars.org/documentation#servlet3)