---
layout: post
title: "Mengenal lebih jauh tentang polymorpism"
date: 2017-11-15T22:10:39+07:00
lang: java-core
categories:
- Java
- Core
refs: []
youtube: 
comments: true
---

Di materi sebelumya kita tau klo _polymorpism_ ini merupakan salah satu fitur _Object Oriented Programming_. Beberapa fitur diataranya yaitu _Override_ dan _Overload_

## _Override_

Mungkin dari temen-temen pasti tau apa itu _override_, yap dari namanya ja udah _override_ artinya kurang lebih sama kayak _rename_ atau _replace_. Jadi penjelasnya dari kelas _parent_ misalnya punya method dengan nama `hitung()` maka di kelas _child_ dibuat ulang dengan nama yang sama kemudian isinya pun memungkinkan berbeda. Contohnya seperti berikut:

### ParentOverride

{% highlight java linenos %}
package tdi.training.java.core;

public class ParentOverride{

    public void hitung(){
        System.out.println("Ini dari kelas parent");
    }
}
{% endhighlight %}

### ChildOverride

{% highlight java linenos %}
package tdi.training.java.core;

public class ChildOverride extends ParentOverride {

    @Override
    public void hitung(){
        System.out.println("ini dari kelas child");
    }
}
{% endhighlight %}

### MainApplication

{% highlight java linenos %}
package tdi.training.java.core;

public class MainApplication{

    public static void main(String[] args){
        ParentOverride ganti = new ParentOverride();
        System.out.println("nilai hitung dari parent override ");
        ganti.hitung();

        ganti = new ChildOverride();
        System.out.println("nilai hitung dari child override ");
        ganti.hitung();
    }
}
{% endhighlight %}

## _Overloading_

Di bahasa pemograman Java, untuk _function_ atau method yang memiliki nama yang sama dalam satu _class_ yang sama itu memang dilarang tapi ada _exeption_ untuk yang _Approach_ yang satu ini. Tapi ada syarat dan ketentuanya sebagai berikut:

1. Jumlah paramenter atau _arguments_ yang berbeda-beda.
2. Urutan tipe data untuk parameter atau _arguments_ yang berbeda.
3. _Return type_ yang berbeda tidak mempengaruhi.

Supaya lebih jelasnya berikut ini contoh, implementasinya:

### ParentOverloading

{% highlight java linenos %}
package tdi.training.java.core;

import java.math.BigDecimal;

public class ParentOverloading{

    public void hitung() {
        System.out.println("10");
    }

    public void hitung(Integer bil1){
        System.out.println(bil1);
    }

    public void hitung(Integer bil1, Integer bil2){
        System.out.println(bil1 + bil2);
    }

    public void hitung(BigDecimal bil1, Integer bil2){
        System.out.println(bil1.add(new BigDecimal(bil2)));
    }
}
{% endhighlight %}

### MainApplication

{% highlight java linenos %}
package tdi.training.java.core;

import java.math.BigDecimal;

public class MainApplication{

    public static void main(String[] args){
        ParentOverloading calkulator = new ParentOverloading();
        calkulator.hitung(); // out -> 10
        calkulator.hitung(20); // out -> 20
        calkulator.hitung(10, 20); // out -> 30
        calkulator.hitung(new BigDecimal(1000), 10); // out -> 1010
    }
}
{% endhighlight %}