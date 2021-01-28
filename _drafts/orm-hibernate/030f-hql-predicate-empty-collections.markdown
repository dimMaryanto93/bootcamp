---
layout: post
title: "Empty Collections Predicate dengan HQL"
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#hql-empty-collection-predicate
youtube: 
comments: true
image_path: /resources/posts/orm-hibernate-030f
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
---

Hai, di materi kali ini saya mau membahas tentang operation `Empty Collection` menggunakan HQL. pada dasarnya operator empty collection terdiri dari `is empty` dan `is not empty` seperti berikut contoh implementasi DAO:

{% gist page.gist "HQLEmptyCollectionPredicateDao.java" %}

Implementasi Unit Testing: 

{% gist page.gist "TestHQLEmptyCollectionPredicates.java" %}

Setelah itu, kita check dulu datanya pada tabel di databse, seperti berikut:

![select-tables]({{ page.image_path | prepend: site.baseurl }}/select-tables.png)

Kemudian kita coba jalankan unit testingnya pada method `testMethodAsType()`, maka hasilnya seperti berikut:

```bash
Jan 28, 2021 2:27:08 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        mahasiswae0_.id as id1_2_,
        mahasiswae0_.nama as nama2_2_,
        mahasiswae0_.nim as nim3_2_ 
    from
        collections.mahasiswa_listastype mahasiswae0_ 
    where
        not (exists (select
            addresses1_.kecamatan,
            addresses1_.kelurahan,
            addresses1_.kode_pos,
            addresses1_.kota,
            addresses1_.nama_jalan,
            addresses1_.provinsi,
            addresses1_.rt,
            addresses1_.rw 
        from
            collections.mahasiswa_address addresses1_ 
        where
            mahasiswae0_.id=addresses1_.mahasiswa_id))
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLEmptyCollectionPredicates - list is empty: []
Hibernate: 
    select
        mahasiswae0_.id as id1_2_,
        mahasiswae0_.nama as nama2_2_,
        mahasiswae0_.nim as nim3_2_ 
    from
        collections.mahasiswa_listastype mahasiswae0_ 
    where
        exists (
            select
                addresses1_.kecamatan,
                addresses1_.kelurahan,
                addresses1_.kode_pos,
                addresses1_.kota,
                addresses1_.nama_jalan,
                addresses1_.provinsi,
                addresses1_.rt,
                addresses1_.rw 
            from
                collections.mahasiswa_address addresses1_ 
            where
                mahasiswae0_.id=addresses1_.mahasiswa_id
        )
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLEmptyCollectionPredicates - list is not empty: [MahasiswaElementCollectionAsType(id=14, nim=10511148, name=Dimas Maryanto)]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLEmptyCollectionPredicates - destroy hibernate session!
```

Kemudian coba jalankan method `testMethodAsValue()`, maka hasilnya seperti berikut:

```bash
Jan 28, 2021 2:28:02 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        mahasiswae0_.id as id1_3_,
        mahasiswae0_.alamat as alamat2_3_,
        mahasiswae0_.nama as nama3_3_,
        mahasiswae0_.nim as nim4_3_ 
    from
        collections.mahasiswa_listasvalue mahasiswae0_ 
    where
        not (exists (select
            hobies1_.hobi 
        from
            collections.mahasiswa_hoby hobies1_ 
        where
            mahasiswae0_.id=hobies1_.mahasiswa_id))
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLEmptyCollectionPredicates - list is empty: [MahasiswaElementCollectionAsValue(id=2, nim=empty, name=empty, address=empty)]
Hibernate: 
    select
        mahasiswae0_.id as id1_3_,
        mahasiswae0_.alamat as alamat2_3_,
        mahasiswae0_.nama as nama3_3_,
        mahasiswae0_.nim as nim4_3_ 
    from
        collections.mahasiswa_listasvalue mahasiswae0_ 
    where
        exists (
            select
                hobies1_.hobi 
            from
                collections.mahasiswa_hoby hobies1_ 
            where
                mahasiswae0_.id=hobies1_.mahasiswa_id
        )
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLEmptyCollectionPredicates - list is not empty: [MahasiswaElementCollectionAsValue(id=1, nim=test, name=test, address=test)]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLEmptyCollectionPredicates - destroy hibernate session!
```

Dan yang terakhir coba jalankan method `testMethodAsEntity()`, maka hasilnya seperti berikut:

```bash
Jan 28, 2021 2:28:54 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        mahasiswao0_.id as id1_30_,
        mahasiswao0_.nama as nama2_30_,
        mahasiswao0_.nim as nim3_30_,
        mahasiswao0_.tahun_masuk as tahun_ma4_30_,
        mahasiswao0_.tanggal_lahir as tanggal_5_30_ 
    from
        mapping.mahasiswa_onetomany mahasiswao0_ 
    where
        not (exists (select
            alamatenti2_.id 
        from
            mapping.mahasiswa_alamat_list listalamat1_,
            mapping.alamat alamatenti2_ 
        where
            mahasiswao0_.id=listalamat1_.mahasiswa_id 
            and listalamat1_.alamat_id=alamatenti2_.id))
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLEmptyCollectionPredicates - list is empty: [MahasiswaOneToManyEntity(id=2, nim=test1, nama=empty, tanggalLahir=2021-01-26, tahunMasuk=2010)]
Hibernate: 
    select
        mahasiswao0_.id as id1_30_,
        mahasiswao0_.nama as nama2_30_,
        mahasiswao0_.nim as nim3_30_,
        mahasiswao0_.tahun_masuk as tahun_ma4_30_,
        mahasiswao0_.tanggal_lahir as tanggal_5_30_ 
    from
        mapping.mahasiswa_onetomany mahasiswao0_ 
    where
        not (exists (select
            alamatenti2_.id 
        from
            mapping.mahasiswa_alamat_list listalamat1_,
            mapping.alamat alamatenti2_ 
        where
            mahasiswao0_.id=listalamat1_.mahasiswa_id 
            and listalamat1_.alamat_id=alamatenti2_.id))
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLEmptyCollectionPredicates - list is not empty: [MahasiswaOneToManyEntity(id=2, nim=test1, nama=empty, tanggalLahir=2021-01-26, tahunMasuk=2010)]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLEmptyCollectionPredicates - destroy hibernate session!
```