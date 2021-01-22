---
layout: post
title: "Inherintance Mapping metode MappedSuperclass"
date: 2021-01-16T12:04:41+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#entity-inheritance-mapped-superclass
youtube: https://www.youtube.com/watch?v=TpY90QrAsIc&list=PLV1-tdmPblvxHxNh867D1JR4u52LgzeIr&index=24
comments: true
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-25a
---

Hai, di materi kali ini saya mau ngebahas tentang Inherintance Mapping dengan Metode MappedSuperclass. Untuk mencoba mapping ini, kita membutuhkan 2 tabel yang memiliki column yang hampir sama contohnya `mobil` sama `motor` berikut adalah perancangan databasenya:

![erd]({{site.baseurl}}{{page.image_path}}/erd.png)

Implementasi Entity superclass:

{% gist page.gist "KendaraanMappedSuperclass.java" %}

Implementasi Entity child `mobil`:

{% gist page.gist "MobilMappedSuperclass.java" %}

Implementasi Entity child `motor`:

{% gist page.gist "MotorMappedSuperClass.java" %}

Implementasi DAO untuk `mobil`:

{% gist page.gist "MobilMappedSuperClassDao.java" %}

Implementasi DAO untuk `motor`:

{% gist page.gist "MotorMappedSuperClassDao.java" %}

Kemudian kita buat unit testingnya seperti berikut:

{% gist page.gist "TestMappedSuperClass.java" %}

Jika di running maka hasilnya seperti berikut:

```bash
INFO: HHH10001501: Connection obtained from JdbcConnectionAccess [org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator$ConnectionProviderJdbcConnectionAccess@1e1e837d] for (non-JTA) DDL execution was not in auto-commit mode; the Connection 'local transaction' will be committed and the Connection will be set into auto-commit mode.
Hibernate: 
    
    create table inherintance.mobil_mappedsuperclass (
       id varchar(64) not null,
        cc int4,
        jumlah_cylinder int4,
        jumlah_roda int4,
        nama varchar(50),
        nama_pabrikan varchar(50) not null,
        is_all_wheel_drive boolean not null,
        jumlah_kursi int4,
        primary key (id)
    )
Hibernate: 
    
    create table inherintance.motor_mappedsuperclass (
       id varchar(64) not null,
        cc int4,
        jumlah_cylinder int4,
        jumlah_roda int4,
        nama varchar(50),
        nama_pabrikan varchar(50) not null,
        jenis_rantai varchar(255),
        primary key (id)
    )
Jan 16, 2021 12:00:08 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    insert 
    into
        inherintance.mobil_mappedsuperclass
        (cc, jumlah_cylinder, jumlah_roda, nama, nama_pabrikan, is_all_wheel_drive, jumlah_kursi, id) 
    values
        (?, ?, ?, ?, ?, ?, ?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestMappedSuperClass - mobil: MobilMappedSuperclass(super=KendaraanMappedSuperclass(nama=Honda BRIO, jumlahRoda=4, jumlahCylinder=4, cc=1000, namaPabrikan=PT. Honda Motor Company), id=c5a7398c-a79c-4abd-9c55-deb3ec1e2bad, jumlahKursi=4, allWheelDrive=false)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestMappedSuperClass - destroy hibernate session!
```