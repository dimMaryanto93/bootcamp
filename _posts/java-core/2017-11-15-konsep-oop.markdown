---
layout: post
title: "Object Oriented Approach"
date: 2017-11-15T18:47:26+07:00
lang: java-core
categories:
- Java
- Core
gist: 
youtube: 
comments: true
---

Object Oriented Approach pada dasarnya ada 3 konsep yang bisa diimplementasikan. yaitu seperti berikut:

1. Inheritance
2. Polymorpism
3. Encapsulation

## Inheritance atau Pewarisan

Konsep ini adalah mewariskan objek yang ada didalam _class_ induk ke kelas turunannya, sedangkan _class child_ juga memiliki _variable_ dan _method_ tetapi tidak dapat digunakan oleh _class parent_

![Inheritance konsep]({{ site.baseurl }}/resources/posts/java-konsep-oop/inheritance.jpg)

berikut implementasi di Javanya:

### Sepeda

{% highlight java linenos %}
package tdi.training.java.core;

public class Sepeda {
    protected Integer roda = 2;
    protected String rangka = "Besi";

}
{% endhighlight %}

### Motor

{% highlight java linenos %}
package tdi.training.java.core;

public class Motor extends Sepeda {

    public Motor() {
        super.rangka = "Tralis";
    }
    private String mesin = "4 Tak, 2 Cylinder";

}
{% endhighlight %}

### Mobil

{% highlight java linenos %}
package tdi.training.java.core;

public class Mobil extends Sepeda {

    public Mobil() {
        super.roda = 4;
        super.rangka = "Baja";
    }

    private String mesin = "6 Cylinder, 1200cc";

}
{% endhighlight %}

## Polymorpism

Polimorpism adalah kembar tapi tidak sama, magsudnya jadi kita khan punya behavier atau prilaku atau method dengan nama yang sama nilai kembalian yang sama tapi yang menjadi pembedanya adalah dia memiliki nilai masukan atau parameter yang berbeda seperti gambar berikut:

![Polymorpism konsep]({{ site.baseurl }}/resources/posts/java-konsep-oop/polymorpism.jpg)

Berikut implementasi kodingnya:

### Service

{% highlight java linenos %}
package tdi.training.java.core;

public class Service{

    private String nama;

    public String cari(String nama){
        return nama;
    }
}
{% endhighlight %}

### MahasiswaService

{% highlight java linenos %}
package tdi.training.java.core;

public class MahasiswaService extends Service{

    public String cari(){
        return "Ketemu";
    }

    public String cari(String nama, Integer angkatan){
        return new StringBuilder(nama)
            .append(" ")
            .append(angkatan).toString();
    }

    public String cari(Integer angkatan){
        return angkatan.toString();
    }
}
{% endhighlight %}

## Encapsulation

Encapsulation pada dasarnya kita harus mengembunyikan sesuatu, supaya tidak bisa diexpose ke luar kelas tersebut dengan menggunakan keyword `private`, `protected` dan `public`. Tetapi biasanya orang-orang menyembunyikan variable supaya tidak bisa diakses secara langsung untuk aksesnya biasanya menggunakan method yaitu `setter & getter` _approach_.

### Private

Akses _modifier private_ itu jadi intinya **hanya bisa digunakan di _class_ dia sendiri** artinya tidak bisa digunakan / dipanggil ke luar kelas tersebut.

### Protected

Akses _modifier protected_ itu jadi intinya hampir sama dengan keyword _private_ hanya kelebihannya adalah masih bisa diturunkan artinya **tidak bisa di akses _public_** tetapi ketika _class_ itu _extends_ dari _class_ yang mengimplementasikan method tersebut, maka method tersebut bisa digunakan atau dipanggil.

### Public

Akses _modifier public_ itu jadi intinya kebalikan dari akses _modifier private_ atau bisa digunakan / **diakses ke luar _class_**.

### Setter & Getter

Method _setter & getter_ pada dasarnya method biasa hanya fungsinya untuk _inject value_ ke _variable_ mengunakan method _setter_ dan untuk mengeluarkan nilai menggunakan method namanya _getter_ contohnya seperti berikut:

{% highlight java linenos %}
package tdi.training.java.core;

public class EncapsulationExcample{

    private String nama;

    // ini method getter
    public String getNama(){
        return this.nama;
    }

    // ini method setter
    public void setNama(String nama){
        this.nama = nama;
    }
}
{% endhighlight %}