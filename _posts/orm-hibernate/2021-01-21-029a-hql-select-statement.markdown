---
layout: post
title: "Select Statement dengan HQL"
date: 2021-01-21T11:57:38+07:00
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
image_path: /resources/posts/orm-hibernate-29a
---

Hai, di materi kali ini saya mau ngebahas tentang Select Statement dengan menggunakan HQL. OK misalnya disini saya menggunakan entity yang udah pernah saya buat di materi sebelumnya yaitu:

{% gist page.gist "MataKuliahEntity.java" %}

Dan berikut adalah implementasi DAO:

{% gist page.gist "HQLMatakuliahReadDao.java" %}

kemudian berikut adalah implementasi Unit Testing: 

{% gist page.gist "TestHQLMatakuliahRead.java" %}

Sebelum kita coba siapkan dulu datanya contohnya seperti berikut:

![select-tables]({{ page.image_path | prepend: site.baseurl}}/select-tables.png)

Setelah itu baru kita coba jalankan method unit testing `testFindAll` maka hasilnya seperti berikut:

```bash
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        matakuliah0_.id as id1_32_,
        matakuliah0_.nama_kuliah as nama_kul2_32_,
        matakuliah0_.jumlah_sks as jumlah_s3_32_ 
    from
        mapping.matakuliah matakuliah0_
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLMatakuliahRead - data: [MataKuliahEntity(id=79c06b62-e70c-41f3-b42d-3aa63ab8d366, nama=Pemograman Java 1, sks=3), MataKuliahEntity(id=733be4ef-20fb-4d16-bbfe-b4b6c31ee8d3, nama=SKRIPSI, sks=6)]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLMatakuliahRead - destroy hibernate session!
```

Kemudian kita coba jalankan method `testFindByIdWithIndex`, maka hasilnya seperti berikut:

```bash
Jan 21, 2021 11:51:39 AM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        matakuliah0_.id as id1_32_,
        matakuliah0_.nama_kuliah as nama_kul2_32_,
        matakuliah0_.jumlah_sks as jumlah_s3_32_ 
    from
        mapping.matakuliah matakuliah0_ 
    where
        matakuliah0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLMatakuliahRead - data: MataKuliahEntity(id=79c06b62-e70c-41f3-b42d-3aa63ab8d366, nama=Pemograman Java 1, sks=3)
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLMatakuliahRead - destroy hibernate session!
```

Lalu coba jalankan method `testFindByNameWithNamedParameter`, maka hasilnya seperti berikut:

```bash
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        matakuliah0_.id as id1_32_,
        matakuliah0_.nama_kuliah as nama_kul2_32_,
        matakuliah0_.jumlah_sks as jumlah_s3_32_ 
    from
        mapping.matakuliah matakuliah0_ 
    where
        matakuliah0_.nama_kuliah=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLMatakuliahRead - data: [MataKuliahEntity(id=733be4ef-20fb-4d16-bbfe-b4b6c31ee8d3, nama=SKRIPSI, sks=6)]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLMatakuliahRead - destroy hibernate session!
```

Dan yang terakhir, coba jalankan method `testFindByNameAndSks`, maka hasilnya seperti berikut:

```bash
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        matakuliah0_.id as id1_32_,
        matakuliah0_.nama_kuliah as nama_kul2_32_,
        matakuliah0_.jumlah_sks as jumlah_s3_32_ 
    from
        mapping.matakuliah matakuliah0_ 
    where
        matakuliah0_.nama_kuliah=? 
        and matakuliah0_.jumlah_sks=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLMatakuliahRead - data: [MataKuliahEntity(id=733be4ef-20fb-4d16-bbfe-b4b6c31ee8d3, nama=SKRIPSI, sks=6)]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLMatakuliahRead - destroy hibernate session!
```

## Summary

HQL Select statement ini, kurang-lebih sama dengan native sql. untuk execute query digantikan dengan method `getResultList()` untuk **multi rows object** dan `getSingleResult` untuk **single row object**