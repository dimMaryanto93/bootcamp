---
layout: post
title: "Inherintance Mapping metode Single Table menggunakan Descriminator column dan value"
date: 2021-01-16T16:16:42+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- http://docs.jboss.org/hibernate/orm/5.2/quickstart/html_single/
- https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#entity-inheritance-discriminator
youtube: 
comments: true
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-25c
---

Hai pada materi kali ini saya mau mengebahas tentang annotation @Discriminator, dengan annotation tersebut kita bisa menubah property/column `dtype` yang hibernate buat. contohnya disini saya mau ganti menjadi `jenis_kendaraan` dengan pilihan class `MobilSingleTable = Mobil` dan `MotorSingleTable = Motor`. berikut Implementasi Entity Kendaraan:

{% gist page.gist "KendaraanSingleTableDiscriminatorEntity.java" %}

Impementasi Entity Mobil:

{% gist page.gist "MobilSingleTableDiscriminatorEntity.java" %}

Implementasi Entity Motor:

{% gist page.gist "MotorSingleTableDiscriminatorEntity.java" %}

Implementasi DAO Kendaraan:

{% gist page.gist "KendaraanSingleTableDiscriminatorDao.java" %}

Implementasi Unit Testing Kendaraan:

{% gist page.gist "KendaraanSingleTableDiscriminatorDao.java" %}

Jika unit testing di running maka hasilnya seperti berikut:

```bash
INFO: HHH10001501: Connection obtained from JdbcConnectionAccess [org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator$ConnectionProviderJdbcConnectionAccess@595f9916] for (non-JTA) DDL execution was not in auto-commit mode; the Connection 'local transaction' will be committed and the Connection will be set into auto-commit mode.
Hibernate: 
    
    create table inherintance.kendaraan_singletable_discriminator (
       jenis_kendaraan varchar(31) not null,
        id varchar(255) not null,
        cc int4,
        jumlah_cylinder int4,
        jumlah_roda int4,
        nama varchar(50),
        nama_pabrikan varchar(50) not null,
        is_all_wheel_drive boolean,
        jumlah_kursi int4,
        jenis_rantai varchar(255),
        primary key (id)
    )
Jan 16, 2021 3:59:53 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanSingleTableDiscriminator - connected!
Hibernate: 
    insert 
    into
        inherintance.kendaraan_singletable_discriminator
        (cc, jumlah_cylinder, jumlah_roda, nama, nama_pabrikan, is_all_wheel_drive, jumlah_kursi, jenis_kendaraan, id) 
    values
        (?, ?, ?, ?, ?, ?, ?, 'Mobil', ?)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanSingleTableDiscriminator - mobil: MobilSingleTableDiscriminatorEntity(super=KendaraanSingleTableDiscriminatorEntity(id=c5896473-7455-4e0d-8863-d386366e43d1, nama=Honda BRIO, jumlahRoda=4, jumlahCylinder=4, cc=1000, namaPabrikan=PT. Honda Motor Company), jumlahKursi=4, allWheelDrive=false)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.inherintance.TestKendaraanSingleTableDiscriminator - destroy hibernate session!
```

Nah coba kita check tabelnya, maka hasilnya sebagai berikut:

![select-tables]({{page.image_path | prepend: site.baseurl }}/select-tables.png)