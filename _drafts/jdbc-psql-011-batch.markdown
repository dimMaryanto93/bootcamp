---
layout: post
title: "Batch processing dengan JDBC"
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

Hai [sebelumnya]({{site.baseurl}}{% post_url jdbc-psql/2020-05-29-010-transactional %}) kita udah membahas tentang transactional di JDBC. nah sekarang kita akan melanjutkan pembahasan tentang batch proccessing atau orang-orang lebih sering menyebutnya bulk query. batch processing biasanya penerapannya untuk melakukan insert secara berulang seperti berikut contoh penerapan dalam sql:

{% highlight sql linenos %}
begin;

insert into example_table (name, created_date, created_time, is_active, counter, currency, description, floating)
values 
    ('Dimas Maryanto', now(), now(), false, 0, 0, '', 0.0),
    ('Muhamad Purwadi', now(), now(), false, 0, 0, '', 0.0),
    ('Muhamad Yusuf', now(), now(), false, 0, 0, '', 0.0),
    ('Junaedi', now(), now(), false, 0, 0, '', 0.0),
    ('Prima', now(), now(), false, 0, 0, '', 0.0);

commit;
{% endhighlight %}


berikut implementasi menggunakan JDBC:

Tambahkann method `save(List<ExampleTable> values)` sebagai berikut:

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

    public List<String> save(List<ExampleTable> values) throws SQLException {
        List<String> newList = new ArrayList<>();
        //language=PostgreSQL
        String query = "insert into example_table (name, created_date, created_time, is_active, counter, currency, description, floating)\n" +
                "values (?, ?, ?, ?, ?, ?, ?, ?)";
        PreparedStatement preparedStatement = connection.prepareStatement(query, Statement.RETURN_GENERATED_KEYS);
        for (ExampleTable value : values) {
            preparedStatement.setString(1, value.getName());
            preparedStatement.setDate(2, value.getCreatedDate());
            preparedStatement.setTimestamp(3, value.getCreatedTime());
            preparedStatement.setBoolean(4, value.getActive());
            preparedStatement.setLong(5, value.getCounter());
            preparedStatement.setBigDecimal(6, value.getCurrency());
            preparedStatement.setString(7, value.getDescription());
            preparedStatement.setFloat(8, value.getFloating());
            preparedStatement.addBatch();
        }

        preparedStatement.executeBatch();
        ResultSet generatedKeys = preparedStatement.getGeneratedKeys();
        while (generatedKeys.next())
            newList.add(generatedKeys.getString(1));
        preparedStatement.close();
        return newList;
    }   
}
{% endhighlight %}

Dan tambahkan method untuk melakukan integration testnya sebagai berikut:

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
    public void testSaveBatchData() {
        Connection connection = null;
        try {
            connection = this.dataSource.getConnection();
            connection.setAutoCommit(false);
            this.dao = new ExampleTableDao(connection);
            List<ExampleTable> list = Arrays.asList(
                    new ExampleTable(
                            null,
                            "Muhamad Purwadi",
                            Date.valueOf(LocalDate.now()),
                            Timestamp.valueOf(LocalDateTime.now()),
                            true,
                            0l, new
                            BigDecimal(100000),
                            "test data",
                            0f),
                    new ExampleTable(
                            null,
                            "Junaedi",
                            Date.valueOf(LocalDate.now()),
                            Timestamp.valueOf(LocalDateTime.now()),
                            true,
                            0l, new
                            BigDecimal(100000),
                            "test data",
                            0f)
            );

            List<String> listIds = this.dao.save(list);
            log.info("{}", listIds);
            for (String id : listIds) {
                this.dao.removeById(id);
            }

            connection.commit();


        } catch (SQLException ex) {
            if (connection != null) {
                try {
                    connection.rollback();
                } catch (SQLException throwables) {
                    log.error("can't rollback");
                }
            }
            log.error("can't fetch data", ex);
        }
    }
}
{% endhighlight %}