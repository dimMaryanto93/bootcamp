---
layout: post
title: "Perintah select dalam SQL"
date: 2017-11-27T11:02:09+07:00
lang: psql
categories:
- RDBMS
- PostgreSQL
gist: 
youtube: 
comments: true
---

Perintah / klausa `select` pada dasarnya adalah perintah yang dilakukan _query_ terhadap _database_ untuk mengambil atau mendapatkan data berupa baris (_rows_) dan kolom (_columns_) dalam sebuah _table_ seperti berikut:

![sql to db](/resources/downloads/imgs/psql/select/sql-to-db.jpg)

Nah seperti yang kita tahu kalo dalam **sebuah _database_** bisa terdiri dari **banyak _tables_**, dalam **sebuah _table_** terdiri **banyak _rows_ dan _colums_**, dalam **satu _row_ dan _column_** terdiri dari **sebuah nilai**.

Jadi perintah _sql_ `select` memiliki format sebagai berikut:

{% highlight sql linenos %}
select 
     * | columns...  
from 
    table_name 
{% endhighlight %}

Contohnya di _database_ `hr` sekarang saya punya daftar _tables_ seperti berikut:

## Menampilkan daftar _tables_ dalam sebuah _database_

{% highlight postgresql-console %}
hr=# \dt
 public | countries    | table | hr
 public | departments  | table | hr
 public | employees    | table | hr
 public | job_history  | table | hr
 public | jobs         | table | hr
 public | locations    | table | hr
 public | regions      | table | hr
{% endhighlight %}

## Menampilkan daftar _columns_ dalam sebuah _table_
Kemudian di dalam _table_ `depertements` terdiri dari beberapa _columns_ seperti berikut:

{% highlight postgresql-console %}
hr=# \dt
 department_id   | integer               | not null default nextval('departments_department_id_seq'::regclass)
 department_name | character varying(30) | 
 manager_id      | integer               | 
 location_id     | integer               | 
{% endhighlight %}

## Menampilkan semua data dalam sebuah _table_

Untuk menampilkan semua data / semua column yang dipilih dalam sebuah tabel kita bisa menggunakan spesial karakter `*` (asteric / bintang) dalam perintah _select_ seperti berikut:

{% highlight postgresql-console linenos %}
select * 
from departments;
{% endhighlight %}

Maka akan tampil datanya seperti berikut:

| dep_id | department_name     | manager_id | location_id |
| :--   | :------------        | :----      |  :--- |
|   10  | Administration       |        200 |  1700 |
|   40  | Human Resources      |        203 |  2400 |
|   50  | Shipping             |        121 |  1500 |
|   60  | IT                   |        103 |  1400 |
|   90  | Executive            |        100 |  1700 |
{:.table .striped .bordered }

## Menampilkan hanya beberapa _columns_

Selain menggunakan menampilkan semua kolom dengan `*`, kita juga bisa sebutkan nama kolomnya secara langsung contohnya seperti berikut:

{% highlight postgresql-console linenos %}
select 
    departement_id,
    departement_name
from 
    departments;
{% endhighlight %}

Maka akan tampil datanya seperti berikut:

| department_id | department_name       |
| :--           | :------------         |
|   10          | Administration        |
|   40          | Human Resources       |
|   50          | Shipping              |
|   60          | IT                    |
|   90          | Executive             |
{:.table .striped .bordered }

