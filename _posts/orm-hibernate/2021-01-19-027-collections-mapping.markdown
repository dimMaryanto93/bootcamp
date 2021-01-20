---
layout: post
title: "Collections Mapping"
date: 2021-01-19T15:30:41+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- http://docs.jboss.org/hibernate/orm/5.2/quickstart/html_single/
- https://docs.jboss.org/hibernate/stable/orm/userguide/html_single/Hibernate_User_Guide.html#collections
comments: true
youtube: https://www.youtube.com/watch?v=OjtSmqKNcVA&list=PLV1-tdmPblvxHxNh867D1JR4u52LgzeIr&index=30 
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-27
---

Hai, di materi kali ini saya mau membahas tentang element collection dengan ORM Hibernate.

Element Collection pada dasarnya teridiri dari:

1. Value Type Collection
2. Embedded Type Collection
3. Entity Collection

Hibernate menggunakan collection yang memiliki fitur lazy-loading, caching atau state chnage detection semantics. untuk menggunakan Element Collection kita hanya bisa menggunakan class 

1. `java.util.Collection`
2. `java.util.List`
3. `java.util.Set`
4. `java.util.Map`
5. `java.util.SortedSet`
6. `java.util.SortedMap`

selain yang di sebukan di atas, maka biasanya gak bisa atau akan menyebabkan throwing exception.