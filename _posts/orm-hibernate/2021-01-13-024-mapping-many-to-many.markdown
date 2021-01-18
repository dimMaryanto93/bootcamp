---
layout: post
title: "ManyToMany Mapping"
date: 2021-01-13T15:08:30+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- http://docs.jboss.org/hibernate/orm/5.2/quickstart/html_single/
- http://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/Hibernate_User_Guide.html
youtube: https://www.youtube.com/watch?v=cz0jiWqM2HY&list=PLV1-tdmPblvxHxNh867D1JR4u52LgzeIr&index=22
comments: true
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-24
---

Untuk menggunakan mapping `@ManyToMany` kita akan buat table baru yaitu `mahasiswa` dan `matakuliah`, berikut adalah perancangan databasenya:

![erd]({{site.baseurl}}{{page.image_path}}/erd.png)

Implementasi Entity `Matakuliah`:

{% gist page.gist "MataKuliahEntity.java" %}

Implementasi DAO `Matakuliah`:

{% gist page.gist "MataKuliahEntityDao.java" %}

Implementasi Entity `Mahasiswa`:

{% gist page.gist "MahasiswaManyToManyEntity.java" %}

Implementasi DAO `Mahasiswa`:

{% gist page.gist "MahasiswaManyToManyEntityDao.java" %}

Implementasi Unit Testing `Mahasiswa`:

{% gist page.gist "TestMahasiswaManyToManyEntity.java" %}

Jika di running, maka hasilnya seperti berikut:

```bash
INFO: HHH10001501: Connection obtained from JdbcConnectionAccess [org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator$ConnectionProviderJdbcConnectionAccess@2eda2062] for (non-JTA) DDL execution was not in auto-commit mode; the Connection 'local transaction' will be committed and the Connection will be set into auto-commit mode.
Hibernate: 
    
    create table mapping.mahasiswa_manytomany (
       id varchar(255) not null,
        nama varchar(50) not null,
        nim varchar(8) not null,
        tahun_masuk int4 not null,
        tanggal_lahir date not null,
        primary key (id)
    )
Hibernate: 
    
    create table mapping.mahasiswa_matakuliah_list (
       mahasiswa_id varchar(255) not null,
        matakuliah_id varchar(255) not null,
        primary key (mahasiswa_id, matakuliah_id)
    )
Hibernate: 
    
    create table mapping.matakuliah (
       id varchar(255) not null,
        nama_kuliah varchar(255),
        jumlah_sks int4,
        primary key (id)
    )
Hibernate: 
    
    alter table if exists mapping.mahasiswa_manytomany 
       drop constraint if exists UK_4vh8maxlaemdx4ffu3ey3dym5
Jan 13, 2021 2:28:20 PM org.hibernate.engine.jdbc.spi.SqlExceptionHelper$StandardWarningHandler logWarning
WARN: SQL Warning Code: 0, SQLState: 00000
Jan 13, 2021 2:28:20 PM org.hibernate.engine.jdbc.spi.SqlExceptionHelper$StandardWarningHandler logWarning
WARN: constraint "uk_4vh8maxlaemdx4ffu3ey3dym5" of relation "mahasiswa_manytomany" does not exist, skipping
Hibernate: 
    
    alter table if exists mapping.mahasiswa_manytomany 
       add constraint UK_4vh8maxlaemdx4ffu3ey3dym5 unique (nim)
Hibernate: 
    
    alter table if exists mapping.mahasiswa_matakuliah_list 
       add constraint fk_msh_kuliah_matakuliah_id 
       foreign key (matakuliah_id) 
       references mapping.matakuliah
Hibernate: 
    
    alter table if exists mapping.mahasiswa_matakuliah_list 
       add constraint fk_msh_kuliah_mahasiswa_id 
       foreign key (mahasiswa_id) 
       references mapping.mahasiswa_manytomany
Jan 13, 2021 2:28:20 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaManyToManyEntity - mahasiswa baru: MahasiswaManyToManyEntity(id=24c3eb73-9857-4432-a3c7-d175fb0fc7dc, nim=10512148, nama=Dimas Maryanto, tanggalLahir=1993-03-01, tahunMasuk=2012)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaManyToManyEntity - mahasiswa baru: MahasiswaManyToManyEntity(id=c495b72a-6ca8-4fb0-830b-932c105c4447, nim=10512150, nama=Muhamad Yusuf, tanggalLahir=1992-01-01, tahunMasuk=2012)
Hibernate: 
    insert 
    into
        mapping.matakuliah
        (nama_kuliah, jumlah_sks, id) 
    values
        (?, ?, ?)
Hibernate: 
    insert 
    into
        mapping.matakuliah
        (nama_kuliah, jumlah_sks, id) 
    values
        (?, ?, ?)
Hibernate: 
    insert 
    into
        mapping.mahasiswa_manytomany
        (nama, nim, tahun_masuk, tanggal_lahir, id) 
    values
        (?, ?, ?, ?, ?)
Hibernate: 
    insert 
    into
        mapping.mahasiswa_manytomany
        (nama, nim, tahun_masuk, tanggal_lahir, id) 
    values
        (?, ?, ?, ?, ?)
Hibernate: 
    insert 
    into
        mapping.mahasiswa_matakuliah_list
        (mahasiswa_id, matakuliah_id) 
    values
        (?, ?)
Hibernate: 
    insert 
    into
        mapping.mahasiswa_matakuliah_list
        (mahasiswa_id, matakuliah_id) 
    values
        (?, ?)
Hibernate: 
    insert 
    into
        mapping.mahasiswa_matakuliah_list
        (mahasiswa_id, matakuliah_id) 
    values
        (?, ?)
Hibernate: 
    insert 
    into
        mapping.mahasiswa_matakuliah_list
        (mahasiswa_id, matakuliah_id) 
    values
        (?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaManyToManyEntity - destroy hibernate session!
```

dan jika kita running unit test untuk find by mahasiswa id maka hasilnya seperti berikut:

```bash
Jan 13, 2021 2:30:04 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        mahasiswam0_.id as id1_13_0_,
        mahasiswam0_.nama as nama2_13_0_,
        mahasiswam0_.nim as nim3_13_0_,
        mahasiswam0_.tahun_masuk as tahun_ma4_13_0_,
        mahasiswam0_.tanggal_lahir as tanggal_5_13_0_ 
    from
        mapping.mahasiswa_manytomany mahasiswam0_ 
    where
        mahasiswam0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaManyToManyEntity - mahasiswa: MahasiswaManyToManyEntity(id=24c3eb73-9857-4432-a3c7-d175fb0fc7dc, nim=10512148, nama=Dimas Maryanto, tanggalLahir=1993-03-01, tahunMasuk=2012)
Hibernate: 
    select
        count(matakuliah_id) 
    from
        mapping.mahasiswa_matakuliah_list 
    where
        mahasiswa_id =?
Hibernate: 
    select
        listmataku0_.mahasiswa_id as mahasisw1_15_0_,
        listmataku0_.matakuliah_id as matakuli2_15_0_,
        matakuliah1_.id as id1_18_1_,
        matakuliah1_.nama_kuliah as nama_kul2_18_1_,
        matakuliah1_.jumlah_sks as jumlah_s3_18_1_ 
    from
        mapping.mahasiswa_matakuliah_list listmataku0_ 
    inner join
        mapping.matakuliah matakuliah1_ 
            on listmataku0_.matakuliah_id=matakuliah1_.id 
    where
        listmataku0_.mahasiswa_id=?
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaManyToManyEntity - list matakuliah {
    size: 2, 
    data: [MataKuliahEntity(id=733be4ef-20fb-4d16-bbfe-b4b6c31ee8d3, nama=SKRIPSI, sks=6), MataKuliahEntity(id=79c06b62-e70c-41f3-b42d-3aa63ab8d366, nama=Pemograman Java 1, sks=3)]
}
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaManyToManyEntity - destroy hibernate session!
```

And yang terakhir untuk unit testing yang find by matakuliah id, hasilnya seperti berikut:

```bash
Jan 13, 2021 3:02:51 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        matakuliah0_.id as id1_18_0_,
        matakuliah0_.nama_kuliah as nama_kul2_18_0_,
        matakuliah0_.jumlah_sks as jumlah_s3_18_0_ 
    from
        mapping.matakuliah matakuliah0_ 
    where
        matakuliah0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaManyToManyEntity - kelas: MataKuliahEntity(id=733be4ef-20fb-4d16-bbfe-b4b6c31ee8d3, nama=SKRIPSI, sks=6)
Hibernate: 
    select
        listmahasi0_.matakuliah_id as matakuli2_15_0_,
        listmahasi0_.mahasiswa_id as mahasisw1_15_0_,
        mahasiswam1_.id as id1_13_1_,
        mahasiswam1_.nama as nama2_13_1_,
        mahasiswam1_.nim as nim3_13_1_,
        mahasiswam1_.tahun_masuk as tahun_ma4_13_1_,
        mahasiswam1_.tanggal_lahir as tanggal_5_13_1_ 
    from
        mapping.mahasiswa_matakuliah_list listmahasi0_ 
    inner join
        mapping.mahasiswa_manytomany mahasiswam1_ 
            on listmahasi0_.mahasiswa_id=mahasiswam1_.id 
    where
        listmahasi0_.matakuliah_id=?
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaManyToManyEntity - list mahasiswa {
size: 2, 
data: [MahasiswaManyToManyEntity(id=24c3eb73-9857-4432-a3c7-d175fb0fc7dc, nim=10512148, nama=Dimas Maryanto, tanggalLahir=1993-03-01, tahunMasuk=2012), MahasiswaManyToManyEntity(id=c495b72a-6ca8-4fb0-830b-932c105c4447, nim=10512150, nama=Muhamad Yusuf, tanggalLahir=1992-01-01, tahunMasuk=2012)]
}
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.TestMahasiswaManyToManyEntity - destroy hibernate session!
```

## Summary 

Untuk menggunakan mapping `@ManyToMany` ini perlu ketelitian, jika tidak biasanya akan terjadi **problem endless loop** (berulang secara terus-menerus). Dengan annotation `@ToString.Exclude`, `@EqualsAndHashCode.Exclude`, `@FieldNameConstants.Exclude` untuk mencegah pemanggilan secara berulang (kalo temen-temen menggunakan project lombok)