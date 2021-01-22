---
layout: post
title: "Inherintance Mapping metode Join Table"
date: 2021-01-16T18:51:36+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#entity-inheritance-joined-table
youtube: https://www.youtube.com/watch?v=dMhism_6dXc&list=PLV1-tdmPblvxHxNh867D1JR4u52LgzeIr&index=27
comments: true
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-25d
---

Hai di materi kali ini saya mau ngebahas Inherintance Mapping dengan metode Join Table. masih dalam contoh yang sama yaitu `kendaraan` yaitu `mobil` dan `motor` namun kali ini berikut adalah perancangan tabelnya:

![erd]({{ page.image_path | prepend: site.baseurl }}/erd.png)

and berikut adalah adalah Implementasi Entity Kendaraan:

{% gist page.gist "KendaraanJoinTableEntity.java" %}

Implementasi Entity Mobil:

{% gist page.gist "MobilJoinTableEntity.java" %}

Implementasi Entity Motor: 

{% gist page.gist "MotorJoinTableEntity.java" %}

Implementasi DAO Kendaraan:

{% gist page.gist "KendaraanJoinTableDao.java" %}

dan yang terakhir berikut adalah Implementasi Unit Testingnya:

{% gist page.gist "TestKendaraanJoinTable.java" %}

Jika di jalankan unit testing untuk method `testSaveMotor` maka hasilnya seperti berikut:

```bash
INFO: HHH10001501: Connection obtained from JdbcConnectionAccess [org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator$ConnectionProviderJdbcConnectionAccess@35563e4c] for (non-JTA) DDL execution was not in auto-commit mode; the Connection 'local transaction' will be committed and the Connection will be set into auto-commit mode.
Hibernate: 
    
    create table inherintance.kendaraan_jointable (
       id varchar(255) not null,
        cc int4,
        jumlah_cylinder int4,
        jumlah_roda int4,
        nama varchar(50),
        nama_pabrikan varchar(50) not null,
        primary key (id)
    )
Hibernate: 
    
    create table inherintance.mobil_jointable (
       is_all_wheel_drive boolean,
        jumlah_kursi int4,
        kendaraan_id varchar(255) not null,
        primary key (kendaraan_id)
    )
Hibernate: 
    
    create table inherintance.motor_jointable (
       jenis_rantai varchar(255),
        kendaraan_id varchar(255) not null,
        primary key (kendaraan_id)
    )
Hibernate: 
    
    alter table if exists inherintance.mobil_jointable 
       add constraint fk_kendaraan_mobil_id 
       foreign key (kendaraan_id) 
       references inherintance.kendaraan_jointable
Hibernate: 
    
    alter table if exists inherintance.motor_jointable 
       add constraint fk_kendaraan_motor_id 
       foreign key (kendaraan_id) 
       references inherintance.kendaraan_jointable
Jan 16, 2021 6:38:34 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    insert 
    into
        inherintance.kendaraan_jointable
        (cc, jumlah_cylinder, jumlah_roda, nama, nama_pabrikan, id) 
    values
        (?, ?, ?, ?, ?, ?)
Hibernate: 
    insert 
    into
        inherintance.motor_jointable
        (jenis_rantai, kendaraan_id) 
    values
        (?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanJoinTable - mobil: MotorJoinTableEntity(super=KendaraanJoinTableEntity(id=ba765eb1-14fc-43fd-aede-620158775065, nama=BMW S1000RR, jumlahRoda=2, jumlahCylinder=4, cc=1000, namaPabrikan=PT. BMW Motorrad), jenisRantai=Rantai)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanJoinTable - destroy hibernate session!
```

Kemudian coba jalankan unit testing untuk method `testSaveMobil` maka hasilnya seperti berikut:

```bash
Jan 16, 2021 6:39:56 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    insert 
    into
        inherintance.kendaraan_jointable
        (cc, jumlah_cylinder, jumlah_roda, nama, nama_pabrikan, id) 
    values
        (?, ?, ?, ?, ?, ?)
Hibernate: 
    insert 
    into
        inherintance.mobil_jointable
        (is_all_wheel_drive, jumlah_kursi, kendaraan_id) 
    values
        (?, ?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanJoinTable - mobil: MobilJoinTableEntity(super=KendaraanJoinTableEntity(id=3463b2ea-cf49-49f1-b1a1-682d46f95573, nama=Honda BRIO, jumlahRoda=4, jumlahCylinder=4, cc=1000, namaPabrikan=PT. Honda Motor Company), jumlahKursi=4, allWheelDrive=false)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanJoinTable - destroy hibernate session!
```

Setelah 2 data terinsert coba test untuk `findById` ganti dengan id yang udah tersedia di table, maka outputnya seperti berikut:

```bash
Jan 16, 2021 6:41:26 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        kendaraanj0_.id as id1_4_0_,
        kendaraanj0_.cc as cc2_4_0_,
        kendaraanj0_.jumlah_cylinder as jumlah_c3_4_0_,
        kendaraanj0_.jumlah_roda as jumlah_r4_4_0_,
        kendaraanj0_.nama as nama5_4_0_,
        kendaraanj0_.nama_pabrikan as nama_pab6_4_0_,
        kendaraanj0_1_.is_all_wheel_drive as is_all_w1_7_0_,
        kendaraanj0_1_.jumlah_kursi as jumlah_k2_7_0_,
        kendaraanj0_2_.jenis_rantai as jenis_ra1_9_0_,
        case 
            when kendaraanj0_1_.kendaraan_id is not null then 1 
            when kendaraanj0_2_.kendaraan_id is not null then 2 
            when kendaraanj0_.id is not null then 0 
        end as clazz_0_ 
    from
        inherintance.kendaraan_jointable kendaraanj0_ 
    left outer join
        inherintance.mobil_jointable kendaraanj0_1_ 
            on kendaraanj0_.id=kendaraanj0_1_.kendaraan_id 
    left outer join
        inherintance.motor_jointable kendaraanj0_2_ 
            on kendaraanj0_.id=kendaraanj0_2_.kendaraan_id 
    where
        kendaraanj0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanJoinTable - mobil: MobilJoinTableEntity(super=KendaraanJoinTableEntity(id=3463b2ea-cf49-49f1-b1a1-682d46f95573, nama=Honda BRIO, jumlahRoda=4, jumlahCylinder=4, cc=1000, namaPabrikan=PT. Honda Motor Company), jumlahKursi=4, allWheelDrive=false)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanJoinTable - destroy hibernate session!
```

Sekarang coba test untuk method `findByMobilId`, maka hasilnya seperti berikut:


```bash
Jan 16, 2021 6:42:40 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        mobiljoint0_.kendaraan_id as id1_4_0_,
        mobiljoint0_1_.cc as cc2_4_0_,
        mobiljoint0_1_.jumlah_cylinder as jumlah_c3_4_0_,
        mobiljoint0_1_.jumlah_roda as jumlah_r4_4_0_,
        mobiljoint0_1_.nama as nama5_4_0_,
        mobiljoint0_1_.nama_pabrikan as nama_pab6_4_0_,
        mobiljoint0_.is_all_wheel_drive as is_all_w1_7_0_,
        mobiljoint0_.jumlah_kursi as jumlah_k2_7_0_ 
    from
        inherintance.mobil_jointable mobiljoint0_ 
    inner join
        inherintance.kendaraan_jointable mobiljoint0_1_ 
            on mobiljoint0_.kendaraan_id=mobiljoint0_1_.id 
    where
        mobiljoint0_.kendaraan_id=?
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanJoinTable - mobil: MobilJoinTableEntity(super=KendaraanJoinTableEntity(id=3463b2ea-cf49-49f1-b1a1-682d46f95573, nama=Honda BRIO, jumlahRoda=4, jumlahCylinder=4, cc=1000, namaPabrikan=PT. Honda Motor Company), jumlahKursi=4, allWheelDrive=false)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanJoinTable - destroy hibernate session!
```

Nah gimana ada perbedaan? yes jadi klo kita search pake model super / induknya maka dia akan join ke semua tabel tetapi jika menggunakan spesifik model dia akan join ke tabel tertentu saja.

Berikut adalah hasil data yang di simpan dengan menggunakan join_table

![select-tables]({{ page.image_path | prepend: site.baseurl }}/select-tables.png)

## Summary 

Dengan menggunakan metode `@Inheritance(strategy = InheritanceType.JOINED)` ini akan mepengaruhi performa aplikasi jadi _beaware_ dalam pengguanaanya