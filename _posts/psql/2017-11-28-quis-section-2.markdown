---
layout: post
title: "Time is your practice part 2"
date: 2017-11-28T09:40:59+07:00
lang: psql
categories:
- RDBMS
- PostgreSQL
gist: 
youtube: 
comments: true
---

1. buatlah _query_ untuk menampilkan data sebagai berikut:
![Hasil soal no 1](/resources/downloads/imgs/psql/quis-2/soal1.png)
Dengan ketentuan:
    1. `Nama Lengkap`: pengabungan antara `first_name` dan `last_name` dari tabel `employees`
    2. `Nama Department`: diambil dari table `departements`
    3. `Gaji sebulan`: diabil dari colomn `salary` dalam table `employees` yang diformat dipisahkan dengan `,` (koma)
    4. `Mendapatkan Komisi`: Jika column `commission_pct` bernilai `null` tampilkan `Tidak punya komisi` tetapi jika memiliki komisi maka tampilkan berapa komisi yang karyawan tersebut dapatkan berdaksarkan `salary`.
    5. `gaji_terima`: Gaji yang harus diterima oleh karyawan tersebut setelah ditambakan dengan komisi.
2. Buatlah query untuk menampilkan data, karyawan berserta nama managernya tetapi jika tidak punya manager tampilkan 'Saya Tidak punya manager' seperti berikut contohnya:
![Hasil soal no 2](/resources/downloads/imgs/psql/quis-2/soal2.png)
Ketentuannya:
    1. `nama_karyawan`: gabungkan ke dua kolom `last_name` dan `fist_name`
    2. `Nama Bagian`: diambil dari kolom `depertment_name` di tabel `departments`
    3. `manager_name`: diambil dari kolom `first_name` dan `last_name` berdasarkan `manager_id` di tabel `employees`, jika tidak punya manager tampilkan 'Saya tidak punya manager'
    4. `Nama Jabatan`: dimabil dari kolom `job_title` di tabel `jobs`
    5. Diurutkan `manager_name` dan `nama_karyawan`
3. Buatlah query, untuk menampilkan data total gaji seluruh karyawan dari setiap department kemudian urutkan berdasarkan gaji terbesar ke terkecil seperti berikut:
![Hasil soal no 3](/resources/downloads/imgs/psql/quis-2/soal3.png)
4. Buatlah query untuk menampilkan data, jumlah karyawan yang dikategorikan berdasarkan gaji setahun kemudian diurutkan berdasarkan kategori gaji tersebut dari terbesar hingga terkecil tetapi hanya yang memiliki komisi saja seperti berikut:
![Hasil no 4](/resources/downloads/imgs/psql/quis-2/soal4.png)
5. Buatlah sebuah query untuk menampilkan semua data karyawan yang memiliki gaji lebih besar sama dengan nilai maximum setiap karyawan yang bekerja di department `IT_PROG` contohnya seperti berikut:
![hasil no 5](/resources/downloads/imgs/psql/quis-2/soal5.png)