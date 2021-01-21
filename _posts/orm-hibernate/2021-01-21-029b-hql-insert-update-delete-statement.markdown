---
layout: post
title: "Insert, Update dan Delete Statement dengan HQL"
date: 2021-01-21T12:54:57+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- http://docs.jboss.org/hibernate/orm/5.2/quickstart/html_single/
- https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#hql
youtube: 
comments: true
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-29b
---

Hai, pada materi kali ini saya mau membahas tentang Insert, Update, dan Delete Statement menggunakan HQL (Hibernate Query Language). Ok nah jadi kita masih pake entity yang sama yaitu 

{% gist page.gist "MataKuliahEntity.java" %}

Dan berikut adalah implementasi DAO:

{% gist page.gist "HQLMatakuliahCUDDao.java" %}

Implementasi Unit Testing: 

{% gist page.gist "TestHQLMatakuliahCreateUpdateDelete.java" %}

Jika teman-temen jalankan unit testing pada method `testDeleteById`, maka hasilnya seperti berikut:

```bash
Jan 21, 2021 12:46:52 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    insert 
    into
        mapping.matakuliah
        (nama_kuliah, jumlah_sks, id) 
    values
        (?, ?, ?)
Hibernate: 
    delete 
    from
        mapping.mahasiswa_matakuliah_list 
    where
        (
            matakuliah_id
        ) in (
            select
                id 
            from
                mapping.matakuliah 
            where
                id=?
        )
Hibernate: 
    delete 
    from
        mapping.matakuliah 
    where
        id=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLMatakuliahCreateUpdateDelete - Data berhasil di hapus? true
Hibernate: 
    select
        matakuliah0_.id as id1_32_,
        matakuliah0_.nama_kuliah as nama_kul2_32_,
        matakuliah0_.jumlah_sks as jumlah_s3_32_ 
    from
        mapping.matakuliah matakuliah0_ 
    where
        matakuliah0_.id=?
[main] ERROR com.maryanto.dimas.bootcamp.example.query.hql.dao.HQLMatakuliahCUDDao - data not found
```

Kemudian coba jalankan method `testUpdateData`, maka berikut hasilnya:

```bash
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLMatakuliahCreateUpdateDelete - sebelum di updated: MataKuliahEntity(id=9e5ab8c0-fade-4da3-bcf1-9620db5b0412, nama=Matakuliah lama, sks=2)
Hibernate: 
    insert 
    into
        mapping.matakuliah
        (nama_kuliah, jumlah_sks, id) 
    values
        (?, ?, ?)
Hibernate: 
    update
        mapping.matakuliah 
    set
        nama_kuliah=?,
        jumlah_sks=? 
    where
        id=?
Hibernate: 
    update
        mapping.matakuliah 
    set
        nama_kuliah=?,
        jumlah_sks=? 
    where
        id=?
Hibernate: 
    select
        matakuliah0_.id as id1_32_,
        matakuliah0_.nama_kuliah as nama_kul2_32_,
        matakuliah0_.jumlah_sks as jumlah_s3_32_ 
    from
        mapping.matakuliah matakuliah0_ 
    where
        matakuliah0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLMatakuliahCreateUpdateDelete - setelah di updated: MataKuliahEntity(id=9e5ab8c0-fade-4da3-bcf1-9620db5b0412, nama=Matakuliah baru, sks=2)
Hibernate: 
    delete 
    from
        mapping.mahasiswa_matakuliah_list 
    where
        (
            matakuliah_id
        ) in (
            select
                id 
            from
                mapping.matakuliah 
            where
                id=?
        )
Hibernate: 
    delete 
    from
        mapping.matakuliah 
    where
        id=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLMatakuliahCreateUpdateDelete - destroy hibernate session!
```

## Summary

Dengan perintah HQL, kita bisa melakukan update dan delete layaknya seperti perintah native query (sql). Tetapi disini untuk Insert statement ada limitasi yaitu tidak bisa menggunakan `values` tetapi hanya bisa menggunakan `insert into EntityName1 (props) select * from EntityName2` coba lihat [ref disini](https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#hql-insert)