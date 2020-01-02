---
layout: post
title: "Single Row Function di PostgreSQL"
date: 2018-11-10T20:02:02+07:00
lang: psql
categories:
- RDBMS
- PostgreSQL
refs: []
youtube: 
comments: true
---

Single row function, yaitu digunakan untuk memformat data per baris. Berikut ilustrasinya:

![single row funcation]({{site.baseurl}}/resources/posts/psql-single-row/konsep-single-row-funcation.png)

Beberapa fungsi yang dapat digunakan untuk memformat data di single row, di antarnya dikategorikan sebagai berikut:

# Text formated

Untuk fungsi text ini lumayan banyak, seperti berikut:

| Function  | Keterangan                        |
|:----------|:----------------------------------|
| `ASCII`   | Menformat dari charater ke asci   |
| `CHR`     | Memformat dari asci ke character  |
| `CONCAT`  | Menggabungkan 2 karakter          |
| `INITCAP` | Format awal huruf dari kata menjadi kapital |
| `LOWER`   | Format semua huruf menjadi huruf kecil | 
| `UPPER`   | Format semua huruf menjadi huruf kapital |
| `INSTR`   | Mencari posisi / index dari suatu kalimat berdasarkan parameter tertentu |
| `LENGTH`  | Menghitung jumlah karakter|
| `LPAD`    | Memformat menjadi rata kirim |
| `RPAD`    | Memformat menjadi rata kanan |
| `LTRIM`   | Memotong kalimat dari sebelah kirim berdasarkan parameter |
| `RTRIM`   | Memotong kalimat dari sebelah kanan berdasarkan parameter |
| `TRIM`    | Memotong kalimat dari 2 sisi berdasarkan parameter |
| `REPLACE` | Mengganti kalimat berdasarkan parameter |
| `SUBSTR`  | Mengambil beberapa huruf berdasarkan posisi awal dan akhir |
{:.bordered .striped}

Untuk lebih lengkapnya lagi bisa check [dokumentasi](https://www.postgresql.org/docs/9.1/functions-string.html)

Berikut adalah contoh salah satu penggunaannya, saya mau memformat data karyawan `first_name` di jadikan huruf kapital, sedangkan untuk `last_name` saya mau hitung jumlahnya berapa, gabungkan column `first_name` dan `last_name`. Berikut querynya:

{% highlight sql linenos %}
select 
    employee_id as kode,
    upper(first_name) as nama_depan_kapital,
    last_name as nama_belakang,
    length(last_name) as jumlah,
    concat(first_name, ' ', last_name) as nama_lengkap
from employees
limit 10;
{% endhighlight %}

Berikut hasilnya:

```postgresql-console
 kode | nama_depan_kapital | nama_belakang | jumlah |   nama_lengkap   
------+--------------------+---------------+--------+------------------
  100 | STEVEN             | King          |      4 | Steven King
  101 | NEENA              | Kochhar       |      7 | Neena Kochhar
  102 | LEX                | De Haan       |      7 | Lex De Haan
  103 | ALEXANDER          | Hunold        |      6 | Alexander Hunold
  104 | BRUCE              | Ernst         |      5 | Bruce Ernst
  105 | DAVID              | Austin        |      6 | David Austin
  106 | VALLI              | Pataballa     |      9 | Valli Pataballa
  107 | DIANA              | Lorentz       |      7 | Diana Lorentz
  108 | NANCY              | Greenberg     |      9 | Nancy Greenberg
  109 | DANIEL             | Faviet        |      6 | Daniel Faviet
(10 rows)
```

# Number format

Ada beberapa function yang kita bisa gunakan untuk memformat number:

| Function  | Keterangan                        |
|:----------|:----------------------------------|
| `CEIL`    | Untuk pembulatan ke atas          |
| `ABS`     | Untuk nilai selalu positif        |
| `FLOOR`   | Untuk pembulatan ke bawah         |
| `MOD`     | Untuk sisa bagi                   |
| `POWER`   | Untuk pangkat                     |
| `ROUND`   | Untuk pembulatan pecahan          |
| `SQRT`    | Untuk menghitung akar             |
| `coalese` | Nilai null dengan default value   |
{:.bordered .striped}

Berikut beberapa contoh penggunakan function di number, berikut querynya:

{% highlight sql linenos %}
select 
    coalesce(commission_pct, 0) as commision_pct,
    salary as gaji,
    mod(2, 4) as sisa_bagi,
    power((salary / 1000), 2) as pangkat,
    sqrt(50) as akar
from employees
limit 10;
{% endhighlight %}

Berikut hasilnya:

```postgresql-console
 commision_pct |   gaji   | sisa_bagi |       pangkat        |       akar       
---------------+----------+-----------+----------------------+------------------
             0 | 24000.00 |         2 | 576.0000000000000000 | 7.07106781186548
             0 | 17000.00 |         2 | 289.0000000000000000 | 7.07106781186548
             0 | 17000.00 |         2 | 289.0000000000000000 | 7.07106781186548
             0 |  9000.00 |         2 |  81.0000000000000000 | 7.07106781186548
             0 |  6000.00 |         2 |  36.0000000000000000 | 7.07106781186548
             0 |  4800.00 |         2 |  23.0400000000000000 | 7.07106781186548
             0 |  4800.00 |         2 |  23.0400000000000000 | 7.07106781186548
             0 |  4200.00 |         2 |  17.6400000000000000 | 7.07106781186548
             0 | 12000.00 |         2 | 144.0000000000000000 | 7.07106781186548
             0 |  9000.00 |         2 |  81.0000000000000000 | 7.07106781186548
(10 rows)
```

# Data type formating funcation

Untuk data type formating berikut, [dokumentasinya silahkan di baca ya](https://www.postgresql.org/docs/9.1/functions-formatting.html)