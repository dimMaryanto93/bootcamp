---
layout: post
title: "Case When dengan HQL"
date: 2021-01-24T13:10:53+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#hql-case-expressions
youtube: 
comments: true
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-29h
---

Hai, pada kesempatan kali ini saya mau membahas tentang `case-when` Expresion menggunakan Hibernate Query Language (HQL). seperti biasa sebelum kita mulai kita check dulu data dan tabel misalnya saya punya data seperti berikut:

![select-tables]({{ page.image_path | prepend: site.baseurl }}/select-tables.png)

Selanjutnya berikut adalah implementasi DAO:

{% gist page.gist "HQLCaseWhenExpresionDao.java" %}

Implementasi Unit Testing:

{% gist page.gist "TestHQLCaseWhenExpresion.java" %}

Jika temen-temen jalankan unit testing pada method `testSimpleExpresion()`, maka hasilnya seperti berikut:

```bash
Jan 24, 2021 1:07:05 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        case 
            when employeepa0_.manager_id is not null then ('your manager name is '||employeepa1_.full_name) 
            else 'you don''t have a manager' 
        end as col_0_0_ 
    from
        parentchild.employees employeepa0_ 
    left outer join
        parentchild.employees employeepa1_ 
            on (
                employeepa0_.manager_id=employeepa1_.id
            ) 
    where
        employeepa0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLCaseWhenExpresion - data: your manager name is Hari Sapto Adi
Hibernate: 
    select
        case 
            when employeepa0_.manager_id is not null then ('your manager name is '||employeepa1_.full_name) 
            else 'you don''t have a manager' 
        end as col_0_0_ 
    from
        parentchild.employees employeepa0_ 
    left outer join
        parentchild.employees employeepa1_ 
            on (
                employeepa0_.manager_id=employeepa1_.id
            ) 
    where
        employeepa0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLCaseWhenExpresion - data: you don't have a manager
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLCaseWhenExpresion - destroy hibernate session!
```

Kemudian coba jalankan method `testMultipleCondition()`, maka hasilnya seperti berikut:

```bash
Jan 24, 2021 1:08:29 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        case 
            when employeepa0_.salary>10000000 then (employeepa0_.full_name||' gajinya lebih dari Rp. 10jt / bulan') 
            when employeepa0_.salary between 5000000 and 10000000 then (employeepa0_.full_name||' gajinya diantara Rp. 10jt s/d Rp. 5jt / bulan') 
            when employeepa0_.salary between 0 and 5000000 then (employeepa0_.full_name||' gajinya dibawah Rp. 5jt / bulan') 
            else (employeepa0_.full_name||' kemungkinan karyawan tersebut belum memiliki pekerjaan') 
        end as col_0_0_ 
    from
        parentchild.employees employeepa0_ 
    where
        employeepa0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLCaseWhenExpresion - data: Dimas Maryanto gajinya dibawah Rp. 5jt / bulan
Hibernate: 
    select
        case 
            when employeepa0_.salary>10000000 then (employeepa0_.full_name||' gajinya lebih dari Rp. 10jt / bulan') 
            when employeepa0_.salary between 5000000 and 10000000 then (employeepa0_.full_name||' gajinya diantara Rp. 10jt s/d Rp. 5jt / bulan') 
            when employeepa0_.salary between 0 and 5000000 then (employeepa0_.full_name||' gajinya dibawah Rp. 5jt / bulan') 
            else (employeepa0_.full_name||' kemungkinan karyawan tersebut belum memiliki pekerjaan') 
        end as col_0_0_ 
    from
        parentchild.employees employeepa0_ 
    where
        employeepa0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLCaseWhenExpresion - data: Hari Sapto Adi gajinya diantara Rp. 10jt s/d Rp. 5jt / bulan
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLCaseWhenExpresion - destroy hibernate session!
```

Kemudian yang terakhir, coba jalankan method `testNestedCondition()`, maka hasilnya seperti berikut:

```bash
Jan 24, 2021 1:09:16 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        case 
            when employeepa0_.manager_id is not null then case 
                when employeepa0_.salary>3000000 then (employeepa0_.full_name||' mendapatan gaji sebulan lebih besar dari Rp.3,000,000.00 dan memiliki atasan bernama '||employeepa1_.full_name) 
                else (employeepa0_.full_name||' mendapatkan gaji sebulan lebih kecil dari Rp.3,000,000.00 dan memiliki atasan bernama '||employeepa1_.full_name) 
            end 
            else (employeepa0_.full_name||' mendapatkan gaji sebulan sebesar '||employeepa0_.salary||' dan tidak memiliki atasan') 
        end as col_0_0_ 
    from
        parentchild.employees employeepa0_ 
    left outer join
        parentchild.employees employeepa1_ 
            on (
                employeepa0_.manager_id=employeepa1_.id
            ) 
    where
        employeepa0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLCaseWhenExpresion - data: Dimas Maryanto mendapatan gaji sebulan lebih besar dari Rp.3,000,000.00 dan memiliki atasan bernama Hari Sapto Adi
Hibernate: 
    select
        case 
            when employeepa0_.manager_id is not null then case 
                when employeepa0_.salary>3000000 then (employeepa0_.full_name||' mendapatan gaji sebulan lebih besar dari Rp.3,000,000.00 dan memiliki atasan bernama '||employeepa1_.full_name) 
                else (employeepa0_.full_name||' mendapatkan gaji sebulan lebih kecil dari Rp.3,000,000.00 dan memiliki atasan bernama '||employeepa1_.full_name) 
            end 
            else (employeepa0_.full_name||' mendapatkan gaji sebulan sebesar '||employeepa0_.salary||' dan tidak memiliki atasan') 
        end as col_0_0_ 
    from
        parentchild.employees employeepa0_ 
    left outer join
        parentchild.employees employeepa1_ 
            on (
                employeepa0_.manager_id=employeepa1_.id
            ) 
    where
        employeepa0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLCaseWhenExpresion - data: Hari Sapto Adi mendapatkan gaji sebulan sebesar 10000000.00 dan tidak memiliki atasan
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLCaseWhenExpresion - destroy hibernate session!
```