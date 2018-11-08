---
layout: post
title: "Perintah select dengan Concatenation"
date: 2018-11-08T20:46:52+07:00
lang: psql
categories:
- RDBMS
- PostgreSQL
gist: 
youtube: 
comments: true
---

Apa itu concatenation?, Concatenation biasanya digunakan untuk mengkombinasikan, menyambungkan beberapa kolom dalam suatu query menjadi satu. seperti berikut ilustrasinya:

![konsep]({{site.baseurl}}/resources/posts/psql-concatenation/konsep-concatenation.png)

Ok misalnya saya punya struktur tabel seperti berikut:

```postgresql-console
hr=# \d employees;
                                            Table "public.employees"
     Column     |         Type          | Collation | Nullable |                    Default
----------------+-----------------------+-----------+----------+------------------------------------------------
 employee_id    | integer               |           | not null | nextval('employees_employee_id_seq'::regclass)
 first_name     | character varying(20) |           |          |
 last_name      | character varying(25) |           | not null |
 email          | character varying(25) |           | not null |
 phone_number   | character varying(20) |           |          |
 job_id         | character varying(10) |           |          |
 salary         | numeric(8,2)          |           |          |
 commission_pct | numeric(2,2)          |           |          |
 manager_id     | integer               |           |          |
 department_id  | integer               |           |          |
Indexes:
    "employees_pkey" PRIMARY KEY, btree (employee_id)
    "employees_email_key" UNIQUE CONSTRAINT, btree (email)
Foreign-key constraints:
    "fk_employees_department_id" FOREIGN KEY (department_id) REFERENCES departments(department_id) ON UPDATE CASCADE ON DELETE CASCADE
    "fk_employees_job_id" FOREIGN KEY (job_id) REFERENCES jobs(job_id) ON UPDATE CASCADE ON DELETE CASCADE
    "fk_employees_manager_id" FOREIGN KEY (manager_id) REFERENCES employees(employee_id) ON UPDATE CASCADE ON DELETE CASCADE
Referenced by:
    TABLE "departments" CONSTRAINT "fk_departments_manager_id" FOREIGN KEY (manager_id) REFERENCES employees(employee_id) ON UPDATE CASCADE ON DELETE CASCADE
    TABLE "employees" CONSTRAINT "fk_employees_manager_id" FOREIGN KEY (manager_id) REFERENCES employees(employee_id) ON UPDATE CASCADE ON DELETE CASCADE
```

Nah saya mau mengambil semua data dari table `employees` untuk menampilkan `kode karyawan` dan `nama depan + nama belakang` digabungkan menjadi satu kolom. Berikut adalah contoh querynya: 

{% highlight sql linenos %}
select 
    employee_id as id, 
    first_name || ' ' || last_name as nama_lengkap
from employees;
{% endhighlight %}

Berikut hasilnya:

```postgresql-console
id  |   nama_lengkap
-----+-------------------
 100 | Steven King
 101 | Neena Kochhar
 102 | Lex De Haan
 103 | Alexander Hunold
 104 | Bruce Ernst
 105 | David Austin
 106 | Valli Pataballa
 107 | Diana Lorentz
 108 | Nancy Greenberg
 109 | Daniel Faviet
 110 | John Chen
 111 | Ismael Sciarra
 112 | Jose Manuel Urman
 113 | Luis Popp
 114 | Den Raphaely
 115 | Alexander Khoo
 116 | Shelli Baida
 ....
 (107 rows)
```

Jadi kesimpulannya dengan menggunakan operator `||` kita bisa menggabunkan 2 kolom dalam satu query tersebut.