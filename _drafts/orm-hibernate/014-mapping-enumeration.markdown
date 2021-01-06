---
layout: post
title: "Mapping Enum Ordinal & String"
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
image_path: /resources/posts/orm-hibernate-14
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
---

Sekarang kita membahas mapping yang paling mudah dulu ya yaitu ENUM Ordinal & String. Enum mapping ini biasanya digunakan untuk status atau bahasa kerennya flaging. nah sebuah flag biasanya tidak hanya bersifat boolean saja tetepi juga bisa custome seperti contohnya `ON | OFF`, `ACTIVE, PASSIVE, INACTIVE` dan lain-lain. contohnya disini saya punya enum seperti berikut:

{% gist page.gist "EmployeeStatus.java" %}

Nah sekarang saya mau ngebahas dulu Enum yang sifatnya ordinal:

## Enum Ordinal

Enum ordinal mapping padasarnya yaitu kita menyimpan data bertipe data Enum ke database dalam urutan angka yang dimulai dari index ke 0. berikut adalah contoh penggunaanya:

Implementasi Entity:

{% gist page.gist "EmployeeEnumOrdinal.java" %}

Implementasi DAO: 

{% gist page.gist "EmployeeEnumOrdinalDao.java" %}

Implementasi Unit Testing:

{% gist page.gist "TestEmployeeEnumOrdianal.java" %}

Jika di running maka hasilnya akan seperti beriktu:

```bash
INFO: HHH10001501: Connection obtained from JdbcConnectionAccess [org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator$ConnectionProviderJdbcConnectionAccess@1dad01fe] for (non-JTA) DDL execution was not in auto-commit mode; the Connection 'local transaction' will be committed and the Connection will be set into auto-commit mode.
Hibernate: 
    
    create table enumeration.employee_ordinal (
       employee_id int8 not null,
        birth_date date not null,
        employee_name varchar(25) not null,
        employee_status int4,
        primary key (employee_id)
    )
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        nextval ('hibernate_sequence')
Hibernate: 
    insert 
    into
        enumeration.employee_ordinal
        (birth_date, employee_name, employee_status, employee_id) 
    values
        (?, ?, ?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.company.TestEmployeeEnumOrdianal - employee: EmployeeEnumOrdinal(id=4, name=Dimas Maryanto, birthDate=1993-03-01, status=LEAVE)
[main] INFO com.maryanto.dimas.bootcamp.test.company.TestEmployeeEnumOrdianal - destroy hibernate session!
```

Sekarang kalo kita check di table maka hasilnya seperti berikut:

![select-enum-ordinal]({{site.baseurl}}{{page.image_path}}/select-enum-ordinal.png)

Nah terlihat bahwa column `employee_status` di simpan di table dalam bentuk numberic berdasarkan urutan Enum dari class `EmployeeStatus`

## Enum String

Sedangkan untuk Enum String Mapping itu disimpan dalam table berbentuk string / varchar. berikut contoh penggunaanya:

Implementasi Entity:

{% gist page.gist "EmployeeEnumString.java" %}

Implementasi DAO:

{% gist page.gist "EmployeeEnumStringDao.java" %}

Implementasi Unit Testing:

{% gist page.gist "TestEmployeeEnumString.java" %}

Jika di running maka hasilnya akan seperti beriktu:

```bash
INFO: HHH10001501: Connection obtained from JdbcConnectionAccess [org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator$ConnectionProviderJdbcConnectionAccess@3e3cd6fe] for (non-JTA) DDL execution was not in auto-commit mode; the Connection 'local transaction' will be committed and the Connection will be set into auto-commit mode.
Hibernate: 
    
    create table enumeration.employee_string (
       employee_id int8 not null,
        birth_date date not null,
        employee_name varchar(25) not null,
        employee_status varchar(255),
        primary key (employee_id)
    )
Jan 06, 2021 2:03:14 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        nextval ('hibernate_sequence')
Hibernate: 
    insert 
    into
        enumeration.employee_string
        (birth_date, employee_name, employee_status, employee_id) 
    values
        (?, ?, ?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.company.TestEmployeeEnumString - employee: EmployeeEnumString(id=5, name=Dimas Maryanto, birthDate=1993-03-01, status=LEAVE)
[main] INFO com.maryanto.dimas.bootcamp.test.company.TestEmployeeEnumString - destroy hibernate session!
```

Sekarang kalo kita check di table maka hasilnya seperti berikut:

![select-enum-ordinal]({{site.baseurl}}{{page.image_path}}/select-enum-string.png)