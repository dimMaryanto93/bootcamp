---
layout: post
title: "Deep dive making decision in SWITCH-CASE statement"
date: 2017-11-11T23:07:06+07:00
lang: java-core
categories:
- Java
- Core
gist: 
youtube: 
comments: true
---

Percabagan ```switch-case``` sebenarnya tidak jauh berbeda tpi disini kita akan lihat bagaimana cara kerja dari percabagan ini, berikut adalah contoh kasus sederhaan dari kodingnya sering kita jumpai yaitu seperti berikut:

{% highlight java linenos %}
package com.maryanto.dimas.tdi.training.java.core;

public class DeepSwichCaseStatement{

    public static void main(String[] args){
        Integer ip = 4;
        switch(ip){
            case 4: System.out.println("A"); break;
            case 3: System.out.println("B"); break;
            case 2: System.out.println("C"); break;
            case 1: System.out.println("D"); break;
            default: System.out.println("E");
        }
    }
}
{% endhighlight %}

Supaya gampang menjelaskannya seperti biasa kita visualisaksikan menggunakan diagram activity seperti berikut:

![Switch case statement basic](/resources/downloads/imgs/java-core/switch-case-statement/switch-basic.jpg)

Nah jadi hasilnya adalah ```A```, kenapa A jadi gini penjelasnnya:

1. Membuat variable ```int ip = 4```, kemudian pada dasarnya sama seperti if yaitu kita memasukan expresinya kemudian si switch ini akan mencari mana value yang cocok
2. Setelah menemukan case pertama yaitu ```case: 4``` maka dia akan menjalankan perintah didalamnya yaitu ```System.out.println("A")``` kemudian ada keyword ```break;``` ini artinya kita keluar dari seleksi. maka dari itu hasilnya ```A```

Selanjutnya sekarang kita modifikasi sedikin dari koding yang sama seperti berikut:

{% highlight java linenos %}
package com.maryanto.dimas.tdi.training.java.core;

public class DeepSwichCaseStatementModif{

    public static void main(String[] args){
        Integer ip = 2;
        switch(ip){
            case 4: System.out.println("A"); 
            case 3: System.out.println("B"); break;
            case 2: System.out.println("C"); 
            case 1: System.out.println("D"); break;
            default: System.out.println("E");
        }
    }
}
{% endhighlight %}

Nah sekarang apa outputnya? 

Seperti biasa kita gunakan diagram activity untuk mempermudah memvisualisasikan dari koding diatas seperti berikut:

![Switch case statement basic without break](/resources/downloads/imgs/java-core/switch-case-statement/switch-modif.jpg)

Berikut penjelasannya

1. Ok jadi gini, pertama sama seperti tadi kita membuat dulu variable ```ip = 2```.
2. Setelah itu si switch meriksa nih case mana yang sesuia.
3. Ketemulah ```case : 2``` setelah itu dia akan menampilkan kelayar yaitu ```C``` setelah itu menampilkan lagi ke layar yaitu ```D``` setelah itu baru dia keluar karena ada keyword ```break;```.
4. Kesimpulannya jadi hasilnya dalah ```CD```.
