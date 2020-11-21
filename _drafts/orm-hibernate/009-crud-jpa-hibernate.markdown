---
layout: post
title: "CRUD menggunakan Hibernate"
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
---

Sekarang saya akan membuat CRUD dengan menggunakan Hibernate Framework. Untuk membuat CRUD di hibernate sebenarnya sangat mudah, karena kita tidak perlu menggunakan query tetapi pemograman SQLnya masih tetap ada tapi nanti kita akan bahas di materi yang namananya Hibernate Query language atau yang lebih dikenal HQL.

## Insert Data

Ok sekarang kita buat unit testing dengan nama `TestSaveMahasiswa` dalam package `com.maryanto.dimas.bootcamp.test` seperti berikut:

{% gist page.gist "TestSaveMahasiswa.java" %}

Setelah itu coba di run file, maka outpunya seperti berikut:

```bash
Nov 21, 2020 2:50:19 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        nextval ('hibernate_sequence')
[main] INFO com.maryanto.dimas.bootcamp.test.TestSaveMahasiswa - mahasiswa saved Mahasiswa(kode=1, nim=10511148, nama=Dimas Maryanto, thnMasuk=2015, tglLahir=1999-09-09, createdDate=2020-11-21T14:50:19.232315300, createdBy=admin, active=true, biodata=null) with id: 1
Hibernate: 
    insert 
    into
        master_mahasiswa
        (is_active, bio, created_by, created_date, nama_mahasiswa, nim_mahasiswa, tanggal_lahir, tahun_masuk, kode) 
    values
        (?, ?, ?, ?, ?, ?, ?, ?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.TestSaveMahasiswa - destroy hibernate session!
```

Untuk mengecek datanya bener telah diinput, coba `select * from master_mahasiswa`

## Update Data

Ok sekarang kita buat unit testing dengan nama `TestUpdateMahasiswa` dalam package `com.maryanto.dimas.bootcamp.test` seperti berikut:

{% gist page.gist "TestUpdateMahasiswa.java" %}

Setelah itu coba di run file, maka outpunya seperti berikut:

```bash
Hibernate: 
    update
        master_mahasiswa 
    set
        is_active=?,
        bio=?,
        created_by=?,
        created_date=?,
        nama_mahasiswa=?,
        nim_mahasiswa=?,
        tanggal_lahir=?,
        tahun_masuk=? 
    where
        kode=?
[main] INFO com.maryanto.dimas.bootcamp.test.TestSaveMahasiswa - mahasiswa was updated: Mahasiswa(kode=1, nim=10511150, nama=Dimas Maryanto (updated), thnMasuk=2014, tglLahir=1999-09-09, createdDate=2020-11-21T15:34:50.448261800, createdBy=admin, active=true, biodata=null)
[main] INFO com.maryanto.dimas.bootcamp.test.TestSaveMahasiswa - destroy hibernate session!
```

## Find By Id

Ok sekarang kita buat unit testing dengan nama `TestFindByIdMahasiswa` dalam package `com.maryanto.dimas.bootcamp.test` seperti berikut:

{% gist page.gist "TestFindByIdMahasiswa.java" %}

Setelah itu coba di run file, maka outpunya seperti berikut:

```bash
Hibernate: 
    select
        mahasiswa0_.kode as kode1_0_0_,
        mahasiswa0_.is_active as is_activ2_0_0_,
        mahasiswa0_.bio as bio3_0_0_,
        mahasiswa0_.created_by as created_4_0_0_,
        mahasiswa0_.created_date as created_5_0_0_,
        mahasiswa0_.nama_mahasiswa as nama_mah6_0_0_,
        mahasiswa0_.nim_mahasiswa as nim_maha7_0_0_,
        mahasiswa0_.tanggal_lahir as tanggal_8_0_0_,
        mahasiswa0_.tahun_masuk as tahun_ma9_0_0_ 
    from
        master_mahasiswa mahasiswa0_ 
    where
        mahasiswa0_.kode=?
[main] INFO com.maryanto.dimas.bootcamp.test.TestSaveMahasiswa - mahasiswa by id: Mahasiswa(kode=1, nim=10511148, nama=Dimas Maryanto, thnMasuk=2015, tglLahir=1999-09-09, createdDate=2020-11-21T15:43:39.220661, createdBy=admin, active=true, biodata=null)
[main] INFO com.maryanto.dimas.bootcamp.test.TestSaveMahasiswa - destroy hibernate session!
```

## Delete Data

dan yang terkahir kita buat unit testing dengan nama `TestDeleteMahasiswa` dalam package `com.maryanto.dimas.bootcamp.test` seperti berikut:

{% gist page.gist "TestDeleteMahasiswa.java" %}

Setelah itu coba di run file, maka outpunya seperti berikut:

```bash
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        mahasiswa0_.kode as kode1_0_0_,
        mahasiswa0_.is_active as is_activ2_0_0_,
        mahasiswa0_.bio as bio3_0_0_,
        mahasiswa0_.created_by as created_4_0_0_,
        mahasiswa0_.created_date as created_5_0_0_,
        mahasiswa0_.nama_mahasiswa as nama_mah6_0_0_,
        mahasiswa0_.nim_mahasiswa as nim_maha7_0_0_,
        mahasiswa0_.tanggal_lahir as tanggal_8_0_0_,
        mahasiswa0_.tahun_masuk as tahun_ma9_0_0_ 
    from
        master_mahasiswa mahasiswa0_ 
    where
        mahasiswa0_.kode=?
Hibernate: 
    delete 
    from
        master_mahasiswa 
    where
        kode=?
[main] INFO com.maryanto.dimas.bootcamp.test.TestSaveMahasiswa - mahasiswa was delete: Mahasiswa(kode=1, nim=10511148, nama=Dimas Maryanto, thnMasuk=2015, tglLahir=1999-09-09, createdDate=2020-11-21T15:39:49.421040, createdBy=admin, active=true, biodata=null)
[main] INFO com.maryanto.dimas.bootcamp.test.TestSaveMahasiswa - destroy hibernate session!
```