---
layout: post
title: "Nullness Predicate dengan HQL"
date: 2021-01-26T10:32:18+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#hql-null-predicate
youtube: 
comments: true
image_path: /resources/posts/orm-hibernate-030b
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
---

Hai, pada kesempatan kali ini saya mau membahas predicate nullless, berikut adalah implementasi DAO:

{% gist page.gist "HQLNullLessPredicateDao.java" %}

Implementasi Unit Testing: 

{% gist page.gist "TestHQLNullLessPredicate.java" %}

Sebelum kita test berikut data yang sudah saya siapkan pada table `parentchild.employees`:

![select-tables]({{ page.image_path | prepend: site.baseurl }}/select-tables.png)

Setelah itu baru kita jalankan unit testingnya pada method `testOperatorIsNotNull()`, maka hasilnya seperti berikut:

```bash
Jan 26, 2021 10:29:00 AM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
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
        employeepa0_.manager_id is not null
Hibernate: 
    select
        employeepa0_.id as id1_33_0_,
        employeepa0_.street_address as street_a2_33_0_,
        employeepa0_.job_id as job_id3_33_0_,
        employeepa0_.manager_id as manager_6_33_0_,
        employeepa0_.full_name as full_nam4_33_0_,
        employeepa0_.salary as salary5_33_0_,
        employeepa1_.id as id1_33_1_,
        employeepa1_.street_address as street_a2_33_1_,
        employeepa1_.job_id as job_id3_33_1_,
        employeepa1_.manager_id as manager_6_33_1_,
        employeepa1_.full_name as full_nam4_33_1_,
        employeepa1_.salary as salary5_33_1_ 
    from
        parentchild.employees employeepa0_ 
    left outer join
        parentchild.employees employeepa1_ 
            on employeepa0_.manager_id=employeepa1_.id 
    where
        employeepa0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLNullLessPredicate - data: [EmployeeParentChildEntity(id=1515ba52-3c78-4baa-bb67-d3aa0c32b351, name=Dimas Maryanto, address=Cinunuk, salary=3500000.00, job=Principal Software Engineer), EmployeeParentChildEntity(id=c8a4c59f-f2f3-413c-80b4-31c797b863db, name=Muhamad Yusuf, address=Ujung Berung, salary=3000000.00, job=Software Engineer)]
```

Dan yang terakhir jalankan method `testOperatorIsNull()`, maka hasilnya seperti berikut:

```bash
Jan 26, 2021 10:29:43 AM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
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
        employeepa0_.manager_id is null
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLNullLessPredicate - data: [EmployeeParentChildEntity(id=aee1795f-816b-4a4b-a8ef-4429fe3069c1, name=Hari Sapto Adi, address=Cicalengka Raya, salary=10000000.00, job=Chief Technology Officer)]
```