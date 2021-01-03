---
layout: post
title: "CRUD menggunakan Hibernate"
date: 2020-11-21T15:47:35+07:00
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

Sebelum membuat CRUD Operation biasanya saya akan membuat interface seperti berikut:

{% gist page.gist "ReadRepository.java" %}

{% gist page.gist "CrudRepository.java" %}

Setelah membuat interface, biasanya saya juga membuat DAO (Data Access Object) yang mengimplement dari Repository tersebut:

{% gist page.gist "MahasiswaDao.java" %}


## Insert Data

Ok sekarang kita buat unit testing dengan nama `TestSaveMahasiswa` dalam package `com.maryanto.dimas.bootcamp.test` seperti berikut:

{% gist page.gist "TestSaveMahasiswa.java" %}

Setelah itu coba di run file, maka outpunya seperti berikut:

```bash
Jan 03, 2021 12:34:23 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    insert 
    into
        master.mahasiswa
        (is_active, bio, created_by, created_date, nama_mahasiswa, nim_mahasiswa, tanggal_lahir, tahun_masuk, kode) 
    values
        (?, ?, ?, ?, ?, ?, ?, ?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.TestSaveMahasiswa - mahasiswa saved: Mahasiswa(kode=1, nim=10511148, nama=Dimas Maryanto, thnMasuk=2015, tglLahir=1999-09-09, createdDate=2021-01-03T12:34:23.840972, createdBy=admin, active=true, biodata=null)
[main] INFO com.maryanto.dimas.bootcamp.test.TestSaveMahasiswa - destroy hibernate session!
```

Untuk mengecek datanya bener telah diinput, coba `select * from master.mahasiswa`

## Update Data

Ok sekarang kita buat unit testing dengan nama `TestUpdateMahasiswa` dalam package `com.maryanto.dimas.bootcamp.test` seperti berikut:

{% gist page.gist "TestUpdateMahasiswa.java" %}

Setelah itu coba di run file, maka outpunya seperti berikut:

```bash
Jan 03, 2021 12:36:06 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    update
        master.mahasiswa 
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
[main] INFO com.maryanto.dimas.bootcamp.test.TestSaveMahasiswa - mahasiswa was updated: Mahasiswa(kode=1, nim=10511150, nama=Dimas Maryanto (updated), thnMasuk=2014, tglLahir=1999-09-09, createdDate=2021-01-03T12:36:06.973299900, createdBy=admin, active=true, biodata=null)
[main] INFO com.maryanto.dimas.bootcamp.test.TestSaveMahasiswa - destroy hibernate session!

Process finished with exit code 0
```

## Find By Id

Ok sekarang kita buat unit testing dengan nama `TestFindByIdMahasiswa` dalam package `com.maryanto.dimas.bootcamp.test` seperti berikut:

{% gist page.gist "TestFindByIdMahasiswa.java" %}

Setelah itu coba di run file, maka outpunya seperti berikut:

```bash
Jan 03, 2021 12:36:43 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
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
        master.mahasiswa mahasiswa0_ 
    where
        mahasiswa0_.kode=?
[main] INFO com.maryanto.dimas.bootcamp.test.TestSaveMahasiswa - mahasiswa by id: Mahasiswa(kode=1, nim=10511150, nama=Dimas Maryanto (updated), thnMasuk=2014, tglLahir=1999-09-09, createdDate=2021-01-03T12:36:06.973300, createdBy=admin, active=true, biodata=null)
[main] INFO com.maryanto.dimas.bootcamp.test.TestSaveMahasiswa - destroy hibernate session!
```

## Delete Data

dan yang terkahir kita buat unit testing dengan nama `TestDeleteMahasiswa` dalam package `com.maryanto.dimas.bootcamp.test` seperti berikut:

{% gist page.gist "TestDeleteMahasiswa.java" %}

Setelah itu coba di run file, maka outpunya seperti berikut:

```bash
Jan 03, 2021 12:37:09 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
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
        master.mahasiswa mahasiswa0_ 
    where
        mahasiswa0_.kode=?
Hibernate: 
    delete 
    from
        master.mahasiswa 
    where
        kode=?
[main] INFO com.maryanto.dimas.bootcamp.test.TestSaveMahasiswa - mahasiswa was delete: Mahasiswa(kode=1, nim=10511150, nama=Dimas Maryanto (updated), thnMasuk=2014, tglLahir=1999-09-09, createdDate=2021-01-03T12:36:06.973300, createdBy=admin, active=true, biodata=null)
[main] INFO com.maryanto.dimas.bootcamp.test.TestSaveMahasiswa - destroy hibernate session!
```