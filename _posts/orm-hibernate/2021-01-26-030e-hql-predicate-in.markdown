---
layout: post
title: "Predicate IN dengan HQL"
date: 2021-01-26T14:52:10+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#hql-in-predicate
youtube: 
comments: true
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-030e
---

Hai pada kesempatan kali ini saya mau membahas tentang predicate `in` dengan menggunakan Hibernate Query Language (HQL), berikut adalah contoh implementasi DAO:

{% gist page.gist "HQLInPredicateDao.java" %}

Implementasi Unit Testing:

{% gist page.gist "TestHQLInPredicate.java" %}

Seperti biasa, kita check dulu data pada table yang kita gunakan kali ini yaitu `enumeration.employee_string` dan `parentchild.employees` seperti berikut:

![select-tables]({{ page.image_path | prepend: site.baseurl }}/select-tables.png)

Ok, setelah coba jalankan unit testing pada method `testInPredicateAsString()`, maka hasilnya seperti berikut:

```bash
Jan 26, 2021 2:47:32 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
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
        employeepa0_.job_id in (
            ? , ?
        )
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLInPredicate - data: [EmployeeParentChildEntity(id=aee1795f-816b-4a4b-a8ef-4429fe3069c1, name=Hari Sapto Adi, address=Cicalengka Raya, salary=10000000.00, job=Chief Technology Officer), EmployeeParentChildEntity(id=c8a4c59f-f2f3-413c-80b4-31c797b863db, name=Muhamad Yusuf, address=Ujung Berung, salary=3000000.00, job=Software Engineer)]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLInPredicate - destroy hibernate session!
```

Setelah itu coba jalankan method `testInPredicateAsDate()`, maka hasilnya seperti berikut:

```bash
Jan 26, 2021 2:48:23 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
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
        employeeen0_.birth_date in (
            ? , ? , ?
        )
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLInPredicate - data: [EmployeeEnumString(id=5, name=Dimas Maryanto, birthDate=1993-03-01, status=LEAVE), EmployeeEnumString(id=7, name=Abdul Arraisi, birthDate=1994-01-07, status=ACTIVE), EmployeeEnumString(id=8, name=Rega, birthDate=2021-01-01, status=RESIGN)]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLInPredicate - destroy hibernate session!
```

Kemudian coba jalankan method `testInPredicateAsEnum()`, maka berikut adalah hasilnya:

```bash
Jan 26, 2021 2:49:12 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
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
        employeeen0_.employee_status in (
            ? , ?
        )
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLInPredicate - data: [EmployeeEnumString(id=5, name=Dimas Maryanto, birthDate=1993-03-01, status=LEAVE), EmployeeEnumString(id=8, name=Rega, birthDate=2021-01-01, status=RESIGN)]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLInPredicate - destroy hibernate session!
```

dan yang terakhir coba jalankan method `testInPredicateAsNumber()`, maka hasilnya seperti berikut:

```bash
Jan 26, 2021 2:51:12 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
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
        employeepa0_.salary in (
            ? , ?
        )
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLInPredicate - data: [EmployeeParentChildEntity(id=c8a4c59f-f2f3-413c-80b4-31c797b863db, name=Muhamad Yusuf, address=Ujung Berung, salary=3000000.00, job=Software Engineer)]
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLInPredicate - destroy hibernate session!
```