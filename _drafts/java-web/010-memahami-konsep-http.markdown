---
layout: post
title: "Konsep Hypertext Transper Protocol (HTTP)"
lang: java-web
categories:
- java
- web
- war
refs: 
- https://en.wikipedia.org/wiki/List_of_HTTP_status_codes
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages
- https://en.wikipedia.org/wiki/Query_string
youtube: 
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-010
---

Hypertext Transper Protocol atau yang sering di singkat HTTP yaitu sebuah protocol untuk distributed, collaboration, hypermedia information system. Http biasanya digunakan untuk bertukar data melalui World Wide Web.

HTTP function terdiri dari request dan response protocol di jaringan yang memiliki model computasi client-server. seperti yang saya gambarkan pada gambar berikut:

![server-side]({{site.baseurl}}/resources/posts/java-web-010/server-side.jpg)

## Request Methods

Http mendefinisikan method yang terdiri dari 
1. `GET`, request pada umumnya
2. `HEAD`, digunakan untuk meng-identfikasi response selain data contohnya untuk menerima metadata
3. `POST`, method yang biasanya digunakan untuk mengirimkan data secara private ke server
4. `PUT`, method yg bisanya digunakan untuk melakukan update data ke server
5. `DELETE`, method yang biasanya digunakan untuk menghapus data ke server
6. `TRACE`, method yang biasanya digunakan untuk mengecheck server up atau istilah kerennya echo
7. `OPTIONS`, method ini biasanya sebuah response yang mengembailkan authetication session
8. `CONNECT`
9. `PATCH`, method ini biasanya digunakan untuk melakukan update data sebagian ke server

## Request Message

Sebuah request, biasanya memiliki data atau variable yang kita bisa kirim sesuai dengan specifikasi server. Ada beberapa cara untuk mengirimkan data seperti:

1. Path Variable, variable yang dynamic pada url contohnya `host:port/context-path/0001/variable`, `host:port/context-path/0002/variable`
2. Query Parameter, variable yang menggunakan parameter URL contohnya `host:port/context-path/params?param1=value1&param2=value2`
3. Message Body, data yang dikirimkan disimpan dalam body biasanya berbentuk `json` atau `xml` tergantung dari spesifikasi server. contohnya seperti berikut:
```json
{
    "nama": "Dimas Maryanto",
    "userId": "dimasm93",
    "passwd": "12344321"
}
```

## Response Status

Http response memiliki response code atau orang-orang biasanya mengebutnya `RC` nah response-code ini biasanya berupa 3 digit numberik yang di classifikasikan sebagai berikut:

1. RC `1XX` biasanya bersifat Informational
2. RC `2XX` biasanya bersifat Successful
3. RC `3XX` biasanya bersifat Redirection
4. RC `4XX` biasanya bersifat Error Client side seperti contohnya error validation, bad request dan lain-lain
5. RC `5XX` biasanya bersifat Error Server side contohnya seperti Internal Server Error, Bad Gateway, Connection Timeout dan lain-lain.