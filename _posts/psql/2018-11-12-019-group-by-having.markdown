---
layout: post
title: "Klausa having dan where dalam select"
date: 2018-11-12T15:58:05+07:00
lang: psql
categories:
- RDBMS
- PostgreSQL
refs: []
youtube: 
comments: true
---

Untuk filter data dengan klausa `where` di dalam `group by` secara ilustrasi bisa digambarkan seperti berikut:

![ilustrasi filter dengan where]({{site.baseurl}}/resources/posts/psql-group-by/konsep-group-by-where.png)

Jadi klausa dengan `whare` dia prosesnya akan melakukan filter terlebih dahulu sebelum dilakukan proses `group by`. berikut contoh kasusnya, Tampilkan jumlah karyawan yang memiliki gaji perbulan lebih sebesar sama dengan `5000` kemudian kategorikan berdasarkan `manager_id`. Berikut querynya:

{% highlight sql linenos %}
select 
    manager_id, 
    count(*) as jumlah_karyawan
from employees
    where salary >= 5000
group by manager_id
order by manager_id;
{% endhighlight %}

Berikut hasilnya:

```postgresql_console
 manager_id | jumlah_karyawan 
------------+-----------------
        100 |              14
        101 |               4
        102 |               1
        103 |               1
        108 |               5
        145 |               6
        146 |               6
        147 |               6
        148 |               6
        149 |               6
        201 |               1
        205 |               1
            |               1
(13 rows)
```

Sekarang, bagaimana jika saya mau filternya setelah di `group by` maka gunakan `having` berikut ilustrasinya:

![ilustrasi having]({{site.baseurl}}/resources/posts/psql-group-by/konsep-group-by-having.png)

contoh kasusnya seperti berikut. Tampilkan jumlah karyawan per `manager_id` kemudian filter data karyawan yang jumlahnya lebih dari sama dengan `5`. Berikut querynya:

{% highlight sql linenos %}
select 
    manager_id,
    count(*) as jumlah_karyawan
from employees
group by manager_id
    having count(*) >= 5
order by manager_id;
{% endhighlight %}

Berikut hasilnya:

```postgresql-console
 manager_id | jumlah_karyawan 
------------+-----------------
        100 |              14
        101 |               5
        108 |               5
        114 |               5
        120 |               8
        121 |               8
        122 |               8
        123 |               8
        124 |               8
        145 |               6
        146 |               6
        147 |               6
        148 |               6
        149 |               6
(14 rows)
```

Selain itu juga kita gunakan filter `having` dan `whare` secara bersamaan contohnya seperti berikut:

{% highlight sql linenos %}
select 
    manager_id, 
    count(*) as jumlah_karyawan
from employees
    where salary >= 5000
group by manager_id
    having count(*) >= 5
order by manager_id;
{% endhighlight %}

Berikut hasilnya:

```postgresql-console
 manager_id | jumlah_karyawan 
------------+-----------------
        100 |              14
        108 |               5
        145 |               6
        146 |               6
        147 |               6
        148 |               6
        149 |               6
(7 rows)
```