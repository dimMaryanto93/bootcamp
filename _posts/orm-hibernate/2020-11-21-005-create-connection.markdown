---
layout: post
title: "Build Hibernate Session Factory"
date: 2020-11-21T13:06:49+07:00
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

Sama halnya dengan menggunakan JDBC, untuk menggunakan Hibernate kita harus setup dulu connectionnya. Untuk menghubungkan antara `Database <-> Hibernate` kita membutuhkan hibernate configurasi yaitu dengan cara membuat file `hibernate.cfg.xml` dalam classpath karena kita menggunakan Apache Maven jadi kita simpan file tersebut di `src/main/resources`.

## Setup `hibernate.cfg.xml`

Meng-konfigurasi hibernate sebenarnya ada 2 cara yaitu dengan Java Konfigurasi dan juga XML seperti yang sebelumnya saya sebutkan. nah kali ini saya mau menggunakan konfigurasi XML karena pada kenyataannya konfigurasi XML itu mudah untuk di baca tetapi jujur saja saya sih lebih prepare ke Java Konfigurasi karena sekarang XML udah mulai ditinggalkan orang-orang. tapi gak apa-apa, khan namanya belajar kita harus mulai dari yang paling mudah dulu.

Buat file `hibernate.cfg.xml` dalam folder `src/main/resources` seperti berikut:

{% gist page.gist "hibernate.cfg.xml" %}

*Developer Notes:

1. Ada beberapa property yang harus temen-temen sesuaikan seperti username, password, url database dll
2. Selebihnya nanti akan kita bahas di materi selanjutnya :)

## Build Session Factory

SessionFactory ini pada dasarnya sama seperti objek `Connection` atau `DataSource`, jadi untuk mengeceknya kita harus membuatnya dulu. SessionFactory ini mengambil property settingnya yang ada pada file `hibernate.cfg.xml` jadi alurnya kita harus load file `hibernate.cfg.xml` tersebut dengan perintah seperti berikut, buat kelas baru dengan nama `HibernateConfiguration` pada package `com.maryanto.dimas.bootcamp.example.config` seperti berikut:

{% gist page.gist "HibernateConfiguration.java" %}

Untuk melakukan testing open connection ke database kita akan membuat Unit Testing menggunakan JUnit sebagai berikut:

Buat class dalam folder `src/test/java` kemudian buatlah package `com.maryanto.dimas.bootcamp.test` dan nama classnya yaitu `TestOpeningConnectionHibernate` seperti berikut:

{% gist page.gist "TestOpeningConnectionHibernate.java" %}

Sekarang kita coba run test nya dengan perintah 

{% highlight bash %}
mvn clean test
{% endhighlight %}

berikut hasilnya

```bash
com.intellij.rt.junit.JUnitStarter -ideVersion5 -junit4 com.maryanto.dimas.bootcamp.test.TestOpeningConnectionHibernate
[main] INFO com.maryanto.dimas.bootcamp.test.TestOpeningConnectionHibernate - init hibernate session
Nov 21, 2020 12:57:48 PM org.hibernate.Version logVersion
INFO: HHH000412: Hibernate ORM core version 5.4.22.Final
Nov 21, 2020 12:57:48 PM org.hibernate.annotations.common.reflection.java.JavaReflectionManager <clinit>
INFO: HCANN000001: Hibernate Commons Annotations {5.1.0.Final}
Nov 21, 2020 12:57:48 PM org.hibernate.engine.jdbc.connections.internal.ConnectionProviderInitiator instantiateC3p0Provider
WARN: HHH000022: c3p0 properties were encountered, but the c3p0 provider class was not found on the classpath; these properties are going to be ignored.
Nov 21, 2020 12:57:48 PM org.hibernate.engine.jdbc.connections.internal.DriverManagerConnectionProviderImpl configure
WARN: HHH10001002: Using Hibernate built-in connection pool (not for production use!)
Nov 21, 2020 12:57:48 PM org.hibernate.engine.jdbc.connections.internal.DriverManagerConnectionProviderImpl buildCreator
INFO: HHH10001005: using driver [org.postgresql.Driver] at URL [jdbc:postgresql://localhost:5432/hibernate_core]
Nov 21, 2020 12:57:48 PM org.hibernate.engine.jdbc.connections.internal.DriverManagerConnectionProviderImpl buildCreator
INFO: HHH10001001: Connection properties: {password=****, autocommit=false, user=bootcamp}
Nov 21, 2020 12:57:48 PM org.hibernate.engine.jdbc.connections.internal.DriverManagerConnectionProviderImpl buildCreator
INFO: HHH10001003: Autocommit mode: false
Nov 21, 2020 12:57:48 PM org.hibernate.engine.jdbc.connections.internal.DriverManagerConnectionProviderImpl$PooledConnections <init>
INFO: HHH000115: Hibernate connection pool size: 10 (min=1)
Nov 21, 2020 12:57:49 PM org.hibernate.dialect.Dialect <init>
INFO: HHH000400: Using dialect: org.hibernate.dialect.PostgreSQL10Dialect
Nov 21, 2020 12:57:49 PM org.hibernate.validator.internal.util.Version <clinit>
INFO: HV000001: Hibernate Validator 6.1.6.Final
Nov 21, 2020 12:57:49 PM org.hibernate.resource.transaction.backend.jdbc.internal.DdlTransactionIsolatorNonJtaImpl getIsolatedConnection
INFO: HHH10001501: Connection obtained from JdbcConnectionAccess [org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator$ConnectionProviderJdbcConnectionAccess@48df4071] for (non-JTA) DDL execution was not in auto-commit mode; the Connection 'local transaction' will be committed and the Connection will be set into auto-commit mode.
Nov 21, 2020 12:57:49 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
[main] INFO com.maryanto.dimas.bootcamp.test.TestOpeningConnectionHibernate - destroy hibernate session!
[main] INFO com.maryanto.dimas.bootcamp.test.TestOpeningConnectionHibernate - init hibernate session
[main] INFO com.maryanto.dimas.bootcamp.test.TestOpeningConnectionHibernate - destroy hibernate session!

Process finished with exit code 0

```

Karena dari hasil testnya success atau tidak ada error maka kita udah bisa konek ke database lewat Hibernate Framework.

