---
layout: post
title: "Composite Primary Key"
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- http://docs.jboss.org/hibernate/orm/5.2/quickstart/html_single/
- http://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/Hibernate_User_Guide.html
- https://www.baeldung.com/jpa-composite-primary-keys
- https://stackoverflow.com/a/3588400
youtube: 
comments: true
image_path: 
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
---

terkadang didalam struktur sebuah tabel, tidak hanya memiliki 1 primary key tetapi juga bisa lebih dari 2 primary key itu dinamakan Composite Primary Key. apakah hibernate bisa handle composite primary key???

tentu aja bisa, ada 2 cara yaitu:

1. `@EmbeddedId`
2. `@ClassId`