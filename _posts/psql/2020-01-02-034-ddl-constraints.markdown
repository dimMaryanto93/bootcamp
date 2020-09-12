---
layout: post
title: "DDL - Macam-macam Constraint pada Database PostgreSQL"
date: 2020-01-02T16:01:04+07:00
lang: psql
categories:
- RDBMS
- PostgreSQL
refs: 
- https://www.postgresql.org/docs/9.6/ddl-constraints.html
youtube: https://www.youtube.com/watch?v=XI2EFI0pfJI&list=PLV1-tdmPblvypZXSk2GC932nludT345xk&index=27
comments: true
---

Sebuah **Constraint** digunakan untuk memvalidasi / mengontrol data yang dapat di simpan pada sebuah table / kolom. **Constraint** dibagi menjadi beberapa macam yaitu:

1. Not Null
2. Unique
3. Check
4. Primary key
5. Foreign keys

## Constraint Not Null

Constraint **Not Null** diterapkan pada column tertentu dalam sebuah table, dengan tujuan untuk memvalidasi data yang kita entry tidak dapat bernilai null. Contoh penggunaanya seperti berikut:

```sql
CREATE TABLE products (
    product_no integer NOT NULL,
    name text NOT NULL,
    price numeric
);
```

Jadi dengan ddl untuk membuat table `products` seperti diatas, maka kita **harus mengisi nilai** pada kolom `product_no` dan `name`, tidak boleh `null`. Contohnya dengan perintah entry yang salah seperti berikut:

```sql
insert into products (product_no, name, price)
values (null, null, 0);
```

Bila di execute maka akan terjadi error: `error insert because constraint violence not null`

## Constraint Unique

Constraint **Unique** diterapkan pada column tertentu dalam sebuah tabel, dengan tujuan untuk memvalidasi data yang kita entry tidak boleh sama dengan data yang telah tersedia di table pada kolom tersebut. Contoh pengguanya seperti berikut:

```sql
CREATE TABLE products (
    product_no integer unique,
    name text NOT NULL,
    price numeric
);
```

Jadi dengan ddl untuk membuat table `products` seperti diatas, maka kita tidak boleh entry data pada kolom `product_no` dengan nilai yang sama atau sudah ada di table tersebut. Contoh dengan perintah entry yang salah seperti berikut:

```sql
insert into products (product_no, name, price)
values (1, 'Apple Macbook Pro 13" 2017', 28000000);

-- query ini error karena pada kolom product_no
insert into products (product_no, name, price)
values (1, 'Apple Ipad Pro 11" 2018', 15000000);
```

Bila di execute maka akan terjadi error: `error insert because constraint violence unique`.

Selain itu juga Constraint unique dapat di terapkan di beberapa kolom sekaligus, contohnya seperti berikut:

```sql
CREATE TABLE articles (
    file_name character varying(60),
    release_date date,
    author character varying(20)
);

ALTER TABLE articles
ADD CONSTRAINT uq_article_release UNIQUE (file_name, release_date);
```

Jadi berikut adalah contoh query yang error:

```sql
insert into articles (file_name, release_date, author)
values ('java-core-1', '2019-12-02', 'Dimas Maryanto');

insert into articles (file_name, release_date, author)
values ('java-core-1', null, 'Dimas Maryanto');

insert into articles (file_name, release_date, author)
values (null, '2019-12-02', 'Dimas Maryanto');

-- query ini error karena file_name dan release data sama seperti data sebelumnya
insert into articles (file_name, release_date, author)
values ('java-core-1', '2019-12-02', 'Dimas Maryanto');
```

## Constraint Check

Constraint **Check** dapat diterapkan pada kolom tertentu dalam sebuah table, dengan tujuan memvalidasi data yang kita entry harus sesuai dengan criteria yang diterapkan pada constraint tersebut contohnya pada kolom `price` nilai minimal lebih besar dari `0`. Contoh penggunaanya seperti berikut:

```sql
CREATE TABLE products (
    product_no integer unique,
    name text NOT NULL,
    price numeric
);

ALTER TABLE products
ADD CONSTRAINT check_price_must_be_greater_then_1 
CHECK (price >= 1);
```

Jadi dengan ddl untuk membuat table `products` seperti diatas, maka kita tidak boleh entry data pada kolom `price` dengan nilai lebih kecil dari `0` atau harus lebih besar dari `1`. Contoh dengan perintah entry yang salah seperti berikut:

```sql
insert into products (product_no, name, price)
values (1, 'Apple Ipad Pro 11" 2018', -15000000);
```

Bila di execute maka akan terjadi error: `error insert because check constraint`.

## Constraint Primary Key

Constraint **Primary Key** diterapkan pada sebuah kolom dalam table, dengan tujuan menjadikan data dalam satu baris tersebuh menjadi pegangan atau acuan karena sebuah primary key adalah gabungan dari constraint `not null` dan `unique`. Contoh penggunaanya seperti berikut:

```sql
CREATE TABLE products (
    product_no integer primary key,
    name text NOT NULL,
    price numeric
);
```

Setelah itu misalnya kita punya data seperti berikut:

| product_no    | name                  | price         |
|---------------|-----------------------|---------------|
| 1             | Apple Macbook Pro 13" | 28_000_000    |
| 2             | Apple Ipad Pro 11"    | 15_000_000    |
| 3             | iPhone 7 Plus 36gb    | 8_999_000     |
| 4             | Apple Airpod 2        | 2_150_000     |
| 5             | Apple Pencil 2        | 2_500_000     |


Nah dari data di atas, akan lebih mudah jika kita menggunakan kolom `product_no` untuk mendapatkan informasi contohnya untuk menghapus data dengan nama `Apple Macbook Pro 13"` jadi querynya seperti berikut:

```sql
delete from products where product_no = 1;
```

## Constraint Foreign Keys

Constraint **Foreign keys** dapat diterapkan pada sebuah kolom dengan table, dengan tujuan memvalidasi apakan nilai yang di entry terdaftar pada column di table acuannya. Contoh penggunaanya seperti berikut:

```sql
CREATE TABLE sellers (
    seller_id integer primary key,
    seller_name character varying(60) not null,
    seller_address character varying(255) 
)

CREATE TABLE products (
    product_id integer primary key,
    product_name text NOT NULL,
    product_price_sell numeric not null check(price >= 1)
    seller_id integer not null
);

ALTER TABLE products
ADD CONSTRAINT fk_seller_product FOREIGN KEY (seller_id)
REFERENCES sellers(seller_id) ON UPDATE CASCADE ON DELETE CASCADE;
```

Nah jadi dari 2 table tersebut saling berrelasi dengan menggunakan foreign key `salles_id` pada table `products`. Misalnya saya punya data sebagai berikut:

| Sales ID  | Sales Name            | Sales Address |
|-----------|-----------------------|---------------|
| 1         | Dimas Maryanto        | Bandung       |
| 2         | Muhamad Yusuf         | Jakarta       |

Jadi dengan data tersebut kita hanya dapat menyimpan data ke table `products` dengan mengeset nilai `salles_id` yang tersedia di table `sellers`, jika kita menginput data diluar dari data yang tersedia maka akan terkena validasi constraint foreign key. Contohnya entry data yang salah seperti berikut:

```sql
-- error kena validasi
insert into products (product_no, name, price, salles_id)
values (1, 'Apple Ipad Pro 11" 2018', 15000000, 3);
```