---
layout: post
title: "Looping menggunakan For statement part 2"
date: 2017-11-14T10:58:09+07:00
lang: java-core
categories:
- Java
- Core
refs: []
youtube: 
comments: true
---


Di materi [sebelumnya]({% post_url java-core/2017-11-12-for-statement %}) kita udah mengetahui bagaimana perulangan dengan perintah `for` statement. Sekarang kita, akan coba membuat satu kasus yaitu `for` dalam `for` atau didalam perulangan ada perlulangan contohnya seperti berikut:

{% highlight java linenos %}
public class LoopingInnerLoop {

    public static void main(String[] args){
        for(int i = 0; i < 10; i++){
            for(int j = 0; j < 5; j ++){
                System.out.print("j["+ j + "], ");
            }
            System.out.println("i["+ i + "]");
        }
    }
}
{% endhighlight %}

Selain itu juga kita bisa kombinasikan antara looping dengan seleksi. contohnya seperti berikut:

{% highlight java linenos %}
public class IfIntoForStatement{

    public static void main(String[] args){
        for(int i = 0; i < 10; i++){
            if( i == 5 ){
                System.out.println("Sekarang ada di posisi ke 5");
            }
        }
    }
}
{% endhighlight %}

Atau kita bisa juga, di dalam selekasi ada perulangan. contohnya seperti berikut:

{% highlight java linenos %}
public class ForIntoIfStatement{

    public static void main(String[] args){
        boolean isRepeat = true;
        if(isRepeat) {
            for(int i = 0; i < 10; i ++){
                System.out.println("Sekarang ada di index ke "+ i);
            }
        }

    }
}
{% endhighlight %}

Selain kombinasi juga kita bisa main-main dengan indexing dalam perulangan tersebit contohnya di sebelumnya hasil yang dikeluarkan index `[0, 1, 2, 3, ....]` dan seterusnya ya nah sekarang mau saya balik jadi `[...., 4, 3, 2, 1, 0]` contohnya seperti berikut:

{% highlight java linenos %}
public class ForReverseIndex {

    public static void main(String[] args){

        for(int i = 10 ; i > 0; i--){
            System.out.println("Indexnya "+ i);
        }
    }
}
{% endhighlight %}
