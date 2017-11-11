---
layout: post
title: "Deep dive in IF statement"
lang: java-core
categories:
- Java
- Core
gist: 
youtube: 
comments: true
---

Dimateri [sebelumnya]({% post_url java-core/2017-11-11-control-flow %}) saya udah singung tentang penggunaan `if` statement, di section ini kita akan belajar lebih dalam lagi tentang `if` statement supaya lebih paham lagi tentang konsep dan cara penggunaanya. Nah jadi sebelumnya kita hanya punya **satu kondisi** saja bagaimana jika punya **dua kondisi**. Tentunya bahasa Java telah menyediakannya ya, yaitu dengan menggunakan `if-else` berikut contoh penggunaanya

{% highlight java linenos %}
package com.maryanto.dimas.tdi.training.java.core;

public class DeepIfElse{
    
    public static void main(String[] args){
        String word = "Halo";
        if(word.equals("halo")){
            System.out.println("data sama");
        }else {
            System.out.println("data beda!");
        }
    }
}
{% endhighlight %}