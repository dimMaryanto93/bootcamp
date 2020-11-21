---
layout: post
title: "Membuat Simple Entity di Hibernate"
date: 2020-11-21T14:11:27+07:00
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
---

Sekarang kita akan membuat entity dengan menggunakan Annotation. Untuk membuat entity pada dasarnya sama dengan membuat JavaBeans hanya memiliki tambahan annotation seperti `@Entity`, `@Column`, `@Table` dan lain-lain nanti kita akan bahas lebih lanjut di masing-masing annotation pada hibernate.

Ok sekarang kita buat kelas baru dengan nama `Mahasiswa` dalam package `com.maryanto.dimas.bootcamp.entity` seperti berikut:

{% gist page.gist "Mahasiswa.java" %}

Kemudian kita tambahkan property mapping supaya hibernate akan melakukan scan terhadap Annotation dan di translate ke table di database seperti berikut:

{% highlight xml linenos %}
<?xml version='1.0' encoding='utf-8'?>
<!DOCTYPE hibernate-configuration PUBLIC
        "-//Hibernate/Hibernate Configuration DTD//EN"
        "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
<hibernate-configuration>
    <session-factory>
        <!-- connection db -->

        <!-- add mapping here! -->
        <mapping class="com.maryanto.dimas.bootcamp.example.entity.Mahasiswa"/>
    </session-factory>
</hibernate-configuration>
{% endhighlight %}

Atau selain itu juga temen-temen bisa tambahkan di class `HibernateConfiguration` seperti berikut:

{% highlight java linenos %}
package com.maryanto.dimas.bootcamp.example.config;

import com.github.fluent.hibernate.cfg.scanner.EntityScanner;
import com.maryanto.dimas.bootcamp.example.entity.Mahasiswa;
import com.maryanto.dimas.bootcamp.example.entity.buku.Penerbit;
import lombok.extern.slf4j.Slf4j;
import org.hibernate.HibernateException;
import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.boot.MetadataSources;
import org.hibernate.boot.registry.StandardServiceRegistry;
import org.hibernate.boot.registry.StandardServiceRegistryBuilder;

import java.util.List;

@Slf4j
public class HibernateConfiguration {

    private static final SessionFactory ourSessionFactory;

    static {
        final StandardServiceRegistry registry = new StandardServiceRegistryBuilder()
                .configure().build();
        try {
            MetadataSources metadataSources = new MetadataSources(registry);
//            load annotation class here!            
            metadataSources.addAnnotatedClass(Mahasiswa.class);

            ourSessionFactory = metadataSources.buildMetadata()
                    .buildSessionFactory();

        } catch (Throwable ex) {
            StandardServiceRegistryBuilder.destroy(registry);
            throw new ExceptionInInitializerError(ex);
        }
    }
}
{% endhighlight %}

Jika sudah sekarang kita coba jalankan unit testnya kembali dan kita lihat outputnya seperti berikut:

```bash
com.maryanto.dimas.bootcamp.test.TestOpeningConnectionHibernate
[main] INFO com.maryanto.dimas.bootcamp.test.TestOpeningConnectionHibernate - init hibernate session
Nov 21, 2020 2:05:55 PM org.hibernate.Version logVersion
INFO: HHH000412: Hibernate ORM core version 5.4.22.Final
Nov 21, 2020 2:05:55 PM org.hibernate.annotations.common.reflection.java.JavaReflectionManager <clinit>
INFO: HCANN000001: Hibernate Commons Annotations {5.1.0.Final}
Nov 21, 2020 2:05:56 PM org.hibernate.engine.jdbc.connections.internal.ConnectionProviderInitiator instantiateC3p0Provider
WARN: HHH000022: c3p0 properties were encountered, but the c3p0 provider class was not found on the classpath; these properties are going to be ignored.
Nov 21, 2020 2:05:56 PM org.hibernate.engine.jdbc.connections.internal.DriverManagerConnectionProviderImpl configure
WARN: HHH10001002: Using Hibernate built-in connection pool (not for production use!)
Nov 21, 2020 2:05:56 PM org.hibernate.engine.jdbc.connections.internal.DriverManagerConnectionProviderImpl buildCreator
INFO: HHH10001005: using driver [org.postgresql.Driver] at URL [jdbc:postgresql://localhost:5432/hibernate_core]
Nov 21, 2020 2:05:56 PM org.hibernate.engine.jdbc.connections.internal.DriverManagerConnectionProviderImpl buildCreator
INFO: HHH10001001: Connection properties: {password=****, autocommit=false, user=bootcamp}
Nov 21, 2020 2:05:56 PM org.hibernate.engine.jdbc.connections.internal.DriverManagerConnectionProviderImpl buildCreator
INFO: HHH10001003: Autocommit mode: false
Nov 21, 2020 2:05:56 PM org.hibernate.engine.jdbc.connections.internal.DriverManagerConnectionProviderImpl$PooledConnections <init>
INFO: HHH000115: Hibernate connection pool size: 10 (min=1)
Nov 21, 2020 2:05:56 PM org.hibernate.dialect.Dialect <init>
INFO: HHH000400: Using dialect: org.hibernate.dialect.PostgreSQL10Dialect
Nov 21, 2020 2:05:56 PM org.hibernate.validator.internal.util.Version <clinit>
INFO: HV000001: Hibernate Validator 6.1.6.Final
Nov 21, 2020 2:05:56 PM org.hibernate.resource.transaction.backend.jdbc.internal.DdlTransactionIsolatorNonJtaImpl getIsolatedConnection
INFO: HHH10001501: Connection obtained from JdbcConnectionAccess [org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator$ConnectionProviderJdbcConnectionAccess@44d64d4e] for (non-JTA) DDL execution was not in auto-commit mode; the Connection 'local transaction' will be committed and the Connection will be set into auto-commit mode.
Hibernate: 
    
    create table master_mahasiswa (
       kode int8 not null,
        is_active boolean,
        bio text,
        created_by varchar(255),
        created_date timestamp not null,
        nama_mahasiswa varchar(25) not null,
        nim_mahasiswa varchar(8) not null,
        tanggal_lahir date not null,
        tahun_masuk int4,
        primary key (kode)
    )
Hibernate: 
    
    alter table if exists master_mahasiswa 
       drop constraint if exists UK_gld9llgpgky9s6dmyygi9r2lp
Nov 21, 2020 2:05:56 PM org.hibernate.engine.jdbc.spi.SqlExceptionHelper$StandardWarningHandler logWarning
WARN: SQL Warning Code: 0, SQLState: 00000
Nov 21, 2020 2:05:56 PM org.hibernate.engine.jdbc.spi.SqlExceptionHelper$StandardWarningHandler logWarning
WARN: constraint "uk_gld9llgpgky9s6dmyygi9r2lp" of relation "master_mahasiswa" does not exist, skipping
Hibernate: 
    
    alter table if exists master_mahasiswa 
       add constraint UK_gld9llgpgky9s6dmyygi9r2lp unique (nim_mahasiswa)
Hibernate: create sequence hibernate_sequence start 1 increment 1
Nov 21, 2020 2:05:56 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
[main] INFO com.maryanto.dimas.bootcamp.test.TestOpeningConnectionHibernate - destroy hibernate session!
```

Nah dari output tersebut kita akan lihat bahwa hibernate akan membuatkan kita table yang kita buat dari JavaBean `Mahasiswa` dan juga contraint seperti unique key pada kolom `nim_mahasiswa`.