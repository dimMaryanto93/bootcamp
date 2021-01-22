---
layout: post
title: "Collections Mapping as a Value Types"
date: 2021-01-19T15:30:57+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- https://docs.jboss.org/hibernate/stable/orm/userguide/html_single/Hibernate_User_Guide.html#collections-value
comments: true
youtube: https://www.youtube.com/watch?v=PIs1-hBSnsg&list=PLV1-tdmPblvxHxNh867D1JR4u52LgzeIr&index=32 
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-27b
---

Hai, di materi kali ini saya mau membahas tentang element collection dengan embedded type. Berikut adalah perancangan tabelnya:

![erd]({{ page.image_path | prepend: site.baseurl }}/erd.png)

Untuk model embedded kita masih menggunakan embedded alamat seperti sebelumnya yaitu seperti berikut:

{% gist page.gist "AlamatEmbeddable.java" %}

Berikut adalah implementasi Entity:

{% gist page.gist "MahasiswaElementCollectionAsType.java" %}

Implementasi DAO:

{% gist page.gist "MahasiswaElementCollectionAsTypeDao.java" %}

Implementasi Unit Testing:

{% gist page.gist "TestElementCollectionAsType.java" %}

Kemudian coba running unit testingnya pada method `testSaveMahasiswa` maka hasilnya akan seperti berikut:

```bash
INFO: HHH10001501: Connection obtained from JdbcConnectionAccess [org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator$ConnectionProviderJdbcConnectionAccess@51424203] for (non-JTA) DDL execution was not in auto-commit mode; the Connection 'local transaction' will be committed and the Connection will be set into auto-commit mode.
Hibernate: 
    
    create table collections.mahasiswa_address (
       mahasiswa_id int8 not null,
        kecamatan varchar(100),
        kelurahan varchar(100),
        kode_pos int4,
        kota varchar(50),
        nama_jalan varchar(100),
        provinsi varchar(50),
        rt int4,
        rw int4
    )
Hibernate: 
    
    create table collections.mahasiswa_listastype (
       id int8 not null,
        nama varchar(255) not null,
        nim varchar(255),
        primary key (id)
    )
Hibernate: 
    
    alter table if exists collections.mahasiswa_address 
       add constraint fk_address_mahasiswa_id 
       foreign key (mahasiswa_id) 
       references collections.mahasiswa_listastype
Jan 19, 2021 2:59:09 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        nextval ('hibernate_sequence')
Hibernate: 
    insert 
    into
        collections.mahasiswa_listastype
        (nama, nim, id) 
    values
        (?, ?, ?)
Hibernate: 
    insert 
    into
        collections.mahasiswa_address
        (mahasiswa_id, kecamatan, kelurahan, kode_pos, kota, nama_jalan, provinsi, rt, rw) 
    values
        (?, ?, ?, ?, ?, ?, ?, ?, ?)
Hibernate: 
    insert 
    into
        collections.mahasiswa_address
        (mahasiswa_id, kecamatan, kelurahan, kode_pos, kota, nama_jalan, provinsi, rt, rw) 
    values
        (?, ?, ?, ?, ?, ?, ?, ?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.collection.TestElementCollectionAsType - mahasiswa: MahasiswaElementCollectionAsType(id=14, nim=10511148, name=Dimas Maryanto)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.collection.TestElementCollectionAsType - destroy hibernate session!
```

Dan yang terakhir, coba jalankan method `findById` maka hasilnya akan seperti berikut:

```bash
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        mahasiswae0_.id as id1_2_0_,
        mahasiswae0_.nama as nama2_2_0_,
        mahasiswae0_.nim as nim3_2_0_ 
    from
        collections.mahasiswa_listastype mahasiswae0_ 
    where
        mahasiswae0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.collection.TestElementCollectionAsType - mahasiswa: MahasiswaElementCollectionAsType(id=14, nim=10511148, name=Dimas Maryanto)
Hibernate: 
    select
        addresses0_.mahasiswa_id as mahasisw1_0_0_,
        addresses0_.kecamatan as kecamata2_0_0_,
        addresses0_.kelurahan as keluraha3_0_0_,
        addresses0_.kode_pos as kode_pos4_0_0_,
        addresses0_.kota as kota5_0_0_,
        addresses0_.nama_jalan as nama_jal6_0_0_,
        addresses0_.provinsi as provinsi7_0_0_,
        addresses0_.rt as rt8_0_0_,
        addresses0_.rw as rw9_0_0_ 
    from
        collections.mahasiswa_address addresses0_ 
    where
        addresses0_.mahasiswa_id=?
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.collection.TestElementCollectionAsType - alamat: [AlamatEmbeddable(provinsi=Jawa Barat, kota=Kab. Bandung, kelurahan=Cileunyi, kecamatan=Cinunuk, rw=16, rt=7, kodePos=40526, namaJalan=Jl. Bukit Indah NO B8), AlamatEmbeddable(provinsi=DKI Jakarta, kota=Jakarta Selatan, kelurahan=Melawai, kecamatan=Cipete, rw=10, rt=1, kodePos=42105, namaJalan=Jl. Damai Buntu)]
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.collection.TestElementCollectionAsType - destroy hibernate session!
```

Ok sekarang kita check table di databasenya. maka hasilnya seperti berikut:

![select-tables]({{ page.image_path | prepend: site.baseurl }}/select-tables.png)