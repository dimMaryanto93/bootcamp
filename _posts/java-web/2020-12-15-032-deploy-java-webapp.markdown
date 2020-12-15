---
layout: post
title: "Deployment Java Webapp dengan Tomcat Web Server"
date: 2020-12-15T17:32:41+07:00
lang: java-web
categories:
- java
- web
- war
refs: 
- http://tomcat.apache.org/
- https://codehaus-cargo.github.io/cargo/Maven2+plugin.html
youtube: 
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
comments: true
image_path: /resources/posts/java-web-032
---

Setelah kita install Apache Tomcat `8.x`, sekarang kita akan mendeploy aplikasi Java Web kita dengan menggunakan Automate Deployment Approach dengan bantuan plugin `cargo-maven-plugin` jadi kita perlu tambahkan plugin dulu di file `pom.xml` seperti berikut:

{% highlight xml %}
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <dependencies>
       <!-- Other dependency here! -->
    </dependencies>
    <build>
        <finalName>webapp</finalName>
        <!-- Other plugins here! -->
         <plugins>
            <plugin>
                <groupId>org.codehaus.cargo</groupId>
                <artifactId>cargo-maven2-plugin</artifactId>
                <version>1.8.2</version>
                <configuration>
                    <container>
                        <containerId>tomcat8x</containerId>
                        <type>remote</type>
                    </container>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
{% endhighlight %}

Setelah itu kita build project dengan perintah seperti berikut:

{% highlight bash %}
mvn clean -DskipTests package
{% endhighlight %}

Setelah itu kita jalankan Web Server Tomcat nya dengan perintah 

{% highlight bash %}
# arahkan ke directory apache tomcat
cd /opt/apache-tomcat/

# start server
./bin/catalina.sh start

# check logs
tail -f ./log/catalina.out
{% endhighlight %}

Kemudian kita deploy dengan menggunakan perintah seperti berikut:

{% highlight bash %}
mvn cargo:redeploy \
-Dcargo.remote.username=tomcat \
-Dcargo.remote.password=tomcat \
-Dcargo.hostname=localhost \
-Dcargo.servlet.port=18080
{% endhighlight %}

Setelah itu outputnya akan seperti berikut:

```bash
[INFO] [DeployerRedeployMojo] Resolved container artifact org.codehaus.cargo:cargo-core-container-tomcat:jar:1.8.2 for container tomcat8x
[INFO] [mcat8xRemoteDeployer] Redeploying [C:\Users\dimasm93\Workspaces\examples\java-webapp-cargo-tomcat8x\target\webapp.war]
[INFO] [mcat8xRemoteDeployer] Undeploying [C:\Users\dimasm93\Workspaces\examples\java-webapp-cargo-tomcat8x\target\webapp.war]
[INFO] [mcat8xRemoteDeployer] Deploying [C:\Users\dimasm93\Workspaces\examples\java-webapp-cargo-tomcat8x\target\webapp.war]
```

Sekarang kita coba test dari web browser hasilnya seperti berikut:

![browser]({{site.baseurl}}{{page.image_path}}/test-deploy.png)