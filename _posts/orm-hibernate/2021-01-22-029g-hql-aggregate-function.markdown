---
layout: post
title: "Aggregation Function dengan HQL"
date: 2021-01-22T21:11:25+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#hql-aggregate-functions
youtube: 
comments: true
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-29g
---

Hai, pada kesempatan kali ini saya mau membahas tentang Aggregation Function dengan menggunakan HQL. Aggregation pada dasarnya ada beberapa function yang kita bisa gunakan yaitu 

1. `COUNT`
2. `AVG`
3. `MIN`
4. `MAX`
5. `SUM`

Berikut adalah contoh penggunaanya, ok sebelum itu saya mau buat DTO dulu seperti berikut:

{% gist page.gist "AggregateFunctionModel.java" %}

Implementasi DAO:

{% gist page.gist "HQLAggregationFunctionDao.java" %}

Implementasi Unit Testing: 

{% gist page.gist "TestHQLAggregateFunction.java" %}

Seperti biasa, kita siapkan dulu datanya dalam table. kali ini saya menggunakan table `parentchild.employees` seperti berikut:

![select-tables]({{ page.image_path | prepend: site.baseurl }}/select-tables.png)

Nah setelah itu, kita coba jalankan unit testing pada method `testFunctionAggregate`, maka hasilnya seperti berikut:

```bash
Jan 22, 2021 9:05:17 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        count(*) as col_0_0_,
        avg(employeepa0_.salary) as col_1_0_,
        min(employeepa0_.salary) as col_2_0_,
        max(employeepa0_.salary) as col_3_0_,
        sum(employeepa0_.salary) as col_4_0_ 
    from
        parentchild.employees employeepa0_
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLAggregateFunction - data: AggregateFunctionModel(countFunction=3, avgFunction=5500000.0, minFunction=3000000.00, maxFunction=10000000.00, sumFunction=16500000.00)
```

Kemudian kita coba lagi untuk method `testCountData`, maka hasilnya seperti berikut:

```bash
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        count(*) as col_0_0_ 
    from
        parentchild.employees employeepa0_
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLAggregateFunction - data: 3
```

Next, kita coba method `testSumGajiKaryawan`, maka hasilnya seperti berikut:

```bash
Jan 22, 2021 9:07:20 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        sum(employeepa0_.salary) as col_0_0_ 
    from
        parentchild.employees employeepa0_
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLAggregateFunction - data: 16500000.00
```

Next, kita coba method `testRataRataGajiKaryawan`, maka hasilnya seperti berikut:

```bash
Jan 22, 2021 9:08:11 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        avg(employeepa0_.salary) as col_0_0_ 
    from
        parentchild.employees employeepa0_
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLAggregateFunction - data: 5500000.0
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLAggregateFunction - destroy hibernate session!
```

Next, kita coba method `testNilaiMinAndMaxGajiKaryawan`, maka hasilnya seperti berikut:

```bash
Jan 22, 2021 9:08:49 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        min(employeepa0_.salary) as col_0_0_,
        max(employeepa0_.salary) as col_1_0_ 
    from
        parentchild.employees employeepa0_
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLAggregateFunction - data: {min: 3000000.00, max: 10000000.00}
```