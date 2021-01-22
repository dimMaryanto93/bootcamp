---
layout: post
title: "Inherintance Mapping metode Table Per Class"
date: 2021-01-16T20:40:16+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#entity-inheritance-table-per-class
youtube: https://www.youtube.com/watch?v=9X-DHQcFc38&list=PLV1-tdmPblvxHxNh867D1JR4u52LgzeIr&index=28
comments: true
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-25e
---

Hai di materi kali ini kita akan membahas tentang Inherintance metode `TABLE_PER_CLASS` dengan perancangan tabel seperti berikut:

![erd]({{ page.image_path | prepend: site.baseurl }}/erd.png)

Dan berikut adalah implementasi Entity Kendaraan:

{% gist page.gist "KendaraanSeparateTableEntity.java" %}

Implementasi Entity Mobil:

{% gist page.gist "MobilSeparateTableEntity.java" %}

Implementasi Entity Motor:

{% gist page.gist "MotorSeparateTableEntity.java" %}

Implementasi DAO:

{% gist page.gist "KendaraanSeparateTableDao.java" %}

Implementasi Unit Testing:

{% gist page.gist "TestKendaraanSeparateTable.java" %}

Jika di running, method `testSaveMotor` maka hasilnya seperti berikut:

```bash
INFO: HHH10001501: Connection obtained from JdbcConnectionAccess [org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator$ConnectionProviderJdbcConnectionAccess@70091872] for (non-JTA) DDL execution was not in auto-commit mode; the Connection 'local transaction' will be committed and the Connection will be set into auto-commit mode.
Hibernate: 
    
    create table inherintance.kendaraan_tableperclass (
       id varchar(255) not null,
        cc int4,
        jumlah_cylinder int4,
        jumlah_roda int4,
        nama varchar(50),
        nama_pabrikan varchar(50) not null,
        primary key (id)
    )
Hibernate: 
    
    create table inherintance.mobil_tableperclass (
       id varchar(255) not null,
        cc int4,
        jumlah_cylinder int4,
        jumlah_roda int4,
        nama varchar(50),
        nama_pabrikan varchar(50) not null,
        is_all_wheel_drive boolean,
        jumlah_kursi int4,
        primary key (id)
    )
Hibernate: 
    
    create table inherintance.motor_tableperclass (
       id varchar(255) not null,
        cc int4,
        jumlah_cylinder int4,
        jumlah_roda int4,
        nama varchar(50),
        nama_pabrikan varchar(50) not null,
        jenis_rantai varchar(255),
        primary key (id)
    )
Jan 16, 2021 8:29:59 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    insert 
    into
        inherintance.motor_tableperclass
        (cc, jumlah_cylinder, jumlah_roda, nama, nama_pabrikan, jenis_rantai, id) 
    values
        (?, ?, ?, ?, ?, ?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanSeparateTable - mobil: MotorSeparateTableEntity(super=KendaraanSeparateTableEntity(id=600cd3a6-859b-4f63-9c66-dc4331e29c96, nama=BMW S1000RR, jumlahRoda=2, jumlahCylinder=4, cc=1000, namaPabrikan=PT. BMW Motorrad), jenisRantai=Rantai)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanSeparateTable - destroy hibernate session!
```

Setelah itu coba running unit testing untuk method `testSaveMobil` maka hasilnya akan seperti berikut:

```bash
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    insert 
    into
        inherintance.mobil_tableperclass
        (cc, jumlah_cylinder, jumlah_roda, nama, nama_pabrikan, is_all_wheel_drive, jumlah_kursi, id) 
    values
        (?, ?, ?, ?, ?, ?, ?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanSeparateTable - mobil: MobilSeparateTableEntity(super=KendaraanSeparateTableEntity(id=d98e1588-05a1-4c6f-950b-9204174c9009, nama=Honda BRIO, jumlahRoda=4, jumlahCylinder=4, cc=1000, namaPabrikan=PT. Honda Motor Company), jumlahKursi=4, allWheelDrive=false)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanSeparateTable - destroy hibernate session!
```

Setelah data mobil dan motor tersimpan, sekarang coba jalankan method `testFindById` maka hasilnya seperti berikut:

```bash
Jan 16, 2021 8:32:07 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        kendaraans0_.id as id1_7_0_,
        kendaraans0_.cc as cc2_7_0_,
        kendaraans0_.jumlah_cylinder as jumlah_c3_7_0_,
        kendaraans0_.jumlah_roda as jumlah_r4_7_0_,
        kendaraans0_.nama as nama5_7_0_,
        kendaraans0_.nama_pabrikan as nama_pab6_7_0_,
        kendaraans0_.is_all_wheel_drive as is_all_w1_10_0_,
        kendaraans0_.jumlah_kursi as jumlah_k2_10_0_,
        kendaraans0_.jenis_rantai as jenis_ra1_13_0_,
        kendaraans0_.clazz_ as clazz_0_ 
    from
        ( select
            id,
            cc,
            jumlah_cylinder,
            jumlah_roda,
            nama,
            nama_pabrikan,
            null::boolean as is_all_wheel_drive,
            null::int4 as jumlah_kursi,
            null::varchar as jenis_rantai,
            0 as clazz_ 
        from
            inherintance.kendaraan_tableperclass 
        union
        all select
            id,
            cc,
            jumlah_cylinder,
            jumlah_roda,
            nama,
            nama_pabrikan,
            is_all_wheel_drive,
            jumlah_kursi,
            null::varchar as jenis_rantai,
            1 as clazz_ 
        from
            inherintance.mobil_tableperclass 
        union
        all select
            id,
            cc,
            jumlah_cylinder,
            jumlah_roda,
            nama,
            nama_pabrikan,
            null::boolean as is_all_wheel_drive,
            null::int4 as jumlah_kursi,
            jenis_rantai,
            2 as clazz_ 
        from
            inherintance.motor_tableperclass 
    ) kendaraans0_ 
where
    kendaraans0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanSeparateTable - mobil: MobilSeparateTableEntity(super=KendaraanSeparateTableEntity(id=d98e1588-05a1-4c6f-950b-9204174c9009, nama=Honda BRIO, jumlahRoda=4, jumlahCylinder=4, cc=1000, namaPabrikan=PT. Honda Motor Company), jumlahKursi=4, allWheelDrive=false)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanSeparateTable - destroy hibernate session!
```

Dan yang terakhir jalankan unit testing method `testFindByMobilId` maka hasilnya seperti berikut:

```bash
Jan 16, 2021 8:33:15 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        mobilsepar0_.id as id1_7_0_,
        mobilsepar0_.cc as cc2_7_0_,
        mobilsepar0_.jumlah_cylinder as jumlah_c3_7_0_,
        mobilsepar0_.jumlah_roda as jumlah_r4_7_0_,
        mobilsepar0_.nama as nama5_7_0_,
        mobilsepar0_.nama_pabrikan as nama_pab6_7_0_,
        mobilsepar0_.is_all_wheel_drive as is_all_w1_10_0_,
        mobilsepar0_.jumlah_kursi as jumlah_k2_10_0_ 
    from
        inherintance.mobil_tableperclass mobilsepar0_ 
    where
        mobilsepar0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanSeparateTable - mobil: MobilSeparateTableEntity(super=KendaraanSeparateTableEntity(id=d98e1588-05a1-4c6f-950b-9204174c9009, nama=Honda BRIO, jumlahRoda=4, jumlahCylinder=4, cc=1000, namaPabrikan=PT. Honda Motor Company), jumlahKursi=4, allWheelDrive=false)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanSeparateTable - destroy hibernate session!
```

Dan berikut adalah data pada tabelnya:

![select-tables]({{ page.image_path | prepend: site.baseurl }}/select-tables.png)

## Summary

Untuk menggunakan `@Inheritance(strategy = InheritanceType.TABLE_PER_CLASS)` pastikan database management system yang digunakan support dengan `UNION`, `UNION ALL` contohnya seperti `PostgreSQL`, `MySQL`, `Oracle`, `DB2`, `H2`.