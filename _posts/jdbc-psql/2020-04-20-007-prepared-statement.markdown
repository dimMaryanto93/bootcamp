---
layout: post
title: "Mengenal class java.sql.PreparedStatement"
date: 2020-04-20T19:56:20+07:00
lang: java-jdbc-psql
categories:
- Java
- JDBC
- Postgresql  
refs: 
- https://docs.oracle.com/javase/7/docs/api/java/sql/PreparedStatement.html
youtube: 
comments: true
---

Hai, [sebelumnya]({{site.baseurl}}{% post_url jdbc-psql/2020-04-19-006-statement %}) kita udah bisa mengambil data dengan menggunakan API class `Statement` sekarang kita bahas kaka-nya yaitu API class `java.sql.PreparedStatement`. Penggunaan API `PreparedStatement` biasanya digunakan untuk melakukan Insert, Update, Delete, Find By id, atau query yang membutuhkan parameter.

Ok sekarang kita lanjutkan membuat Data Access Object-nya dengan menggunakan API class `PreparedStatement`. Masih ingetkann kemarin kita udah membuat interface `CrudRepository` nah sekarang kita implement semua methodnya di class `ExampleTableDao` sebagai berikut:


{% highlight java linenos %}
package com.maryanto.dimas.bootcamp.dao;

import com.maryanto.dimas.bootcamp.entity.ExampleTable;

import java.sql.*;
import java.util.ArrayList;
import java.util.List;
import java.util.Optional;

public class ExampleTableDao implements CrudRepository<ExampleTable, String> {

    private Connection connection;

    public ExampleTableDao(Connection connection) {
        this.connection = connection;
    }

    @Override
    public ExampleTable save(ExampleTable value) throws SQLException {
        //language=PostgreSQL
        String query = "insert into example_table (name, created_date, created_time, is_active, counter, currency, description, floating)\n" +
                "values (?, ?, ?, ?, ?, ?, ?, ?)";
        PreparedStatement preparedStatement = connection.prepareStatement(query, Statement.RETURN_GENERATED_KEYS);
        preparedStatement.setString(1, value.getName());
        preparedStatement.setDate(2, value.getCreatedDate());
        preparedStatement.setTimestamp(3, value.getCreatedTime());
        preparedStatement.setBoolean(4, value.getActive());
        preparedStatement.setLong(5, value.getCounter());
        preparedStatement.setBigDecimal(6, value.getCurrency());
        preparedStatement.setString(7, value.getDescription());
        preparedStatement.setFloat(8, value.getFloating());
        preparedStatement.executeUpdate();
        ResultSet generatedKeys = preparedStatement.getGeneratedKeys();
        if (generatedKeys.next())
            value.setId(generatedKeys.getString(1));
        preparedStatement.close();
        return value;
    }

    @Override
    public ExampleTable update(ExampleTable value) throws SQLException {
        //language=PostgreSQL
        String query = "update example_table\n" +
                "set name        = ?,\n" +
                "    is_active   = ?,\n" +
                "    counter     = ?,\n" +
                "    currency    = ?,\n" +
                "    description = ?,\n" +
                "    floating    = ?\n" +
                "where id = ?";
        PreparedStatement preparedStatement = connection.prepareStatement(query);
        preparedStatement.setString(1, value.getName());
        preparedStatement.setBoolean(2, value.getActive());
        preparedStatement.setLong(3, value.getCounter());
        preparedStatement.setBigDecimal(4, value.getCurrency());
        preparedStatement.setString(5, value.getDescription());
        preparedStatement.setFloat(6, value.getFloating());
        preparedStatement.setString(7, value.getId());
        preparedStatement.executeUpdate();
        preparedStatement.close();
        return value;
    }

    @Override
    public Boolean removeById(String value) throws SQLException {
        //language=PostgreSQL
        String query = "delete from example_table where id = ?";
        PreparedStatement preparedStatement = connection.prepareStatement(query);
        preparedStatement.setString(1, value);
        preparedStatement.executeUpdate();
        preparedStatement.close();
        return true;
    }

    @Override
    public Optional<ExampleTable> findById(String value) throws SQLException {
        //language=PostgreSQL
        String query = "select id           as id,\n" +
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

    @Override
    public List<ExampleTable> findAll() throws SQLException {
        // method Statement sebelumnya
    }

    @Override
    public List<ExampleTable> findAll(Long start, Long limit, Long orderIndex, String orderDirection, ExampleTable param) throws SQLException {
        List<ExampleTable> list = new ArrayList<>();
        //language=PostgreSQL
        String baseQuery = "select id           as id,\n" +
                "       name         as name,\n" +
                "       created_date as createdDate,\n" +
                "       created_time as createdTime,\n" +
                "       is_active    as active,\n" +
                "       counter      as counter,\n" +
                "       currency     as currency,\n" +
                "       description  as description,\n" +
                "       floating     as floating\n" +
                "from example_table\n" +
                "where 1 = 1 \n" +
                "limit ? offset ?";

        PreparedStatement preparedStatement = connection.prepareStatement(baseQuery);
        preparedStatement.setLong(1, limit);
        preparedStatement.setLong(2, start);

        ResultSet resultSet = preparedStatement.executeQuery();
        while (resultSet.next()) {
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
            list.add(data);
        }

        resultSet.close();
        preparedStatement.close();
        return list;
    }
}
{% endhighlight %}

Ok setelah itu kita tambahkan unit test case untuk melakukan test terhadap method yang telah kita buat diatas, seperti berikut:

{% highlight java linenos %}
package com.maryanto.dimas.bootcamp;

import com.maryanto.dimas.bootcamp.config.DatasourceConfig;
import com.maryanto.dimas.bootcamp.dao.ExampleTableDao;
import com.maryanto.dimas.bootcamp.entity.ExampleTable;
import junit.framework.TestCase;
import lombok.extern.slf4j.Slf4j;
import org.junit.Test;

import javax.sql.DataSource;
import java.math.BigDecimal;
import java.sql.Connection;
import java.sql.Date;
import java.sql.SQLException;
import java.sql.Timestamp;
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.util.Arrays;
import java.util.List;
import java.util.Optional;

@Slf4j
public class TestIntegrationExampleTable extends TestCase {

    private DataSource dataSource;

    private ExampleTableDao dao;

    @Override
    protected void setUp() throws Exception {
        this.dataSource = new DatasourceConfig().getDataSource();
    }

    @Test
    public void testFindById() {
        try (Connection connection = this.dataSource.getConnection()) {
            this.dao = new ExampleTableDao(connection);

            Optional<ExampleTable> existId = this.dao.findById("001");
            assertTrue("find by id 001 data exist", existId.isPresent());
            ExampleTable id001 = existId.get();
            assertEquals("name with id 001 is Dimas Maryanto actualy",
                    id001.getName(),
                    "Dimas Maryanto");

            Optional<ExampleTable> notExistId = this.dao.findById("006");
            assertFalse("find by id 006 data not exist actualy", notExistId.isPresent());
        } catch (SQLException ex) {
            log.error("can't fetch data", ex);
        }
    }

    @Test
    public void testPagingList() {
        try (Connection connection = this.dataSource.getConnection()) {
            this.dao = new ExampleTableDao(connection);

            List<ExampleTable> showMoreThanStored = this.dao.findAll(0l, 10l, null, null, null);
            assertEquals("jumlah data example table when limit 10 and offset 0", showMoreThanStored.size(), 5);

            List<ExampleTable> showOnly3 = this.dao.findAll(0l, 3l, null, null, null);
            assertEquals("jumlah data example table when limit 3 and offset 0", showOnly3.size(), 3);

            List<ExampleTable> showOnly2 = this.dao.findAll(3l, 3l, null, null, null);
            assertEquals("jumlah data example table when limit 3 and offset 3", showOnly2.size(), 2);
        } catch (SQLException ex) {
            log.error("can't fetch data", ex);
        }
    }

    @Test
    public void testSavingData() {
        try (Connection connection = this.dataSource.getConnection()) {
            this.dao = new ExampleTableDao(connection);
            ExampleTable returnValue = this.dao.save(
                    new ExampleTable(
                            null,
                            "Muhamad Purwadi",
                            Date.valueOf(LocalDate.now()),
                            Timestamp.valueOf(LocalDateTime.now()),
                            true,
                            0l, new
                            BigDecimal(100000),
                            "test data",
                            0f)
            );
            assertNotNull("employee id not null", returnValue.getId());
            log.info("employee: {}", returnValue);

            this.dao.removeById(returnValue.getId());

            List<ExampleTable> list = this.dao.findAll();
            assertEquals("jumlah data example table", list.size(), 5);
        } catch (SQLException ex) {
            log.error("can't fetch data", ex);
        }
    }

}
{% endhighlight %}

Kemudian kita jalankan kembali unit testnya dengan perintah berikut:

```bash
mvn clean compile test
```

berikut hasilnya:

```bash
-------------------------------------------------------
 T E S T S
-------------------------------------------------------
Running com.maryanto.dimas.bootcamp.TestConnection
[main] INFO com.zaxxer.hikari.HikariDataSource - HikariPool-1 - Starting...
[main] INFO com.zaxxer.hikari.HikariDataSource - HikariPool-1 - Start completed.
[main] INFO com.maryanto.dimas.bootcamp.TestConnection - status connected
Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.375 sec
Running com.maryanto.dimas.bootcamp.TestIntegrationExampleTable
[main] INFO com.zaxxer.hikari.HikariDataSource - HikariPool-2 - Starting...
[main] INFO com.zaxxer.hikari.HikariDataSource - HikariPool-2 - Start completed.
[main] INFO com.zaxxer.hikari.HikariDataSource - HikariPool-3 - Starting...
[main] INFO com.zaxxer.hikari.HikariDataSource - HikariPool-3 - Start completed.
[main] INFO com.maryanto.dimas.bootcamp.TestIntegrationExampleTable - employee: ExampleTable(id=97aadfe6-dac1-4084-9128-785e02177669, name=Muhamad Purwadi, createdDate=2020-04-20, createdTime=2020-04-20 19:54:31.349, active=true, counter=0, currency=100000, description=test data, floating=0.0)
[main] INFO com.zaxxer.hikari.HikariDataSource - HikariPool-4 - Starting...
[main] INFO com.zaxxer.hikari.HikariDataSource - HikariPool-4 - Start completed.
Tests run: 3, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.289 sec

Results :

Tests run: 4, Failures: 0, Errors: 0, Skipped: 0

[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  5.429 s
[INFO] Finished at: 2020-04-20T19:54:31+07:00
[INFO] ------------------------------------------------------------------------
```

Jika temen-temen perhatikan API class `PreparedStatement` apa perbedaanya dengan API class `Statement`?.... ya berikut jawabannya:

1. PreparedStatement menunjukan bahwa value yang kita inject tidak di hardcode dalam query
2. PreparedStatement perlu di compile dulu oleh JDBC sehingga terhindar dari serangan SQL Injection.
3. PreparedStatement lebih mudah di maintanance, karena lebih mudah di baca
4. Dan masih ada beberapa kelebihan lain.



Summary

Munkin temen-temen yang pemula / awam bingung, pertanyaan-nya kapan kita menggunakan `PreparedStatement` atau `Statement` jawabanya `Depands on problem you want to solve` mau pake API Statement silahkan mau pake API PreparedStatement silahkan.