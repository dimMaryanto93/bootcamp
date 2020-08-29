---
layout: post
title: "Memahami Struktur Project dengan maven-archetype-webapp"
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
    ├── bootcamp-java-webapp.war
    ├── classes
    ├── maven-archiver
    │   └── pom.properties
    ├── maven-status
    │   └── maven-compiler-plugin
    │       ├── compile
    │       │   └── default-compile
    │       │       └── inputFiles.lst
    │       └── testCompile
    │           └── default-testCompile
    │               └── inputFiles.lst
    └── test-classes
{% endhighlight %}