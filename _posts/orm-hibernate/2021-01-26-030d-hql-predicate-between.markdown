---
layout: post
title: "Predicate BETWEEN dengan HQL"
date: 2021-01-26T14:07:53+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#hql-between-predicate
youtube: 
comments: true
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-030d
---

Hai pada kesempatan kali ini saya mau membahas tantang between dengan menggunakan Hibernate Query Language (HQL). berikut adalah contoh implementasi DAO:

{% gist page.gist "HQLBetweenPredicateDao.java" %}

Implementasi Unit Testing:

{% gist page.gist "TestHQLBetweenPredicate.java" %}

Setelah membuat unit testing, seperti biasa berikut adalah data yang kita gunakan untuk melakukan testing pada table `parentchild.employees` dan `enumeration.employee_string`:

![select-tables]({{ page.image_path | prepend: site.baseurl }}/select-tables.png)

Ok sekarang, coba jalankan unit testingnya pada method `testBetweenNumber()`, maka berikut adalah hasilnya:

```bash
Jan 26, 2021 2:05:36 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
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
        coalesce(employeepa0_.salary, 0) between ? and ?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLBetweenPredicate - data: [EmployeeParentChildEntity(id=1515ba52-3c78-4baa-bb67-d3aa0c32b351, name=Dimas Maryanto, address=Cinunuk, salary=3500000.00, job=Principal Software Engineer), EmployeeParentChildEntity(id=c8a4c59f-f2f3-413c-80b4-31c797b863db, name=Muhamad Yusuf, address=Ujung Berung, salary=3000000.00, job=Software Engineer)]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLBetweenPredicate - destroy hibernate session!
```

Selanjutnya, coba jalankan method `testBetweenDate()`, maka hasilnya seperti berikut:

```bash
Jan 26, 2021 2:06:28 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        employeeen0_.employee_id as employee1_7_,
        employeeen0_.birth_date as birth_da2_7_,
        employeeen0_.employee_name as employee3_7_,
        employeeen0_.employee_status as employee4_7_ 
    from
        enumeration.employee_string employeeen0_ 
    where
        employeeen0_.birth_date between ? and ?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLBetweenPredicate - data: [EmployeeEnumString(id=5, name=Dimas Maryanto, birthDate=1993-03-01, status=LEAVE), EmployeeEnumString(id=6, name=Muhamad Yusuf, birthDate=1992-01-21, status=ACTIVE)]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLBetweenPredicate - destroy hibernate session!
```

Dan yang terakhir jalankan method `testBetweenCharacter()`, maka hasilnya seperti berikut:

```bash
Jan 26, 2021 2:07:15 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
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
        substring(lower(employeepa0_.full_name), 1, 1) between ? and ?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLBetweenPredicate - data: [EmployeeParentChildEntity(id=1515ba52-3c78-4baa-bb67-d3aa0c32b351, name=Dimas Maryanto, address=Cinunuk, salary=3500000.00, job=Principal Software Engineer)]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLBetweenPredicate - destroy hibernate session!
```