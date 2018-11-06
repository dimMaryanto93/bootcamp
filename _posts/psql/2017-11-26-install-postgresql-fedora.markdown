---
layout: post
title: "How install PostgreSQL & PgAdmin3 in Fedora 25"
date: 2017-11-26T19:55:50+07:00
lang: psql
categories:
- RDBMS
- PostgreSQL
gist: 
youtube: 
comments: true
---

_operation system_ yang berkaitan dengan Linux atau UNIX pasti tidak akan lepas dari yang namanya command line (terminal) so buka terminalnya kemudian masukan script berikut:

{% highlight bash %}
sudo dnf install postgresql-server postgresql-contrib pgadmin3 -y
{% endhighlight %}

Setelah semuanya di install tahap selajutnya adalah melakukan inisialisasi config untuk data. masukan command berikut berikut ini:

{% highlight bash %}
sudo postgresql-setup initdb
{% endhighlight %}

![Init DB]({{ site.baseurl }}/resources/downloads/imgs/psql/install-fedora/postgresql-setup-initdb.png)

Jika berhasil maka hasilnya seperti berikut:

![Successed init db]({{ site.baseurl }}/resources/downloads/imgs/psql/install-fedora/postgresql-initdb-post.png)

Tetapi jika menemukan error seperti berikut:

![Error init DB]({{ site.baseurl }}/resources/downloads/imgs/psql/install-fedora/postgresql-initdb-error.png)

Solusinya adalah hapus folder `pgsql/data`

{% highlight bash %}
sudo rm -rf /var/lib/pgsql/
{% endhighlight %}

Setelah itu **lakukan initdb lagi**, klo berhasil masuk ke step selanjutnya untuk saat ini berarti anda sudah menginstall Database di System anda, apakah udah selesai? tentu belum, kita harus **setting untuk menjalankan servicenya** tpi ini optional sih apakah mau dijalankan secara otomatis atau dijalankan secara manual oleh kita? klo mau otomatis berikut adalah perintahnya:

{% highlight bash %}
sudo systemctl enable postgresql.service && sudo systemctl start postgresql.service
{% endhighlight %}

Nah setelah itu coba cek statunya dengan perintah berikut:

{% highlight bash %}
sudo systemctl status postgresql.service
# this is output
postgresql.service - PostgreSQL database server
   Loaded: loaded (/usr/lib/systemd/system/postgresql.service; disabled; vendor preset: disabled)
   Active: active (running) since Mon 2016-04-18 08:16:38 WIB; 7h ago
  Process: 5930 ExecStart=/usr/libexec/postgresql-ctl start -D ${PGDATA} -s -w -t ${PGSTARTTIMEOUT} (code=exited, status=0/SUCCESS)
  Process: 5926 ExecStartPre=/usr/libexec/postgresql-check-db-dir %N (code=exited, status=0/SUCCESS)
 Main PID: 5934 (postgres)
   CGroup: /system.slice/postgresql.service
           ├─5934 /usr/bin/postgres -D /var/lib/pgsql/data
           ├─5935 postgres: logger process   
           ├─5937 postgres: checkpointer process   
           ├─5938 postgres: writer process   
           ├─5939 postgres: wal writer process   
           ├─5940 postgres: autovacuum launcher process   
           └─5941 postgres: stats collector process   

Apr 18 08:16:37 localhost.localdomain systemd[1]: Starting PostgreSQL databas...
Apr 18 08:16:37 localhost.localdomain postgresql-ctl[5930]: LOG:  redirecting...
Apr 18 08:16:37 localhost.localdomain postgresql-ctl[5930]: HINT:  Future log...
Apr 18 08:16:38 localhost.localdomain systemd[1]: Started PostgreSQL database...
Hint: Some lines were ellipsized, use -l to show in full.
{% endhighlight %}

Tahap selanjutnya jika servicenya udah jalan seperti output diatas kita harus update configurasi file berikut dengan cara update file `/var/lib/pgsql/data/pg_hba.conf` untuk lebih mudah bisa gunakan text editor default fedora yaitu `gedit`

{% highlight bash %}
sudo gedit /var/lib/pgsql/data/pg_hba.conf
{% endhighlight %}

Setelah file tersebut terbuka di gedit maka ubahlah method menjadi `md5` seperti berikut:

```properties
# TYPE  DATABASE        USER            ADDRESS                 METHOD

# "local" is for Unix domain socket connections only
local   all             all                                     md5
# IPv4 local connections:
host    all             all             127.0.0.1/32            md5
# IPv6 local connections:
host    all             all             ::1/128                 ident
```

Kemudian restart servicenya, dengan perintah berikut:

{% highlight bash %}
sudo systemctl restart postgresql.service
{% endhighlight %}

Setelah itu coba login dengan user postgres dan db postgres (masih dalam root / superuser):

{% highlight bash %}
psql -h localhost -U postgres postgres
{% endhighlight %}

Jika berhasil login maka tampilnya seperti berikut:

```postgresql
psql (9.4.7)
Type "help" for help.

postgres=#
```

Setelah itu ubah password defaultnya menjadi (bebas terserah anda) klo saya menggunakan admin menggunakan perintah berikut:

{% highlight psql %}
postgres=# \password

Enter new password: # admin
Enter it again: # admin
{% endhighlight %}