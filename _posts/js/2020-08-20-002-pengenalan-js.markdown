---
layout: post
title: "Pengenalan scripting language dengan Javascript"
date: 2020-08-20T16:47:51+07:00
lang: js
categories:
- web
- js
refs: 
- https://developer.mozilla.org/en-US/docs/Web/JavaScript
youtube: 
comments: true
---

## Apa itu Javascript?

> Menurut MDN (Mozilla Developer Network) JavaScript (JS) is a lightweight, interpreted, programming language with first-class functions. While it is most well-known as the scripting language for Web pages, many non-browser environments also use it, such as node.js and Apache CouchDB. JS is a prototype-based, multi-paradigm, dynamic scripting language, supporting object-oriented, imperative, and declarative (e.g. functional programming) styles.

Dari penjelasan diatas coba kita extract kalimat berikut lightweight, interpreted, programming language with first-class functions.

1. Lightweight, JavaScript adalah bahasa pemograman yang ringan dan portable magsudnya protable artinya tidak tergantung pada bahasa bahasa pemograman lain dan bisa juga diintegrasikan seperti PHP <-> JavaScript, Java Web <-> JavaScript, Ruby <-> JavaScript dll.
2. Interpreted, JavaScript tidak membutuhkan compiler seperti di Java atau C++ makanya disebut Interpreted
3. first-class functions.

## Kapan kita membutuhkan Javascript?

1. Biasanya JavaScript digunakan untuk melakukan validasi disisi client, jadi sebelum data di kirim ke server atau web server data tersebut telah di validasi terlebih dahulu sehingga tidak membuat proses server overload karana bolak balik (request -> response)
2. JavaScript akan menghasilkan DOM (Domain Object Model) yang Dinamic.
3. Selain itu juga dengan javascript content dari aplikasi web kita bisa bersifat **responsif** bisa dalam bentuk animasi atau multiplatform seperti jika di dekstop tampilanya lebar jika di mobile atau table tampilannya lebih kecil dari yang versi desktop.

## Javascript server-side vs client-side

JavaScript jaman sekarang tidak hanya digunakan untuk client side tetapi juga bisa untuk server side berikut adalah framework yang paling banyak digunakan:

1. Server side
- [NodeJS](https://nodejs.org/en/)
- [EmberJS](http://emberjs.com/)

2. Client side
- [Angular](https://angular.io/)
- [VueJS](https://vuejs.org/)
- [ReactJS](https://reactjs.org/)
- [JQuery](https://jquery.com/)
