---
layout: post
title: "Transitive dependency dengan Embbeded Mapping"
date: 2021-01-07T12:57:19+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- http://docs.jboss.org/hibernate/orm/5.2/quickstart/html_single/
- http://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/Hibernate_User_Guide.html
youtube: https://www.youtube.com/watch?v=dzEVXB5noo8&list=PLV1-tdmPblvxHxNh867D1JR4u52LgzeIr&index=17
comments: true
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-16
---

Hai, di materi kali ini saya akan membahas embedded mapping, Embedded mapping ini biasanya digunakan untuk mapping sebuah entity dengan model yang terpisah kedalam sebuah single database table. contohnya seperti berikut:

Implementasi Embedded Model: 

{% gist page.gist "AlamatEmbeddable.java" %}

Implementasi Entity: 

{% gist page.gist "MahasiswaEmbedded.java" %}

Implementasi DAO:

{% gist page.gist "MahasiswaEmbeddedDao.java" %}

Implementasi Unit Test:

{% gist page.gist "TestMahasiswaEmbedded.java" %}

Jika di running, maka hasilnya seperti berikut:

```bash
INFO: HHH10001501: Connection obtained from JdbcConnectionAccess [org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator$ConnectionProviderJdbcConnectionAccess@553da911] for (non-JTA) DDL execution was not in auto-commit mode; the Connection 'local transaction' will be committed and the Connection will be set into auto-commit mode.
Hibernate: 
    
    create table embedded.mahasiswa_embedded (
       id int8 not null,
        kecamatan varchar(100),
        kelurahan varchar(100),
        kode_pos int4,
        kota varchar(50),
        provinsi varchar(50),
        rt int4,
        rw int4,
        nama varchar(50) not null,
        nim varchar(8) not null,
        tahun_masuk int4 not null,
        tanggal_lahir date not null,
        primary key (id)
    )
Hibernate: 
    
    alter table if exists embedded.mahasiswa_embedded 
       drop constraint if exists UK_51hpfp15l52864g1il3uebyyl
Jan 06, 2021 7:59:02 PM org.hibernate.engine.jdbc.spi.SqlExceptionHelper$StandardWarningHandler logWarning
WARN: SQL Warning Code: 0, SQLState: 00000
Jan 06, 2021 7:59:02 PM org.hibernate.engine.jdbc.spi.SqlExceptionHelper$StandardWarningHandler logWarning
WARN: constraint "uk_51hpfp15l52864g1il3uebyyl" of relation "mahasiswa_embedded" does not exist, skipping
Hibernate: 
    
    alter table if exists embedded.mahasiswa_embedded 
       add constraint UK_51hpfp15l52864g1il3uebyyl unique (nim)
Jan 06, 2021 7:59:02 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        nextval ('hibernate_sequence')
Hibernate: 
    insert 
    into
        embedded.mahasiswa_embedded
        (kecamatan, kelurahan, kode_pos, kota, provinsi, rt, rw, nama, nim, tahun_masuk, tanggal_lahir, id) 
    values
        (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.embedded.TestMahasiswaEmbedded - destroy hibernate session!
```

Sekarang kita coba check di tabelnya hasilnya seperti berikut:

![mahasiswa-embedded]({{site.baseurl}}{{page.image_path}}/mahasiswa_embedded.png)