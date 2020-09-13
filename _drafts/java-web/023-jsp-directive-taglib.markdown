---
layout: post
title: "JSP Taglib Directive (JSTL)"
lang: java-web
categories:
- java
- web
- war
refs: []
youtube: 
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-023
---

JavaServet Page API mengijinkan untuk kita mendefinisikan custom JSP tag dengan format XML atau HTML, yang artinya kita bisa buat sendiri tag atau menggunakan lib yang sudah di define seperti JSTL atau JavaServer Pages Standard Tag Libaray. 

Fitur utamanya teridiri dari:

1. Core Tag
2. Formatting Tag
3. SQL Tag
4. XML Tag
5. JSTL Function

Untuk menggunakan JSTL ini kita perlu menambahkan dependency di `pom.xml` seperti berikut:

{% highlight xml lineos %}
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    
    <!-- project settings -->

    <dependencies>
        <!-- enabled jstl -->
        <dependency>
            <groupId>jstl</groupId>
            <artifactId>jstl</artifactId>
            <version>1.2</version>
        </dependency>

        <!-- other dependencies -->
    </dependencies>
    <build>
        <!-- build plugins -->
    </build>
</project>
{% endhighlight %}