---
layout: post
title: "Organisasi class file dengan package"
date: 2017-11-14T23:04:06+07:00
lang: java-core
categories:
- Java
- Core
refs: []
youtube: 
comments: true
---

Semakin lama, aplikasi yang kita develop khan pasti semakin besar dan semakin banyak file _class_. Nah untuk itu kita bisa organisasi _source code_ kita dengan _package_ atau _file class_ dimasukan kedalam folder. Jadi sebelum-sebelumnya struktur direktor kita seperti berikut:

```bash
[ ~/Documents/package ] 
 ➜ tree .
.
└── src
    ├── Quis2Latihan1.java
    ├── Quis2Latihan2.java
    ├── Quis2Latihan3.java
    ├── QuisLatihan1.java
    └── QuisLatihan2.java

1 directory, 5 files
```

Alangkah lebih baik jika kita menggunakan folder seperti berikut:

```bash
[ ~/Documents/package ] 
 ➜ tree .
.
└── src
    ├── latihan1
    │   ├── QuisLatihan1.java
    │   └── QuistLatihan2.java
    └── latihan2
        ├── Quis2Latihan1.java
        ├── Quis2Latihan2.java
        └── Quis2Latihan3.java

3 directories, 5 files
```

Bagaimana? terlihat lebih teroraganisasi khan ya? trus bagaimana didalamnya? apakah koding ada perubahan?

Ok ok, sebentar ya kita bahasa satu persatu.

1. Terlihat _file_ lebih rapih? mudah dicari? jawabanyanya tentu. dengan menggunakan folder tentu saja akan mudah dicari yang terpenting adalah penulisan keyword pada folder tersebut harus tepat.
2. Apakah ada perubahan di sisi koding? ada tetapi tidak secara keseluruhan hanya ada beberapa tambahan keyword saja yaitu `package` dan jika ada _class_ yang berada di luar package tersebut menggunakan `import`.

Berikut adalah salah satu contoh implementasinya dari konsep diatas:

## QuisLatihan1

{% highlight java linenos %}
package latihan1;

public class QuisLatihan1 {

    // statement here
    public String name(){
        return "Dimas Maryanto";
    }
}
{% endhighlight %}

## Quis2Latihan3

{% highlight java linenos %}
package latihan2;

import latihan1.QuisLatihan1;

public class Quis2Latihan3 {

    public void useOtherClass(){
        QuisLatihan1 lat = new QuisLatihan1();
        System.out.print(lat.name());
    }
}
{% endhighlight %}