---
layout: post
title: "Parent-Child Mapping"
date: 2021-01-18T20:33:15+07:00
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
image_path: /resources/posts/orm-hibernate-26
---

Hai, di materi kali ini saya mau ngebahas tentang Parent-Child mapping. ok jadi berikut adalah perancangan tabelnya:

![erd]({{ page.image_path | prepend: site.baseurl }}/erd.png)

Berikut adalah implementasi Entity Employee:

{% gist page.gist "EmployeeParentChildEntity.java" %}

Implementasi DAO Employee: 

{% gist page.gist "EmployeeParentChildDao.java" %}

Implementasi Unit Testing:

{% gist page.gist "TestParentChildEmployee.java" %}

Jika dijalankan unit testing untuk method `testSave` maka hasilnya seperti berikut:

```bash
INFO: HHH10001501: Connection obtained from JdbcConnectionAccess [org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator$ConnectionProviderJdbcConnectionAccess@54895681] for (non-JTA) DDL execution was not in auto-commit mode; the Connection 'local transaction' will be committed and the Connection will be set into auto-commit mode.
Hibernate: 
    
    create table parentchild.employees (
       id varchar(255) not null,
        street_address varchar(100),
        job_id varchar(255) not null,
        full_name varchar(50),
        salary numeric(19, 2) not null,
        manager_id varchar(255),
        primary key (id)
    )
Hibernate: 
    
    alter table if exists parentchild.employees 
       add constraint fk_employee_manager_id 
       foreign key (manager_id) 
       references parentchild.employees
Jan 18, 2021 8:26:49 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    insert 
    into
        parentchild.employees
        (street_address, job_id, manager_id, full_name, salary, id) 
    values
        (?, ?, ?, ?, ?, ?)
Hibernate: 
    insert 
    into
        parentchild.employees
        (street_address, job_id, manager_id, full_name, salary, id) 
    values
        (?, ?, ?, ?, ?, ?)
Hibernate: 
    insert 
    into
        parentchild.employees
        (street_address, job_id, manager_id, full_name, salary, id) 
    values
        (?, ?, ?, ?, ?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.parentchild.TestParentChildEmployee - destroy hibernate session!
```

Nah sekarang coba jalankan unit testing pada method `testFindByIdWithListEmployee` maka hasilnya seperti berikut:

```bash
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        employeepa0_.id as id1_29_0_,
        employeepa0_.street_address as street_a2_29_0_,
        employeepa0_.job_id as job_id3_29_0_,
        employeepa0_.manager_id as manager_6_29_0_,
        employeepa0_.full_name as full_nam4_29_0_,
        employeepa0_.salary as salary5_29_0_,
        employeepa1_.id as id1_29_1_,
        employeepa1_.street_address as street_a2_29_1_,
        employeepa1_.job_id as job_id3_29_1_,
        employeepa1_.manager_id as manager_6_29_1_,
        employeepa1_.full_name as full_nam4_29_1_,
        employeepa1_.salary as salary5_29_1_ 
    from
        parentchild.employees employeepa0_ 
    left outer join
        parentchild.employees employeepa1_ 
            on employeepa0_.manager_id=employeepa1_.id 
    where
        employeepa0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.parentchild.TestParentChildEmployee - karyawan: EmployeeParentChildEntity(id=aee1795f-816b-4a4b-a8ef-4429fe3069c1, name=Hari Sapto Adi, address=Cicalengka Raya, salary=10000000.00, job=Chief Technology Officer)
Hibernate: 
    select
        employees0_.manager_id as manager_6_29_0_,
        employees0_.id as id1_29_0_,
        employees0_.id as id1_29_1_,
        employees0_.street_address as street_a2_29_1_,
        employees0_.job_id as job_id3_29_1_,
        employees0_.manager_id as manager_6_29_1_,
        employees0_.full_name as full_nam4_29_1_,
        employees0_.salary as salary5_29_1_ 
    from
        parentchild.employees employees0_ 
    where
        employees0_.manager_id=?
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.parentchild.TestParentChildEmployee - daftar karyawan yang pimpin manager Hari Sapto Adi: 
[EmployeeParentChildEntity(id=1515ba52-3c78-4baa-bb67-d3aa0c32b351, name=Dimas Maryanto, address=Cinunuk, salary=3500000.00, job=Principal Software Engineer), EmployeeParentChildEntity(id=c8a4c59f-f2f3-413c-80b4-31c797b863db, name=Muhamad Yusuf, address=Ujung Berung, salary=3000000.00, job=Software Engineer)]
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.parentchild.TestParentChildEmployee - destroy hibernate session!
```

Dan yang terakhir coba jalankan unit testing pada method `testFindByIdWithManager` maka hasilnya seperti berikut:

```bash
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        employeepa0_.id as id1_29_0_,
        employeepa0_.street_address as street_a2_29_0_,
        employeepa0_.job_id as job_id3_29_0_,
        employeepa0_.manager_id as manager_6_29_0_,
        employeepa0_.full_name as full_nam4_29_0_,
        employeepa0_.salary as salary5_29_0_,
        employeepa1_.id as id1_29_1_,
        employeepa1_.street_address as street_a2_29_1_,
        employeepa1_.job_id as job_id3_29_1_,
        employeepa1_.manager_id as manager_6_29_1_,
        employeepa1_.full_name as full_nam4_29_1_,
        employeepa1_.salary as salary5_29_1_ 
    from
        parentchild.employees employeepa0_ 
    left outer join
        parentchild.employees employeepa1_ 
            on employeepa0_.manager_id=employeepa1_.id 
    where
        employeepa0_.id=?
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.parentchild.TestParentChildEmployee - karyawan: EmployeeParentChildEntity(id=c8a4c59f-f2f3-413c-80b4-31c797b863db, name=Muhamad Yusuf, address=Ujung Berung, salary=3000000.00, job=Software Engineer)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.parentchild.TestParentChildEmployee - karyawan dengan nama Muhamad Yusuf managernya adalah: EmployeeParentChildEntity(id=aee1795f-816b-4a4b-a8ef-4429fe3069c1, name=Hari Sapto Adi, address=Cicalengka Raya, salary=10000000.00, job=Chief Technology Officer)
[main] INFO com.maryanto.dimas.bootcamp.test.mapping.parentchild.TestParentChildEmployee - destroy hibernate session!
```

Jika kita lihat pada tabel maka hasilnya seperti berikut:

![select-tables]({{ page.image_path | prepend: site.baseurl }}/select-tables.png)