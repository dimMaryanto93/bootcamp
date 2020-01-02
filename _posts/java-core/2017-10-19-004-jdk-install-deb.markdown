---
layout: post
title: "Install Oracle JDK 8 di Linux Debian Based (UBuntu 16.04 dan 17.04)"
date: 2017-10-19T01:32:10+07:00
lang: java-core
categories:
- java
- core
refs: []
youtube: https://www.youtube.com/watch?v=DtucedMOSts&list=PLV1-tdmPblvz0NCFYgVQaQEOTWJCjjucO&index=5
comments: true
---

Setelah install di Windows 10, sekarang saya mau install di Sistem Operation Linux Debian based dengan distro `Ubuntu 16.04` . Kalo di ubuntu sih sebenernya gampang kita bisa install via ppa dengan menambahkan ```ppa:webupd8team/java``` berikut perintahnya


```sh
sudo add-apt-repository ppa:webupd8team/java
```

Setelah itu kita update systemnya

```sh
sudo apt-get update && sudo apt-get install oracle-java8-installer
```

Setelah itu kita update konfigurasi runtime environmentnya menggunakan perintah berikut ini:


```sh
sudo update-alternatives --config java
```

maka akan menampilkan output seperti berikut:

```sh
# root@Aspire-E5-473G:~# update-alternatives --config java
There are 2 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                            Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-8-oracle/jre/bin/java          1083      auto mode
  1            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      manual mode
  2            /usr/lib/jvm/java-8-oracle/jre/bin/java          1083      manual mode

Press <enter> to keep the current choice[*], or type selection number:
```

Nah dari output diatas kita pilih yang **java-8-oracle** jadi kita input ```0``` sebagai default runtime environmentnya. kemudian kita cek deh dengan terminal:


```sh
java -version && javac -version
```

berikut adalah outputnya:

```sh
dimmaryanto@Aspire-E5-473G:~$ java -version && javac -version
java version "1.8.0_101"
Java(TM) SE Runtime Environment (build 1.8.0_101-b13)
Java HotSpot(TM) 64-Bit Server VM (build 25.101-b13, mixed mode)
javac 1.8.0_101
```