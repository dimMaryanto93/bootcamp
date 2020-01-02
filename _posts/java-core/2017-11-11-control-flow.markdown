---
layout: post
title: "Flow control in Java"
date: 2017-11-11T20:29:17+07:00
lang: java-core
categories:
- Java
- Core
refs: []
youtube: 
comments: true
---

Setelah mengelesaikan [latihan pertama]({% post_url java-core/2017-11-10-quis-section-1 %}), materi selajutnya adalah tentang flow atau alur control. Flow Control ini pada dasarnya ada 2 macem yaitu

1. Decision making (Percabangan) statement
2. Looping (Perulangan) statement

Dengan flow control kita bisa ngatur aplikasi yang kita develop atau buat melakukan sesuatu dengan ketentuan tertentu dan melakukannya beberapa kali tanpa menulis ulang perintahnya.

## Decision making

Di bahasa pemograman java percabangan atau selection ada 2 method yaitu dengan `if` statement dan `switch` statement. Masing-masing punya kelebihan-kekurangan dan kegunaannya masing-masing tapi pada dasarnya sama yaitu tujuannya melakukan making decision.

Berikut adalah Sample penggunaan percabangan

### `IF` statement

If statement, biasanya ada 2 statement yaitu `control` dan `statement`. Dimana `control` merupakan atau berisi logika atau nilai pembanding sedangkan `statement` merupakan blok yang akan di eksekusi jika `control` terpenuhi atau bernilai `true` contohnya seperti berikut:

{% highlight java linenos %}
public class FlowIfStatement {

    public static void main(String[] args){
        Integer bil1 = 10;
        if(bil1 == 10){
            System.out.println("Bilangan Sama");
        }
    }
}
{% endhighlight %}

### `SWITCH` statement

Switch statement serupa dengan if, hanya berbeda dengan sintaxnya contohnya seperti berikut:

{% highlight java linenos %}
public class FlowSwitchStatement {
    
    public static void main(String[] args){
        Integer value = 20;
        switch(value){
            case 10 : 
                System.out.println("Nilai sama dengan 10");
                break;
            case 20 :
                System.out.println("Nilai sama dengan 20");
                break;
            default : System.out.println("Nilai tidak ada yang sama!");
        }
    }
}
{% endhighlight %}

## Looping

selain percabangan, perulangan juga tidak kalah penting. Karena setiap program pasti tidak akan lepas dari selection dan looping. Perlulangan atau loop di java initnya ada 3 meskipun saat ini (2017 in JDK 8) dikatakan ada 4 macem yaitu `for`, `do-while`, `while` dan `foreach`. 

Untuk loop statement initnya ada 3 hal yang perlu di ingat yaitu `index`, `control` dan `iterator`. `index` ini pada initinya kita sedang ada di iterasi ke berapa dalam suatu perlulangan, untuk `control` ini yang mengatur bagaimana perlulangan terjadi dan `iterator` sebagai nilai increment (`i++`) atau deincrement (`i--`). Ok kita bahas ya satu-persatu mulai dari `for`

### `FOR` statement

Perulangan yang satu ini, paling banyak ditemukan dibandingkan dengan perlulangan yang lainnya karena dari secara sintax paling sederhana dan paling mudah dibaca. Format umum dari for sebagai berikut 

{% highlight java linenos %}
public class FlowForStatement {

    for(int i = 1; i < 11; i++){
        System.out.println("Saya berulang sebangak " + i);
    }
}
{% endhighlight %}

### `WHILE` statement

Selain perluangan `for` ada juga menggunakan `while`, Perlulangan while ini biasaya digunakan untuk kasus yang lebih sepesifik contohnya tidak memiliki kepastian akan `index` atau biasanya digunakan untuk me-loop suatu event yang tertentu misalnya data yang diambil dari database, file ataupun dari hal lainnya. Contoh penggunaannya seperti berikut:

{% highlight java linenos %}
public class FlowWhileStatement {

    public static void main(String[] args){
        Integer i = 0;
        while(i < 10){
            System.out.println("Saya berulang sebangak " + i);
            i++;
        }
    }
}
{% endhighlight %}

### `DO-WHILE` statement

Perulangan tipe ini serupa dengan `while` tetapi bedanya adalah klo `while` itu kodisinya di cek dulu sebelum di lakukan, nah sedangkan dengan `do-while` di kerjakan dulu baru di cek kondisinya. Berikut contoh penggunaanya:

{% highlight java linenos %}
public class FlowDoWhileStatement {

    public static void main(String[] args){
        Integer i = 0;
        do {
            System.out.println("Saya berulang sebangak " + i);
            i++;
        } while( i < 10 );
    }
}
{% endhighlight %}