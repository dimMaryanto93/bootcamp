---
layout: post
title: "Collections Mapping as a Value"
date: 2021-01-19T15:30:51+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- http://docs.jboss.org/hibernate/orm/5.2/quickstart/html_single/
- https://docs.jboss.org/hibernate/stable/orm/userguide/html_single/Hibernate_User_Guide.html#collections-synopsis
comments: true
image_path: 
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-27a
---

Hai, pada materi kali ini saya mau membahas tentang Element Collection As Value. berikut adalah perancangan tabelnya:

![erd]({{ page.image_path | prepend: site.baseurl }}/erd.png)

Berikut adalah implementasi Entity:

{% gist page.gist "MahasiswaElementCollectionAsValue.java" %}

Implementasi DAO:

{% gist page.gist "MahasiswaElementCollectionAsValueDao.java" %}

Implementasi Unit Testing:

{% gist page.gist "TestElementCollectionAsValue.java" %}

Jika di running pada method `testSaveMahasiswa` maka hasilnya seperti berikut:

```bash
INFO: HHH10001501: Connection obtained from JdbcConnectionAccess [org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator$ConnectionProviderJdbcConnectionAccess@374c3975] for (non-JTA) DDL execution was not in auto-commit mode; the Connection 'local transaction' will be committed and the Connection will be set into auto-commit mode.
Hibernate: 
    
    create table embedded.mahasiswa_hoby (
       mahasiswa_id int8 not null,
        hobi varchar(255)
    )
Hibernate: 
    
    create table embedded.mahasiswa_listasvalue (
       id int8 not null,
        alamat varchar(255) not null,
        nama varchar(255) not null,
        nim varchar(255),
        primary key (id)
    )
Hibernate: 
    
    alter table if exists embedded.mahasiswa_hoby 
       add constraint fk_hobi_mahasiswa_id 
       foreign key (mahasiswa_id) 
       references embedded.mahasiswa_listasvalue
Jan 19, 2021 2:40:10 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        nextval ('hibernate_sequence')
Hibernate: 
    insert 
    into
        embedded.mahasiswa_listasvalue
        (alamat, nama, nim, id) 
    values
        (?, ?, ?, ?)
Hibernate: 
    insert 
    into
        embedded.mahasiswa_hoby
        (mahasiswa_id, hobi) 
    values
        (?, ?)
Hibernate: 
    insert 
    into
        embedded.mahasiswa_hoby
        (mahasiswa_id, hobi) 
    values
        (?, ?)
Hibernate: 
    insert 
    into
        embedded.mahasiswa_hoby
        (mahasiswa_id, hobi) 
    values
        (?, ?)
Hibernate: 
    insert 
    into
        embedded.mahasiswa_hoby
        (mahasiswa_id, hobi) 
    values
        (?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.collection.TestElementCollectionAsValue - mahasiswa: MahasiswaElementCollectionAsValue(id=12, nim=10511148, name=Dimas Maryanto, address=Bandung)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.collection.TestElementCollectionAsValue - destroy hibernate session!
```

Kemudian kita coba jalankan method `testFindById` maka hasilnya seperti berikut:

```bash
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        mahasiswae0_.id as id1_2_0_,
        mahasiswae0_.alamat as alamat2_2_0_,
        mahasiswae0_.nama as nama3_2_0_,
        mahasiswae0_.nim as nim4_2_0_ 
    from
        embedded.mahasiswa_listasvalue mahasiswae0_ 
    where
        mahasiswae0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.collection.TestElementCollectionAsValue - mahasiswa: MahasiswaElementCollectionAsValue(id=12, nim=10511148, name=Dimas Maryanto, address=Bandung)
Hibernate: 
    select
        hobies0_.mahasiswa_id as mahasisw1_1_0_,
        hobies0_.hobi as hobi2_1_0_ 
    from
        embedded.mahasiswa_hoby hobies0_ 
    where
        hobies0_.mahasiswa_id=?
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.collection.TestElementCollectionAsValue - hobies: [Gaming, Programing, Movies, Sharing]
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.collection.TestElementCollectionAsValue - destroy hibernate session!
```

Sekarang, kita coba check tabelnya. maka hasilnya seperti berikut:

![select-table]({{ page.image_path | prepend: site.baseurl }}/select-tables.png)