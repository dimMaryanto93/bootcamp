---
layout: post
title: "Break dan Continue statement dalam perulangan"
date: 2017-11-14T13:38:24+07:00
lang: java-core
categories:
- Java
- Core
refs: []
youtube: 
comments: true
---

Statement `break` dan `continue` mungkin dari temen-temen udah agak familiar, mungkin jika temen-temen masih ingat di materi seleksi menggunakan `switch-case` pasti ada statement `break;` nah jadi selain di seleksi di perulangan pun bisa diterapkan untuk statement `break` dan `continue`, jadi tujuannya adalah untuk menghentikan atau skip suatu iterasi pada perlulangan contohnya seperti berikut:

{% highlight java linenos %}
public class BreakLoopStatement {

    public static void main(String[] args){

        for(int i = 0; i < 100; i++){
            if(i == 5) break;
            System.out.println("Saya berada di index ke " + i);
        }
    }
}
{% endhighlight %}

Dan untuk `continue` statement seperti berikut:

{% highlight java linenos %}
public class ContinueLoopStatement {

    public static void main(String[] a){
        
        for(int x = 0 ; x < 3 ; x++){
            if(x == 2) continue;
            System.out.println("Saya berada di index ke " + x);
        }
    }
}
{% endhighlight %}