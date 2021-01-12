---
layout: post
title: "Hibernate @ManyToOne Mapping"
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
image_path: /resources/posts/orm-hibernate-23
---

Untuk menggunakan mapping @ManyToOne kita akan buat mapping baru yaitu `mahasiswa` dan `kelas`, contohnya seperti berikut:

Implementasi Entity kelas:

{% gist page.gist "KelasEntity.java" %}

Implementasi DAO Kelas:

{% gist page.gist "KelasEntityDao.java" %}

Implementasi Entity Mahasiswa:

{% gist page.gist "MahasiswaManyToOneEntity.java" %}

Implementasi DAO Mahasiswa:

{% gist page.gist "MahasiswaManyToOneEntityDao.java" %}

Berikut adalah implementasi Unit testing:

{% gist page.gist "TestMahasiswaManyToOneEntity.java" %}

Jika unit testing di running untuk method `testSaveMahasiswa` maka hasilnya seperti berikut:

```bash
INFO: HHH10001501: Connection obtained from JdbcConnectionAccess [org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator$ConnectionProviderJdbcConnectionAccess@553d2579] for (non-JTA) DDL execution was not in auto-commit mode; the Connection 'local transaction' will be committed and the Connection will be set into auto-commit mode.
Hibernate: 
    
    create table mapping.kelas (
       id varchar(255) not null,
        tahun_angkatan int4 not null,
        nama_kelas varchar(255) not null,
        program_studi varchar(255),
        primary key (id)
    )
Hibernate: 
    
    create table mapping.mahasiswa_manytoone (
       id varchar(255) not null,
        nama varchar(50) not null,
        nim varchar(8) not null,
        tahun_masuk int4 not null,
        tanggal_lahir date not null,
        kelas_id varchar(255) not null,
        primary key (id)
    )
Hibernate: 
    
    alter table if exists mapping.mahasiswa_manytoone 
       drop constraint if exists UK_sk3k6b2siwq7vk20exd12c9jm
Jan 12, 2021 8:20:42 PM org.hibernate.engine.jdbc.spi.SqlExceptionHelper$StandardWarningHandler logWarning
WARN: SQL Warning Code: 0, SQLState: 00000
Jan 12, 2021 8:20:42 PM org.hibernate.engine.jdbc.spi.SqlExceptionHelper$StandardWarningHandler logWarning
WARN: constraint "uk_sk3k6b2siwq7vk20exd12c9jm" of relation "mahasiswa_manytoone" does not exist, skipping
Hibernate: 
    
    alter table if exists mapping.mahasiswa_manytoone 
       add constraint UK_sk3k6b2siwq7vk20exd12c9jm unique (nim)
Hibernate: 
    
    alter table if exists mapping.mahasiswa_manytoone 
       add constraint FKctjdgm537ew2hufr8mp27f6cp 
       foreign key (kelas_id) 
       references mapping.kelas
Jan 12, 2021 8:20:42 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaManyToOneEntity - mahasiswa baru: MahasiswaManyToOneEntity(id=a36b7e84-c41a-4ff0-a693-f0053d7d31c9, nim=10512148, nama=Dimas Maryanto, tanggalLahir=1993-03-01, tahunMasuk=2012, kelas=KelasEntity(id=5f5e61ea-a46c-4ffe-b05a-8831232b29af, nama=IS-01, angkatan=2011, programStudi=Informatika, listMahasiswa=null))
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaManyToOneEntity - mahasiswa baru: MahasiswaManyToOneEntity(id=884a8d4c-f74d-498c-8174-89da28d7caa1, nim=10512150, nama=Muhamad Yusuf, tanggalLahir=1992-01-01, tahunMasuk=2012, kelas=KelasEntity(id=5f5e61ea-a46c-4ffe-b05a-8831232b29af, nama=IS-01, angkatan=2011, programStudi=Informatika, listMahasiswa=null))
Hibernate: 
    insert 
    into
        mapping.kelas
        (tahun_angkatan, nama_kelas, program_studi, id) 
    values
        (?, ?, ?, ?)
Hibernate: 
    insert 
    into
        mapping.mahasiswa_manytoone
        (kelas_id, nama, nim, tahun_masuk, tanggal_lahir, id) 
    values
        (?, ?, ?, ?, ?, ?)
Hibernate: 
    insert 
    into
        mapping.mahasiswa_manytoone
        (kelas_id, nama, nim, tahun_masuk, tanggal_lahir, id) 
    values
        (?, ?, ?, ?, ?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaManyToOneEntity - destroy hibernate session!
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaManyToOneEntity - init hibernate session
```

Kemudian kita check ke tabel `kelas` dan `mahasiswa_manytoone` seperti berikut:

![select-tables]({{site.baseurl}}{{page.image_path}}/select-tables.png)

Dan kemudian juga selain itu klo kita jalankan find by id, untuk yang mahasiswa maka hasilnya seperti berikut:

```bash
Jan 12, 2021 8:26:32 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        mahasiswam0_.id as id1_13_0_,
        mahasiswam0_.kelas_id as kelas_id6_13_0_,
        mahasiswam0_.nama as nama2_13_0_,
        mahasiswam0_.nim as nim3_13_0_,
        mahasiswam0_.tahun_masuk as tahun_ma4_13_0_,
        mahasiswam0_.tanggal_lahir as tanggal_5_13_0_,
        kelasentit1_.id as id1_11_1_,
        kelasentit1_.tahun_angkatan as tahun_an2_11_1_,
        kelasentit1_.nama_kelas as nama_kel3_11_1_,
        kelasentit1_.program_studi as program_4_11_1_ 
    from
        mapping.mahasiswa_manytoone mahasiswam0_ 
    inner join
        mapping.kelas kelasentit1_ 
            on mahasiswam0_.kelas_id=kelasentit1_.id 
    where
        mahasiswam0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaManyToOneEntity - mahasiswa: MahasiswaManyToOneEntity(id=a36b7e84-c41a-4ff0-a693-f0053d7d31c9, nim=10512148, nama=Dimas Maryanto, tanggalLahir=1993-03-01, tahunMasuk=2012, kelas=KelasEntity(id=5f5e61ea-a46c-4ffe-b05a-8831232b29af, nama=IS-01, angkatan=2011, programStudi=Informatika))
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaManyToOneEntity - destroy hibernate session!
```

Dan kemudian find by id kelas, maka hasilnya seperti berikut:

```bash
Jan 12, 2021 8:28:44 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        kelasentit0_.id as id1_11_0_,
        kelasentit0_.tahun_angkatan as tahun_an2_11_0_,
        kelasentit0_.nama_kelas as nama_kel3_11_0_,
        kelasentit0_.program_studi as program_4_11_0_ 
    from
        mapping.kelas kelasentit0_ 
    where
        kelasentit0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaManyToOneEntity - kelas: KelasEntity(id=5f5e61ea-a46c-4ffe-b05a-8831232b29af, nama=IS-01, angkatan=2011, programStudi=Informatika)
Hibernate: 
    select
        listmahasi0_.kelas_id as kelas_id6_13_0_,
        listmahasi0_.id as id1_13_0_,
        listmahasi0_.id as id1_13_1_,
        listmahasi0_.kelas_id as kelas_id6_13_1_,
        listmahasi0_.nama as nama2_13_1_,
        listmahasi0_.nim as nim3_13_1_,
        listmahasi0_.tahun_masuk as tahun_ma4_13_1_,
        listmahasi0_.tanggal_lahir as tanggal_5_13_1_ 
    from
        mapping.mahasiswa_manytoone listmahasi0_ 
    where
        listmahasi0_.kelas_id=?
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaManyToOneEntity - list mahasiswa: [MahasiswaManyToOneEntity(id=a36b7e84-c41a-4ff0-a693-f0053d7d31c9, nim=10512148, nama=Dimas Maryanto, tanggalLahir=1993-03-01, tahunMasuk=2012, kelas=KelasEntity(id=5f5e61ea-a46c-4ffe-b05a-8831232b29af, nama=IS-01, angkatan=2011, programStudi=Informatika)), MahasiswaManyToOneEntity(id=884a8d4c-f74d-498c-8174-89da28d7caa1, nim=10512150, nama=Muhamad Yusuf, tanggalLahir=1992-01-01, tahunMasuk=2012, kelas=KelasEntity(id=5f5e61ea-a46c-4ffe-b05a-8831232b29af, nama=IS-01, angkatan=2011, programStudi=Informatika))]
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaManyToOneEntity - destroy hibernate session!
```

## Summary 

Untuk menggunakan `@ManyToOne` sebetulnya sama seperti `@OneToOne` mapping hanya saja kita perlu pastikan dari data apakah sesuai. kadang beberapa orang tidak mempertimbangkan annotationnya yang dipilih apakah `@OneToOne` atau `@ManyToOne` meskipun tidak berpengaruh ke bisnis aplikasi tetapi untuk menyamakan prospectif sesama developer!!.

Dan untuk mapping `@OneToMany(mappedBy="property")` ini optional ya (boleh kalo gak pake juga gpp kok). tujuannya saya pake itu, untuk memanggil daftar mahasiswa yang ada pada kelas tersebut seperti yang saya praktekan pada unit testing find by id kelas.