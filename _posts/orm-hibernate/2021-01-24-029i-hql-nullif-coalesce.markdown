---
layout: post
title: "Coalesce & NullIF menggunakan HQL"
date: 2021-01-24T14:28:08+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#hql
youtube: 
comments: true
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-29i
---

Hai, pada kesempatan kali ini saya mau membahas tentang function `coalesce` dan `nullif` menggunakan Hibernate Query Language. ok seperti biasa kita siapkan dulu datanya. contohnya saya punya tabel dan data seperti berikut:

![select-tables]({{ page.image_path | prepend: site.baseurl }}/select-tables.png)

Selanjutnya, kita buat DAO seperti berikut:

{% gist page.gist "HQLCoalesceAndNullIfDao.java" %}

Implementasi Unit Testing: 

{% gist page.gist "TestHQLCoalesceAndNullIF.java" %}

Setelah itu coba jalankan unit testing untuk method `testCoalesceFunction()`, maka hasilnya seperti berikut:

```bash
Jan 24, 2021 2:25:55 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        coalesce(penerbit0_.noFax,
        penerbit0_.phoneNumber,
        'publisher not have contact number!') as col_0_0_ 
    from
        Penerbit penerbit0_ 
    where
        penerbit0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLCoalesceAndNullIF - data: 1
Hibernate: 
    select
        coalesce(penerbit0_.noFax,
        penerbit0_.phoneNumber,
        'publisher not have contact number!') as col_0_0_ 
    from
        Penerbit penerbit0_ 
    where
        penerbit0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLCoalesceAndNullIF - data: 2
Hibernate: 
    select
        coalesce(penerbit0_.noFax,
        penerbit0_.phoneNumber,
        'publisher not have contact number!') as col_0_0_ 
    from
        Penerbit penerbit0_ 
    where
        penerbit0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLCoalesceAndNullIF - data: 2
Hibernate: 
    select
        coalesce(penerbit0_.noFax,
        penerbit0_.phoneNumber,
        'publisher not have contact number!') as col_0_0_ 
    from
        Penerbit penerbit0_ 
    where
        penerbit0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLCoalesceAndNullIF - data: publisher not have contact number!
```

Dan kemudian yang terakhir, coba jalankan method `testNullIfFunction()`, maka hasilnya seperti berikut:

```bash
Jan 24, 2021 2:26:44 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        nullif(penerbit0_.noFax,
        penerbit0_.phoneNumber) as col_0_0_ 
    from
        Penerbit penerbit0_ 
    where
        penerbit0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLCoalesceAndNullIF - data: 1
Hibernate: 
    select
        nullif(penerbit0_.noFax,
        penerbit0_.phoneNumber) as col_0_0_ 
    from
        Penerbit penerbit0_ 
    where
        penerbit0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLCoalesceAndNullIF - data: null
Hibernate: 
    select
        nullif(penerbit0_.noFax,
        penerbit0_.phoneNumber) as col_0_0_ 
    from
        Penerbit penerbit0_ 
    where
        penerbit0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLCoalesceAndNullIF - data: null
Hibernate: 
    select
        nullif(penerbit0_.noFax,
        penerbit0_.phoneNumber) as col_0_0_ 
    from
        Penerbit penerbit0_ 
    where
        penerbit0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLCoalesceAndNullIF - data: null
```