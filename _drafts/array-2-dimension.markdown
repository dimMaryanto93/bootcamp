---
layout: post
title: "Array 2 dimensi"
lang: java-core
categories:
- Java
- Core
gist: 
youtube: 
comments: true
---

Sebelumya kita udah mengenal array single dimentions, sekarang kita akan buat array dengan multidimention atau orang-orang sering menggunakan istilah kordinal `xy` jika 2 dimention dan untuk tiga dimention `xyz` conthnya seperti berikut:

{% highlight java linenos %}
public class Array2Dimension {
	
	public static void main(String[] args){
		Integer[][] values = { {1,2,3}, {2,3,5}, {3,4,5} };

        // menampilkan data pada index ke 0 dan 2
        System.out.println(values[0][2]);

        // menampilkan isi yang ada di array 2 dimention
		for(int i = 0; i < 3; i++){
			for(int j = 0; j < 3; j++){
				System.out.print(values[i][j]);
			}
			System.out.println();		
		}
	}
}
{% endhighlight %}

Contoh lainnya 

{% highlight java linenos %}
public class Array2Dimension {
	
	public static void main(String[] args){
		Integer[][] values = new Integer[5][2];

        values[0][0] = 1;
        values[0][1] = 2;
        values[1][0] = 3;
        values[1][1] = 4;
        values[2][0] = 5;
        values[2][1] = 6;
        

        // menampilkan data pada index ke 0 dan 1
        System.out.println(values[0][1]);

        // menampilkan isi yang ada di array 2 dimention
		for(int i = 0; i < 5; i++){
			for(int j = 0; j < 2; j++){
				System.out.print(values[i][j]);
			}
			System.out.println();		
		}
	}
}
{% endhighlight %}