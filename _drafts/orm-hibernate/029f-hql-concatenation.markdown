---
layout: post
title: "Concatnation dengan HQL"
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- http://docs.jboss.org/hibernate/orm/5.2/quickstart/html_single/
- https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#hql
youtube: 
comments: true
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-29f
---

Hai, pada kesempatan kali ini saya mau membahas tentang Concatnation menggunakan JPQL dan HQL. untuk concatnation kita bisa menggunakan function `concat(...)` dan operator `||`

Ok, sekarang kita buat dulu DTO / Model seperti berikut:

{% gist page.gist "ConcatnationModel.java" %}

Implementasi DAO:

{% gist page.gist "HQLConcatnationDao.java" %}

Implementasi Unit Testing:

{% gist page.gist "TestHQLConcatnation.java" %}

Seperti biasa sebelum kita jalankan, kita check dulu tabelnya di database, berikut adalah data yang ada:

![select-tables]({{ page.image_path | prepend: site.baseurl}}/select-tables.png)

Kemudian kita coba jalankan unit testing pada method `testFunctionConcatByJpa`, maka hasilnya seperti berikut:

```bash
Jan 22, 2021 5:03:06 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        mahasiswao0_.nama as col_0_0_,
        (alamatenti1_.provinsi||', '||alamatenti1_.kota) as col_1_0_ 
    from
        mapping.mahasiswa_onetoone mahasiswao0_ 
    inner join
        mapping.alamat alamatenti1_ 
            on (
                mahasiswao0_.alamat=alamatenti1_.id
            )
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLConcatnation - data: [ConcatnationModel(nama=Dimas Maryanto, alamat=Jawa Barat, Kab. Bandung)]
```

Dan yang terakhir jalankan juga method `testFunctionConcatByHQL`, maka hasilnya seperti berikut:

```bash
Jan 22, 2021 5:04:00 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        mahasiswao0_.nama as col_0_0_,
        (alamatenti1_.provinsi||', '||alamatenti1_.kota) as col_1_0_ 
    from
        mapping.mahasiswa_onetoone mahasiswao0_ 
    inner join
        mapping.alamat alamatenti1_ 
            on (
                mahasiswao0_.alamat=alamatenti1_.id
            )
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLConcatnation - data: [ConcatnationModel(nama=Dimas Maryanto, alamat=Jawa Barat, Kab. Bandung)]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLConcatnation - destroy hibernate session!
```