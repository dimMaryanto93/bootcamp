---
layout: post
title: "Pengenalan ORM dengan Hibernate Framework"
date: 2020-11-21T11:44:22+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- http://docs.jboss.org/hibernate/orm/5.2/quickstart/html_single/
- http://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/Hibernate_User_Guide.html
- https://dzone.com/articles/about-transparent-persistence
youtube: https://www.youtube.com/watch?v=HlLrTQMX0E0&list=PLV1-tdmPblvxHxNh867D1JR4u52LgzeIr&index=2
comments: true
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
---

Halo kali ini saya mau membahas salah satu framework yang sifatnya ORM (Object Relational Mapping) yaitu Hibernate Framework. Tapi sebelum kita mulai belajar koding saya mau cerita dulu nih. Jadi...

Jaman dulu sebelum ada JPA (Java Persistance API) kita murni kita menggunakan JDBC, Dengan menggunakan JDBC semuanya kita harus atur mulai dari Open Connection ke database, Data Definision Language (DDL), Data Manipulation Language (DML), Transaction Control Management (TCL) dll. klo digambarin alurnya seperti beriku:

1. Membuat DDL statement untuk membuat database, table.
2. Membuat Konfigurasi Koneksi untuk Java dapat berkomunikasi ke database. biasanya dengan menggunakan configrasi `DataSource` atau `Connection`
3. Membuat perintah query dalam Java yang dikirim ke database menggunakan `PrepareStatement` dan `Statement`.
4. Menjalankan query atau mengirim ke database dengan menggunakan `executeUpdate()` atau `executeQuery()`.
5. Jika menampilkan data ke database menggunakan `ResultSet`
6. Menutup koneksi
7. Belum lagi kita harus try-catch handle klo ada error sql, koding yang kita tulis penuh dengan try catch deh pokonya.

Jadi jaman sekarang kita tidak perlu dipusingkan lagi dengan menggunakan query-query tersebut, meskipun saya background dari Database System Management tapi jujur aja saya juga rada males sih klo berurusan dengan SQL, PL/SQL, dan sejenisnya soalnya sekarang khan Database itu banyak versinya mulai dari Oracle, MySQL, PostgreSQL, MariaDB dan lain-lain toh juga fungsinnya cuman mempermudah proses penyimpanan, update, hapus dan pencarian data.

Nah jadi klo menggunakan Hibernate kita cukup membuat konfigurasinya kemudian tanpa menggunakan query (DDL maupun DML) udah bisa digunakan. adapun berikut alur lebih jelasnya:

1. Membuat konfigurasi `SessionFactory`
2. Membuat `POJO` (Plain Old Java Object) atau katalainnya `JavaBeans`
3. Kita bisa memanggil fungsi-fungsi yang disedian oleh hibernate contohnya `save(obj)`, `update(obj)`,  `get(obj)` dan `delete(obj)`.

Selain itu juga, framework hibernate ini bisa menggenarate table dalam database secara otomatis sesuia dengan Model yang kita buat di Java Source Code yang di tandai dengan `@Entity` atau membuat mapping dengan XML. jadi kesimpulannya kita tidak perlu lagi membuat Table dengan perintah SQL.

karena Hibernate ini support dengan banyak database, framework hibernate sekarang udah sangat cerdas magsunya bisa membedakan antara database yang menggunakan `AUTO_INCREMENT` atau `SEQUENCE` contohnya klo `SessionFactory` kita menggunakan MySQL maka akan otomatis akan dibuatkan `AUTO_INCREMENT` ketika menggunakan `@GeneratedValue` sedangkan jika `SessionFactory` kita menggunakan Oracle atau PostgreSQL maka secara otomatis juga akan dibuatkan menggunakan `SEQUANCE`

## History of Hibernate Framework

Hibernate mulai di perkenalkan di 2001 oleh `Gavin King` dan kawan-kawannya dari `Cirrus Tehcnologies` sebagai alternative EJB2 style entity beans. yang menjadi tujuan utama dari Hibernate ORM adalah better persistance capabilities dari EJB2 dan simplifying the complexities and supplementing certain missing feature.

## Hibernate Features

1. Modern ORM Solution
2. Transparent Persistance (POJO/JavaBeans)
3. Persistent/transient instance
4. Automatic Dirty Checking
5. Transitive Persistance
6. Lazy Fetching
7. Outer Join Fetching
8. Runtime SQL Generation

## Why Hibernate?

1. Natural Programming Model
2. Minimize LOC (Line of code)
3. Minimize Database Access dengan smart fetching strategis.

## ORM Alternative 

- [myBatis](https://mybatis.org/mybatis-3/)
- [eclipse link](https://www.eclipse.org/eclipselink/)
- EJB
- TopLink