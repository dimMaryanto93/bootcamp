---
layout: post
title: "Predicate LIKE dengan HQL"
date: 2021-01-26T12:32:34+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#hql-like-predicate
youtube: 
comments: true
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-030c
---

Hai pada kesempatan kali ini saya mau membahas tentang operator like menggunakan Hibernate Query Language (HQL). pada dasarnya operator like di terapkan pada tipe data varchar atau String. selain itu juga jika kita biasa menggunakan escape character, string expression seperti `%` dan `_`.

Berikut adalah contoh penggunaan operator like expression dengan menggunakan HQL. Implementasi DAO:

{% gist page.gist "HQLLikePredicatesDao.java" %}

Implementasi Unit Testing: 

{% gist page.gist "TestHQLLikePredicate.java" %}

Seperti biasa kita check dulu table pada `parentchild.employees`:

![select-tables]({{ page.image_path | prepend: site.baseurl }}/select-tables.png)

Setelah itu jalankan unit testing pada method `testWithoutExpresion()`, maka hasilnya seperti berikut:

```bash
Jan 26, 2021 12:29:29 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
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
        employeepa0_.full_name like ?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLLikePredicate - data: [EmployeeParentChildEntity(id=1515ba52-3c78-4baa-bb67-d3aa0c32b351, name=Dimas Maryanto, address=Cinunuk, salary=3500000.00, job=Principal Software Engineer)]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLLikePredicate - destroy hibernate session!
```

Kemudian coba jalankan method `testStringExpressionContainChar()`, maka berikut hasilnya:

```bash
Jan 26, 2021 12:30:11 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
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
        employeepa0_.full_name like ?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLLikePredicate - data: [Hari Sapto Adi, Dimas Maryanto, Muhamad Yusuf]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLLikePredicate - destroy hibernate session!
```

Dan yang terakhir coba jalankan method `testStringExpressionSecondCharIs()`, maka hasilnya seperti berikut:

```bash
Jan 26, 2021 12:32:03 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
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
        employeepa0_.full_name like ?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLLikePredicate - data: [Dimas Maryanto]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLLikePredicate - destroy hibernate session!
```