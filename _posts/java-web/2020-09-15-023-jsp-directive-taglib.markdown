---
layout: post
title: "JSP Taglib Directive (JSTL)"
date: 2020-09-15T21:11:16+07:00
lang: java-web
categories:
- java
- web
- war
refs: 
- https://www.oracle.com/java/technologies/jstl-documentation.html
- https://jcp.org/en/jsr/detail?xd_co_f=09ec3a41-b3f4-4b21-a917-90d5623c064d&id=52
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

{% highlight xml linenos %}
<project xmlns="http://maven.apache.org/POM/4.0.0" 
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
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

## Core Tags

Core tag itu taglib yang most commons you should know. Untuk penggunaanya kita harus import dalam file jsp seperti berikut:

{% highlight jsp linenos %}
<%@ taglib prefix = "c" uri = "http://java.sun.com/jsp/jstl/core" %>
{% endhighlight %}

Tag yang tersedia diantaranya meliputi seperti berikut:

| Tags          | Description   |
| :---          | :---          |
| `<c:out>`     | Perintahnya sama seperti `<%= ... %>` dalam jsp tetapi untuk expresion    |
| `<c:if>`      | Perintah sama seperti if statement hanya berbentuk xml                    |
| `<c:catch>`   | Perintah untuk menangkat throwable exception                              |
| `<c:choose>`  | Perintah conditional statement sama seperti `switch-case`                 |
| `<c:forEach>` | Perintah loop statement                                                   |
| `<c:url>`     | Perintah untuk menampilkan informasi URL, URI, servlet-context dll        |

Tag tersebut tidak seluruhnya saya tulis di materi ini, tetapi ini hanya yang sering kita gunakan saja jika temen-temen mau lebih lengkap silahkan baca artikelnya [disini](https://www.oracle.com/java/technologies/jstl-documentation.html)

Berikut adalah contoh penggunaannya:

{% gist page.gist "jstl-core.jsp" %}

## Formating Tags

Formating tags, yak ini sesuai dengan judulnya biasanya digunakan untuk melakukan transformasi data misalnya dari string ke tanggal atau sebaliknya. Untuk menggunakan formating kita perlu import taglib sebagai berikut:

{% highlight jsp linenos %}
<%@ taglib prefix = "formatter" uri = "http://java.sun.com/jsp/jstl/fmt" %>
{% endhighlight %}

| Tags                      | Description   |
| :---                      | :---          |
| `<fomatter:formatNumber>` | Untuk memformat number ke string dengan format misalnya currency, pecahan dan lain-lain |
| `<formatter:formatDate>`  | Untuk memformat date ke string dengan pattern tertentu    |
| `<formatter:parseNumber>` | Untuk memformat string ke number |
| `<formatter:parseDate>`   | Untuk memformat string ke date |
| `<formatter:message>`     | Untuk menampilkan i18n (Internationalization and localization) |

Tag diatas tidak semua saya tulis, masih ada tag lainnya tentang formatting. berikut adalah contoh penggunaanya:

{% gist page.gist "jstl-format.jsp" %}

dan berikut adalah file `messages` (Resource Bundle) untuk i18n yang disimpan di folder `src/main/resources`

{% gist page.gist "messages_en.properties" %}

{% gist page.gist "messages_in_ID.properties" %}

## SQL Tags

Untuk tag sql ini saya akan skip karena fitur ini saya gak pernah gunakan supaya gak include sql di dalam jsp. Dengan tag ini kita bisa memanggil data dari database dengan menggunakan format xml.


## XML tags

Untuk tag xml ini juga saya akan skip, karena fitur ini udah gak saya pake lagi tapi secara fungsi bisanya digunakan untuk memformat xml ke object class di java dan begitu pula sebaliknya.

## Function Tags

Untuk tag function ini ada beberapa function yang mungkin kita akan gunakan seperti untuk menge-check string mengandung karakter tertentu, atau menghintung jumlah kalimat tertentu dan lain-lain. Untuk menggunakan tag function kita harus import taglibnya seperti berikut:

{% highlight jsp linenos %}
<%@ taglib prefix = "fn" uri = "http://java.sun.com/jsp/jstl/functions" %>
{% endhighlight %}

| Tags                      | Description   |
| :---                      | :---          |
| `<fn:contains>`           | Untuk menge-check string mengandung karakter tertentu |
| `<fn:containsIgnoreCase>` | sama seperti containers tetapi tanpa case-sensitive   |
| `<fn:indexOf>`            | Check posisi index pada sebuah array                  |
| `<fn:length>`             | Menghitung jumlah dari array                          |

Dan masih banyak lagi.