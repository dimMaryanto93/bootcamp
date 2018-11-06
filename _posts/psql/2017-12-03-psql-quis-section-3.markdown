---
layout: post
title: "Time is your to practice part 3"
date: 2017-12-03T22:25:31+07:00
lang: psql
categories:
- RDBMS
- PostgreSQL
gist: 
youtube: 
comments: true
---

1. Tambahkan data ke tabel `countries` dengan data seperti berikut
![data insert query countries]({{ site.baseurl }}/resources/downloads/imgs/psql/quis-3/soal1.png)
2. Tambahkan data ke tabel `locations` dengan data seperti berikut
![data insert query locations]({{ site.baseurl }}/resources/downloads/imgs/psql/quis-3/soal2.png)
3. Updatelah `commission_pct` menjadi `10%` dari table `employees` yang memiliki `job_id = 'IT_PROG'` kecuali `employee_id = 104`, jika di tampilkan hasilnya seperti berikut:
![hasil query]({{ site.baseurl }}/resources/downloads/imgs/psql/quis-3/hasil3.png)
4. Buatlah tabel `karyawan_tdi` dengan perancagan seperti berikut:
![perancangan tabel]({{ site.baseurl }}/resources/downloads/imgs/psql/quis-3/soal4.png)
**Keterangan**
    1. column `kode_karyawan` adalah _primary key_
    2. column `alamat_rumah` berelasi dengan table `locations`
    3. column `alamat_domisili` berelasi dengan tabel `locations`
    4. column `jabatan` berelasi dengan `jobs`
    5. column `bagian` berelasi dengan `departments`
5. Buatlah data pada tabel `karyawan_tdi` seperti berikut:
![data insert query tabel karyawan_tdi]({{ site.baseurl }}/resources/downloads/imgs/psql/quis-3/soal5.png)
6. Buatlah query untuk menapilkan data seperti berikut:
![data karyawan_tdi]({{ site.baseurl }}/resources/downloads/imgs/psql/quis-3/soal6.png)
7. Buatlah query untuk menggabungkan data dari table `employees` dan `karyawan_tdi` yang memiliki `job_id = 'IT_PROG'` seperti berikut:
![union table]({{ site.baseurl }}/resources/downloads/imgs/psql/quis-3/soal7.png)

## My Solution

This is my way, download [disini]({{ site.baseurl }}/resources/downloads/file/psql.quis-3.zip)