---
layout: post
title: "Perbedaan method executeQuery() dan executeUpdate()"
date: 2020-05-23T04:33:04+07:00
lang: java-jdbc-psql
categories:
- Java
- JDBC
- Postgresql
refs: 
- https://github.com/dimMaryanto93/jdbc-psql-example
youtube: 
comments: true
---

Hai, [Pada post sebelumnya]({{site.baseurl}}{% post_url jdbc-psql/2020-04-20-007-prepared-statement %}) kita udah belajar tentang Class API [Statement](https://docs.oracle.com/javase/7/docs/api/java/sql/Statement.html) dan [PreparedStatement](https://docs.oracle.com/javase/7/docs/api/java/sql/PreparedStatement.html). Pembahasan kali ini kita akan lihat perbedaan antara method `executeUpdate()` dan `executeQuery()`. Ok yang pertama kita bahas dulu method `executeUpdate()`

## Method `executeUpdate()`

Method `executeUpdate()` biasanya digunakan untuk meng-eksekusi perintah `insert`, `update`, `delete`, `alter`, `create` initinya semua query yang tidak menghasilkan data pada perintah sqlnya.

Contoh penggunaanya seperti berikut:

```java
@Override
public Boolean removeById(String value) throws SQLException {
    //language=PostgreSQL
    String query = "delete from example_table where id = ?";
    PreparedStatement preparedStatement = connection.prepareStatement(query);
    preparedStatement.setString(1, value);
    int rows = preparedStatement.executeUpdate();
    preparedStatement.close();
    return true;
}
```

Method `executeUpdate()` hanya mengembalikan `jumlah row/object yang terpengaruh`, kenapa saya bilang object, karena tidak cuman data tapi juga bisa berbentuk table, sequance, dan lain-lain.

## Method `executeQuery()`

Pada method `executeQuery()` biasanya digunakan untuk meng-eksekusi perintah `select`, `function` atau perintah sql yang mengembalikan data.

Contoh penggunaanya seperti berikut:

```java
@Override
public Optional<ExampleTable> findById(String value) throws SQLException {
    //language=PostgreSQL
    String query = "select id    as id,\n" +
            "       name         as name,\n" +
            "       created_date as createdDate,\n" +
            "       created_time as createdTime,\n" +
            "       is_active    as active,\n" +
            "       counter      as counter,\n" +
            "       currency     as currency,\n" +
            "       description  as description,\n" +
            "       floating     as floating\n" +
            "from example_table\n" +
            "where id = ?";
    PreparedStatement preparedStatement = connection.prepareStatement(query);
    preparedStatement.setString(1, value);
    ResultSet resultSet = preparedStatement.executeQuery();
    if (!resultSet.next()) {
        preparedStatement.close();
        return Optional.empty();
    }

    ExampleTable data = new ExampleTable(
            resultSet.getString("id"),
            resultSet.getString("name"),
            resultSet.getDate("createdDate"),
            resultSet.getTimestamp("createdTime"),
            resultSet.getObject("active", Boolean.class),
            resultSet.getLong("counter"),
            resultSet.getBigDecimal("currency"),
            resultSet.getString("description"),
            resultSet.getFloat("floating")
    );
    resultSet.close();
    preparedStatement.close();
    return Optional.of(data);
}
```

Ketika `preparedStatement.executeQuery()` di eksekusi maka menghasilkan class API [ResultSet](https://docs.oracle.com/javase/7/docs/api/java/sql/ResultSet.html). API Class `ResultSet` adalah sebuah Pointer / Nodes / Array dimana data ditampung pada Class tersebut. 

Untuk mengambil datanya kita bisa menggunakan loop atau selection tergantung dari jumlah baris yang di keluarkan. Jika data yang dihasilkan hanya 1 baris kita cukup menggunakan `if statement` seperti contoh di atas dan jika data terdapat lebih dari 1 baris kita bisa menggunakan `loop iterator` seperti pada contoh sebelumnya.