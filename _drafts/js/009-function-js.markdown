---
layout: post
title: "Function di JavaScript"
lang: js
categories:
- web
- js
refs: 
- https://developer.mozilla.org/en-US/docs/Web/JavaScript
youtube: 
comments: true
gist: dimMaryanto93/b956151354fb8a1454d3b36d22d61a63
---

seperti yang ketahui JavaScript ini tidak mengenal yang namanya `Class` sebagai gantinya kita bisa menggunakan function sebagai pembungkusnya.

Sekarang kita akan membuat function di JavaScript format dasarnya kurang lebih seperti berikut:

{% gist page.gist "function-basic.js" %}

Jadi disini untuk membuat function kita cukup gunakan keyword `function` kemudian diikuti dengan nama functionnya contohnya seperti diatas `halo` setelah itu untuk memanggil fungsi tersebut atau menjalankannya seperti berikut:

```js
halo();
```

Lanjut, sekarang kita akan membuat function dengan menggunakan parameter atau arguments, arguments ini digunakan untuk meng-inject sebuah atau beberapa nilai ke dalam variable supaya dikenali di dalam function tersebut contohnya seperti berikut:

{% gist page.gist "function-args.js" %}

Jadi koding di atas kita melakukan perkalian berdasarkan `bil1` dan `bil2` yang di inject dari luar nilainya kemudian mengembalikan nilanya dengan menggunakan keyword `return`. Selain itu ada hal unique yang bisa dilakukan di JavaScript yaitu function dalam function seperti berikut:

{% gist page.gist "function-inner-function.js" %}

Nah jadi disini kesimpulannya dengan menggunakan function kita bisa me reuseable atau menggunakannya secara berkali-kali tanpa perlu menulis ulang kode programnya dari awal cukup dengan memanggil fungsinya saja.