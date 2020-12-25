---
layout: post
title: "Embbeded Mapping"
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

{% highlight postgresql-console %}
tutorial_hibernate=# select * from m_mahasiswa;
 kode |                               alamat_rumah                                | nama_mahasiswa | nim_mahasiswa | tahun_masuk
------+---------------------------------------------------------------------------+----------------+---------------+-------------
    4 | Jl.Bukit indah no B8 Rt.09 Rw.01 kec.Cilenyi kab.Bandung 40526 Jawa Barat | Dimas Maryanto | 10511148      |        2011
    5 | Jl.Dipatiukur no 111 Rt.10 Rw.2 kota.Bandung Jawa Barat                   | Karina         | 10512111      |        2012
(2 rows)
{% endhighlight %}