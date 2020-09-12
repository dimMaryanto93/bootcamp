---
layout: post
title: "Pemberian alias pada kolom atau tabel"
date: 2017-11-27T11:05:09+07:00
lang: psql
categories:
- RDBMS
- PostgreSQL
refs: []
youtube: https://www.youtube.com/watch?v=Ws8ZVcer0Kw&list=PLV1-tdmPblvypZXSk2GC932nludT345xk&index=3
comments: true
---

Secara _default_ kalau kita melakukan perintah `select` terhadap suatu _table_ contohnya misalnya `departments`, di _table_ `departments` ada _columns_ diataranya `department_id, department_name, manager_id, location_id` jika saya melakukan perintah `select` seperti berikut:

{% highlight postgresql linenos %}
select * from departments
{% endhighlight %}

Maka secara default nama _columns_ yang ditampilkan akan sesuai dengan nama asli dari _column_ yang ada di tabel `departments` seperti berikut:

{% highlight postgresql %}
 department_id |   department_name    | manager_id | location_id 
---------------+----------------------+------------+-------------
           300 | System Analis        |            |        1700
            10 | Administration       |        200 |        1700
            20 | Marketing            |        201 |        1800
            30 | Purchasing           |        114 |        1700
            40 | Human Resources      |        203 |        2400
            50 | Shipping             |        121 |        1500
            60 | IT                   |        103 |        1400
{% endhighlight %}

## Memberikan alias untuk _column_

Dengan menggunakan _column alias_ kita bisa memberikan nama kolomnya sesuai yang kita inginkan, contohnya seperti berikut:

{% highlight postgresql linenos %}
select 
    -- menggunakan keyword as, untuk mendefinisikan sebagai variable
    department_id as kode_divisi,
    -- tanpa menggunakan keyword as
    department_name nama_department,
    -- menggunakan nama kolom custome
    manager_id as "Kode Manager"  
from departments
{% endhighlight %}

Maka hasilnya seperti berikut:

{% highlight postgresql %}
 kode_department |   nama_deparment    | Kode Manager | 
---------------+----------------------+------------+
           300 | System Analis        |            |
            10 | Administration       |        200 |
            20 | Marketing            |        201 |
            30 | Purchasing           |        114 |
            40 | Human Resources      |        203 |
            50 | Shipping             |        121 |
            60 | IT                   |        103 |
{% endhighlight %}

Aturan penamaan variable atau kolom alias, diantaranya:

Jika menggunakan keyword `as` dan tanpa `as`, tidak boleh menggunakan charakter khusus seperti **SPACE**, **HashTag**, **Dolar** dan lain-lain, karakter yang **diperbolehkan** yaitu **huruf, angka, dan underscore**. Ini karena dengan menggunakan _column alias_ tersebut nantinya bisa digunakan sebagai variable untuk melakukan _ordering_.
