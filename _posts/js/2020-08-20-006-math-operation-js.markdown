---
layout: post
title: "Operator Matematika di JavaScript"
date: 2020-08-20T16:48:03+07:00
lang: js
categories:
- web
- js
refs: 
- https://developer.mozilla.org/en-US/docs/Web/JavaScript
youtube: https://www.youtube.com/watch?v=RhGx1tx4YRU&list=PLV1-tdmPblvyDBVppluBbB_4ryZvjDWvv&index=6
comments: true
gist: dimMaryanto93/b956151354fb8a1454d3b36d22d61a63
---

Operator pada dasarnya dibagi 3 yaitu 
1. Aritmatika, 
2. Assignment dan 
3. Bitwise. 

Kali ini saya mau membahas dulu tentang assignment atau penugasan (inisialisasi).

ok sekarang coba perhatikan contoh koding berikut ini:

{% gist page.gist "assignment.js" %}

Seperti yang dijelaskan di postingan sebelumnya penugasan adalah memberikan nilai ke variable lainnya. Hanya di disini ada yang unique dari bahasa JavaScript, kenapa unique? contohnya terlihat dari koding baris ke 7. kita melakukan concat dengan berbeda tipe data yaitu string dan number tpi hasil akhirnya menjadi string.

Selanjutnya kita akan membahas tentang aritmatika atau perhitungan matematika seperti pertambahan, pengurangan, perkalian, pembagian dan lain-lain seperti berikut:

{% gist page.gist "aritmath.js" %}

Berikut ini hasilnya:

{% highlight bash %}
bil1 : 10; bil2 : 20;

bil1 + bil2 : 30
bil1 x bil2 : 200
bil1 / bil2 : 0.5
bil1 - bil2 : -10
Math.sqrt(bil1) : 3.1622776601683795
bil1+= 1 : 11
bil2-= 2 : 18
{% endhighlight %}