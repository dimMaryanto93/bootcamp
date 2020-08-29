---
layout: post
title: "Memahami Struktur Project dengan maven-archetype-webapp"
date: 2020-08-29T18:45:59+07:00
lang: java-web
categories:
- java
- web
- war
refs: []
youtube: 
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-009
---

Setelah kita membuat project dengan maven menggunakan template `maven-archetype-webapp` berikut adalah struktur directory yang kita harus ketahui, berikut adalah folder dan file configurasinya:

{% highlight bash %}
.
├── pom.xml
├── src
│   ├── main
│   │   ├── java
│   │   ├── resources
│   │   └── webapp
│   │       ├── WEB-INF
│   │       │   └── web.xml
│   │       └── index.jsp
│   └── test
│       ├── java
│       └── resources
└── target
    ├── bootcamp-java-webapp
    │   ├── META-INF
    │   ├── WEB-INF
    │   │   ├── classes
    │   │   ├── lib
    │   │   └── web.xml
    │   └── index.jsp
    └── bootcamp-java-webapp.war
{% endhighlight %}

Berikut adalah penjelasannya:

| File & Directory | Descriptions |
| :--- |:--- |
| `pom.xml` | Maven configuration, Project Dependency management |
| `src/main/java` | Java Source Code, berisi file `*.java` dan `package` |
| `src/main/resources` | Resources, berisi file seperti `*.jpg`, `*.png`, `*.jrxml` |
| `src/main/filter` | Resource servlet filter |
| `src/main/webapp` | Web Pages seperti `*.html`, `*.jsp`, `*.js`, `*.css` |
| `src/main/webapp/WEB-INF/web.xml` | Java Web Descriptor configuration |
| `src/test/java` | Test Sources |
| `src/test/resources` | Test Resources |
| `target` | Build files location |
