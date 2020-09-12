---
layout: post
title: "Membuat project Java Web dengan Apache Maven"
date: 2020-08-27T22:54:34+07:00
lang: java-web
categories:
- java
- web
- war
refs: []
youtube: https://www.youtube.com/watch?v=_PpFIcqq-IA&list=PLV1-tdmPblvyaCTcYR9u7k4G24uVDZT0v&index=7
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-003
---

kali ini saya akan membuat project Java Web dengan menggunakan Apache Maven dengan template project ```maven-archetype-webapp```. berikut adalah langkah-langkahnya:

## Create Project dengan Apache Maven

{% highlight bash %}
mvn archetype:generate \
-DgroupId=com.maryanto.dimas.example \
-DartifactId=bootcamp-java-webapp \
-Dversion=1.0.0-release \
-DarchetypeCatalog=internal \
-DarchetypeGroupId=org.apache.maven.archetypes \
-DarchetypeArtifactId=maven-archetype-webapp
{% endhighlight %}

berikut adalah outputnya: 

```bash
[INFO] ----------------------------------------------------------------------------
[INFO] Using following parameters for creating project from Old (1.x) Archetype: maven-archetype-webapp:1.0
[INFO] ----------------------------------------------------------------------------
[INFO] Parameter: basedir, Value: C:\Users\dimasm93\Workspaces\examples
[INFO] Parameter: package, Value: com.maryanto.dimas.example
[INFO] Parameter: groupId, Value: com.maryanto.dimas.example
[INFO] Parameter: artifactId, Value: bootcamp-java-webapp
[INFO] Parameter: packageName, Value: com.maryanto.dimas.example
[INFO] Parameter: version, Value: 1.0.0-release
[INFO] project created from Old (1.x) Archetype in dir: C:\Users\dimasm93\Workspaces\examples\bootcamp-java-webapp
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  2.920 s
[INFO] Finished at: 2020-08-21T14:51:52+07:00
[INFO] ------------------------------------------------------------------------
```

## Embeded tomcat7 to run

Untuk menjalankan project, kita memerlukan Web Server seperti tomcat, undertow, jboss eap dll, dalam phase development akan lebih mudah menggunakan plugin maven yaitu `tomcat7-maven-plugin` berikut cara installnya:

kita edit file `pom.xml` dengan menambahkan `plugins` seperti berikut:

{% highlight xml %}
<project    xmlns="http://maven.apache.org/POM/4.0.0" 
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.maryanto.dimas.example</groupId>
    <artifactId>javaee-webapp</artifactId>
    <packaging>war</packaging>
    <version>1.0.0-release</version>
    <name>javaee-webapp-maven</name>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <endorsed.dir>${project.build.directory}/endorsed</endorsed.dir>
    </properties>

    <build>
        <finalName>${project.artifactId}</finalName>
        <!-- tambahkan dari sini -->
        <plugins>
            <plugin>
                <groupId>org.apache.tomcat.maven</groupId>
                <artifactId>tomcat7-maven-plugin</artifactId>
                <version>2.2</version>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.1</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                    <compilerArguments>
                        <endorseddirs>${endorsed.dir}</endorseddirs>
                    </compilerArguments>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>3.2.3</version>
                <configuration>
                    <failOnMissingWebXml>false</failOnMissingWebXml>
                </configuration>
            </plugin>
            <!-- sampai sini -->
        </plugins>
    </build>
</project>
{% endhighlight %}

Kemudian untuk menjalankan gunakan ```tomcat7:run```seperti berikut:

{% highlight bash %}
mvn -DskipTests clean package tomcat7:run
{% endhighlight %}

Maka hasilnya seperti berikut:

![tomcat running]({{site.baseurl}}{{ page.image_path }}/tomcat7-works-it.png)

## Enabled Servlet Annotation, JSP, JSTL & Lombok

Untuk mengaktifkan fitur Annotation kita harus menambahkan dependency `javax:javaee-web-api`, `jstl:jstl` seperti berikut:

{% highlight xml %}
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.maryanto.dimas.example</groupId>
    <artifactId>javaee-webapp</artifactId>
    <packaging>war</packaging>
    <version>1.0.0-release</version>

    <properties>
        <java.version>1.8</java.version>
        <slf4j.version>1.7.25</slf4j.version>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <endorsed.dir>${project.build.directory}/endorsed</endorsed.dir>
    </properties>

    <dependencies>
        <!-- enabled jstl -->
        <dependency>
            <groupId>jstl</groupId>
            <artifactId>jstl</artifactId>
            <version>1.2</version>
        </dependency>
        <!-- enabled JSP -->
        <dependency>
            <groupId>javax</groupId>
            <artifactId>javaee-web-api</artifactId>
            <version>7.0</version>
            <scope>provided</scope>
        </dependency>
        <!-- enabled logger using slf4j -->
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-jdk14</artifactId>
            <version>${slf4j.version}</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>${slf4j.version}</version>
        </dependency>
        <!-- project lombok -->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.12</version>
            <scope>provided</scope>
        </dependency>

        <!-- update version junit ke version 4.13 -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
    <build>
        <finalName>${project.artifactId}</finalName>
        <!-- plugins -->
    </build>
</project>

{% endhighlight %}