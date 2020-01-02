---
layout: post
title: "Mengenal keyword super dan this"
date: 2017-11-15T23:11:40+07:00
lang: java-core
categories:
- Java
- Core
refs: []
youtube: 
comments: true
---

Mungkin dari temen-temen masih agak bingung apa sih yang membedakan antara _super_ dan _this_ dan juga mungkin melihat dari materi sebelumnya bagian inherintace dan bagian encapsulation tapi belum dijelaskan apa magsud dan tujuannya. Ok nah masilnya saya punya contoh seperti berikut:

### ParentClass

{% highlight java linenos %}
package tdi.training.java.core;

public class ParentClass {
	
    public String hitung(){
        return "Parent class";
    }	
}
{% endhighlight %}

### ChildClass

{% highlight java linenos %}
package tdi.training.java.core;

public class ChildClass extends ParentClass {

    @Override
    public String hitung(){
        return "Child class";
    }

    public void dariKelasIni(){
        System.out.println(this.hitung());
    }

    public void dariKelasInduk(){
        System.out.println(super.hitung());
    }
}
{% endhighlight %}

Coba perhatikan di method `dariKelasIni()` mengunakan _keyword this_ sedangkan di method `dariKelasInduk()` menggunakan _keyword super_

### MainApplication

{% highlight java linenos %}
package tdi.training.java.core;

public class MainApplication{

    public static void main(String[] args){
        ChildClass anak = new ChildClass();
        anak.dariKelasIni();
        anak.dariKelasInduk();
    }
}
{% endhighlight %}

Intinya adalah kita menggunakan _keyword this_ maka akan menunjuk _class_ `ChildClass` sedangkan untuk _keyword super_ maka akan menunjuk _class_ `ParentClass` karena _class_ `ChildClass` turunan dari `ParentClass`.