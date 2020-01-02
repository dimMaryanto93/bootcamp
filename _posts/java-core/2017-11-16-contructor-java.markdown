---
layout: post
title: "Contructor adalah method"
date: 2017-11-16T21:56:08+07:00
lang: java-core
categories:
- Java
- Core
refs: []
youtube: 
comments: true
---

Secara _default_ di Java constuktor akan dibuatkan otomatis ketika kita tidak mendefinisikan construktor di _class_ yang kita buat. Yang mungkin jadi pertanyaan, apa itu construktor?

Construktor yaitu sama halnya dengan method atau _function_ tetapi namanya sama dengan nama _class_ contohnya disini saya punya _class_ dengan nama `Deposito` seperti berikut:

{% highlight java linenos %}
package tdi.training.java.core;

public class Deposito {

    // this is constructor
    public Deposito(){
        // do something here!
    }
}
{% endhighlight %}

Nah sebenarnya, biasanya di materi sebelumnya kita tidak mendifinisikan _method constructor_ karena memang belum diperlukan dan juga tidak ada _action_ apapun. _Constructor_ biasanya digunakan untuk melakukan inisialisasi suatu nilai karena sebenarnya selain method `main()`, _contructor_ yang pertama kali di eksekusi dengan perintah seperti `new Deposito()` artinya kita memanggil method _constructor_ tanpa kita sadari.

Sebenanya kita tidak menggunakan contruktor juga tidak masalah karena, coba anda perhatikan di method `Deposito()` tidak ada satupun perintah yang di definisikan didalam method tersebut. jadi kita cukup seperti berikut:

{% highlight java linenos %}
package tdi.training.java.core;

public class Deposito {

}
{% endhighlight %}

Mengapa method yang kita buat `Deposito()` dihapus, ya karena di Java udah dibuat secara otomatis tanpa di definisikan seperti perintah yang diatas. tetapi jika misalnya kita mau ketika Object deposito dipanggil dan diinisialisasi maka saya mau mengisi variable yang saya definisikan kemudian diisi nilanya ketika di inisialisasi object maka dengan menggunakan _constructor_ ini adalah cara yang tepat contohnya seperti berikut:

{% highlight java linenos %}
package tdi.training.java.core;

import java.math.BigDecimal;

public class Deposito {

    private boolean active;
    private BigDecimal saldo;

    // this is constructor
    public Deposito(){
        this.active = false;
        this.saldo = new BigDecimal(0);
    }
}
{% endhighlight %}

Jadi sekarang ketika saya panggil object deposito setelah di inisialisasi maka variable `active` dan `saldo` otomatis nilainya ada tidak null lagi.

{% highlight java linenos %}
package tdi.training.java.core;

import java.math.BigDecimal;

public class MainApplication{

    public static void main(String[] args){
        Deposito dep = new Deposito();
        System.out.println(
            "status deposito " + 
            dep.active + 
            " sedangkan saldonya " + 
            dep.saldo
        );
    }
}
{% endhighlight %}

Selain itu juga, di _constructor_ bisa sebagai setter method dengan manambahkan parameter seperti berikut contohnya:

 {% highlight java linenos %}
package tdi.training.java.core;

import java.math.BigDecimal;

public class Deposito {

    private boolean active;
    private BigDecimal saldo;

    // this is constructor
    public Deposito(){
        this.active = false;
        this.saldo = new BigDecimal(0);
    }

    public Deposito(boolean isActive, BigDecimal saldo){
        this.active = isActive;
        this.saldo = saldo;
    }
}
{% endhighlight %}

Nah sekarang jadi cara panggilnya menggunakan parameter seperti berikut:

{% highlight java linenos %}
package tdi.training.java.core;

import java.math.BigDecimal;

public class MainApplication{

    public static void main(String[] args){
        Deposito dep = new Deposito(true, new BigDecimal(10000));
        System.out.println(
            "status deposito " + 
            dep.active + 
            " sedangkan saldonya " + 
            dep.saldo
        );
    }
}
{% endhighlight %}

Nah jadi sekarang status depositonya bukan bernilai `false` lagi ya tapi bernilai `true` sedangkan nilai saldonya sekarang yaitu `10000.00`