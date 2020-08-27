---
layout: post
title: "Pengenalan Pemograman Client Side dengan JS"
date: 2020-08-27T22:19:05+07:00
lang: java-web
categories:
- java
- web
- war
refs: []
youtube: 
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-005
---

Client side programming dalam 1 decade terakhir memang sedang jadi perbincangan, lantas apakah kita harus menggunakan?

> Jawabanya bisa iya bisa juga gak, ya klo saya lebih konsern dengan kebutuhan. Artinya kalo kita mau buat aplikasi kita prosesnya dilakukan di setiap client baru kita gunakan contohnya seperti validasi, prediksi perhitungan dan lain-lain.

Dengan adanya client side proccessing ini ada benefit dan kekuranganya:

## Kelebihan meng-kombine Server dan Client side

1. Mengurangi request ke server
2. Terlihat lebih responsif dan interactive

## Kekurangan 

1. Kita harus memastikan bahwa client (browser) support dengan yang kita develop.
2. Terkadang file js masih di cache oleh browser, padahal filenya sudah tidak dibutuhkan ([resource cache](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching))

## Penggunaan Javascript dalam HTML

Untuk menggunakan js dalam HTML, bisa dilakukan dengan dalam html atau dibuat file terpisah yang kemudian di include di HTML seperti berikut:

{% highlight html linenos %}
<!DOCTYPE html>
<html>
  <head>
    <title>Parcel Sandbox</title>
    <meta charset="UTF-8" />
    <!-- inline javascript -->
    <script lang="application/js">
      function onButtonClick() {
      	alert("button clicked!");
      }
    </script>
  </head>

  <body>
    <div id="app">Ini text dari html</div>
    <input type="text" name="nama" id="nama" />
    <button type="button" onclick="onButtonClick()">Kirim</button>
  </body>
  <!-- include javascript -->
  <script src="src/index.js"></script>
</html>

{% endhighlight %}

berikut adalah file jsnya dengan nama `index.js`:

{% highlight js linenos %}
document.title = "Belajar Javascript";

var divElement = document.getElementById("app");
divElement.innerHTML = "Halo ini saya dari Javascript " + new Date();
{% endhighlight %}

## Javascript Framework

Jaman sekarang udah banyak sekali javascript framework, ada yang bisa combine dengan teknologi server side seperti:

1. [JQuery](https://jquery.com/)
2. [AngularJS](https://angularjs.org/)
3. [VueJS](https://vuejs.org/)

Atau ada bisa juga kita buat 2 state berbeda dengan front-end dan back-end seperti:

1. [AngularJS](https://angularjs.org/)
2. [VueJS](https://vuejs.org/)
3. [Angular](https://angular.io/)
4. [ReactJS](https://reactjs.org/)