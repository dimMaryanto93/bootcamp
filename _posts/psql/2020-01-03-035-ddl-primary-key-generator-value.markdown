---
layout: post
title: "DDL - Generator default value untuk Primary Key"
date: 2020-01-03T14:33:33+07:00
lang: psql
categories:
- RDBMS
- PostgreSQL
refs: 
- https://www.postgresql.org/docs/9.1/datatype-uuid.html
- https://www.postgresql.org/docs/9.5/sql-createsequence.html
youtube: https://www.youtube.com/watch?v=WFGyithp2SE&list=PLV1-tdmPblvypZXSk2GC932nludT345xk&index=28
comments: true
---

Untuk membuat unique value ada 2 type yang kita bisa gunakan yaitu dengan Sequence Method dan Unique Identifier Method. 

## Sequential

yang pertama kita bahas tentang sequential yaitu sebuah nilai generator yang secara value akan naik terus atau increment. Mengunakan sequence sebagai nilai default pada primary key, ada beberapa cara yaitu 

1. Medefininsikan column bertipe data `serial` atau `bigserial`

    ```sql
    CREATE TABLE products (
        id bigserial primary key,
        name character varying(60) not null,
        price_sell decimal
    );
    ```

    secara default akan membuat sequence dengan nama `[table-name]_[column-use]_seq`

2. Mendefinisikan object sequence secara terpisah:

    ```sql
    CREATE SEQUENCE IF NOT EXISTS products_id_seq 
    START WITH  1 
    INCREMENT  BY 1;

    CREATE TABLE products (
        id integer primary key default nextval('products_id_seq'),
        name character varying(60) not null,
        price_sell decimal
    );
    ```

Setelah kita mendefinisikan sequence kita bisa entry data tanpa harus set kolom `id` karena secara otomatis nilainya diisi dengan object sequence, berikut querynya:

```sql
insert into products (name, price_sell)
values ('Macbook Pro 13" 2017', 28000000), 
        ('Ipad Pro 11" 2018 Wifi + Celular', 15000000);
```

## Unique Identifier / UUID

UUID yaitu random value dengan format sequence of lower-case hexadecimal digits yang berjumlah 32 karakter, tetapi secara default UUID ini belum aktif, untuk mengaktifkannya kita harus execute query berikut:

```sql
DROP EXTENSION IF NOT EXISTS "uuid-ossp";
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";
```

Berikut adalah contoh penggunaan UUID sebagai default value primary key:

```sql
CREATE TABLE articles (
    id              character varying(64)           primary key default uuid_generate_v4(),
    filename        character varying(60) not null,
    release_date    date
);
```

Setelah kita mengaktifkan module `uuid-ossp`, kita bisa entry data tanpa harus set kolom `id` karena secara otomatis nilainya diisi dengan object UUID, berikut querynya:

```sql
insert into articles (filename, release_date)
values ('Java core', '2019-12-10'), 
        ('Elasticsearc for query searching', '2019-12-10');
```