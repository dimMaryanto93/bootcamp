---
layout: post
title: "Memahami fungsi hibernate.cfg.xml"
date: 2020-11-21T13:19:34+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- http://docs.jboss.org/hibernate/orm/5.2/quickstart/html_single/
- http://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/Hibernate_User_Guide.html
youtube: https://www.youtube.com/watch?v=i-gJWAppCtc&list=PLV1-tdmPblvxHxNh867D1JR4u52LgzeIr&index=6
comments: true
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
---

Konfigurasi Hibernate pada dasarnya ada 2 jenis konfigurasi yaitu dengan Source Code java atau saya lebih sering sebut Java Config dan XML (hibernate.cfg.xml). Jaman sekarang Konfigurasi dengan XML udah sangat jarang karena mengikuti style Java yang berbau _annotation_ (`@Annotations`). Tpi gak apa karena kita mau niatnya belajar jadi Ya ikutin aja ya... karena klo kita menggunakan XML juga gak ada ruginya kok toh XML juga lebih mudah dibaca dibandingkan Java Config.

Ok langsung aja buka lagi file `hibernate.cfg.xml` nya, kalo kita lihat seperti berikut:

{% gist page.gist "hibernate.cfg.xml" %}

Nah jadi konfigurasi yang wajib ada yaitu ada 2 hal yaitu

1. `hibernate.dialect`
2. `hibernate.connection.*`

## `hibernate.dialect`

Karena hibernate memiliki support database yang lumanyan banyak, maka kita harus tentukan `dialect` atau analogikanya seperti ini contohnya setiap negara punya bahasa masing masing di ibaratkan dengan DBMS seperti indonesia berhasasa indonesia sedangkan jepang berbahasa jepang tatapi bahasa internasinal tetap bahasa inggris. konsep tersebut juga serupa dengan hibernate ibaratnya bahasa internasinal. jadi apapun databasenya **Hibernate harus menentukan targetnya akan di proses ke database apa** atau bisa dikatakan Translator. itulah fungsi dari `hibernate.dialect`

beberapa `hibernate.dialect` yang paling sering digunakan atau berdasarkan database yang popular

| Database Name     | hibernate.dialect |
| :-------------    | :------------- |
| Oracle            |  	org.hibernate.dialect.OracleDialect |
| MySQL             | org.hibernate.dialect.MySQLDialect |
| SQL Server        | org.hibernate.dialect.SQLServerDialect |
| PostgreSQL        | org.hibernate.dialect.PostgreSQLDialect |
| HSQL              | org.hibernate.dialect.HSQLDialect |
| DB2               | org.hibernate.dialect.DB2Dialect |

## `hibernate.connection.*`

Untuk `hibernate.connection` ini pada dasarnya Untuk menentukan username, password, nama database dan lain-lain yang berkaitan dengan koneksi ke database.

## `hibernate.show_sql`

Property ini fungsinya untuk menampilkan SQL yang di execute oleh hibernate seperti Data Definition Language (`CREATE`, 'ALTER', dan 'DROP'), Data Manipulation Language (`INSERT`, 'UPDATE', dan `DELETE`) serta perintah Querty ('SELECT').

berikut perintahnya:

{% highlight xml %}
<property name="hibernate.show_sql">true</property>
{% endhighlight %}

`hibernate.show_sql` hanya bernilai:

1. `true` (untuk menampilkan SQL statement)
2. `false` (untuk mengembungikan SQL statement)

## `hibernate.hbm2ddl.auto`

Property ini digunakan untuk meng-generate table yang dibuat berdasarkan JavaBeans atau POJO yang menggunakan mapping hibernate (hbm.xml) atau annotation (`@Entity`).

Berikut perintahnya:

{% highlight xml %}
<property name="hibernate.hbm2ddl.auto">create</property>
{% endhighlight %}

`hibernate.hbm2ddl.auto` ini pada dasarnya terdapat 4 yaitu:

1. `create`, ketika `SessionFactory` dipanggil maka dia akan `create table` tetapi setelah `SessionFactory` berakhir atau di `close` datanya akan dihapus (`delete`).
2. `create-drop`, ketika `SessionFactory` dipanggil maka dia akan `drop table` yang ada setelah itu baru dia `create table`
3. `update`, ketika `SessionFactory` dipanggil pertama kali maka dia akan `create table` tetapi ketika ke dua kalinya sampai seterunya maka jika table dalam databasenya udah ada maka dia `update` atau perintah sqlnya `alter` tetapi jika kalo yang berubah adalah field atau column atau atribute maka dia akan membuat field tersebut `add column` bukan `alter column rename`
4. `validate`, ketika `SessionFactory` dipanggil maka dia **tidak akan melakukan generate** karena fungsinya hanya melakukan check aja. keteka table yang di panggil tidak ada maka terjadi error.