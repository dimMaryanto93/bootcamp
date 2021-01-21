---
layout: post
title: "Distinct dengan HQL"
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
image_path: /resources/posts/orm-hibernate-29d
---

Hai, di materi kali ini saya mau membahas tentang clause `DISTINCT`. clausa distinct sendiri pada dasarnya untuk meng-eliminasi nilai yang redudant. Nah jadi clausa distinct ini di ORM Hibernate terdiri dari 

1. Distinct with SQL Projections
2. Distinct with Entity queries

## Distinct with SQL Projection

Untuk menggunakan perintah distinct dengan projection kita perlu menambahkan data dulu ke table `enumeration.employee_string` untuk melakukan pengecheckannya seperti berikut:

![select-table-distinct-projections]({{ page.image_path | prepend: site.baseurl}}/select-tables-projections.png)

Dan berikut adalah implementasi DAO untuk select distinct dengan projections query:

{% gist page.gist "HQLDistinctAsProjectionsDao.java" %}

Implementasi Unit Testing distinct dengan projections:

{% gist page.gist "TestHQLDistinctAsProjection.java" %}

Jika di running unit testingnya, maka hasilnya seperti berikut:

```bash
Jan 21, 2021 5:49:09 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        distinct employeeen0_.employee_status as col_0_0_ 
    from
        enumeration.employee_string employeeen0_
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLDistinctAsProjection - data: [ACTIVE, RESIGN, LEAVE]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLDistinctAsProjection - destroy hibernate session!
```

## Distinct with entity queries

Untuk menggunakan perintah distinct dengan entity queries, kita perlu menambahkan data dulu di table `mapping.kelas` dan `mapping.mahasiswa_manytoone` seperti berikut:

![select-table-distinct-entity]({{ page.image_path | prepend: site.baseurl}}/select-tables-entity.png)

Dan berikut adalah implementasi DAO distinct with entity queries:

{% gist page.gist "HQLDistinctAsEntityDao.java" %}

Implementasi Unit Testing distinct dengan entity queries:

{% gist page.gist "TestHQLDistinctAsEntity.java" %}

Jika di running unit testingnya, maka hasilnya seperti berikut:

```bash
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        distinct kelasentit1_.id as id1_25_,
        kelasentit1_.tahun_angkatan as tahun_an2_25_,
        kelasentit1_.nama_kelas as nama_kel3_25_,
        kelasentit1_.program_studi as program_4_25_ 
    from
        mapping.mahasiswa_manytoone mahasiswam0_ 
    inner join
        mapping.kelas kelasentit1_ 
            on mahasiswam0_.kelas_id=kelasentit1_.id
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLDistinctAsEntity - data: [KelasEntity(id=1, nama=SI-01, angkatan=2011, programStudi=IF), KelasEntity(id=3, nama=IF-01, angkatan=2011, programStudi=IF), KelasEntity(id=4, nama=IF-02, angkatan=2011, programStudi=IF)]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLDistinctAsEntity - destroy hibernate session!
```