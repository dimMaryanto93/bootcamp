---
layout: post
title: "Macam-Macam Inherintance Mapping"
date: 2021-01-14T15:04:24+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- http://docs.jboss.org/hibernate/orm/5.2/quickstart/html_single/
- https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#entity-inheritance
youtube: https://www.youtube.com/watch?v=k9_Jk-9hK_w&list=PLV1-tdmPblvxHxNh867D1JR4u52LgzeIr&index=23
comments: true
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-25
---

Hai, di materi kali ini kita akan membahas tentang Inheritance Mapping menggunakan ORM Hibernate Framework. nah FYI klo semua relational database tidak support inherintance ya! nah jadi di sini hibernate menawarkan beberapa solusi yaitu sebagai berikut: 

1. MappedSupperclass
2. Single Table
3. Joined Table
4. Table Per Class