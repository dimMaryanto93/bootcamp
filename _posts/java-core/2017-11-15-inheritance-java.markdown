---
layout: post
title: "Mengenal lebih jauh tentang inheritance"
date: 2017-11-15T20:19:57+07:00
lang: java-core
categories:
- Java
- Core
gist: 
youtube: 
comments: true
---

Mungkin _inheritance_ di Java agak _anti-mainstream_ artinya beda dari teknologi pesaingnya seperti `.NET`, `PHP` dan lain-lain, yang menerapkan _single extends_. Seperti di konsep sebelumya yaitu seperti berikut:

![Single extends]({{ site.baseurl }}/resources/downloads/imgs/java-core/konsep-oop/inheritance.jpg)

Sedangkan untuk _multiple extends_ di Java digantikan dengan sistem _interface_ atau lebih dikenal dengan _abstract class_. Kalau digambarkan jadi seperti berikut:

![Multiple extends]({{ site.baseurl }}/resources/downloads/imgs/java-core/inherintance/multi-inherintance.jpg)

Di Java tidak mengenal _multiple inherintace_ dalam _class_ sebagai gantinya menggunakan sebuah _interface_ seperti berikut contohnya:

### Engine

{% highlight java linenos %}
package tdi.training.java.core;

public interface Engine{
    String engineBlock = "V4 inline";
    Integer cylinder = 4;
}
{% endhighlight %}

### BreakCPU

{% highlight java linenos %}
package tdi.training.java.core;

public interface BreakCPU{
    boolean ktrc = true;
    boolean abs = true;
}
{% endhighlight %}

### SportBike

{% highlight java linenos %}
package tdi.training.java.core;

public interface SportBike extends Engine, BreakCPU{
    boolean raceMode();
}
{% endhighlight %}

### ZX10RR

{% highlight java linenos %}
package tdi.training.java.core;

public class ZX10RR implements SportBike {

    public boolean raceMode(){
        return true;
    }

    public static void main(String[] args){
        ZX10RR rea = new ZX10RR();
        System.out.println(
            "Engine : [ engineBlock : " + rea.engineBlock + ", cylinder : " + rea.cylinder + "], breaking system : [ abs : " + rea.abs + "], profile race mode is " + rea.raceMode()
        ); 	
    }
}
{% endhighlight %}

