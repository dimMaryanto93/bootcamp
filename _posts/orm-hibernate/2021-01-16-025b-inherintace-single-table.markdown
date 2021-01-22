---
layout: post
title: "Inherintance Mapping methode Single Table"
date: 2021-01-16T13:22:35+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#entity-inheritance-single-table
youtube: https://www.youtube.com/watch?v=ulhVCds7sHI&list=PLV1-tdmPblvxHxNh867D1JR4u52LgzeIr&index=25
comments: true
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-25b
---

Hai, di materi kali ini akan membahas Inherintance menggunakan metode Single Table. Untuk mencobanya disini masih menggunakan contoh kasus yang sama yaitu kendaran yang terdiri dari mobil dan motor. berikut adalah perancangan tabelnya:

![erd]({{site.baseurl}}{{page.image_path}}/erd.png)

contoh implementasinya seperti berikut

Implementasi Entity kendaraan:

{% gist page.gist "KendaraanSingleTableEntity.java" %}

Implementasi Entity Mobil:

{% gist page.gist "MobilSingleTableEntity.java" %}

Implementasi Entity Motor:

{% gist page.gist "MotorSingleTableEntity.java" %}

Setelah itu kita buat DAO, karena kita menggunakan single table jadi kita cukup membuat 1 class DAO saja contohnya seperti berikut:

{% gist page.gist "KendaraanSingleTableDao.java" %}

Kemudian kita buat unit testing untuk menyimpan data mobil dan motor, implementasinya seperti berikut:

{% gist page.gist "TestKendaraanSingleTable.java" %}

Jika di running maka hasilnya seperti berikut:

```bash
INFO: HHH10001501: Connection obtained from JdbcConnectionAccess [org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator$ConnectionProviderJdbcConnectionAccess@30f28b5] for (non-JTA) DDL execution was not in auto-commit mode; the Connection 'local transaction' will be committed and the Connection will be set into auto-commit mode.
Hibernate: 
    
    create table inherintance.kendaraan_singletable (
       DTYPE varchar(31) not null,
        id varchar(255) not null,
        cc int4,
        jumlah_cylinder int4,
        jumlah_roda int4,
        nama varchar(50),
        nama_pabrikan varchar(50) not null,
        is_all_wheel_drive boolean,
        jumlah_kursi int4,
        jenis_rantai varchar(255),
        primary key (id)
    )
Jan 16, 2021 12:53:13 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanSingleTable - connected!
Hibernate: 
    insert 
    into
        inherintance.kendaraan_singletable
        (cc, jumlah_cylinder, jumlah_roda, nama, nama_pabrikan, is_all_wheel_drive, jumlah_kursi, DTYPE, id) 
    values
        (?, ?, ?, ?, ?, ?, ?, 'MobilSingleTableEntity', ?)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanSingleTable - mobil: MobilSingleTableEntity(super=KendaraanSingleTableEntity(id=a010edcd-e33c-4e4e-b33e-75df8e3f1f31, nama=Honda BRIO, jumlahRoda=4, jumlahCylinder=4, cc=1000, namaPabrikan=PT. Honda Motor Company), jumlahKursi=4, allWheelDrive=false)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanSingleTable - destroy hibernate session!
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanSingleTable - init hibernate session
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanSingleTable - connected!
Hibernate: 
    insert 
    into
        inherintance.kendaraan_singletable
        (cc, jumlah_cylinder, jumlah_roda, nama, nama_pabrikan, jenis_rantai, DTYPE, id) 
    values
        (?, ?, ?, ?, ?, ?, 'MotorSingleTableEntity', ?)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanSingleTable - mobil: MotorSingleTableEntity(super=KendaraanSingleTableEntity(id=9e3515af-1138-4738-9a0c-d1bfa18f4360, nama=BMW S1000RR, jumlahRoda=2, jumlahCylinder=4, cc=1000, namaPabrikan=PT. BMW Motorrad), jenisRantai=Rantai)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanSingleTable - destroy hibernate session!
```

Jika kita check ke table, hasilnya seperti berikut:

![select-table]({{site.baseurl}}{{page.image_path}}/select-tables.png)