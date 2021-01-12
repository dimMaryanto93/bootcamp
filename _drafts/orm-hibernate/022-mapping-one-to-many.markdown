---
layout: post
title: "Hibernate @OneToMany Mapping"
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
image_path: /resources/posts/orm-hibernate-22
---

Untuk mencoba mapping OneToMany kita membutuhkan 3 table, contohnya `mahasiswa`, `alamat`, relasi antara `mahasiswa` dan `alamat` misal namanya kita sebut `mahasiswa_alamat_list`. Untuk alamat kita masih menggunakan class yang sebelunya yaitu 

Implementasi Entity Alamat:

{% gist page.gist "AlamatEntity.java" %}

Implementasi DAO Alamat:

{% gist page.gist "AlamatEntityDao.java" %}

Sedangkan untuk mahasiswa kita buat class baru, contohnya seperti berikut:

Implementasi Entity Mahasiswa:

{% gist page.gist "MahasiswaOneToManyEntity.java" %}

Implementasi DAO Mahasiswa:

{% gist page.gist "MahasiswaOneToManyEntityDao.java" %}

Setelah itu kita akan buat unit testingnya, seperti berikut:

{% gist page.gist "TestMahasiswaOneToManyEntity.java" %}


Jika di running maka akan menghasilkan seperti berikut:

```bash
INFO: HHH10001501: Connection obtained from JdbcConnectionAccess [org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator$ConnectionProviderJdbcConnectionAccess@64502326] for (non-JTA) DDL execution was not in auto-commit mode; the Connection 'local transaction' will be committed and the Connection will be set into auto-commit mode.
Hibernate: 
    
    create table mapping.mahasiswa_alamat_list (
       mahasiswa_id varchar(255) not null,
        alamat_id varchar(255) not null
    )
Hibernate: 
    
    create table mapping.mahasiswa_onetomany (
       id varchar(255) not null,
        nama varchar(50) not null,
        nim varchar(8) not null,
        tahun_masuk int4 not null,
        tanggal_lahir date not null,
        primary key (id)
    )
Hibernate: 
    
    alter table if exists mapping.mahasiswa_alamat_list 
       drop constraint if exists UK_931a2tmanbisy2blist4hpad3
Jan 12, 2021 7:34:52 PM org.hibernate.engine.jdbc.spi.SqlExceptionHelper$StandardWarningHandler logWarning
WARN: SQL Warning Code: 0, SQLState: 00000
Jan 12, 2021 7:34:52 PM org.hibernate.engine.jdbc.spi.SqlExceptionHelper$StandardWarningHandler logWarning
WARN: constraint "uk_931a2tmanbisy2blist4hpad3" of relation "mahasiswa_alamat_list" does not exist, skipping
Hibernate: 
    
    alter table if exists mapping.mahasiswa_alamat_list 
       add constraint UK_931a2tmanbisy2blist4hpad3 unique (alamat_id)
Hibernate: 
    
    alter table if exists mapping.mahasiswa_onetomany 
       drop constraint if exists UK_6jp8c1te4duklyhwsj8vhfbi3
Jan 12, 2021 7:34:52 PM org.hibernate.engine.jdbc.spi.SqlExceptionHelper$StandardWarningHandler logWarning
WARN: SQL Warning Code: 0, SQLState: 00000
Jan 12, 2021 7:34:52 PM org.hibernate.engine.jdbc.spi.SqlExceptionHelper$StandardWarningHandler logWarning
WARN: constraint "uk_6jp8c1te4duklyhwsj8vhfbi3" of relation "mahasiswa_onetomany" does not exist, skipping
Hibernate: 
    
    alter table if exists mapping.mahasiswa_onetomany 
       add constraint UK_6jp8c1te4duklyhwsj8vhfbi3 unique (nim)
Hibernate: 
    
    alter table if exists mapping.mahasiswa_alamat_list 
       add constraint fk_alamat_id 
       foreign key (alamat_id) 
       references mapping.alamat
Hibernate: 
    
    alter table if exists mapping.mahasiswa_alamat_list 
       add constraint fk_mahasiswa_id 
       foreign key (mahasiswa_id) 
       references mapping.mahasiswa_onetomany
Jan 12, 2021 7:34:52 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaOneToManyEntity - mahasiswa baru: MahasiswaOneToManyEntity(id=12bd5796-5dcf-4db7-b365-98c1928c149c, nim=10511148, nama=Dimas Maryanto, tanggalLahir=1993-03-01, tahunMasuk=2011, listAlamat=[AlamatEntity(id=a24c86f6-a628-4250-9496-518f4f149f05, provinsi=Jawa Barat, kota=Kab. Bandung, kelurahan=Cileunyi, kecamatan=Cinunuk, rw=18, rt=6, kodePos=40526, namaJalan=Jl Bukit indah B8), AlamatEntity(id=c344fd83-0274-4188-bb2a-85ba135fb62f, provinsi=Jawa Barat, kota=Kab. Bandung, kelurahan=Cileunyi, kecamatan=Cinunuk, rw=18, rt=6, kodePos=40526, namaJalan=Jl Bukit indah B8 A)])
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
        mapping.alamat
        (kecamatan, kelurahan, kode_pos, kota, nama_jalan, provinsi, rt, rw, id) 
    values
        (?, ?, ?, ?, ?, ?, ?, ?, ?)
Hibernate: 
    insert 
    into
        mapping.mahasiswa_onetomany
        (nama, nim, tahun_masuk, tanggal_lahir, id) 
    values
        (?, ?, ?, ?, ?)
Hibernate: 
    insert 
    into
        mapping.mahasiswa_alamat_list
        (mahasiswa_id, alamat_id) 
    values
        (?, ?)
Hibernate: 
    insert 
    into
        mapping.mahasiswa_alamat_list
        (mahasiswa_id, alamat_id) 
    values
        (?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaOneToManyEntity - destroy hibernate session!
```

Kemudian kita check di tabel `mahasiswa`, `alamat` dan `mahasiswa_alamat_list` berikut:

![select-tables]({{site.baseurl}}{{page.image_path}}/select-tables.png)

## Summary 

Untuk OneToMany Mapping kita harus menggunakan `@OneToMany` dan menggunakan `@JoinTable` sebagai tabel penghubung antara property `List<AlamatEntity>` dan class `MahasiswaOneToManyEntity`