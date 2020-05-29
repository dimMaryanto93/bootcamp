---
layout: post
title: "Mengenal Transactional dengan JDBC"
date: 2020-05-29T11:19:37+07:00
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

Hai pada pembahasan kali ini kita akan mempelajari tentang transactional di JDBC. seperti yang kita tau klo untuk mengaktifkan transaksi dengan cara sebagai berikut:

```sql
begin;

-- sql in transaction

commit;
```

Jika menggunakan JDBC disarankan untuk tidak menggunakan `begin` dan `commmit` dalam query yang di execute. tetapi menggunakan method `statement.setAutoCommit(false)` dan `statement.commit()` seperti berikut contoh implementasinya:


{% highlight java linenos %}
package com.maryanto.dimas.bootcamp;

import com.maryanto.dimas.bootcamp.config.DatasourceConfig;
import com.maryanto.dimas.bootcamp.dao.ExampleTableDao;
import com.maryanto.dimas.bootcamp.entity.ExampleTable;
import junit.framework.TestCase;
import lombok.extern.slf4j.Slf4j;
import org.junit.Test;

import javax.sql.*;
import java.math.BigDecimal;
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.util.*;

@Slf4j
public class TestIntegrationExampleTable extends TestCase {

    private DataSource dataSource;

    private ExampleTableDao dao;

    @Override
    protected void setUp() throws Exception {
        this.dataSource = new DatasourceConfig().getDataSource();
    }

    @Test
    public void testSavingDataWithTransactional() {
        Connection connection = null;
        try {
            connection = this.dataSource.getConnection();
            connection.setAutoCommit(false);
            this.dao = new ExampleTableDao(connection);

            ExampleTable muhamadPurwadi = new ExampleTable(
                    null,
                    "Muhamad Purwadi",
                    Date.valueOf(LocalDate.now()),
                    Timestamp.valueOf(LocalDateTime.now()),
                    true,
                    0l, 
                    new BigDecimal(100000),
                    "test data",
                    0f);
            ExampleTable save1 = this.dao.save(muhamadPurwadi);

            assertNotNull("employee id not null", save1.getId());
            log.info("employee: {}", save1);

            List<ExampleTable> list = this.dao.findAll();
            assertEquals("jumlah data example table", list.size(), 6);

            this.dao.removeById(save1.getId());

            muhamadPurwadi.setCurrency(null);
            ExampleTable save2 = this.dao.save(muhamadPurwadi);

            list = this.dao.findAll();
            assertEquals("jumlah data example table", list.size(), 6);

            log.info("employee: {}", save2);
            this.dao.removeById(save2.getId());

            list = this.dao.findAll();
            assertEquals("jumlah data example table", list.size(), 5);
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