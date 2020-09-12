---
layout: post
title: "Membuat connection ke Database PostgreSQL via JDBC"
date: 2020-04-19T16:36:52+07:00
lang: java-jdbc-psql
categories:
- Java
- JDBC
- Postgresql
refs: 
- https://github.com/dimMaryanto93/jdbc-psql-example
- https://github.com/brettwooldridge/HikariCP
- https://docs.oracle.com/javase/tutorial/jdbc/basics/connecting.html
youtube: https://www.youtube.com/watch?v=6LmohNreU74&list=PLV1-tdmPblvxVAb1P-CRsPraIv3ks3A16&index=4
comments: true
---

Hi, di materi kali kita akan menghubungkan antara Java dengan Database dengann menggunakan teknologi JDBC atau Java Database Connectivity setelah sebelumnya kita membuat project dengan Apache Maven. Object `connection` yang kita buat kali ini menggunakan framework/library connection pooling yaitu [HikariCP](https://github.com/brettwooldridge/HikariCP).

Dengan menggunakan HikariCP, performa database kita akan selalu terjaga karena terkadang klo connection ke database di hit melamapui batas sering hang atau error too many connection. maka kita kali ini mencoba dengan HikariCP agar connection life cycle di terjaga.

Ok sekarang kita akan membuat koneksi ke database, berikut stepnya:

## Create Connection

Untuk membuat connection kita perlu mendefine object `connection`, object `connection` membutuhkan minimal 3 property yaitu 

1. User database
2. Password database
3. URL database

Jadi make sure, temen-temen udah install Database, membuat database, membuat user/schema. Teknologi yang akan kita gunakan adalah JDBC maka URL database yang kita gunakan menggunakan spesifikasi dari JDBC juga seperti pada [dockumentasi berikut](https://docs.oracle.com/javase/tutorial/jdbc/basics/connecting.html).

Jadi contohnya berikut adalah config database server:

```yaml
Database server: PostgreSQL 12.1
Host: localhost
Port: 5432
User: bootcamp
Password: bootcamp
Database name: bootcamp
```

Maka klo di terjemahkan ke JDBC URL seperti berikut: `jdbc:postgresql://localhost:5432/bootcamp`, Setelah itu kita buat class dengan nama `DatasourceConfig` dalam package `config` seperti berikut:


{% highlight java linenos %}
package com.maryanto.dimas.bootcamp.config;

import com.zaxxer.hikari.HikariConfig;
import com.zaxxer.hikari.HikariDataSource;

import javax.sql.DataSource;

@Slf4j
public class DatasourceConfig {

    private final HikariConfig config;

    public DatasourceConfig(String url, String username, String password) {
        this.config = new HikariConfig();
        config.setJdbcUrl(url);
        config.setUsername(username);
        config.setPassword(password);
        config.addDataSourceProperty("cachePrepStmts", "true");
        config.addDataSourceProperty("prepStmtCacheSize", "250");
        config.addDataSourceProperty("prepStmtCacheSqlLimit", "2048");
    }

    public DataSource getDataSource() {
        return new HikariDataSource(config);
    }
}
{% endhighlight %}

Setelah itu kita test apakah sudah terhubung dengan database, menggunakan method Integration Test dengan JUnit seperti berikut

## Test Connection using JUnit

Ok sekarang kita buat class baru lagi dalam folder `src/test/java` dengan nama `TestConnection` dalam package yang sama dengan default package maven yaitu `com.maryanto.dimas.bootcamp` seperti berikut:

{% highlight java linenos %}
package com.maryanto.dimas.bootcamp;

import com.maryanto.dimas.bootcamp.config.DatasourceConfig;
import junit.framework.TestCase;
import lombok.extern.slf4j.Slf4j;
import org.junit.Test;

import javax.sql.DataSource;
import java.sql.Connection;
import java.sql.SQLException;

@Slf4j
public class TestConnection extends TestCase {

    private DatasourceConfig config;

    @Override
    protected void setUp() throws Exception {
        this.config = new DatasourceConfig("jdbc:postgresql://localhost:5432/bootcamp", "bootcamp", "bootcamp");
    }

    @Test
    public void testConnectionToDB() throws SQLException {
        DataSource dataSource = this.config.getDataSource();
        Connection connection = dataSource.getConnection();
        log.info("status connected");
    }
}

{% endhighlight %}

Kemudian kita jalankan test unitnya dengan menggunakan perintah sebagai berikut:

```bash
mvn clean compile test
```

dan berikut hasilnya:

```bash
Running com.maryanto.dimas.bootcamp.TestConnection
[main] INFO com.zaxxer.hikari.HikariDataSource - HikariPool-1 - Starting...
[main] INFO com.zaxxer.hikari.HikariDataSource - HikariPool-1 - Start completed.
[main] INFO com.maryanto.dimas.bootcamp.TestConnection - status connected
Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.287 sec

Results :

Tests run: 1, Failures: 0, Errors: 0, Skipped: 0

[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  4.451 s
[INFO] Finished at: 2020-04-19T16:19:39+07:00
[INFO] ------------------------------------------------------------------------
```

Jika ada output seperti berikut maka selamat, anda telah memasuki dunia baru di Java.

## Externalization configuration

Jika kita perhatikan koding di atas, ada value yang di hardcode yaitu connection ke database seperti berikut 

```java
@Override
protected void setUp() throws Exception {
    this.config = new DatasourceConfig("jdbc:postgresql://localhost:5432/bootcamp", "bootcamp", "bootcamp");
}
```

Sometime jika property connection database di hardcode di koding akan sulit di baca/dirubah oleh divisi operation akan lebih baik kita bisahkan dengan menggunakan Externalization configuration dengan cara seperti berikut:

Buat file baru dengan nama `application.properties` kemudian simpan didalam folder `src/main/resources` seperti berikut:

```properties
jdbc.url=jdbc:postgresql://localhost:5432/bootcamp
jdbc.username=bootcamp
jdbc.password=bootcamp
```

Kemudian kita tambahkan di class `DatasourceConfig` untuk meload file properties tersebut seperti berikut:

{% highlight java linenos %}
package com.maryanto.dimas.bootcamp.config;

import com.zaxxer.hikari.HikariConfig;
import com.zaxxer.hikari.HikariDataSource;
import lombok.extern.slf4j.Slf4j;

import javax.sql.DataSource;
import java.io.IOException;
import java.io.InputStream;
import java.util.Properties;

@Slf4j
public class DatasourceConfig {

    private final HikariConfig config;

    <!-- tambahkan method ini -->
    public DatasourceConfig() {
        Properties prop = new Properties();
        InputStream input = DatasourceConfig.class.getResourceAsStream("/application.properties");
        try {
            prop.load(input);
            input.close();
        } catch (IOException e) {
            log.error("can't load file property", e);
        }

        this.config = new HikariConfig();
        config.setJdbcUrl(prop.getProperty("jdbc.url"));
        config.setUsername(prop.getProperty("jdbc.username"));
        config.setPassword(prop.getProperty("jdbc.password"));
        config.addDataSourceProperty("cachePrepStmts", "true");
        config.addDataSourceProperty("prepStmtCacheSize", "250");
        config.addDataSourceProperty("prepStmtCacheSqlLimit", "2048");
    }

    <!-- other method -->
}
{% endhighlight %}

Setelah itu kita rubah juga pointing untuk pemanggilan URLnya pada class `TestConnection` seperti berikut:


{% highlight java linenos %}
package com.maryanto.dimas.bootcamp;

import com.maryanto.dimas.bootcamp.config.DatasourceConfig;
import junit.framework.TestCase;
import lombok.extern.slf4j.Slf4j;
import org.junit.Test;

import javax.sql.DataSource;
import java.sql.Connection;
import java.sql.SQLException;

@Slf4j
public class TestConnection extends TestCase {

    private DatasourceConfig config;

    @Override
    protected void setUp() throws Exception {
        <!-- change args parameter to this -->
        this.config = new DatasourceConfig();
    }

    @Test
    public void testConnectionToDB() throws SQLException {
        DataSource dataSource = this.config.getDataSource();
        Connection connection = dataSource.getConnection();
        log.info("status connected");
    }
}

{% endhighlight %}

Setelah itu baru di test lagi dengan menggunakan perintah maven test.