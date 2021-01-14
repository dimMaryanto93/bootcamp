---
layout: post
title: "OneToOne Mapping"
date: 2021-01-12T19:55:24+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- http://docs.jboss.org/hibernate/orm/5.2/quickstart/html_single/
- http://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/Hibernate_User_Guide.html
youtube: 
comments: true
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-21
---

Untuk mencoba mapping OneToOne kita perlu 2 table, contohnya disini kita buat antara `mahasiswa` dan `alamat`. pertama kita buat dulu entity untuk alamat seperti berikut

Implementasi Entity Alamat:

{% gist page.gist "AlamatEntity.java" %}

Implementasi DAO Alamat:

{% gist page.gist "AlamatEntityDao.java" %}

Setelah itu alamat akan berrelasi dengan mahasiswa dengan mapping @OneToOne. seperti berikut:

Implementasi Entity Mahasiswa:

{% gist page.gist "MahasiswaOneToOneEntity.java" %}

Implementasi DAO Mahasiswa:

{% gist page.gist "MahasiswaOneToOneEntityDao.java" %}

Setelah itu kita akan buat unit testingnya, seperti berikut:

{% gist page.gist "TestMahasiswaOneToOneEntityOneToOne.java" %}

Jika di running hasilnya seperti berikut:

```bash
INFO: HHH10001501: Connection obtained from JdbcConnectionAccess [org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator$ConnectionProviderJdbcConnectionAccess@29bcf51d] for (non-JTA) DDL execution was not in auto-commit mode; the Connection 'local transaction' will be committed and the Connection will be set into auto-commit mode.
Hibernate: 
    
    create table mapping.alamat (
       id varchar(255) not null,
        kecamatan varchar(100),
        kelurahan varchar(100),
        kode_pos int4,
        kota varchar(50),
        nama_jalan varchar(100),
        provinsi varchar(50),
        rt int4,
        rw int4,
        primary key (id)
    )
Hibernate: 
    
    create table mapping.mahasiswa_onetoone (
       id varchar(255) not null,
        nama varchar(50) not null,
        nim varchar(8) not null,
        tahun_masuk int4 not null,
        tanggal_lahir date not null,
        alamat varchar(255),
        primary key (id)
    )
Hibernate: 
    
    alter table if exists mapping.mahasiswa_onetoone 
       drop constraint if exists UK_pphjot1ymr0wvpn46lf87i8xp
Jan 12, 2021 7:21:35 PM org.hibernate.engine.jdbc.spi.SqlExceptionHelper$StandardWarningHandler logWarning
WARN: SQL Warning Code: 0, SQLState: 00000
Jan 12, 2021 7:21:35 PM org.hibernate.engine.jdbc.spi.SqlExceptionHelper$StandardWarningHandler logWarning
WARN: constraint "uk_pphjot1ymr0wvpn46lf87i8xp" of relation "mahasiswa_onetoone" does not exist, skipping
Hibernate: 
    
    alter table if exists mapping.mahasiswa_onetoone 
       add constraint UK_pphjot1ymr0wvpn46lf87i8xp unique (nim)
Hibernate: 
    
    alter table if exists mapping.mahasiswa_onetoone 
       add constraint FK1sp9lq015h4m5fag7jbakcy3j 
       foreign key (alamat) 
       references mapping.alamat
Jan 12, 2021 7:21:35 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaOneToOneEntityOneToOne - mahasiswa baru: MahasiswaOneToOneEntity(id=d9aa105a-78aa-4168-a5d8-f1665f0b9730, nim=10511148, nama=Dimas Maryanto, tanggalLahir=1993-03-01, tahunMasuk=2011, alamat=AlamatEntity(id=f3d7f449-85fb-4e10-835e-cc5983fd2876, provinsi=Jawa Barat, kota=Kab. Bandung, kelurahan=Cileunyi, kecamatan=Cinunuk, rw=18, rt=6, kodePos=40526, namaJalan=Jl Bukit indah))
Hibernate: 
    insert 
    into
        mapping.alamat
        (kecamatan, kelurahan, kode_pos, kota, nama_jalan, provinsi, rt, rw, id) 
    values
        (?, ?, ?, ?, ?, ?, ?, ?, ?)
Hibernate: 
    insert 
    into
        mapping.mahasiswa_onetoone
        (alamat, nama, nim, tahun_masuk, tanggal_lahir, id) 
    values
        (?, ?, ?, ?, ?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaOneToOneEntityOneToOne - destroy hibernate session!
```

Berikut adalah hasilnya di table `mahasiswa` dan `alamat` :

![select-tables]({{site.baseurl}}{{page.image_path}}/select-tables.png)

## Summary 

OneToOne mapping, kita harus menggunakan annotation` @OneToOne` dan `@JoinColumn` untuk melakukan modifikasi spesifikasi pada column referencenya.
