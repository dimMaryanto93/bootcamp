---
layout: post
title: "Persiapan belajar PostgreSQL"
date: 2017-11-26T20:27:57+07:00
lang: psql
categories:
- RDBMS
- PostgreSQL
gist: 
youtube: 
comments: true
---

Setelah melakukan proses installasi _software_ PostgreSQL dan PgAdmin3 / PgAdmin4, tahap selanjutnya kita akan membuat scema atau role, berikut adalah caranya.

## Login as user `postgres`

Login sebagai postgres, yang pertama harus di ingat adalah _password_ postgres didapatkan ketika melakukan installasi software PostgreSQL. setelah itu baru bisa login sebagai user postgres dengan cara seperti berikut:

{% highlight postgresql %}
psql -h localhost -U postgres
{% endhighlight %}

Kemudian kita buat schema dengan perintah seperti berikut:

{% highlight postgres-console %}
-- create user schema database
CREATE USER hr WITH SUPERUSER LOGIN PASSWORD 'hr';
{% endhighlight %}

Setelah membuat user dengan _username_ `hr` dan passwornya sama dengan _username_ yaitu `hr`, tahap selanjutnya kita login sebagai user `hr`, dengan perintah seperti berikut:

## Login as user `hr`

{% highlight psql %}
psql -h localhost -U hr
{% endhighlight %}

Setelah login sebagai `hr` kemudian kita buat satu database dengan nama yang sama dengan username, dengan perintah seperti berikut:

{% highlight psql %}
-- create database for user hr
CREATE DATABASE hr WITH OWNER hr;
{% endhighlight %}

Setelah database terbuat, kemudian download [file ini](/resources/downloads/file/psql-schema.sql) setelah itu jalankan querynya dengan connection user `hr`.