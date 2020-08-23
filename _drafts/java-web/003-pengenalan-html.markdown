---
layout: post
title: "Pengenalan Scripting language dengan HTML"
lang: java-web
categories:
- java
- web
- war
refs: 
- https://www.w3schools.com/
youtube: 
comments: true
gist: dimMaryanto93/c0a51e92e23ada4ecb71f9c18c803fea
image_path: /resources/posts/java-web-004
---

Internet yang kita akses itu berisi document media type `application/html`, HTML (Hypertext Markup Language) yaitu dokument web yang static yang berisi text, image, video dan media lain-nya.

Format HTML berbentuk XML contohnya seperti berikut:

{% highlight html %}
<!DOCTYPE html>
<html>
<head>
    <!-- Judul Page, akan muncil di tab browser -->
    <title>Halamat Web</title>
</title>
<body>
    <!-- Tulis semua element html disini, seperti input, table, list, image dan lain-lain -->
    Halo World!
</body>
</html>
{% endhighlight %}

Pada dasarnya HTML terdiri dari berapa element:
1. Tag / Closing Tag
2. Attribute
3. Value

Beberapa element yang utama yaitu

| tag                       | keterangan            |
| :---                      | :---                  |
| `<p>...</p>`              | Paragraf              |
| `<b>...</b>`              | Text Bold             |
| `<i>...</i>`              | Part of Text          |
| `<img src="url"/>`        | Image                 |
| `<form>...</form>`        | Form untuk user input |
| `<input type="text"/>`    | Input field           |
| `<button type="submit"></button>` | Button submit |
| `<table></table>`         | Table element         |
| `<ul>...</ul>`            | Unordered list        |
| `<ol>...</ol>`            | Ordered list          |
| `<script>...</script>`    | used to embed a client-side script |
| `<style>...</style>`                 | used to define style information (CSS) |
| `<div>...</div>`          | defines a division or a section in an HTML document |
