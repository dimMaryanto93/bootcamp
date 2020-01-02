---
layout: post
title: "Element Collection"
date: 2017-11-22T19:09:52+07:00
lang: java-core
categories:
- Java
- Core
refs: []
youtube: 
comments: true
---

Di materi sebelumnya kita udah membuat _array_, nah kita tau kalo _array_ itu untuk menyimpan data yang lebih dari satu dalam sebuah _variable_, Tetapi dengan menggunakan _array_ tersebut memiliki kekurangan yaitu agak susah untuk menambahkan dan menghapus suatu _element_ dalam array tersebut

Contohnya saya mendefinisikan sebuah _array_ dengan jumlah memory `10` ketika saya menambahkan element ke `11` contohnya itu tidak bisa secara langsung kita definisikan tetapi harus membuat array baru dengan jumlah memori yang baru juga seperti berikut

{% highlight java linenos %}
package tdi.training.java.core.array;

public class ArrayAddValue {

    public static void main(String[] args){
        Integer[] values = new Integer[10];
        values[0] = 1;
        values[2] = 10;
        values = add(values ,50);
        System.out.println("Nilai values jumlanya sekarang ada "+ values.length);
        values = add(values, 51);
        System.out.println("Nilai values jumlanya sekarang ada "+ values.length);	
    }

    public static Integer[] add(Integer[] oldList, Integer newValue){
        Integer[] newList = new Integer[oldList.length + 1];
        for(int i = 0; i < oldList.length; i++)
            newList[i] = oldList[i];
        newList[oldList.length] = newValue;
        return newList;
    }
}
{% endhighlight %}

Kalau kita liat agak ribet ya, kita harus semuanya satu-persatu. Nah kalo jaman sekarang ada _framework element collection_ yang di sediakan oleh Java yaitu dalam package `java.util.*` diantaranya 

1. List
    1. LinkedList
    2. ArrayList
2. Map
    1. HashMap
    2. TreeSet
    3. LinkedHashMap
3. Set
    1. HashSet
    2. TreeSet
    3. LinkedHashSet

Baca lebih lanjut [di sini](https://docs.oracle.com/javase/7/docs/technotes/guides/collections/overview.html)

## `java.util.List`

Untuk `java.util.List` adalah bentuk umum dari _array_ contohnya seperti berikut

{% highlight java linenos %}
package tdi.training.java.core.data;

import java.util.List;
import java.util.ArrayList;

public class MahasiswaList {

    public static void main(String[] args){
        List<String> daftarMahasiswa = new ArrayList<>();
        daftarMahasiswa.add("Dimas Maryanto");
        daftarMahasiswa.add("Hadi Siswanto");

        System.out.println(
            "Index ke 1 dari daftar mahasiswa adalah " + 
            daftarMahasiswa.get(1) + 
            " dari jumlah data " + 
            daftarMahasiswa.size()
        );

        daftarMahasiswa.remove(0);
        System.out.println(
            "jumlah array sekarang adalah " + daftarMahasiswa.size()
        );
    }
}
{% endhighlight %}

## `java.util.Set`

Untuk `java.util.Set` ini sama seperti `java.util.List` hanya dia valuenya _unique_ atau hanya menerima yang nilanya berbeda dengan element yang telah terdaftar di _list_ tersebut. Contohnya seperti berikut:

{% highlight java linenos %}
package tdi.training.java.core.data;

import java.util.Set;
import java.util.HashSet;

public class MahasiswaSet{

    public static void main(String[] args){
        Set<String> daftarMahasiswa = new HashSet<>();
        daftarMahasiswa.add("Dimas Maryanto");
        daftarMahasiswa.add("Hadi Siswanto");
        daftarMahasiswa.add("Hadi Siswanto");

        System.out.println(
            "Index ke 1 dari daftar mahasiswa adalah " + 
            daftarMahasiswa.get(1) + 
            " dari jumlah data " + 
            daftarMahasiswa.size()
        );

        daftarMahasiswa.remove(0);
        System.out.println(
            "jumlah array sekarang adalah " + daftarMahasiswa.size()
        );
    }
}
{% endhighlight %}

Untuk lebih jelasnya bisa baca [disini](https://docs.oracle.com/javase/7/docs/api/java/util/HashSet.html)

## `java.util.Map`

Untuk element ini berbeda dengan kedua element diatas yaitu `List` dan `Set`, perbedaanya terletak di jika di `Set` atau `List` hanya menggunakan _index_ di `Map` menggunakan `key` dan `value` jadi contohnya seperti berikut:

{% highlight java linenos %}
package tdi.training.java.core.data;

import java.util.Map;
import java.util.HashMap;

public class MahasiswaSet {

    public static void main(String[] args){
        Map<Integer, String> daftarMahasiswa = new HashMap<>();
        daftarMahasiswa.put(1 , "Dimas Maryanto");
        daftarMahasiswa.put(2 , "Hadi Siswanto");
        daftarMahasiswa.put(3 , "Hadi Siswanto");

        System.out.println(
            "Key ke 1 dari daftar mahasiswa adalah " + 
            daftarMahasiswa.get(1) + 
            " dari jumlah data " + 
            daftarMahasiswa.size()
        );

        daftarMahasiswa.remove(2);
        System.out.println(
            "jumlah array sekarang adalah " + daftarMahasiswa.size()
        );
    }
}
{% endhighlight %}

Untuk lebih lengkapnya bisa baca [di sini](https://docs.oracle.com/javase/7/docs/api/java/util/HashMap.html)