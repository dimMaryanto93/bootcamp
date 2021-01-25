---
layout: post
title: "Relational Comparison Predicate dengan HQL"
date: 2021-01-25T13:29:57+07:00
lang: orm-hibernate
categories:
- Java
- ORM
- Hibernate
- PostgreSQL
refs: 
- https://docs.jboss.org/hibernate/orm/5.4/userguide/html_single/Hibernate_User_Guide.html#hql-relational-comparisons
youtube: 
comments: true
image_path: /resources/posts/orm-hibernate-030a
gist: dimMaryanto93/e8d2abb5361e811860d6a462270f119b
---

Hai, di materi kali ini saya mau membahas tentang Relational Comparison Predicate dengan menggunakan HQL, berikut adalah operator 

| Symbol                        | Keterangan    |
| :---                          | :---          |
| `=`                           | Melakukan perbandingan dengan nilai yang **bernilai sama** |
| `!=`                          | Melakukan perbandingan dengan nilai yang **bernilai tidak sama** |
| `<>`                          | Melakukan perbandingan dengan nilai yang **bernilai tidak sama** |
| `>`                           | Melakukan perbandingan terhadap 2 variable apakah variable yang satu **lebih besar** dari variable lainnya |
| `>=`                          | Melakukan perbandingna terhadap 2 variable apakah variable yang satu **lebih besar atau sama dengan** variable lainnya |
| `<`                           | Kebalikan dari symbol `>` yaitu **lebih kecil** |
| `<=`                          | Kebalikan dari symbol `>=` yaitu **lebih kecil atau sama dengan** |
{: .striped .highlight }

Berdasarkan operator tersebut, kita coba masing-masing ya menggunakan berbagai tipe data 

1. String
2. Number
3. Date and Time
4. Boolean
5. Enum

## String Operator

Untuk tipe data String, kita bisa menggunakan operator seperti `=`, `<>` dan `!=` contohnya seperti berikut implementasi DAO:

{% gist page.gist "HQLRelationalComparisonStringDao.java" %}

Kemudian berikut adalah implementasi Unit Testing untuk tipe data String:

{% gist page.gist "TestHQLRelationalComparisonString.java" %}

Dan sebelum kita test methodnya berikut adalah contoh sample datanhya:

![select-table-string]({{ page.image_path | prepend: site.baseurl }}/select-table-string.png)

Sekarang coba jalankan unit testing, pada method `testStringComparison()`, maka hasilnya seperti berikut:

```bash
Jan 25, 2021 1:08:49 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        kelasentit0_.id as id1_25_,
        kelasentit0_.tahun_angkatan as tahun_an2_25_,
        kelasentit0_.nama_kelas as nama_kel3_25_,
        kelasentit0_.program_studi as program_4_25_ 
    from
        mapping.kelas kelasentit0_ 
    where
        kelasentit0_.nama_kelas=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLRelationalComparisonString - data: [KelasEntity(id=3, nama=IF-01, angkatan=2011, programStudi=IF), KelasEntity(id=5, nama=IF-01, angkatan=2012, programStudi=IF), KelasEntity(id=6, nama=IF-01, angkatan=2013, programStudi=IF)]
Hibernate: 
    select
        kelasentit0_.id as id1_25_,
        kelasentit0_.tahun_angkatan as tahun_an2_25_,
        kelasentit0_.nama_kelas as nama_kel3_25_,
        kelasentit0_.program_studi as program_4_25_ 
    from
        mapping.kelas kelasentit0_ 
    where
        kelasentit0_.nama_kelas=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLRelationalComparisonString - data: []
```

## Number

Untuk tipe data number, kita bisa menggunakan operator dengan sebagai berikut implementasi DAO:

{% gist page.gist "HQLRelationalComparisonNumberDao.java" %}

Berikut adalah implementasi Unit Testing:

{% gist page.gist "TestHQLRelationalComparisonNumber.java" %}

Untuk datanya masih sama dengan tipe data string yaitu:

![select-table-string]({{ page.image_path | prepend: site.baseurl }}/select-table-string.png)

Sekarang coba jalankan unit testing dengan method `testEqualNumberComparison()`, maka hasilnya seperti berikut:

```bash
Jan 25, 2021 1:12:38 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        kelasentit0_.id as id1_25_,
        kelasentit0_.tahun_angkatan as tahun_an2_25_,
        kelasentit0_.nama_kelas as nama_kel3_25_,
        kelasentit0_.program_studi as program_4_25_ 
    from
        mapping.kelas kelasentit0_ 
    where
        kelasentit0_.tahun_angkatan=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLRelationalComparisonNumber - data: [KelasEntity(id=2, nama=SI-02, angkatan=2011, programStudi=IF), KelasEntity(id=4, nama=IF-02, angkatan=2011, programStudi=IF), KelasEntity(id=3, nama=IF-01, angkatan=2011, programStudi=IF), KelasEntity(id=1, nama=SI-01, angkatan=2011, programStudi=IF)]
```

Selanjutnya coba jalankan untuk method `testNotEqualNumberComparison()`, maka hasilnya seperti berikut:

```bash
Jan 25, 2021 1:13:37 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        kelasentit0_.id as id1_25_,
        kelasentit0_.tahun_angkatan as tahun_an2_25_,
        kelasentit0_.nama_kelas as nama_kel3_25_,
        kelasentit0_.program_studi as program_4_25_ 
    from
        mapping.kelas kelasentit0_ 
    where
        kelasentit0_.tahun_angkatan<>?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLRelationalComparisonNumber - data: [KelasEntity(id=5, nama=IF-01, angkatan=2012, programStudi=IF), KelasEntity(id=6, nama=IF-01, angkatan=2013, programStudi=IF)]
Hibernate: 
    select
        kelasentit0_.id as id1_25_,
        kelasentit0_.tahun_angkatan as tahun_an2_25_,
        kelasentit0_.nama_kelas as nama_kel3_25_,
        kelasentit0_.program_studi as program_4_25_ 
    from
        mapping.kelas kelasentit0_ 
    where
        kelasentit0_.tahun_angkatan<>?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLRelationalComparisonNumber - data: [KelasEntity(id=5, nama=IF-01, angkatan=2012, programStudi=IF), KelasEntity(id=6, nama=IF-01, angkatan=2013, programStudi=IF)]
```

dan yang terakhir coba jalankan method `testHigherNumberComparison()`, maka hasilnya seperti berikut:

```bash
Jan 25, 2021 1:14:40 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        kelasentit0_.id as id1_25_,
        kelasentit0_.tahun_angkatan as tahun_an2_25_,
        kelasentit0_.nama_kelas as nama_kel3_25_,
        kelasentit0_.program_studi as program_4_25_ 
    from
        mapping.kelas kelasentit0_ 
    where
        kelasentit0_.tahun_angkatan>?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLRelationalComparisonNumber - data: [KelasEntity(id=5, nama=IF-01, angkatan=2012, programStudi=IF), KelasEntity(id=6, nama=IF-01, angkatan=2013, programStudi=IF)]
Hibernate: 
    select
        kelasentit0_.id as id1_25_,
        kelasentit0_.tahun_angkatan as tahun_an2_25_,
        kelasentit0_.nama_kelas as nama_kel3_25_,
        kelasentit0_.program_studi as program_4_25_ 
    from
        mapping.kelas kelasentit0_ 
    where
        kelasentit0_.tahun_angkatan>=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLRelationalComparisonNumber - data: [KelasEntity(id=2, nama=SI-02, angkatan=2011, programStudi=IF), KelasEntity(id=4, nama=IF-02, angkatan=2011, programStudi=IF), KelasEntity(id=3, nama=IF-01, angkatan=2011, programStudi=IF), KelasEntity(id=1, nama=SI-01, angkatan=2011, programStudi=IF), KelasEntity(id=5, nama=IF-01, angkatan=2012, programStudi=IF), KelasEntity(id=6, nama=IF-01, angkatan=2013, programStudi=IF)]
```

## Enumeration

Untuk tipe data enum, berikut adalah implementasi DAO:

{% gist page.gist "HQLRelationalComparisonEnumDao.java" %}

Implementasi Unit Testing: 

{% gist page.gist "TestHQLRelationalComparisonEnum.java" %}

Dan berikut adalah contoh data yang menggunakan enum:

![select-table-enum]({{ page.image_path | prepend: site.baseurl }}/select-table-enum.png)

Sekarang coba jalankan unit testing pada method `testEqualEnumeration()`, maka hasilnya seperti berikut:

```bash
Jan 25, 2021 1:18:45 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        employeeen0_.employee_id as employee1_6_,
        employeeen0_.birth_date as birth_da2_6_,
        employeeen0_.employee_name as employee3_6_,
        employeeen0_.employee_status as employee4_6_ 
    from
        enumeration.employee_ordinal employeeen0_ 
    where
        employeeen0_.employee_status=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLRelationalComparisonEnum - data: [EmployeeEnumOrdinal(id=4, name=Dimas Maryanto, birthDate=1993-03-01, status=LEAVE)]
```

## Date and Time

Untuk tipe data Date & Time, berikut adalah implementasi DAO:

{% gist page.gist "HQLRelationalComparisonDateAndTimeDao.java" %}

Implementasi Unit Testing:

{% gist page.gist "TestHQLRelationalComparisonDateAndTime.java" %}

Sebelum di jalakan berikut adalah data yang saya gunakan,

![select-table-date-time]({{ page.image_path | prepend: site.baseurl }}/select-table-date-time.png)

Kemudian coba jalankan unit testing pada method `testEqualDate()`, maka hasilnya seperti berikut:

```bash
Jan 25, 2021 1:23:09 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        mahasiswao0_.id as id1_31_,
        mahasiswao0_.alamat as alamat6_31_,
        mahasiswao0_.nama as nama2_31_,
        mahasiswao0_.nim as nim3_31_,
        mahasiswao0_.tahun_masuk as tahun_ma4_31_,
        mahasiswao0_.tanggal_lahir as tanggal_5_31_ 
    from
        mapping.mahasiswa_onetoone mahasiswao0_ 
    where
        mahasiswao0_.tanggal_lahir=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLRelationalComparisonDateAndTime - data: [MahasiswaOneToOneEntity(id=58c440a0-ccb1-4bba-8ff4-b55295f8dd86, nim=10511148, nama=Dimas Maryanto, tanggalLahir=1993-03-01, tahunMasuk=2011), MahasiswaOneToOneEntity(id=test, nim=10511150, nama=Muhamad Yusuf, tanggalLahir=1993-03-01, tahunMasuk=2011)]
```

Kemudian coba jalankan method `testNotEqualDate()`, maka hasilnya seperti berikut:

```bash
Jan 25, 2021 1:23:52 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        mahasiswao0_.id as id1_31_,
        mahasiswao0_.alamat as alamat6_31_,
        mahasiswao0_.nama as nama2_31_,
        mahasiswao0_.nim as nim3_31_,
        mahasiswao0_.tahun_masuk as tahun_ma4_31_,
        mahasiswao0_.tanggal_lahir as tanggal_5_31_ 
    from
        mapping.mahasiswa_onetoone mahasiswao0_ 
    where
        mahasiswao0_.tanggal_lahir<>?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLRelationalComparisonDateAndTime - data: []
Hibernate: 
    select
        mahasiswao0_.id as id1_31_,
        mahasiswao0_.alamat as alamat6_31_,
        mahasiswao0_.nama as nama2_31_,
        mahasiswao0_.nim as nim3_31_,
        mahasiswao0_.tahun_masuk as tahun_ma4_31_,
        mahasiswao0_.tanggal_lahir as tanggal_5_31_ 
    from
        mapping.mahasiswa_onetoone mahasiswao0_ 
    where
        mahasiswao0_.tanggal_lahir<>?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLRelationalComparisonDateAndTime - data: [MahasiswaOneToOneEntity(id=58c440a0-ccb1-4bba-8ff4-b55295f8dd86, nim=10511148, nama=Dimas Maryanto, tanggalLahir=1993-03-01, tahunMasuk=2011), MahasiswaOneToOneEntity(id=test, nim=10511150, nama=Muhamad Yusuf, tanggalLahir=1993-03-01, tahunMasuk=2011)]
```

dan yang terakhir kita coba method `testHigherDate()`, maka hasilnya seperti berikut:

```bash
Jan 25, 2021 1:24:59 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        mahasiswao0_.id as id1_31_,
        mahasiswao0_.alamat as alamat6_31_,
        mahasiswao0_.nama as nama2_31_,
        mahasiswao0_.nim as nim3_31_,
        mahasiswao0_.tahun_masuk as tahun_ma4_31_,
        mahasiswao0_.tanggal_lahir as tanggal_5_31_ 
    from
        mapping.mahasiswa_onetoone mahasiswao0_ 
    where
        mahasiswao0_.tanggal_lahir>?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLRelationalComparisonDateAndTime - data: []
Hibernate: 
    select
        mahasiswao0_.id as id1_31_,
        mahasiswao0_.alamat as alamat6_31_,
        mahasiswao0_.nama as nama2_31_,
        mahasiswao0_.nim as nim3_31_,
        mahasiswao0_.tahun_masuk as tahun_ma4_31_,
        mahasiswao0_.tanggal_lahir as tanggal_5_31_ 
    from
        mapping.mahasiswa_onetoone mahasiswao0_ 
    where
        mahasiswao0_.tanggal_lahir>=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLRelationalComparisonDateAndTime - data: [MahasiswaOneToOneEntity(id=58c440a0-ccb1-4bba-8ff4-b55295f8dd86, nim=10511148, nama=Dimas Maryanto, tanggalLahir=1993-03-01, tahunMasuk=2011), MahasiswaOneToOneEntity(id=test, nim=10511150, nama=Muhamad Yusuf, tanggalLahir=1993-03-01, tahunMasuk=2011)]
```

## Boolean

Untuk tipe data boolean, berikut adalah implementasi DAO:

{% gist page.gist "HQLRelationalComparisonBooleanDao.java" %}

Implementasi Unit testing:

{% gist page.gist "TestHQLRelataionComparisonBoolean.java" %}

sebelum kita coba berikut adalah data yang saya gunakan:

![select-table-boolean]({{ page.image_path | prepend: site.baseurl }}/select-table-boolean.png)

Setelah itu coba jalankan unit testing pada method `testBoolean()`, maka hasilnya seperti berikut:

```bash
Jan 25, 2021 1:29:09 PM org.hibernate.engine.transaction.jta.platform.internal.JtaPlatformInitiator initiateService
INFO: HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
Hibernate: 
    select
        mobilsingl0_.id as id2_9_,
        mobilsingl0_.cc as cc3_9_,
        mobilsingl0_.jumlah_cylinder as jumlah_c4_9_,
        mobilsingl0_.jumlah_roda as jumlah_r5_9_,
        mobilsingl0_.nama as nama6_9_,
        mobilsingl0_.nama_pabrikan as nama_pab7_9_,
        mobilsingl0_.is_all_wheel_drive as is_all_w8_9_,
        mobilsingl0_.jumlah_kursi as jumlah_k9_9_ 
    from
        inherintance.kendaraan_singletable mobilsingl0_ 
    where
        mobilsingl0_.DTYPE='MobilSingleTableEntity' 
        and mobilsingl0_.is_all_wheel_drive=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLRelataionComparisonBoolean - data: [MobilSingleTableEntity(super=KendaraanSingleTableEntity(id=a010edcd-e33c-4e4e-b33e-75df8e3f1f31, nama=Honda BRIO, jumlahRoda=4, jumlahCylinder=4, cc=1000, namaPabrikan=PT. Honda Motor Company), jumlahKursi=4, allWheelDrive=false)]
Hibernate: 
    select
        mobilsingl0_.id as id2_9_,
        mobilsingl0_.cc as cc3_9_,
        mobilsingl0_.jumlah_cylinder as jumlah_c4_9_,
        mobilsingl0_.jumlah_roda as jumlah_r5_9_,
        mobilsingl0_.nama as nama6_9_,
        mobilsingl0_.nama_pabrikan as nama_pab7_9_,
        mobilsingl0_.is_all_wheel_drive as is_all_w8_9_,
        mobilsingl0_.jumlah_kursi as jumlah_k9_9_ 
    from
        inherintance.kendaraan_singletable mobilsingl0_ 
    where
        mobilsingl0_.DTYPE='MobilSingleTableEntity' 
        and mobilsingl0_.is_all_wheel_drive=?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLRelataionComparisonBoolean - data: []
Hibernate: 
    select
        mobilsingl0_.id as id2_9_,
        mobilsingl0_.cc as cc3_9_,
        mobilsingl0_.jumlah_cylinder as jumlah_c4_9_,
        mobilsingl0_.jumlah_roda as jumlah_r5_9_,
        mobilsingl0_.nama as nama6_9_,
        mobilsingl0_.nama_pabrikan as nama_pab7_9_,
        mobilsingl0_.is_all_wheel_drive as is_all_w8_9_,
        mobilsingl0_.jumlah_kursi as jumlah_k9_9_ 
    from
        inherintance.kendaraan_singletable mobilsingl0_ 
    where
        mobilsingl0_.DTYPE='MobilSingleTableEntity' 
        and mobilsingl0_.is_all_wheel_drive<>?
[main] INFO com.maryanto.dimas.bootcamp.test.query.hql.TestHQLRelataionComparisonBoolean - data: [MobilSingleTableEntity(super=KendaraanSingleTableEntity(id=a010edcd-e33c-4e4e-b33e-75df8e3f1f31, nama=Honda BRIO, jumlahRoda=4, jumlahCylinder=4, cc=1000, namaPabrikan=PT. Honda Motor Company), jumlahKursi=4, allWheelDrive=false)]
```