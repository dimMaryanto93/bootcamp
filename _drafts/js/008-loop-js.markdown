---
layout: post
title: "Perulangan atau Looping dengan JavaScript"
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

perulangan sebenarnya juga gak ada yang aneh kurang lebih sama seperti bahasa pemograman yang lain contohnya perulangan menggunakan `for`, `do-while`, `while` dan `for-in`.

## Perulangan dengan FOR

perulangan dengan for basicnya sama seperti biasa yaitu seperti berikut contohnya:

{% gist page.gist "for-loop.js" %}

Jika dijalakan outputnya akan menghasilkan `halo ini pesan ke x` sebangak 10x  dan `x` akan diganti dari nilainya menjadi `1` sampai `10`

## Perulangan dengan WHILE

Perulangan dengan while pada dasarnya dibagi menjadi 2 yaitu `while` dan `do-while` sekarang kita buat dulu yang `while` seperti berikut:

{% gist page.gist "while-loop.js" %}

Jika dihasilkan maka akan menampilkan output `loop ke x` sebanyak 10x dan nilai `x` bernilai dari `1` sampai `10`, sedangkan untuk `do-while` seperti berikut:

{% gist page.gist "dowhile-loop.js" %}

Kalo di jakankan kurang lebih sama dengan perulangan while hanya bedanya adalah klo `do-while` dia perulangannya dikerjakan terlebih dahulu baru diseleksi.