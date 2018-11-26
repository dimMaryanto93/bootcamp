---
layout: post
title: "Memahami perintah Outer Join di PostgreSQL"
date: 2018-11-20T12:15:12+07:00
lang: psql
categories:
- RDBMS
- PostgreSQL
gist: 
youtube: 
comments: true
---

Dengan klausa `join` ada juga kondisi lain, jika sebelumnya menggunakan `inner join` hanya mendapatkan data yang ada di antara kedua tabel atau istilahnya irisan. Ada juga kodisi yaitu dengan `outter join` seperti berikut ilustrasinya:

![diagram join]({{site.baseurl}}/resources/posts/psql-join/outer-join-definision.png)

Berikut contoh kasus dalam bentuk gambar:

![contoh data right join]({{site.baseurl}}/resources/posts/psql-join/outer-join.png)

Berikut contoh penggunaan, 

**Menggunakan `left join`**

{% highlight sql linenos %}
select
    d.department_id as kode_department,
    d.department_name as nama_department,
    l.location_id as kode_lokasi,
    l.street_address as alamat
from 
    locations l left join departments d on (l.location_id = d.location_id);
{% endhighlight %}

Berikut hasilnya:

```postgresql-console
 kode_department |   nama_department    | kode_lokasi |                  alamat                  
-----------------+----------------------+-------------+------------------------------------------
             300 | System Analis        |        1700 | 2004 Charade Rd
              10 | Administration       |        1700 | 2004 Charade Rd
              20 | Marketing            |        1800 | 147 Spadina Ave
              30 | Purchasing           |        1700 | 2004 Charade Rd
             110 | Accounting           |        1700 | 2004 Charade Rd
             120 | Treasury             |        1700 | 2004 Charade Rd
             130 | Corporate Tax        |        1700 | 2004 Charade Rd
             140 | Control And Credit   |        1700 | 2004 Charade Rd
             150 | Shareholder Services |        1700 | 2004 Charade Rd
             160 | Benefits             |        1700 | 2004 Charade Rd
             250 | Retail Sales         |        1700 | 2004 Charade Rd
             260 | Recruiting           |        1700 | 2004 Charade Rd
             270 | Payroll              |        1700 | 2004 Charade Rd
                 |                      |        2900 | 20 Rue des Corps-Saints
                 |                      |        1600 | 2007 Zagora St
                 |                      |        1100 | 93091 Calle della Testa
                 |                      |        2300 | 198 Clementi North
                 |                      |        3100 | Pieter Breughelstraat 837
                 |                      |        3000 | Murtenstrasse 921
                 |                      |        1300 | 9450 Kamiya-cho
                 |                      |        1900 | 6092 Boxwood St
...
(44 rows)
```

**Menggunakan `right join`**

{% highlight sql linenos %}
select
    d.department_id as kode_department,
    d.department_name as nama_department,
    l.location_id as kode_lokasi,
    l.street_address as alamat
from 
    locations l right join departments d on (l.location_id = d.location_id);
{% endhighlight %}

Berikut hasilnya:

```postgresql-console
 kode_department |   nama_department    | kode_lokasi |                  alamat                  
-----------------+----------------------+-------------+------------------------------------------
             300 | System Analis        |        1700 | 2004 Charade Rd
              10 | Administration       |        1700 | 2004 Charade Rd
              20 | Marketing            |        1800 | 147 Spadina Ave
              30 | Purchasing           |        1700 | 2004 Charade Rd
              40 | Human Resources      |        2400 | 8204 Arthur St
              50 | Shipping             |        1500 | 2011 Interiors Blvd
              60 | IT                   |        1400 | 2014 Jabberwocky Rd
             190 | Contracting          |        1700 | 2004 Charade Rd
             200 | Operations           |        1700 | 2004 Charade Rd
             210 | IT Support           |        1700 | 2004 Charade Rd
             220 | NOC                  |        1700 | 2004 Charade Rd
             230 | IT Helpdesk          |        1700 | 2004 Charade Rd
             240 | Government Sales     |        1700 | 2004 Charade Rd
             250 | Retail Sales         |        1700 | 2004 Charade Rd
             260 | Recruiting           |        1700 | 2004 Charade Rd
             270 | Payroll              |        1700 | 2004 Charade Rd
...
(28 rows)
```

**Menggunakan `inner join`**

{% highlight sql linenos %}
select
    d.department_id as kode_department,
    d.department_name as nama_department,
    e.employee_id as kode_karyawan,
    concat(e.first_name, ' ', e.last_name) as nama_karyawan
from 
    employees e inner join departments d on (e.department_id = d.department_id);
{% endhighlight %}


Berikut hasilnya:

```postgresql-console
 kode_department | nama_department  | kode_karyawan |   nama_karyawan   
-----------------+------------------+---------------+-------------------
              90 | Executive        |           100 | Steven King
              90 | Executive        |           101 | Neena Kochhar
              90 | Executive        |           102 | Lex De Haan
              60 | IT               |           103 | Alexander Hunold
              60 | IT               |           104 | Bruce Ernst
              60 | IT               |           105 | David Austin
              60 | IT               |           106 | Valli Pataballa
              60 | IT               |           107 | Diana Lorentz
              50 | Shipping         |           125 | Julia Nayer
              50 | Shipping         |           126 | Irene Mikkilineni
              50 | Shipping         |           127 | James Landry
              50 | Shipping         |           128 | Steven Markle
              50 | Shipping         |           129 | Laura Bissot
              50 | Shipping         |           130 | Mozhe Atkinson
              50 | Shipping         |           131 | James Marlow
              50 | Shipping         |           132 | TJ Olson
              50 | Shipping         |           133 | Jason Mallin
...
(106 rows)
```