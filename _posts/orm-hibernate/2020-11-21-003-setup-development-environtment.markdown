---
layout: post
title: "Setup Development Environment"
date: 2020-11-21T12:16:35+07:00
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

Halo di [postingan sebelumnya]({% post_url orm-hibernate/2020-11-21-002-pengenalan-jpa-with-hibernate %}) kita udah berkenalan nih dengan Hibernate Framework, jadi sekarang kita akan mulai untuk persiapan-persiapan apa aja yang perlu di setup sebelum memulai koding dengan Hibernate.

## Persiapan

1. Install Java 1.8
2. Install Apache Maven
3. Install Database PostgreSql
4. Text editor atau IDE seperti Netbeans, Eclipse, InteliJIDEA atau lain-lain. klo saya akan menggunakan **IntelliJ IDEA Ultimate**.

## Setup Java 1.8

Untuk setup java 1.8 udah pernah saya bahas di materi [Java Core]({{site.baseurl}}{% post_url java-core/2017-10-16-001-silabus-java %})

## Setup Apache Maven

Untuk install apache maven udah pernah saya bahas juga di blog saya.

1. Untuk Windows [How to Install Apache Maven for Windows 10](https://www.dimas-maryanto.com/notes/fedora-23/install-maven-fedora)
2. Untuk Linux [How to Install Apache Maven for Linux Ubuntu](https://www.dimas-maryanto.com/notes/ubuntu-16.04/install-maven-ubuntu)
3. Untuk Linux Centos [How to Install Apache Maven for linux Centos / Fedora / RedHat](https://www.dimas-maryanto.com/notes/fedora-23/install-maven-fedora)

## Setup Database

Nah sayangnya Hibernate ini tidak memiliki fitur untuk membuat Database, jadi hanya bisa menggenerate table, column dan object lagi seperti `constraint`, `auto_increment`, dan `sequance`.

Jadi kita buat dulu database dengan nama `hibernate_core` seperti berikut:

{% highlight sql %}
# login as postgres
psql -h localhost -U postgres

# create user tutorial_hibernate
create user bootcamp with superuser login password 'bootcamp';

# membuat database bootcamp_hibernate dengan ownernya user tutorial_hibernate
create database bootcamp_hibernate with owner bootcamp;
{% endhighlight %}