---
layout: post
title: "Operator pada klausa where di PostgreSQL"
date: 2018-11-09T20:40:04+07:00
lang: psql
categories:
- RDBMS
- PostgreSQL
refs: []
youtube: https://www.youtube.com/watch?v=7MLBNM576gA&list=PLV1-tdmPblvypZXSk2GC932nludT345xk&index=8
comments: true
---

Operator kondisi pada where di PostgreSQL teridiri dari:

| Symbol                        | Keterangan |
| `=`                           | Melakukan perbandingan dengan nilai yang **bernilai sama** |
| `!=`                          | Melakukan perbandingan dengan nilai yang **bernilai tidak sama** |
| `<>`                          | Melakukan perbandingan dengan nilai yang **bernilai tidak sama** |
| `>`                           | Melakukan perbandingan terhadap 2 variable apakah variable yang satu **lebih besar** dari variable lainnya |
| `>=`                          | Melakukan perbandingna terhadap 2 variable apakah variable yang satu **lebih besar atau sama dengan** variable lainnya |
| `<`                           | Kebalikan dari symbol `>` yaitu **lebih kecil** |
| `<=`                          | Kebalikan dari symbol `>=` yaitu **lebih kecil atau sama dengan** |
| `LIKE`                        | Melakukan perbadingan dengan nilai yang bernilai sama menggunakan expresion seperti `%`, `_` |
| `IN`                          | Melakukan perbandingan terhadap multi data  |
| `BETWEEN ... AND ...`         | Melakukan perbandingan diantara nilai terbesar dan terkecil |
| `IS NULL`                     | Mencari nilai yang **bernilai null** |
{:.bordered .striped}

Ok sekarang kita bahas satu persatu operator-operator yang telah saya jabarkan diatas untuk memperjelas dan cara bagimana contoh kasusnya.

# Operator equals

Berikut contoh kasus, untuk mencari data pegawai dengan kode yang sama dengan `100` berikut querynya:

{% highlight sql linenos %}
select employee_id, first_name, last_name, email, phone_number, job_id, salary
from employees 
where employee_id = 100;
{% endhighlight %}

Berikut ini hasilnya:

```postgresql-console
 employee_id | first_name | last_name | email | phone_number | job_id  |  salary  | 
-------------+------------+-----------+-------+--------------+---------+----------+
         100 | Steven     | King      | SKING | 515.123.4567 | AD_PRES | 24000.00 |
(1 row)
```

# Operator not equals

Berikut contoh kasus, untuk mencari data pegawai dengan jabatan yang bukan merupakan `IT_PROG`. berikut querynya:

Menggunakan operator `<>`

{% highlight sql linenos %}
select employee_id, first_name, last_name, email, phone_number, job_id, salary
from employees 
where job_id <> 'IT_PROG';
{% endhighlight %}

Menggunakan operator `!=`

{% highlight sql linenos %}
select employee_id, first_name, last_name, email, phone_number, job_id, salary
from employees 
where job_id != 'IT_PROG';
{% endhighlight %}

Berikut ini hasilnya:

```postgresql-console
 employee_id | first_name  |  last_name  |  email   |    phone_number    |   job_id   |  salary  |
-------------+-------------+-------------+----------+--------------------+------------+----------+
         100 | Steven      | King        | SKING    | 515.123.4567       | AD_PRES    | 24000.00 |
         101 | Neena       | Kochhar     | NKOCHHAR | 515.123.4568       | AD_VP      | 17000.00 |
         102 | Lex         | De Haan     | LDEHAAN  | 515.123.4569       | AD_VP      | 17000.00 |
         108 | Nancy       | Greenberg   | NGREENBE | 515.124.4569       | FI_MGR     | 12000.00 |
         109 | Daniel      | Faviet      | DFAVIET  | 515.124.4169       | FI_ACCOUNT |  9000.00 |
         110 | John        | Chen        | JCHEN    | 515.124.4269       | FI_ACCOUNT |  8200.00 |
         111 | Ismael      | Sciarra     | ISCIARRA | 515.124.4369       | FI_ACCOUNT |  7700.00 |
         112 | Jose Manuel | Urman       | JMURMAN  | 515.124.4469       | FI_ACCOUNT |  7800.00 |
         113 | Luis        | Popp        | LPOPP    | 515.124.4567       | FI_ACCOUNT |  6900.00 |
         114 | Den         | Raphaely    | DRAPHEAL | 515.127.4561       | PU_MAN     | 11000.00 |
         115 | Alexander   | Khoo        | AKHOO    | 515.127.4562       | PU_CLERK   |  3100.00 |
         116 | Shelli      | Baida       | SBAIDA   | 515.127.4563       | PU_CLERK   |  2900.00 |
         117 | Sigal       | Tobias      | STOBIAS  | 515.127.4564       | PU_CLERK   |  2800.00 |
         118 | Guy         | Himuro      | GHIMURO  | 515.127.4565       | PU_CLERK   |  2600.00 |
         119 | Karen       | Colmenares  | KCOLMENA | 515.127.4566       | PU_CLERK   |  2500.00 |
...
(102 rows)
```

# Operator more than

Berikut contoh kasus, untuk mencari data pegawai dengan gaji yang lebih besar dari `12000`. berikut querynya:

{% highlight sql linenos %}
select employee_id, first_name, last_name, email, phone_number, job_id, salary
from employees 
where salary > 12000;
{% endhighlight %}

Berikut hasilnya:

```postgresql-console
 employee_id | first_name | last_name |  email   |    phone_number    | job_id  |  salary  
-------------+------------+-----------+----------+--------------------+---------+----------
         100 | Steven     | King      | SKING    | 515.123.4567       | AD_PRES | 24000.00
         101 | Neena      | Kochhar   | NKOCHHAR | 515.123.4568       | AD_VP   | 17000.00
         102 | Lex        | De Haan   | LDEHAAN  | 515.123.4569       | AD_VP   | 17000.00
         145 | John       | Russell   | JRUSSEL  | 011.44.1344.429268 | SA_MAN  | 14000.00
         146 | Karen      | Partners  | KPARTNER | 011.44.1344.467268 | SA_MAN  | 13500.00
         201 | Michael    | Hartstein | MHARTSTE | 515.123.5555       | MK_MAN  | 13000.00
(6 rows)
```

# Operator bigger equals to

Berikut contoh kasus, untuk mencari data pegawai dengan gaji yang lebih besar dari `24000`. in case gaji `24000` adalah gaji paling besar jika di cari dengan menggunakan operator `>` maka hasilnya `(0 rows)` berikut querynya:

{% highlight sql linenos %}
select employee_id, first_name, last_name, email, phone_number, job_id, salary
from employees 
where salary >= 24000;
{% endhighlight %}

Berikut hasilnya:

```postgresql-console
 employee_id | first_name | last_name | email | phone_number | job_id  |  salary  |
-------------+------------+-----------+-------+--------------+---------+----------+
         100 | Steven     | King      | SKING | 515.123.4567 | AD_PRES | 24000.00 |
(1 row)
```

# Operator less then & smaller equal to

Untuk operator `<` dan `<=` ini kurang lebih sama seperti operator `>` hanya kebalikannya saja yaitu yang lebih kecil.

# Operator like

Operator like biasanya digunakan untuk tipe data `varchar` atau string, ada 2 expresion yang kita bisa gunakan di operator ini yaitu 

1. `_` atau underscore, digunakan untuk mewakili expresion satu karakter.
2. `%` atau persent, digunakan untuk mewakili expresion beberapa karakter.

Contoh kasus untuk expresion `%`, saya ingin mencari nama depan karyawan yang diawali oleh huruf `A`. Berikut querynya:

{% highlight sqll linenos %}
select employee_id, first_name, last_name, email, phone_number, job_id, salary
from employees 
where last_name like 'A%;
{% endhighlight %}

Berikut hasilnya:

```postgresql-console
 employee_id | first_name | last_name |  email   |    phone_number    |  job_id  |  salary  
-------------+------------+-----------+----------+--------------------+----------+----------
         105 | David      | Austin    | DAUSTIN  | 590.423.4569       | IT_PROG  |  4800.00
         130 | Mozhe      | Atkinson  | MATKINSO | 650.124.6234       | ST_CLERK |  2800.00
         166 | Sundar     | Ande      | SANDE    | 011.44.1346.629268 | SA_REP   |  6400.00
         174 | Ellen      | Abel      | EABEL    | 011.44.1644.429267 | SA_REP   | 11000.00
(4 rows)

hr=# 
```

Contoh kasus untuk expresion `_`, saya ingin mencari huruf ke 2 dari kolom `job_id` di tabel `jobs` mengadung `T`. Berikut querynya:

{% highlight sql linenos %}
select * 
from jobs 
where job_id like '_T%';
{% endhighlight %}

Berikut hasilnya:

```postgresql-console
  job_id  |   job_title   | min_salary | max_salary 
----------+---------------+------------+------------
 ST_MAN   | Stock Manager |       5500 |       8500
 ST_CLERK | Stock Clerk   |       2000 |       5000
 IT_PROG  | Programmer    |       4000 |      10000
(3 rows)
```

# Operator IN

Operator ini, agak berbeda dari sebelumnya jadi membandingkan banyak nilai contoh kasusnya seperti berikut, Jadi saya ingin mencari data karyawan yang bekerja di `department_id = [10, 20, 90]` biasanya cara simple untuk solusi seperti dilakuan satu persatu yaitu dengan `select .... where departement_id = 10`, kemudian `select ... where departement_id = 20` dan seterusnya. Alangkah baiknya kita menggunakan operator `IN` seperti berikut:

{% highlight sql linenos %}
select employee_id, first_name, last_name, email, phone_number, job_id, salary, department_id
from employees 
where department_id IN (10, 20, 90);
{% endhighlight %}

Berikut hasilnya:

```sql
 employee_id | first_name | last_name |  email   | phone_number | job_id  |  salary  | department_id 
-------------+------------+-----------+----------+--------------+---------+----------+---------------
         100 | Steven     | King      | SKING    | 515.123.4567 | AD_PRES | 24000.00 |            90
         101 | Neena      | Kochhar   | NKOCHHAR | 515.123.4568 | AD_VP   | 17000.00 |            90
         102 | Lex        | De Haan   | LDEHAAN  | 515.123.4569 | AD_VP   | 17000.00 |            90
         200 | Jennifer   | Whalen    | JWHALEN  | 515.123.4444 | AD_ASST |  4400.00 |            10
         201 | Michael    | Hartstein | MHARTSTE | 515.123.5555 | MK_MAN  | 13000.00 |            20
         202 | Pat        | Fay       | PFAY     | 603.123.6666 | MK_REP  |  6000.00 |            20
(6 rows)
```

# Operator between

Operator `BETWEEN` digunakan untuk memfilter dengan interval/rentang tertentu diantar nilai terkecil dan terbesar. contoh kasusnya, Saya mau menampilkan data yang karywan yang memiliki gaji dari `4000` s/d `6000`. Berikut querynya:

{% highlight sql linenos %}
select employee_id, first_name, last_name, email, phone_number, job_id, salary, department_id
from employees 
where salary between 4000 and 6000;
{% endhighlight %}

Berikut hasilnya:

```postgresql-console
 employee_id | first_name | last_name |  email   | phone_number |  job_id  | salary  | department_id 
-------------+------------+-----------+----------+--------------+----------+---------+---------------
         104 | Bruce      | Ernst     | BERNST   | 590.423.4568 | IT_PROG  | 6000.00 |            60
         105 | David      | Austin    | DAUSTIN  | 590.423.4569 | IT_PROG  | 4800.00 |            60
         106 | Valli      | Pataballa | VPATABAL | 590.423.4560 | IT_PROG  | 4800.00 |            60
         107 | Diana      | Lorentz   | DLORENTZ | 590.423.5567 | IT_PROG  | 4200.00 |            60
         124 | Kevin      | Mourgos   | KMOURGOS | 650.123.5234 | ST_MAN   | 5800.00 |            50
         184 | Nandita    | Sarchand  | NSARCHAN | 650.509.1876 | SH_CLERK | 4200.00 |            50
         185 | Alexis     | Bull      | ABULL    | 650.509.2876 | SH_CLERK | 4100.00 |            50
         192 | Sarah      | Bell      | SBELL    | 650.501.1876 | SH_CLERK | 4000.00 |            50
         200 | Jennifer   | Whalen    | JWHALEN  | 515.123.4444 | AD_ASST  | 4400.00 |            10
         202 | Pat        | Fay       | PFAY     | 603.123.6666 | MK_REP   | 6000.00 |            20
(10 rows)
```

# Operator is null

Operator `IS NULL` digunakan untuk memfiter data yang bernilai null. Contoh kasusnya, saya mau menampilkan data karywan yang tidak memiliki manager. Berikut querynya:

{% highlight sql linenos %}
select employee_id, first_name, last_name, email, phone_number, job_id, salary, department_id
from employees 
where manager_id is null;
{% endhighlight %}

Berikut hasilnya:

```postgresql-console
 employee_id | first_name | last_name | email | phone_number | job_id  |  salary  | department_id 
-------------+------------+-----------+-------+--------------+---------+----------+---------------
         100 | Steven     | King      | SKING | 515.123.4567 | AD_PRES | 24000.00 |            90
(1 row)
```