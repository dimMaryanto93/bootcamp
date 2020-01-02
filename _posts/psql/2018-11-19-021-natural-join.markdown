---
layout: post
title: "Mamahami perintah Natural Join di PostgreSQl"
date: 2018-11-19T21:14:34+07:00
lang: psql
categories:
- RDBMS
- PostgreSQL
refs: []
youtube: 
comments: true
---

Natural join, query yang paling mudah untuk menerapkan join tetapi ada syaratnya yaitu:

1. Diantara tabel yang berelasi, column name harus sama
2. Harus memiliki `constraint` foreign key

Contohnya saya ingin menampilakan. selurauh data location  yang ditampilkan adalah `location_id`, `city`, `state_province`, `country_name` yang diambil dari table `countries`. Berikut querynya:

{% highlight sql linenos %}
select 
    l.location_id kode_lokasi,
    l.city as kota,
    l.state_province as provinsi,
    c.country_name as negara
from 
    locations l natural join countries c;
{% endhighlight %}

Berikut hasilnya:

```postgresql-console
 kode_lokasi |        kota         |     provinsi      |          negara          
-------------+---------------------+-------------------+--------------------------
        1000 | Roma                |                   | Italy
        1100 | Venice              |                   | Italy
        1200 | Tokyo               | Tokyo Prefecture  | Japan
        1300 | Hiroshima           |                   | Japan
        1400 | Southlake           | Texas             | United States of America
        1500 | South San Francisco | California        | United States of America
        1600 | South Brunswick     | New Jersey        | United States of America
        1700 | Seattle             | Washington        | United States of America
        1800 | Toronto             | Ontario           | Canada
        1900 | Whitehorse          | Yukon             | Canada
        2000 | Beijing             |                   | China
        2100 | Bombay              | Maharashtra       | India
        2200 | Sydney              | New South Wales   | Australia
        2300 | Singapore           |                   | Singapore
        2400 | London              |                   | United Kingdom
        2500 | Oxford              | Oxford            | United Kingdom
        2600 | Stretford           | Manchester        | United Kingdom
        2700 | Munich              | Bavaria           | Germany
        2800 | Sao Paulo           | Sao Paulo         | Brazil
        2900 | Geneva              | Geneve            | Switzerland
        3000 | Bern                | BE                | Switzerland
        3100 | Utrecht             | Utrecht           | Netherlands
        3200 | Mexico City         | Distrito Federal, | Mexico
(23 rows)
```