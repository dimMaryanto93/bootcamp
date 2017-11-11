---
layout: post
title: "Install Java Development Kit di Windows 10"
date: 2017-10-19T00:04:45+07:00
lang: java-core
categories:
- java
- core
gist: 
youtube: https://youtu.be/2zoPD2xRuIg
comments: true
---

Sekarang kita akan menginstall JDK atau Java Development Kit versi Oracle, nah sebenarnya JDK itu tidak hanya punya Oracle tapi ada komunitas juga ya yang megembangin JDK juga yaitu OpenJDK yang dulunya di buat oleh IBM sekarang lisencenya dikasihin ke Eclipse Fundation, nah sekarang (Oktober 2017) kebetulan `Oracle JDK 9` udah releash ya. tapi di artikel ini masih pake `JDK 8u101` ini tidak masalah ya. karena dalam materi ini kita masih mempelajari fundamental artinya core dari Java belum sampai fitur seperti `Lamda Expresion`, `Stream API`, `Modules` dan lain-lain. Nantinya akan saya buat kan materinya secara terpisah.

Ok nah sekarang kita mulai install JDK di Sistem Operation Windows 7, 8, 10 tpi diartikel ini menggunakan sistem Operation Windows 10 untuk pengguna Windows 7 dan Windows 8 caranya kurang lebih sama hanya mungkin berbeda tampilan saja.

## Download Oracle JDK

Download dulu JDKnya di [Website Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html)

![Situs Oracle](/resources/downloads/imgs/java-core/jdk-win10/download-jdk-1.png)

Disana ada 2 pilihan `Java Platform (JDK) 8u101/8u102` dan `Netbeans with JDK 8` nah jadi pilih aja yang `Java Platform (JDK) 8u101/8u102`. tapi kalo anda sudah melakukan install JDK di Operasion System anda tidak perlu download cukup update aja JDK.a dari Control Panel atau Java Updater. Setelah ikut maka akan tampil Form seperti berikut:

![Pilih JDK version dan platform](/resources/downloads/imgs/java-core/jdk-win10/download-jdk-2.png "Pilih Platform sesuia OS dan Download JDK")

Kemudian pilih sesuia dengan Platform System Operasi dan arsitekturnya, karena saya pake Windows 10 yang 64bit jadi saya pilih yang **Windows x64**

## Install Oracle JDK

Setelah selesai di Download langsung aja jalankan **jdk-8u101-windows-x64.exe** maka akan muncul form seperti berikut:

![Form Instalasi JDK](/resources/downloads/imgs/java-core/jdk-win10/install-jdk-1.png)

Klik `Next` untuk menanjutkan, kemudian akan tampil form untuk menentukan lokasi JDK disimpan berikutnya:

![Form Installasi JDK 2 ](/resources/downloads/imgs/java-core/jdk-win10/install-jdk-2.png)

Lokasi JDKnya saya mau biarkan `default` saja, kemudian klik `Next` untuk selanjutnya melakukan instalasi JRE seperti berikut:

![Form Installas JRE](/resources/downloads/imgs/java-core/jdk-win10/install-jdk-3.png)

Sama dengan JDK lokasi JREnya saya mau biarkan `default` aja, Setelah itu klik `Next` lagi dan selesai deh proses extractnya.

![Form Installasi JRE](/resources/downloads/imgs/java-core/jdk-win10/install-jdk-4.png)

Nah setelah itu klick `Close`, installasi Oracle JDK udah selesai. tahap selanjutnya dalah setup PATH environtmentnya.

## Setup System Environtment

Buka `File Explorer` nya kemudian Klik Kanan pada `This PC` setelah itu pilih `Properties`

![Setting Path Command Prompt](/resources/downloads/imgs/java-core/jdk-win10/setpath-jdk-1.png)

Terus klik `Advanced system settings` maka akan tampil Form seperti Berikut:

![System properties](/resources/downloads/imgs/java-core/jdk-win10/setpath-jdk-2.png)

Kemudian klik `Environtment Variables...` maka akan tampil form seperti berikut:

![Setting system variable dan variable name](/resources/downloads/imgs/java-core/jdk-win10/setpath-jdk-3.png)

Di menu `User variables for dimMaryanto` klik button `New` maka akan tampil form seperti berikut:

![Setting JAVA_HOME](/resources/downloads/imgs/java-core/jdk-win10/setpath-jdk-4.png)

Kemudian isi `Variable name:` dengan `JAVA_HOME` *huruf besar semua dan untuk `Variable value:` anda arahkan ke lokasi hasil installasi `JDK` klo saya lokasinya di sini ```C:\Program Files\Java\jdk1.8.0_91``` setelah ikut Klik **OK**, maka hasilnya seperti berikut:

![Setting JAVA HOME hasil](/resources/downloads/imgs/java-core/jdk-win10/setpath-jdk-5.png)

Kemudian kita pindah ke `System variables`, anda cari `variable name:` dengan nama `PATH` atau `Path`

![Setting PATH JAVA](/resources/downloads/imgs/java-core/jdk-win10/setpath-jdk-6.png)

kemudian anda klik button `Edit` maka akan tampil form seperti berikut:

![Setting Path Java 2](/resources/downloads/imgs/java-core/jdk-win10/setpath-jdk-7.png)

Klik button **New** kemudian arahkan ke lokasi yang installasi folder ```bin``` di hasil installasi JDK jadi klo di saya seperti ini ```C:\Program files\Java\jdk-8u101\bin``` hasilnya seperti berikut:

![Setting PATH Java](/resources/downloads/imgs/java-core/jdk-win10/setpath-jdk-8.png)

Setelah itu klik `OK` semua dialog yang ada sampe keluar dari `system properties`. setelah sampe sini proses instalasi di windows udah beres. saatnya tinggal kita cek aja configurasi.a dengan menggunakan `Command Prompt`

Buka Command Prompt dengan menggunakan kombinasi key ```WIN + R``` maka akan tampil form seperti berkut:

![Running CMD](/resources/downloads/imgs/java-core/jdk-win10/run-cmd-1.png)

Kemudian ketik ```cmd``` setelah itu ```Enter``` maka akan tampil Command Prompt seperti berikut:

![Command Prompt](/resources/downloads/imgs/java-core/jdk-win10/run-cmd-2.png)

kemudian coba cek configurasi java.a dengan cara melihat versi yang telah terinstall di OS menggunakan perintah seperti berikut

```bash
C:\Users\softw>java -version && java -version
java version "1.8.0_91"
Java(TM) SE Runtime Environment (build 1.8.0_91-b15)
Java HotSpot(TM) 64-Bit Server VM (build 25.91-b15, mixed mode)
java version "1.8.0_91"
Java(TM) SE Runtime Environment (build 1.8.0_91-b15)
Java HotSpot(TM) 64-Bit Server VM (build 25.91-b15, mixed mode)

C:\Users\softw>
```

Nah untuk setting di Windows udah selesai.

