---
layout: post
title: "Grouping source code dengan class"
date: 2017-11-14T21:52:33+07:00
lang: java-core
categories:
- Java
- Core
gist: 
youtube: 
comments: true
---

Coba kalo temen-temen perhatikan dari materi-materi sebelumya sampe sekarang mungkin klo kita gabungkan kemungkinan _source code_ yang kita tulis udah lumayan banyak ya dan lumayan besar juga khan. Karena topik kita dari [materi sebelumya]({% post_url java-core/2017-11-14-function %}) yaitu modularisasi. 

Modularisasi tidak hanya sebatas dipisahkan dalam _method_ atau _function_ yang saling panggil-memanggil tetepi juga kita bisa pisahkan secara _file_ atau _class_ dengan tujuan lebih teroranisir dan memisahkan function yang tidak berhubungan langsung di _file_ atau _class_ tersebut. Contohnya seperti berikut:

{% highlight java linenos %}
package com.maryanto.dimas.tdi.training.java.core;

public class AplikasiBankBNI{

    public BigDecimal hitungBungaTabungan(Integer idNasabah){
        // proses bisnis untuk menghitung bunga per-nasabah
        return value;
    }

    public BigDecimal hitungBungaDeposito(Integer idNasabah){
        // proses bisnis untuk menghitung buga per-nasabah
        return value;
    }

    public BigDecimal hitungPajakByTabunganAndDepositoPerNasabah(BigDecimal saldoTabungan, BigDecimal SaldoDeposito, Integer idNasabah){
        // proses bisnis untuk menghitung pajak deposito dan tabungan per nasabah
        return value;
    }

    public BigDecimal hitungDendaKreditByNasabah(Integer idNasabah){
        // proses bisnis untuk menghitung denda yang dimiliki nasabah
        return value;
    }
}
{% endhighlight %}

Nah jadi klo saya analisis dari koding diatas, ke empat method tersebut tidak memiliki keterkaitan secara langsung, sebaiknya kita pisahkan secara modul, Misalnya contohnya kita pisahkan jadi 3 modul yaitu `tabungan`, `kredit` dan `deposito`.

Dengan kita pisahkan permodul (3 _class_) yaitu dengan `AplikasiTabungan`, `AplikasiDeposito` dan `AplikasiKredit` seperti berikut:

### Aplikasi Tabungan

{% highlight java linenos %}
package com.maryanto.dimas.tdi.training.java.core;

public class AplikasiTabungan{

    public BigDecimal hitungBunga(Integer idNasabah){
        // proses bisnis untuk menghitung bunga per-nasabah untuk tabungan
        return value;
    }

}
{% endhighlight %}

### Aplikasi Kredit

{% highlight java linenos %}
package com.maryanto.dimas.tdi.training.java.core;

public class AplikasiKredit{

    public BigDecimal hitungBunga(Integer idNasabah){
        // proses bisnis untuk menghitung bunga per-nasabah untuk kredit
        return value;
    }

}
{% endhighlight %}

### Aplikasi Deposito

{% highlight java linenos %}
package com.maryanto.dimas.tdi.training.java.core;

public class AplikasiDeposito{

    public BigDecimal hitungBunga(Integer idNasabah){
        // proses bisnis untuk menghitung bunga per-nasabah untuk deposito
        return value;
    }

}
{% endhighlight %}

### Aplikasi BNI

{% highlight java linenos %}
package com.maryanto.dimas.tdi.training.java.core;

public class AplikasiBNI{

    public static void main(String[] args){
        // cara memanggil method hitungBunga yang ada di file Aplikasi Deposito
        AplikasiDeposito appDepo = new AplikasiDeposito();
        appDepo.hitungBunga(1);

        // cara memanggil method hitungBunga yang ada di file Aplikasi Kredit
        AplikasiKredit appKredit = new AplikasiKredit();
        appKredit.hitungBunga(2);
    }
}
{% endhighlight %}

Nah jadi dengan cara berikut kita bisa lebih dinamis memanage fungsi-fungsi atau proses bisnis tersebut. dan keuntungannya punya secara _source code_ lebih mudah dibaca.

