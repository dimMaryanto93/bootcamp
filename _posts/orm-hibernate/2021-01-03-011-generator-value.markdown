---
layout: post
title: "Macam Macam Generator Value di Hibernate"
date: 2021-01-03T16:41:23+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- http://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/Hibernate_User_Guide.html
youtube: https://www.youtube.com/watch?v=MCjohxKO8Tk&list=PLV1-tdmPblvxHxNh867D1JR4u52LgzeIr&index=11
comments: true
image_path: 
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
---

Untuk generator sebetulnya sama halnya yang telah saya tulis materinya [di sini]({{site.baseurl}}{% post_url psql/2020-01-03-035-ddl-primary-key-generator-value %}) yaitu 
dengan menggunakan:

1. Sequance/Auto_Increment Generator
2. UUID

Ok yang pertama kita bahas dulu dengan menggunakan sequance generator:

## Sequance Generator

Untuk menggunakan sequance yang pasti kita perlu check dulu apakah database yang kita gunakan support dengan sequance, jika tidak kita cukup dengan seperti berikut:

{% highlight java %}
package com.maryanto.dimas.bootcamp.example.simple.entity.kampus;

import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

import javax.persistence.*;
import java.time.LocalDateTime;

@Data
@AllArgsConstructor
@NoArgsConstructor
@Entity
@Table(
        name = "kelas_sequance_table",
        schema = "kampus"
)
public class ClassWithSequanceGenerator {

    @Id
    @Column(name = "kode")
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;
    @Column(name = "nama", length = 10)
    private String name;
    @Column(name = "angkatan", length = 4)
    private Integer year;
    @Column(name = "created_by", length = 100, nullable = false)
    private String createdBy;
    @Column(name = "created_datetime", nullable = false)
    private LocalDateTime createdDateTime;
    @Column(name = "last_updated_by", length = 100)
    private String lastUpdateBy;
    @Column(name = "last_updated_datetime")
    private LocalDateTime lastUpdatedBy;
}
{% endhighlight  %}

Tetapi jika support seperti database yang kita gunakan ini, maka kita bisa menggunakan annotation @SequanceGenerator berikut adalah implementasinya:

Implementasi entity:

{% gist page.gist "ClassWithSequanceGenerator.java" %}

Implementasi DAO:

{% gist page.gist "ClassWithSequanceGeneratorDao.java" %}

Implementasi Unit Testing:

{% gist page.gist "TestClassWIthSequanceGenerator.java" %}

Setelah itu coba dijalankan unit testingnya, maka hasilnya seperti berikut:

```bash
Hibernate: 
    select
        nextval ('kampus.seq_kelas')
[main] INFO com.maryanto.dimas.bootcamp.test.kampus.TestClassWIthSequanceGeneratorConstraint - inserted value: ClassWithSequanceGenerator(id=2, name=IPS 2, year=2001, createdBy=admin, createdDateTime=2021-01-03T16:21:50.589681300, lastUpdateBy=null, lastUpdatedBy=null)
Hibernate: 
    insert 
    into
        kampus.kelas_sequance_table
        (created_by, created_datetime, last_updated_by, last_updated_datetime, nama, angkatan, kode) 
    values
        (?, ?, ?, ?, ?, ?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.kampus.TestClassWIthSequanceGeneratorConstraint - destroy hibernate session!
```

## UUID Generator

Untuk menggunakan UUID, kita bisa menggunakan annotation ```@GenericGenerator``` contohnya seperti berikut:

Implementasi Entity:

{% gist page.gist "ClassWithUuidGenerator.java" %}

Implementasi DAO: 

{% gist page.gist "ClassWIthUuidGeneratorDao.java" %}

Implementasi Unit Testing:

{% gist page.gist "TestClassWIthUuidGenerator.java" %}

Setelah itu coba dijalankan unit testingnya, maka hasilnya seperti berikut:


```bash
Jan 03, 2021 4:35:10 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
[main] INFO com.maryanto.dimas.bootcamp.test.kampus.TestClassWIthUuidGenerator - inserted value: ClassWithUuidGenerator(id=7eca938b-35af-4944-9a18-a3a13dd61112, name=IPS 2, year=2001, createdBy=admin, createdDateTime=2021-01-03T16:35:10.901056400, lastUpdateBy=null, lastUpdatedBy=null)
Hibernate: 
    insert 
    into
        kampus.kelas_check
        (created_by, created_datetime, last_updated_by, last_updated_datetime, nama, angkatan, kode) 
    values
        (?, ?, ?, ?, ?, ?, ?)
[main] INFO com.maryanto.dimas.bootcamp.test.kampus.TestClassWIthUuidGenerator - destroy hibernate session!
```