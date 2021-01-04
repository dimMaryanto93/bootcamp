---
layout: post
title: "Composite Primary Key"
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- http://docs.jboss.org/hibernate/orm/5.2/quickstart/html_single/
- http://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/Hibernate_User_Guide.html
- https://www.baeldung.com/jpa-composite-primary-keys
- https://stackoverflow.com/a/3588400
youtube: 
comments: true
image_path: 
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
---

terkadang didalam struktur sebuah tabel, tidak hanya memiliki 1 primary key tetapi juga bisa lebih dari 2 primary key itu dinamakan Composite Primary Key. apakah hibernate bisa handle composite primary key???

tentu aja bisa, ada 2 cara yaitu:

1. `@EmbeddedId`
2. `@IdClass`

Yang pertama kita bahas menggunakan EmbeddedId

## Embeddable

Untuk EmbeddedId mapping, pertama kita define dulu primary keynya di class Embeddable yang wajib implement serializable seperti berikut:

{% gist page.gist "KeyClassRoomEmbeddedId.java" %}

Dan kita buat entitynya seperti berikut:

{% gist page.gist "ClassRoomEmbeddedMapping.java" %}

Setelah itu kita buat DAO:

{% gist page.gist "ClassRoomEmbeddedDao.java" %}

Dan berikut adalah Unit Testingnya:

{% gist page.gist "TestSaveClassRoomEmbedded.java" %}

Jika dijalankan maka hasilnya seperti berikut:

```bash
Jan 04, 2021 7:20:05 AM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    insert 
    into
        kampus.kelas_embedded
        (description, kelas_name, prodi, class_id, tahun_angkatan) 
    values
        (?, ?, ?, ?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.kampus.TestSaveClassRoomEmbedded - classroom saved: ClassRoomEmbeddedMapping(pk=KeyClassRoomEmbeddedId(year=2011, classId=si-ii), name=SI - II, programStudy=IF, description=System Informasi - II)
[main] INFO com.maryanto.dimas.bootcamp.test.kampus.TestSaveClassRoomEmbedded - destroy hibernate session!
```

## IdClass

Untuk IdClass Mapping, sama seperti embedded kita define dulu class primary key yang wajib implement serializable seperti beriku:

{% gist page.gist "KeyClassRoomIdClass.java" %}

Setelah itu baru kita buat entity dengan multiple @Id dan `@IdClass(KeyClassRoomIdClass.class)` seperti berikut:

{% gist page.gist "ClassRoomMappingIdClass.java" %}

Nah abis itu baru buat DAO:

{% gist page.gist "ClassRoomIdClassDao.java" %}

Dan yang berikutnya adalah Unit Testing: 

{% gist page.gist "TestSaveClassRoomIdClass.java" %}

Jika dijalankan maka hasilnya seperti berikut:

```bash
Jan 04, 2021 7:30:21 AM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    insert 
    into
        kampus.kelas_idclass
        (description, kelas_name, prodi, class_id, tahun_angkatan) 
    values
        (?, ?, ?, ?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.kampus.TestSaveClassRoomIdClass - classroom saved: ClassRoomMappingIdClass(year=2011, classId=si-01, name=SI - II, programStudy=IF, description=System Informasi - II)
[main] INFO com.maryanto.dimas.bootcamp.test.kampus.TestSaveClassRoomIdClass - destroy hibernate session!
```

Dan untuk Unit Test find by id:

{% gist page.gist "TestFindByIdClassRoomIdClass.java" %}

Jika dijalankan maka hasilnya seperti berikut:

```bash
Jan 04, 2021 7:32:46 AM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        classroomm0_.class_id as class_id1_2_0_,
        classroomm0_.tahun_angkatan as tahun_an2_2_0_,
        classroomm0_.description as descript3_2_0_,
        classroomm0_.kelas_name as kelas_na4_2_0_,
        classroomm0_.prodi as prodi5_2_0_ 
    from
        kampus.kelas_idclass classroomm0_ 
    where
        classroomm0_.class_id=? 
        and classroomm0_.tahun_angkatan=?
[main] INFO com.maryanto.dimas.bootcamp.test.kampus.TestFindByIdClassRoomIdClass - classroom: ClassRoomMappingIdClass(year=2011, classId=si-01, name=SI - II, programStudy=IF, description=System Informasi - II)
[main] INFO com.maryanto.dimas.bootcamp.test.kampus.TestFindByIdClassRoomIdClass - destroy hibernate session!
```