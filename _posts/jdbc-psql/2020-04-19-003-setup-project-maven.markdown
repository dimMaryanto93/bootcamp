---
layout: post
title: "Setup Project JDBC dengan Apache Maven"
date: 2020-04-19T14:25:25+07:00
lang: java-jdbc-psql
categories:
- Java
- JDBC
- Postgresql 
refs: 
- https://github.com/dimMaryanto93/jdbc-psql-example
- https://flywaydb.org
- https://search.maven.org/artifact/org.postgresql/postgresql/42.2.12.jre7/bundle
- https://github.com/brettwooldridge/HikariCP
- https://maven.apache.org/plugins/maven-compiler-plugin/
- https://projectlombok.org
youtube: https://www.youtube.com/watch?v=E3VWQssyf0Y&list=PLV1-tdmPblvxVAb1P-CRsPraIv3ks3A16&index=3
comments: true
---

Hi, di materi kali ini kita akan membuat project java dengan Apache Maven dengan kebutuhan CRUD (Create Read Update Delete) database dari Java Application. berikut stepnya:

## Create project

Membuat project dengan maven, cukup mudah kita cukup buka Command line atau Command Promnt kemudian berikut perintanya:

```bash
mvn archetype:generate \
-DartifactId=bootcamp-jdbc-psql \
-DgroupId=com.maryanto.dimas.bootcamp \
-Dversion=2020.04.19.12.40-release \
-DarchetypeCatalog=internal
```

## Update unit testing version

Kemudian setelah project tergenerate oleh apache maven, kita update dependency unit testing ke versi yang lebih baru di file `pom.xml` seperti berikut:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    
    <!-- config project -->

    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```

## Add build compailer for java 1.8

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    
    <!-- config project -->

    <dependencies>
        <!-- other dependency -->
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
        
            <!-- other plugins -->
        </plugins>
    </build>
</project>
```

## Add lombok plugin

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <!-- config project -->

    <dependencies> 
        <!-- enabled setter & getter method automaticly generated -->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.10</version>
        </dependency>
        <!-- enabled logging -->
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>1.7.30</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-simple</artifactId>
            <version>1.7.5</version>
        </dependency>

        <!-- other dependecy -->
    </dependencies>

    <build>
        <plugins>
            <!-- other plugins -->
        </plugins>
    </build>
</project>
```

Untuk menghubungkan antara Java dengan Database yang kita inginkan contohnya PostgreSQL kita membutuhkan software driver. Driver yang kita butuhkan telah tersedia di public maven repository yaitu kita tingal tambahkan dependecy seperti berikut:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    
    <!-- config project -->

    <dependencies>
    <!-- jdbc driver for postgresql -->
        <dependency>
            <groupId>org.postgresql</groupId>
            <artifactId>postgresql</artifactId>
            <version>42.2.12.jre7</version>
            <scope>runtime</scope>
        </dependency>
        <!-- database pooling connection -->
         <dependency>
            <groupId>com.zaxxer</groupId>
            <artifactId>HikariCP</artifactId>
            <version>3.4.2</version>
        </dependency>

        <!-- other dependencies -->
    </dependencies>
</project>

```

Setelah itu kita compile atau package agar semua package yang kita perlukan di resolve oleh maven dengan perintah serti berikut:

```bash
mvn clean package
```

## Add database schema versioning (Optional)

Database schema versioning, adalah commons utils yang kita bisa gunakan untuk me-monitor schema database (not data) antara version aplikasi dan version schema database exacly match. Dengan menambahkan plugin seperti berikut:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    
    <!-- config project -->

    <dependencies>
        <!-- other dependencies -->
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.flywaydb</groupId>
                <artifactId>flyway-maven-plugin</artifactId>
                <version>6.3.3</version>
                <dependencies>
                    <dependency>
                        <groupId>org.postgresql</groupId>
                        <artifactId>postgresql</artifactId>
                        <version>42.2.12.jre7</version>
                        <scope>runtime</scope>
                    </dependency>
                </dependencies>
            </plugin>
        </plugins>
    </build>
</project>
```

Kemudian build menggunakan:

```bash
mvn clean package
```

Setelah sampai sini, setup project untuk CRUD menggunakan Java selesai.



