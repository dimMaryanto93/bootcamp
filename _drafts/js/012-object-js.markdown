---
layout: post
title: "Object Oriented Programming dengan Javascript"
lang: js
categories:
- web
- js
refs: 
- https://developer.mozilla.org/en-US/docs/Web/JavaScript
youtube: 
comments: true
gist: dimMaryanto93/b956151354fb8a1454d3b36d22d61a63
image_path: /resources/posts/js-6
---

JavaScript is Object Oriented Programming. Untuk menulis object di JavaScript ada banyak cara yaitu cara paling sederhana adalah seperti berikut:

```js
var mhs = { key:"value" };
```

dan untuk mengakses object tersebut adalah seperti berikut:

```js
console.log("get value from key is "+ mhs.key);
```

Contoh lainya adalah seperti berikut:

{% gist page.gist "intro-obj.js" %}

Output yang dihasilkan seperti berikut:

![intro obj hasilnya]({{site.baseurl}}{{ page.image_path }}/intro-obj-1.png)

Nah jadi object ini sama konsepnya seperti map di Java jadi memiliki key dan value. keynya harus bersifat unique dan direkomendasikan untuk menggunakan hurus di awal sama halnya seperit kita membuat variable. Dan klo anda perhatikan object yang kita buat formatnya mengerupai dengan JSON.
