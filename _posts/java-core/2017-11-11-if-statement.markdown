---
layout: post
title: "Deep dive in IF statement"
date: 2017-11-11T22:25:36+07:00
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
        if(word.equals("halo")) {
            System.out.println("data sama");
        } else {
            System.out.println("data beda!");
        }
    }
}
{% endhighlight %}

Jadi dengan adanya keyword `else` atau artinya statement pengecualian magsud dari pengecualian ini bukan berarti diabaikan, tapi jika semua kondisi tidak ada yang terpenuhi maka statement `else` yang akan di jalankan. Contoh berikutnya bagaimana jika ada lebih dari 2 kondisi, untuk kasus tersebut kita bisa menggunakan keyword `if-else-if` seperti berikut:

{% highlight java linenos %}
package com.maryanto.dimas.tdi.java.core;

public class DeepIfElseIf {

    public static void main(String[] args){
        int bil1 = 10;
        int bil2 = -10;

        if ( bil1 == bil2 ) {
            System.out.println("10 == -10");
        } else if( bil1 < bil2 ){
            System.out.println("10 < -10");
        } else {
            System.out.println("lain-lain")
        }
    }
}
{% endhighlight %}

Pada dasarnya seleksi dengan IF ini kalo digambarkan ke diagram UML dengan activity diagram berdasarkan koding diatas jadi seperti berikut:

![ Statement if basic ](/resources/downloads/imgs/java-core/if-statement/if-basic.jpg)

Berikut penjelasannya:

1. Nah jadi disini kita mendefinisikan 2 variable integer yaitu ```bil1 = 10``` dan ```bil2 = -10```.
2. Seleksi pertama yaitu ```bil1 == bil2``` jadi kita ubah ke bilangan jadi ```10 == -10``` hasilnya ```false``` karena 10 tidak sama dengan -10 maka perintah dalam ```(bil1 == bil2)``` dilewat atau tidak dijalankan.
3. Seleksi ke dua yaitu ```bil1 < bil2``` jadi kita ubah ke bilangan jadi ```10 < -10``` hasilnya ```false``` karena 10 lebih besar dari -10 maka peritah dalam ```(bil1 < bil2)``` dilewat atau tidak dijakankan.
4. ```else``` adalah pilihan terakhir artinya jika kedua seleksi gagal atau bernilai salah maka otomatis perintah dalam else akan dijalankan dengan begitu kesimpulannya adalah ```lain-lain```

Nah sekarang kita akan coba studi kasus yang lain, berikut codingannya:

{% highlight java linenos %}
package com.maryanto.dimas.tdi.training.java.core;

public class DeepIfTwoValidCondition{
    
    public void static void main(String[] args){
        int bil = 10;
        if (bil == 10) {
            System.out.println("yang ini diksekusi (==)");
        } else if(bil % 2 = 0){
            System.out.println("yang ini diksekusi (%)");
        } else{
            System.out.println("Lain-lain");
        }
    }
}
{% endhighlight %}

Sekarang coba tebak apa ouput yang dihasilkan dari statement diatas?

Ok, nah jadi jawabanya seperti berikut supaya lebih gampang kita buat dulu activity diagramnya dulu seperti berikut:

![If statement with two valid condition](/resources/downloads/imgs/java-core/if-statement/if-aneh.jpg)

Berikut penjelasannya:

1. ```bil = 10``` kemudian diseksi ```10 == 10``` maka hasilnya benar. ok kita udah tau ya jawabanya yang ini. tpi angap ja gak tau.
2. ```bil = 10``` kemudian diseleksi ```10 % 2 = 0``` jadi 10 dibagi 2 sama dengan 5 sisanya khan 0 maka hasilnya benar tpi perintah didalamnya tidak akan diksekusi karena buat apa khan statement pertama udah benar dan sebenarnya statement ke 2 ini tidak dieksekusi lagi karena statement ke 1 udah bener jadi hasilnya adalah ```yang ini dieksekusi (==)```