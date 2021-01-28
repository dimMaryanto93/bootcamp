---
layout: post
title: "Empty Collections Predicate dengan HQL"
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#hql-empty-collection-predicate
youtube: 
comments: true
image_path: /resources/posts/orm-hibernate-030f
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
---

Hai, di materi kali ini saya mau membahas tentang operation `Empty Collection` menggunakan HQL. pada dasarnya operator empty collection terdiri dari `is empty` dan `is not empty` seperti berikut contoh implementasi DAO:

{% gist page.gist "HQLEmptyCollectionPredicateDao.java" %}

Implementasi Unit Testing: 

{% gist page.gist "TestHQLEmptyCollectionPredicates.java" %}