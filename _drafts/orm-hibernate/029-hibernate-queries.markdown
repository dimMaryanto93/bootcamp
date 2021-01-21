---
layout: post
title: "Hibernate Query Language (HQL-JPQL)"
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- http://docs.jboss.org/hibernate/orm/5.2/quickstart/html_single/
- https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#hql
youtube: 
comments: true
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
image_path: /resources/posts/orm-hibernate-29
---

Hai, di materi kali ini saya mau membahas tentang Query di ORM Hibernate Framework, Query pada ORM Hibernate terdiri:

1. [Native Query (SQL)](https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#sql)
2. [Hibernate Query Language (HQL) dan Java Persistenct Query Language (JPQL)](https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#hql)
3. [Criteria API](https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#criteria)

Untuk menggunakan query tersebut, misalnya disini saya kasih contoh entity seperti berikut:

{% gist page.gist "AlamatEntity.java" %}

## Native Query

Native query pada dasarnya kita me-execute query SQL standart dalam object SessionFactory. berikut adalah contoh NativeQuery:

{% highlight java linenos %}
NativeQuery<Penerbit> query = 
    this.session.createNativeQuery(
        "select * from mapping.alamat", 
        AlamatEntity.class
    );
{% endhighlight %}

## HQL & JPQL

Hibernate Query Language (HQL) hampir sama dengan SQL tetepi disini accessnya bukan ke table melainkan ke Entity, Berikut adalah contoh penggunaan HQL: 

{% highlight java lineos %}
Query query = entityManager
    .createQuery("from AlamatEntity");
{% endhighlight %}

## Criteria API

Criteria API sama seperti HQL tpi disini query builder menggunakan Java, berikut adalah contoh penggunaan Criteria API:

{% highlight java lineos %}
CriteriaBuilder builder = session.getCriteriaBuilder();
CriteriaQuery<AlamatEntity> query = builder.createQuery(AlamatEntity.class);
Root<AlamatEntity> root = query.from(AlamatEntity.class);
query.select(root);
{% endhighlight %}