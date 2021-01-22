---
layout: post
title: "Aritmatic dengan HQL"
date: 2021-01-22T15:29:02+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#hql
youtube: 
comments: true
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-29e
---

Hai, pada kesempatan kali ini saya mau ngebahas tentang operator arithmetic pada ORM Hibernate menggunakan HQL. Pada dasarnya Operator Aritmetic bisa di terapkan pada `select [operator] from ...` dan `select ... from ... where [operator]`

Ok langsung aja, berikut adalah implementasi menggunakan Arithmetic dengan HQL.

buat class DTO / Model seperti berikut: 

{% gist page.gist "AritmaticModel.java" %}

Implementasi DAO:

{% gist page.gist "HQLArithmeticDao.java" %}

Implementasi Unit Testing:

{% gist page.gist "TestHQLArithmetic.java" %}

Sebelum dijalankan unit testingnya, disini saya menggunakan data yang ada di table `parentchild.employees` seperti berikut:

![select-tables]({{ page.image_path | prepend: site.baseurl }}/select-tables.png)

Nah jika sudah sekarang coba kita jalankan unit testing method `testHitungSalaryEmployeeDalamSetahun`, maka hasilnya seperti berikut:

```bash
Jan 22, 2021 3:24:01 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        employeepa0_.id as col_0_0_,
        employeepa0_.full_name as col_1_0_,
        employeepa0_.salary*? as col_2_0_ 
    from
        parentchild.employees employeepa0_
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLArithmetic - data: [AritmaticModel(id=aee1795f-816b-4a4b-a8ef-4429fe3069c1, nama=Hari Sapto Adi, salarySetahun=120000000.00), AritmaticModel(id=1515ba52-3c78-4baa-bb67-d3aa0c32b351, nama=Dimas Maryanto, salarySetahun=42000000.00), AritmaticModel(id=c8a4c59f-f2f3-413c-80b4-31c797b863db, nama=Muhamad Yusuf, salarySetahun=36000000.00)]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLArithmetic - destroy hibernate session!
```

Kemudian, coba jalankan unit testing method `testHitungTotalSalarySemuaEmployeeDalamSetahun`, maka hasilnya seperti berikut:

```bash
Jan 22, 2021 3:25:38 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        sum(employeepa0_.salary*12) as col_0_0_ 
    from
        parentchild.employees employeepa0_
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLArithmetic - total salary: 198000000.00
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLArithmetic - destroy hibernate session!
```

Dan yang terakhir, coba jalankan method unit testing `testHCariKaryawanYangSalaryDalamSetahunDiatas40Juta`, maka hasilnya seperti berikut:

```bash
Jan 22, 2021 3:26:38 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        employeepa0_.id as id1_33_,
        employeepa0_.street_address as street_a2_33_,
        employeepa0_.job_id as job_id3_33_,
        employeepa0_.manager_id as manager_6_33_,
        employeepa0_.full_name as full_nam4_33_,
        employeepa0_.salary as salary5_33_ 
    from
        parentchild.employees employeepa0_ 
    where
        employeepa0_.salary*12>=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLArithmetic - data: [EmployeeParentChildEntity(id=aee1795f-816b-4a4b-a8ef-4429fe3069c1, name=Hari Sapto Adi, address=Cicalengka Raya, salary=10000000.00, job=Chief Technology Officer), EmployeeParentChildEntity(id=1515ba52-3c78-4baa-bb67-d3aa0c32b351, name=Dimas Maryanto, address=Cinunuk, salary=3500000.00, job=Principal Software Engineer)]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLArithmetic - destroy hibernate session!
```