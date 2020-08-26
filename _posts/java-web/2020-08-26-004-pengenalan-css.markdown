---
layout: post
title: "Pengenalan Styling dengan CSS"
date: 2020-08-26T21:35:11+07:00
lang: java-web
categories:
- java
- web
- war
refs: 
- https://www.w3schools.com/css/default.asp
youtube: 
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-004
---

Untuk memberikan warna berbeda pada halaman HTML kita bisa melakukan styling menggunakan CSS atau **Cascade Style Sheets**. Dalam menggunakan CSS harus tau dulu apa itu **selector** dan jenis dari **selector**

## Selector

Macam macam seletor dalam penggunakan Javascript yaitu

1. by id -> `#property-id { ... }`
2. by class name -> `.property-class { ... }`
3. by element -> `input { ... }`, `body { ... }` dan lain-lain.
4. by attribut -> `[target] { ... }`
5. by all element -> `* { ... }`

## Menggunakan CSS

Untuk menggunakan CSS kita bisa menggunakan 2 cara yaitu dengan inline style dan include style

{% highlight html linenos %}
<html>
<head>
<style>
    #default {
        color: black;
        background-color: red;
    }
</style>
</head>
<body>
    <!-- inline style -->
    <p style="color: red; background-color: black;">Ini text warna merah dan backgroud hitam</p>

    <hr>

    <p id="default">Ini text warna hitam dan backgrond merah</p>
</body>
</html>
{% endhighlight %}

## CSS Framework

Selain kita bisa membuat sendiri style-nya kita juga bisa menggunakan framework yang ada seperti:

1. [Bootstrap](https://getbootstrap.com/)
2. [Materialize](https://materializecss.com/)
3. [Fondation](https://get.foundation/)
4. [Semantic UI](https://semantic-ui.com/)
5. Dan masih banyak lagi