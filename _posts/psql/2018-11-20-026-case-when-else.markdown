---
layout: post
title: "Seleksi dengan Case When di PostgreSQL"
date: 2018-11-20T13:22:23+07:00
lang: psql
categories:
- RDBMS
- PostgreSQL
refs: []
youtube: https://www.youtube.com/watch?v=ZzXOMSeExHA&list=PLV1-tdmPblvypZXSk2GC932nludT345xk&index=20
comments: true
---

Di sql juga, bisa melakukan seleksi sama halnya dengan bahasa pemograman dengan `if/else` berikut contoh perintahnya:

```sql
CASE WHEN condition THEN result
     [WHEN ...]
     [ELSE result]
END
```

Berikut contoh,

{% highlight sql linenos %}
select
    employee_id as kode_karyawan,
    commission_pct as besar_komisi,
    case    
        when COALESCE(commission_pct, 0) = 0 
            then 'Tidak memiliki komisi'
        else 
            concat('Memiliki komisi sebesar ', commission_pct)
    end as deskripsi
from 
    employees;
{% endhighlight %}

Berikut hasilnya:

```postgresql-console
 kode_karyawan | besar_komisi |          deskripsi           
---------------+--------------+------------------------------
           100 |              | Tidak memiliki komisi
           101 |              | Tidak memiliki komisi
           102 |              | Tidak memiliki komisi
           103 |              | Tidak memiliki komisi
           104 |              | Tidak memiliki komisi
           105 |              | Tidak memiliki komisi
           106 |              | Tidak memiliki komisi
           145 |         0.40 | Memiliki komisi sebesar 0.40
           146 |         0.30 | Memiliki komisi sebesar 0.30
           147 |         0.30 | Memiliki komisi sebesar 0.30
           148 |         0.30 | Memiliki komisi sebesar 0.30
           149 |         0.20 | Memiliki komisi sebesar 0.20
           150 |         0.30 | Memiliki komisi sebesar 0.30
           151 |         0.25 | Memiliki komisi sebesar 0.25
           152 |         0.25 | Memiliki komisi sebesar 0.25
           153 |         0.20 | Memiliki komisi sebesar 0.20
           154 |         0.20 | Memiliki komisi sebesar 0.20
           155 |         0.15 | Memiliki komisi sebesar 0.15
           156 |         0.35 | Memiliki komisi sebesar 0.35
           157 |         0.35 | Memiliki komisi sebesar 0.35
           158 |         0.35 | Memiliki komisi sebesar 0.35
...
(107 rows)
```