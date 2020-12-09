---
layout: post
title: "Persiapan untuk Deploy Java Webapp"
lang: java-web
categories:
- java
- web
- war
refs: 
- http://tomcat.apache.org/
- https://crunchify.com/how-to-change-jvm-heap-setting-xms-xmx-of-tomcat/
youtube: 
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
comments: true
image_path: /resources/posts/java-web-031
---

Halo, kali ini saya akan membahas tentang Deployment menggunakan Apache Tomcat. sebenarnya untuk Web Server sendiri di Servlet Container ada beberapa, diantaranya:

1. [Apache Tomcat](http://tomcat.apache.org/)
2. [Oracle GlassFish](https://javaee.github.io/glassfish/)
3. [Payara](https://www.payara.fish/downloads/)
4. [Redhat JBoss EAP](https://www.redhat.com/en/technologies/jboss-middleware/application-platform)
5. [WildFly](https://www.wildfly.org/)
6. Dan masih banyak lagi.

Nah sekarang kita akan belajar melakukan Deploy aplikasi Java Web ke Web Server dengan menggunakan Apache Tomcat versi `8.5.x`. Sebelum kita mendeploy kita biasanya lakukan installasi dulu dan config server dulu.

## Install Web Server Apache Tomcat `8.5.x`

Untuk menginstall ada beberapa cara, oh ia ada yang lupa. disini os yang kita gunakan adalah `linux server` ya karena mostly operation system yang digunakan adalah linux jadi kita pake linux aja ya. tapi jangan khawatir untuk windows juga bisa kok hanya perlu penyesuaian saja. Untuk linux sebenarnya kita bisa dengan mudah menginstall menggunakan repository seperti apt, yum, dnf, zepper dan lain-lain. tpi kali ini kita akan menggunakan binary saja ya. ok pertama download dulu [Apache Tomcat versi 8.5.x](https://tomcat.apache.org/download-80.cgi)

![Download apache tomcat]({{site.baseurl}}{{page.image_path}}/download.png)

Pilih yang zip ja ya supaya portable.

## Configurasi Apache Tomcat

Setelah kita donwload, biasanya kita upload ke server bisa lewat ssh atau ftp ini bebas sih yang penting filenya udah ada di server target ya.

Kemudian kita extract file zip, dan pindahkan ke lokasi tertentu klo saya biasanya simpan di partision/mounting point yang besar contohnya `/opt` dengan perintah 

{% highlight bash %}
sudo mv apache-tomcat* /opt/tomcat
{% endhighlight %}

Setelah itu kita bisa config seperti port, user management, dan lain-lain.

### Change port

By default tomcat akan jalan di port `8080`, nah saya mau rubah port nya jadi `18080`. kita biasa ubah confignya di file `conf/server.xml`

{% highlight xml %}
<!-- Chanage Server port if you want -->
<Server port="18005" shutdown="SHUTDOWN">
<Listener className="org.apache.catalina.startup.VersionLoggerListener" />
  <!-- Change Connector port -->
  <Connector port="18080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
</Server>
{% endhighlight  %}

### Enabled Tomcat Management GUI

By default kita tidak di berikan akses untuk management GUI di tomcat, untuk mengaktifkan kita bisa ubah confignya di file `conf/tomcat-users.xml`

{% highlight xml %}
<!-- Chanage Server port if you want -->
<tomcat-users xmlns="http://tomcat.apache.org/xml"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:schemaLocation="http://tomcat.apache.org/xml tomcat-users.xsd"
              version="1.0">
    <!-- Uncomment & Ubah menjadi seperti berikut -->
    <role rolename="tomcat"/>
    <user username="tomcat" password="tomcat" roles="tomcat, manager-gui, manager-script, manager-jmx, manager-status, admin-gui, admin-script"/>
</tomcat-users>
{% endhighlight  %}

By default juga management gui, tidak bisa dilakukan selain `localhost` jadi kita perlu allow connection dengan membuat file `conf/Catalina/localhost` dengan nama `manager.xml` seperti berikut:

{% highlight xml %}
<Context privileged="true" antiResourceLocking="false"
        docBase="${catalina.home}/webapps/manager">
    <Valve className="org.apache.catalina.valves.RemoteAddrValve" allow="^.*$" />
</Context>
{% endhighlight  %}

### Change JVM Heap

Optimaze kinerja Web Server dengan menikatkan JVM Heap di tomcat. 

- `-Xmx` yaitu Specifies the maximum size, in bytes, of the memory allocation pool. 
- `-Xmn` yaitu It’s a size of the heap.
- `-XX:PermSize` yaitu It’s used to set size for Permanent Generation.

pertama kita buat file `setenv.sh` (linux) klo di windows `setenv.bat` di dalam folder `tomcat installation/bin` seperti berikut:

{% highlight bash %}
export CATALINA_OPTS="$CATALINA_OPTS -Xms512m"
export CATALINA_OPTS="$CATALINA_OPTS -Xmx8192m"
export CATALINA_OPTS="$CATALINA_OPTS -XX:MaxPermSize=256m"
{% endhighlight %}

## Starting Web Server

Untuk start web server kita bisa menggunakan perintah seperti berikut:

{% highlight bash %}
# path to tomcat, ex i have install in /opt/tomcat
/opt/apache-tomcat/bin/catalina.sh start

# output
Using CATALINA_BASE:   /opt/apache-tomcat
Using CATALINA_HOME:   /opt/apache-tomcat
Using CATALINA_TMPDIR: /opt/apache-tomcat/temp
Using CLASSPATH:       /opt/apache-tomcat/bin/bootstrap.jar:/opt/apache-tomcat/bin/tomcat-juli.jar
Using CATALINA_OPTS:
Tomcat started.

{% endhighlight %}

## Allow port di access dari luar (firewall)

Untuk memberikan akses ke luar (network), kita bisa allow di firewall karena di sini saya pake centos kita bisa aktifkan menggunakan perintah berikut:

{% highlight bash %}
firewall-cmd --zone=public --add-port=18080/tcp --permanent && firewall-cmd --reload
{% endhighlight %}

## Test Run

Sekarang kita bisa test dari laptop/pc kita menggunakan browser jika Web Server udah Jalan. dengan url [host:port](http://192.168.88.254:18080/) maka hasilnya seperti berikut:

![Apache Tomcat Works!]({{site.baseurl}}{{page.image_path}}/tomcat-root.png)

## Struktur Directory Apache Tomcat

Sekarang kita lihat dulu struktur directory pada Apache Tomcat `8.5.x` yaitu seperti berikut:

![Structure Dir Tomcat 8.5]({{site.baseurl}}{{page.image_path}}/tomcat-dir.png)

Terdiri dari:

- `bin`, yaitu digunakan untuk start/stop management tomcat.
- `conf`, yaitu untuk configurasi Apache Tomcat seperti port, jmx dan lain-lain
- `logs`, yaitu tempat menyimpan file berupa log yang di execute oleh tomcat.
- `webapps`, yaitu tempat kita nanti deploy.