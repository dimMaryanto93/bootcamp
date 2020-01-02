---
layout: post
title: "Group Function di PostgreSQL"
date: 2018-11-10T20:50:22+07:00
lang: psql
categories:
- RDBMS
- PostgreSQL
refs: 
- https://www.postgresql.org/docs/9.5/functions-aggregate.html
youtube: 
comments: true
---

Pada dasarnya group function, akan memproses banyak data kemudian menterjemahkannya menjadi satu result seperti berikut ilustrasinya:

![group function]({{site.baseurl}}/resources/posts/psql-group-by/konsep-group-funcation.png)

Ada beberapa function yang kita bisa gunakan, diataranya seperti berikut:

| Function  | Keterangan                        |
|:----------|:----------------------------------|
| `AVG()`   | Menghitung nilai rata             |
| `COUNT()` | Menghitung jumlah baris           |
| `MAX()`   | Menghitung nilai maximum          |
| `MIN()`   | Menghitung nilai minimum          |
| `SUM()`   | Menjumlahkan total                |

Lebih lengkapnya bisa baca dokumentasi [agregate function](https://www.postgresql.org/docs/9.5/functions-aggregate.html). Dan berikut contoh implementasinya:

{% highlight sql linenos %}
select
    round(avg(salary), 2) as rata2_gaji,
    count(*) as jml_baris,
    max(salary) as max_salary,
    min(salary) as min_salary,
    sum(salary) as total_salary
from employees;
{% endhighlight %}

Berikut hasilnya:

```postgresql-console
 rata2_gaji | jml_baris | max_salary | min_salary | total_salary 
------------+-----------+------------+------------+--------------
    6461.68 |       107 |   24000.00 |    2100.00 |    691400.00
(1 row)
```