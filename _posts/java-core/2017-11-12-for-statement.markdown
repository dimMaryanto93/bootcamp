---
layout: post
title: "Looping menggunakan For statement"
date: 2017-11-12T12:04:57+07:00
lang: java-core
categories:
- Java
- Core
refs: []
youtube: 
comments: true
---

Mungkin temen-temen dulu pernah mengalami kejadian dihukum sama guru atau dosen kita harus menulis di papan tulis atau di kertas selembar

> "Saya minta maaf, saya akan lebih rajin dalam bejar dan tidak akan bolos lagi"

Sebanyak 100x seperti ini:

![Meme anak SD di hukum]({{ site.baseurl }}/resources/posts/java-for-statement/meme-anak-sd.jpg)

Nah jadi sama halnya di bahasa pemograman jika saya terjemahkan ke bahasa Java jadi seperti ini ya:

{% highlight java linenos %}
public class HukumanBuatAnakSD {

    public static void main(String[] args){
        System.out.println("Saya minta maaf, saya akan lebih rajin dalam bejar dan tidak akan bolos lagi");
        System.out.println("Saya minta maaf, saya akan lebih rajin dalam bejar dan tidak akan bolos lagi");
        System.out.println("Saya minta maaf, saya akan lebih rajin dalam bejar dan tidak akan bolos lagi");
        System.out.println("Saya minta maaf, saya akan lebih rajin dalam bejar dan tidak akan bolos lagi");
        System.out.println("Saya minta maaf, saya akan lebih rajin dalam bejar dan tidak akan bolos lagi");
        System.out.println("Saya minta maaf, saya akan lebih rajin dalam bejar dan tidak akan bolos lagi");
        /* terusin ya cape ah copy-paste mulu */
    }
}
{% endhighlight %}

If you'r programmer, use the loop statement. like this

{% highlight java linenos %}
public class HukumanBuatPrgrammer {
    public static void main(String[] args){
        Integer times = 100;
        for(int i = 0; i < times ; i++)
            System.out.println("Saya minta maaf, saya akan lebih rajin dalam bejar dan tidak akan bolos lagi");
    }
}
{% endhighlight %}

Gimana keren khan ya!... because i'm a lazy person wkwkwkwkk. 

## What happened inside for loop?

![For loop basic annimate]({{ site.baseurl }}/resources/posts/java-for-statement/for-loop-basic.gif)

Nah dari ilustrasi di atas, jadi penjelasanya lebih detailnya seperti berikut:

1. Tahap pertama, di baris `4` saya membuat variable `times` yang di beri nilai `100` artinya saya mau membuat perulangan sebanyak 100x
2. Tahah ke dua sya membuat variable dengan `i` yang di beri nilai `0` dalam `for(int i = 0; ... ; ... )`, setelah itu saya memberikan kondisi jika nilai `i` lebih kecil dari nilai yang diberikan oleh variable `times` atau sama dengan `100` maka lakukan perluangan. kemudian variable `i` di increment `i = i + 1`.
3. Nah itu tadi struktur dari perulanganya, sekarang kita liat analoginya berdasarkan annimasi di atas.
    1. Iterasi pertama: coba anda perhatikan nilai variable dari `i` untuk saat ini nilai `i = 0`, kemudian di cek sama control apakah `0 < 100` jawabanya yes benar ya jadi dia menjalankan perintah System.out.println("Saya ...");
    2. Iterasi ke 2: baliklagi ke atas, liat kembali variable `i` sekarang variable `i = 1` karena di increment `i = 0 + 1` nilai `0` diabila dari iterasi sebelumya yaitu `0` jadi sekarang `i = 1` ya. Kemudian cek kembali kondisi apakah `1 < 100` jawabanya benar ya jadi masuk ke statement berikutnya yaitu menjalankan perintah System.out.println("Saya ...");
    3. Skip... , Iterasi ke 100 : liat kembali variable `i` sekarang variable `i = 99` jadi kondisinya sekarang `99 < 100` jawabanya benar ya jadi masuk ke statement berikutnya yaitu menampilkan ke console "Saya ..."
    4. Iterasi ke 101 : variable `i` sekarang `i = 100` jadi kondisinya sekarang `100 < 100` jawabanya **salah** nah karena salah perulangan berhenti sama sini **tidak menampilkan lagi saya...**


