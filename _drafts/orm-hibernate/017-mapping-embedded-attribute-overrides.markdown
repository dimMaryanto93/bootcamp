---
layout: post
title: "Embbeded Mapping dengan Override Attributes"
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
image_path: /resources/posts/orm-hibernate-17
---

Hai, di materi kali ini saya mau ngebahas tentang mapping Embedded Override Attribute dengan model dari yang sebelumnya yaitu 

{% gist page.gist "AlamatEmbeddable.java" %}

Dengan penambahan property `alamatRumah` dan `alamatOrangTua` seperti berikut  Implementasi Entitynya: 

{% gist page.gist "MahasiswaEmbeddedOverrideAttributes.java" %}

Implementasi DAO:

{% gist page.gist "MahasiswaEmbeddedOverrideAttributesDao.java" %}

Implementasi Unit Test:

{% gist page.gist "TestMahasiswaEmbeddedOverrideAttribute.java" %}

Jika di running unit testingnya, maka hasilnya seperti berikut:

```bash
INFO: HHH10001501: Connection obtained from JdbcConnectionAccess [org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator$ConnectionProviderJdbcConnectionAccess@73041b7d] for (non-JTA) DDL execution was not in auto-commit mode; the Connection 'local transaction' will be committed and the Connection will be set into auto-commit mode.
Hibernate: 
    
    create table embedded.mahasiswa_override_att (
       id int8 not null,
        ortu_kecamatan varchar(100),
        ortu_kelurahan varchar(100),
        ortu_kode_pos int4,
        ortu_kota varchar(50),
        ortu_jalan varchar(100),
        ortu_provinsi varchar(50),
        ortu_rt int4,
        ortu_rw int4,
        rumah_kecamatan varchar(100) not null,
        rumah_kelurahan varchar(100) not null,
        rumah_kode_pos int4 not null,
        rumah_kota varchar(50) not null,
        rumah_jalan varchar(100),
        rumah_provinsi varchar(50) not null,
        rumah_rt int4 not null,
        rumah_rw int4 not null,
        nama varchar(50) not null,
        nim varchar(8) not null,
        tahun_masuk int4 not null,
        tanggal_lahir date not null,
        primary key (id)
    )
Hibernate: 
    
    alter table if exists embedded.mahasiswa_override_att 
       drop constraint if exists UK_mjjn3dfrmwoi4uo07atagrw4w
Jan 06, 2021 8:37:18 PM org.hibernate.engine.jdbc.spi.SqlExceptionHelper$StandardWarningHandler logWarning
WARN: SQL Warning Code: 0, SQLState: 00000
Jan 06, 2021 8:37:18 PM org.hibernate.engine.jdbc.spi.SqlExceptionHelper$StandardWarningHandler logWarning
WARN: constraint "uk_mjjn3dfrmwoi4uo07atagrw4w" of relation "mahasiswa_override_att" does not exist, skipping
Hibernate: 
    
    alter table if exists embedded.mahasiswa_override_att 
       add constraint UK_mjjn3dfrmwoi4uo07atagrw4w unique (nim)
Jan 06, 2021 8:37:18 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        nextval ('hibernate_sequence')
Hibernate: 
    insert 
    into
        embedded.mahasiswa_override_att
        (ortu_kecamatan, ortu_kelurahan, ortu_kode_pos, ortu_kota, ortu_jalan, ortu_provinsi, ortu_rt, ortu_rw, rumah_kecamatan, rumah_kelurahan, rumah_kode_pos, rumah_kota, rumah_jalan, rumah_provinsi, rumah_rt, rumah_rw, nama, nim, tahun_masuk, tanggal_lahir, id) 
    values
        (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.embedded.TestMahasiswaEmbeddedOverrideAttribute - destroy hibernate session!
```

Sekarang kita check di table, berikut hasilnya:

![embbeded-mapping-override-att]({{site.baseurl}}{{page.image_path}}/embedded-override-attributes.png)