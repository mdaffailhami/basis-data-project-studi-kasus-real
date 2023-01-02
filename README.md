# A. Latar Belakang

Seiring berkembangnya zaman maka bertambah pula kebutuhan teknologi dalam masyarakat, contohnya seperti kebutuhan teknologi untuk mengirimkan uang ke kerabat atau contoh lainnya seperti untuk melakukan jual beli barang / jasa secara online. Oleh karena itu pihak bank menyediakan fitur transfer bank untuk memudahkan masyarakat mengirim uang ke beda wilayah yang jauh maupun yang dekat.

Maka dari itulah kami pun jadi tertarik untuk mengangkat studi kasus Perbankan ini sebagai studi kasus untuk tugas Project Studi Kasus Real ini.

# B. Tujuan
Tujuan kenapa kami memilih studi kasus “Perbankan” adalah sebagai berikut:  
- Menjadikan sarana untuk mengasah logika sebab studi kasusnya bisa dibilang lumayan kompleks.
- Tugas cepat selesai karena sangat relate dengan kasus-kasus di dunia nyata yang pastinya diantara kita pasti pernah melakukan transfer bank.

# C. Normalisasi Database

## 1. Normalisasi Tabel **Nasabah**

Pada tabel di bawah ini masih berada pada tahap Unnormalized Form (UNF)

### **UNF**

| ID Nasabah | Nama            | Jenis Kelamin | Tanggal Lahir | No. Rekening 1  | Saldo Rekening 1 | ID Bank Rekening 1 | Nama Bank Rekening 1   | No. Rekening 2 | Saldo Rekening 2 | ID Bank Rekening 2 | Nama Bank Rekening 2 |
| ---------- | --------------- | ------------- | ------------- | --------------- | ---------------- | ------------------ | ---------------------- | -------------- | ---------------- | ------------------ | -------------------- |
| 1          | Ahmad Trafalgar | L             | 2003-08-18    | 8291759182      | 500000           | 1                  | Bank Syariah Indonesia | 4291028478916  | 150000           | 3                  | Bank Kalsel          |
| 2          | Nefertari Putri | P             | 2004-06-12    | 3192648105      | 300000           | 1                  | Bank Syariah Indonesia |                |                  |                    |                      |
| 3          | Charlote Niko   | P             | 2004-12-27    | 738201928567189 | 1200000          | 2                  | Bank Rakyat Indonesia  |                |                  |                    |                      |

<br>

Untuk mengubahnya menjadi First Normal Form (1NF) maka kita harus membuat agar setiap kolom tidak ada yang berulang, sehingga hasilnya menjadi seperti di bawah ini

### **1NF**

| ID Nasabah | Nama            | Jenis Kelamin | Tanggal Lahir | No. Rekening    | Saldo Rekening   | ID Bank Rekening   | Nama Bank Rekening     |
| ---------- | --------------- | ------------- | ------------- | --------------- | ---------------- | ------------------ | ---------------------- |
| 1          | Ahmad Trafalgar | L             | 2003-08-18    | 8291759182      | 500000           | 1                  | Bank Syariah Indonesia |
| 1          | Ahmad Trafalgar | L             | 2003-08-18    | 4291028478916   | 150000           | 3                  | Bank Kalsel            |
| 2          | Nefertari Putri | P             | 2004-06-12    | 3192648105      | 300000           | 1                  | Bank Syariah Indonesia |
| 3          | Charlote Niko   | P             | 2004-12-27    | 738201928567189 | 1200000          | 2                  | Bank Rakyat Indonesia  |

<br>

Selanjutnya untuk mengubahnya menjadi Second Normal Form (2NF) maka kita harus memecahnya menjadi 2 tabel yaitu “Nasabah” dan “Rekening” agar setiap kolom menjadi bergantung penuh pada primary key

### **2NF**

| ID Nasabah | Nama            | Jenis Kelamin | Tanggal Lahir |
| ---------- | --------------- | ------------- | ------------- |
| 1          | Ahmad Trafalgar | L             | 2003-08-18    |
| 2          | Nefertari Putri | P             | 2004-06-12    |
| 3          | Charlote Niko   | P             | 2004-12-27    |

| No. Rekening    | ID Nasabah | Saldo   | ID Bank | Nama Bank              |
| --------------- | ---------- | ------- | ------- | ---------------------- |
| 8291759182      | 1          | 500000  | 1       | Bank Syariah Indonesia |
| 4291028478916   | 1          | 150000  | 3       | Bank Kalsel            |
| 3192648105      | 2          | 300000  | 1       | Bank Syariah Indonesia |
| 738201928567189 | 3          | 1200000 | 2       | Bank Rakyat Indonesia  |

<br>

Lalu yang terakhir untuk mengubahnya menjadi Third Normal Form (3NF) maka kita harus membuat setiap kolom non-key tidak ada yang bergantung dengan kolom non-key lainnya, dalam kasus ini adalah kolom “Nama Bank” bergantung pada kolom “ID Bank”, jadi kita harus memecahnya menjadi tabel baru lagi yaitu “Bank”.

### **3NF**

| ID Nasabah | Nama            | Jenis Kelamin | Tanggal Lahir |
| ---------- | --------------- | ------------- | ------------- |
| 1          | Ahmad Trafalgar | L             | 2003-08-18    |
| 2          | Nefertari Putri | P             | 2004-06-12    |
| 3          | Charlote Niko   | P             | 2004-12-27    |

| No. Rekening    | ID Nasabah | Saldo   | ID Bank |
| --------------- | ---------- | ------- | ------- |
| 8291759182      | 1          | 500000  | 1       |
| 4291028478916   | 1          | 150000  | 3       |
| 3192648105      | 2          | 300000  | 1       |
| 738201928567189 | 3          | 1200000 | 2       |

| ID Bank | Nama Bank              |
| ------- | ---------------------- |
| 1       | Bank Syariah Indonesia |
| 2       | Bank Rakyat Indonesia  |
| 3       | Bank Kalsel            |

<br>

## 2. Normalisasi Tabel **Struk**

Pada tabel di bawah ini masih berada pada tahap Unnormalized Form (UNF)

### **UNF**

| No. Struk                          | No. Transaksi    | No. Rekening Pengirim | No. Rekening Penerima | Status   | Judul                            | Tanggal    | Jumlah | Biaya Admin | Keterangan                 |
| ---------------------------------- | ---------------- | --------------------- | --------------------- | -------- | -------------------------------- | ---------- | ------ | ----------- | -------------------------- |
| 1671893956347365                   | 1671893930708915 | 3192648105            | 8291759182            | BERHASIL | Transfer sesama BSI              | 2022-12-24 | 500000 | 0           | Selamat atas juaranya!     |
| 1671893983606915, 1671932489958877 | 1671893968574782 | 8291759182            | 738201928567189       | BERHASIL | Transfer dari BSI ke Bank Kalsel | 2022-12-24 | 200000 | 6500        | Nih buat bayar utang wkwkw |

<br>

Untuk mengubahnya menjadi First Normal Form (1NF) maka kita harus membuat agar setiap kolom tidak ada yang multi value, sehingga hasilnya menjadi seperti di bawah ini

### **1NF**

| No. Struk        | No. Transaksi    | No. Rekening Pengirim | No. Rekening Penerima | Status   | Judul                            | Tanggal    | Jumlah | Biaya Admin | Keterangan                 |
| ---------------- | ---------------- | --------------------- | --------------------- | -------- | -------------------------------- | ---------- | ------ | ----------- | -------------------------- |
| 1671893956347365 | 1671893930708915 | 3192648105            | 8291759182            | BERHASIL | Transfer sesama BSI              | 2022-12-24 | 500000 | 0           | Selamat atas juaranya!     |
| 1671893983606915 | 1671893968574782 | 8291759182            | 738201928567189       | BERHASIL | Transfer dari BSI ke Bank Kalsel | 2022-12-24 | 200000 | 6500        | Nih buat bayar utang wkwkw |
| 1671932489958877 | 1671893968574782 | 8291759182            | 738201928567189       | BERHASIL | Transfer dari BSI ke Bank Kalsel | 2022-12-24 | 200000 | 6500        | Nih buat bayar utang wkwkw |

<br>

Selanjutnya untuk mengubahnya menjadi Second Normal Form (2NF) maka kita harus membuat setiap kolom agar bergantung penuh pada primary key

### **2NF & 3NF**

| No. Struk        | No. Transaksi    |
| ---------------- | ---------------- |
| 1671893956347365 | 1671893930708915 |
| 1671893983606915 | 1671893968574782 |
| 1671932489958877 | 1671893968574782 |

| No. Transaksi    | No. Rekening Pengirim | No. Rekening Penerima | Status   | Judul                            | Tanggal    | Jumlah | Biaya Admin | Keterangan                 |
| ---------------- | --------------------- | --------------------- | -------- | -------------------------------- | ---------- | ------ | ----------- | -------------------------- |
| 1671893930708915 | 3192648105            | 8291759182            | BERHASIL | Transfer sesama BSI              | 2022-12-24 | 500000 | 0           | Selamat atas juaranya!     |
| 1671893968574782 | 8291759182            | 738201928567189       | BERHASIL | Transfer dari BSI ke Bank Kalsel | 2022-12-24 | 200000 | 6500        | Nih buat bayar utang wkwkw |

Jika dilihat-lihat pada tabel di atas, setiap kolom non-keynya tidak ada yang bergantung dengan kolom non-key lainnya, sehingga kita bisa menyatakan bahwa tabel di atas juga telah memenuhi syarat normalisasi Third Normal Form (3NF)

<br>

# D. Entity Relationship
![ERD](https://user-images.githubusercontent.com/74972129/210193116-d20bcdd6-72dc-4173-9a7c-2facd64ff594.jpg)
![DB Schema](https://user-images.githubusercontent.com/74972129/210043327-ad24bc07-7091-42c8-9760-54e7b36c3ea4.png)

# E. Implementasi DBMS MySQL

### Menyalakan server MySQL

```sql
mdaffailhami@mdaffailhami-pc:~$ sudo xampp startmysql
XAMPP: Starting MySQL...ok.
```

### Masuk ke MySQL menggunakan user **root**

```sql
mdaffailhami@mdaffailhami-pc:~$ mysql -u root
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 9
Server version: 10.4.25-MariaDB Source distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
```

### Membuat database **perbankan**

```sql
MariaDB [(none)]> CREATE DATABASE perbankan;
Query OK, 1 row affected (0.007 sec)
```

### Membuat user **admin**

```sql
MariaDB [(none)]> CREATE USER 'admin'@'localhost' IDENTIFIED BY 'admin123';
Query OK, 0 rows affected (0.006 sec)

MariaDB [(none)]> GRANT ALL PRIVILEGES ON perbankan.* TO 'admin'@'localhost';
Query OK, 0 rows affected (0.001 sec)
```

### Masuk ke MySQL menggunakan user **admin**

```sql
MariaDB [(none)]> exit
Bye
mdaffailhami@mdaffailhami-pc:~$ mysql -u admin -p
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 10
Server version: 10.4.25-MariaDB Source distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> use perbankan
Database changed

MariaDB [perbankan]>
```

### Membuat tabel **bank**

```sql
MariaDB [perbankan]> CREATE TABLE bank (
    ->   id_bank int NOT NULL AUTO_INCREMENT,
    ->   nama varchar(40) NOT NULL,
    ->   PRIMARY KEY (id_bank)
    -> );
Query OK, 0 rows affected (0.020 sec)
```

### Membuat tabel **nasabah**

```sql
MariaDB [perbankan]> CREATE TABLE nasabah (
    ->   id_nasabah int NOT NULL AUTO_INCREMENT,
    ->   nama varchar(40) NOT NULL,
    ->   jenis_kelamin enum('L', 'P') NOT NULL,
    ->   tanggal_lahir date NOT NULL,
    ->   PRIMARY KEY (id_nasabah)
    -> );
Query OK, 0 rows affected (0.012 sec)
```

### Membuat tabel **rekening**

```sql
MariaDB [perbankan]> CREATE TABLE rekening (
    ->   no_rekening bigint NOT NULL,
    ->   id_bank int NOT NULL,
    ->   id_nasabah int NOT NULL,
    ->   saldo bigint NOT NULL default 0,
    ->   PRIMARY KEY (no_rekening),
    ->   FOREIGN KEY (id_bank) REFERENCES bank(id_bank),
    ->   FOREIGN KEY (id_nasabah) REFERENCES nasabah(id_nasabah)
    -> );
Query OK, 0 rows affected (0.014 sec)
```

### Membuat tabel **transfer**

```sql
MariaDB [perbankan]> CREATE TABLE transfer (
    ->   no_transaksi bigint NOT NULL DEFAULT CONCAT(
    ->     FLOOR(UNIX_TIMESTAMP(CURRENT_TIMESTAMP(3)) * 1000), FLOOR(RAND() * (1000 - 100) + 100)
    ->   ),
    ->   no_rekening_pengirim bigint NOT NULL,
    ->   no_rekening_penerima bigint NOT NULL,
    ->   judul varchar(60) NOT NULL,
    ->   status enum('BERHASIL', 'GAGAL') NOT NULL,
    ->   tanggal date NOT NULL DEFAULT CURDATE(),
    ->   jumlah int NOT NULL,
    ->   biaya_admin int NOT NULL DEFAULT 0,
    ->   keterangan varchar(120),
    ->   PRIMARY KEY (no_transaksi),
    ->   FOREIGN KEY (no_rekening_pengirim) REFERENCES rekening(no_rekening),
    ->   FOREIGN KEY (no_rekening_penerima) REFERENCES rekening(no_rekening)
    -> );
Query OK, 0 rows affected (0.016 sec)
```

### Membuat tabel **struk**

```sql
MariaDB [perbankan]> CREATE TABLE struk (
    ->   no_struk bigint NOT NULL DEFAULT CONCAT(
    ->     FLOOR(UNIX_TIMESTAMP(CURRENT_TIMESTAMP(3)) * 1000), FLOOR(RAND() * (1000 - 100) + 100)
    ->   ),
    ->   no_transaksi bigint NOT NULL,
    ->   PRIMARY KEY (no_struk),
    ->   FOREIGN KEY (no_transaksi) REFERENCES transfer(no_transaksi)
    -> );
Query OK, 0 rows affected (0.012 sec)
```

### Memasukkan baris baru ke dalam tabel **bank**

```sql
MariaDB [perbankan]> INSERT INTO bank (nama) VALUES
    ->   ('Bank Syariah Indonesia'),
    ->   ('Bank Rakyat Indonesia'),
    ->   ('Bank Kalsel');
Query OK, 3 rows affected (0.014 sec)
Records: 3  Duplicates: 0  Warnings: 0
```

### Masuk ke MySQL menggunakan user **root**

```sql
MariaDB [perbankan]> exit
Bye
mdaffailhami@mdaffailhami-pc:~$ mysql -u root
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 15
Server version: 10.4.25-MariaDB Source distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
```

### Membuat user **customer_service**

```sql
MariaDB [(none)]> CREATE USER 'customer_service'@'localhost' IDENTIFIED BY '12345';
Query OK, 0 rows affected (0.007 sec)

MariaDB [(none)]> GRANT SELECT ON perbankan.* TO 'customer_service'@'localhost';
Query OK, 0 rows affected (0.010 sec)

MariaDB [(none)]> GRANT INSERT, SELECT, UPDATE, DELETE ON perbankan.nasabah TO 'customer_service'@'localhost';
Query OK, 0 rows affected (0.003 sec)

MariaDB [(none)]> GRANT INSERT, SELECT, UPDATE, DELETE ON perbankan.rekening TO 'customer_service'@'localhost';
Query OK, 0 rows affected (0.003 sec)
```

### Membuat user **teller**

```sql
MariaDB [(none)]> CREATE USER 'teller'@'localhost' IDENTIFIED BY '54321';
Query OK, 0 rows affected (0.000 sec)

MariaDB [(none)]> GRANT SELECT ON perbankan.* TO 'teller'@'localhost';
Query OK, 0 rows affected (0.006 sec)

MariaDB [(none)]> GRANT UPDATE (saldo) ON perbankan.rekening TO 'teller'@'localhost';
Query OK, 0 rows affected (0.003 sec)

MariaDB [(none)]> GRANT INSERT, SELECT ON perbankan.transfer TO 'teller'@'localhost';
Query OK, 0 rows affected (0.001 sec)

MariaDB [(none)]> GRANT INSERT, SELECT ON perbankan.struk TO 'teller'@'localhost';
Query OK, 0 rows affected (0.000 sec)
```

### Masuk ke MySQL menggunakan user **customer_service**

```sql
MariaDB [(none)]> exit
Bye
mdaffailhami@mdaffailhami-pc:~$ mysql -u customer_service -p
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 16
Server version: 10.4.25-MariaDB Source distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> use perbankan
Database changed

MariaDB [perbankan]>
```

### Memasukkan baris baru ke dalam tabel **nasabah**

```sql
MariaDB [perbankan]> INSERT INTO nasabah (nama, jenis_kelamin, tanggal_lahir) VALUES
    ->   ('Ahmad Trafalgar', 'L', '2003-08-18'),
    ->   ('Nefertari Putri', 'P', '2004-06-12'),
    ->   ('Charlote Perona', 'P', '2004-12-27');
Query OK, 3 rows affected (0.023 sec)
Records: 3  Duplicates: 0  Warnings: 0
```

### Mengubah nama nasabah

```sql
MariaDB [perbankan]> UPDATE nasabah SET nama = "Charlote Niko" WHERE id_nasabah = 3;
Query OK, 1 row affected (0.005 sec)
Rows matched: 1  Changed: 1  Warnings: 0

MariaDB [perbankan]> SELECT * FROM nasabah;
+------------+-----------------+---------------+---------------+
| id_nasabah | nama            | jenis_kelamin | tanggal_lahir |
+------------+-----------------+---------------+---------------+
|          1 | Ahmad Trafalgar | L             | 2003-08-18    |
|          2 | Nefertari Putri | P             | 2004-06-12    |
|          3 | Charlote Niko   | P             | 2004-12-27    |
+------------+-----------------+---------------+---------------+
3 rows in set (0.000 sec)
```

### Memasukkan baris baru ke dalam tabel **rekening**

```sql
MariaDB [perbankan]> INSERT INTO rekening (no_rekening, id_bank, id_nasabah) VALUES
    ->   (8291759182, 1, 1),
    ->   (4291028478916, 3, 1),
    ->   (3192648105, 1, 2),
    ->   (738201928567189, 2, 3);
Query OK, 4 rows affected (0.017 sec)
Records: 4  Duplicates: 0  Warnings: 0

MariaDB [perbankan]> SELECT * FROM rekening;
+-----------------+---------+------------+-------+
| no_rekening     | id_bank | id_nasabah | saldo |
+-----------------+---------+------------+-------+
|      3192648105 |       1 |          2 |     0 |
|      8291759182 |       1 |          1 |     0 |
|   4291028478916 |       3 |          1 |     0 |
| 738201928567189 |       2 |          3 |     0 |
+-----------------+---------+------------+-------+
4 rows in set (0.000 sec)
```

### Masuk ke MySQL menggunakan user **teller**

```sql
MariaDB [perbankan]> exit
Bye
mdaffailhami@mdaffailhami-pc:~$ mysql -u teller -p
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 17
Server version: 10.4.25-MariaDB Source distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> use perbankan
Database changed

MariaDB [perbankan]>
```

### Mengubah jumlah saldo rekening nasabah

```sql
MariaDB [perbankan]> UPDATE rekening SET saldo = 2500000 WHERE no_rekening = 8291759182;
Query OK, 1 row affected (0.014 sec)
Rows matched: 1  Changed: 1  Warnings: 0

MariaDB [perbankan]> UPDATE rekening SET saldo = 400000 WHERE no_rekening = 4291028478916;
Query OK, 1 row affected (0.003 sec)
Rows matched: 1  Changed: 1  Warnings: 0

MariaDB [perbankan]> UPDATE rekening SET saldo = 1200000 WHERE no_rekening = 3192648105;
Query OK, 1 row affected (0.002 sec)
Rows matched: 1  Changed: 1  Warnings: 0

MariaDB [perbankan]> UPDATE rekening SET saldo = 850000 WHERE no_rekening = 738201928567189;
Query OK, 1 row affected (0.003 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

### Melakukan transaksi transfer

```sql
MariaDB [perbankan]> SET
    ->   @no_rekening_pengirim = 3192648105,
    ->   @no_rekening_penerima = 8291759182,
    ->   @jumlah_transfer = 500000;
Query OK, 0 rows affected (0.008 sec)

MariaDB [perbankan]> INSERT INTO transfer (
    ->   no_rekening_pengirim,
    ->   no_rekening_penerima,
    ->   judul,
    ->   status,
    ->   jumlah,
    ->   keterangan
    -> ) VALUES (
    ->   @no_rekening_pengirim,
    ->   @no_rekening_penerima,
    ->   'Transfer sesama BSI',
    ->   'BERHASIL',
    ->   @jumlah_transfer,
    ->   'Selamat atas juaranya!'
    -> );
Query OK, 1 row affected (0.015 sec)
```

### Mengubah saldo rekening yang telah melakukan transfer

```sql
MariaDB [perbankan]> UPDATE rekening SET saldo = saldo - @jumlah_transfer WHERE no_rekening = @no_rekening_pengirim;
Query OK, 1 row affected (0.010 sec)
Rows matched: 1  Changed: 1  Warnings: 0

MariaDB [perbankan]> UPDATE rekening SET saldo = saldo + @jumlah_transfer WHERE no_rekening = @no_rekening_penerima;
Query OK, 1 row affected (0.004 sec)
Rows matched: 1  Changed: 1  Warnings: 0

MariaDB [perbankan]> SELECT * FROM rekening;
+-----------------+---------+------------+---------+
| no_rekening     | id_bank | id_nasabah | saldo   |
+-----------------+---------+------------+---------+
|      3192648105 |       1 |          2 |  700000 |
|      8291759182 |       1 |          1 | 3000000 |
|   4291028478916 |       3 |          1 |  400000 |
| 738201928567189 |       2 |          3 |  850000 |
+-----------------+---------+------------+---------+
4 rows in set (0.000 sec)
```

### Membuatkan struk transaksinya

```sql
MariaDB [perbankan]> SELECT * from transfer;
+------------------+----------------------+----------------------+---------------------+----------+------------+--------+-------------+------------------------+
| no_transaksi     | no_rekening_pengirim | no_rekening_penerima | judul               | status   | tanggal    | jumlah | biaya_admin | keterangan             |
+------------------+----------------------+----------------------+---------------------+----------+------------+--------+-------------+------------------------+
| 1672385308570259 |           3192648105 |           8291759182 | Transfer sesama BSI | BERHASIL | 2022-12-30 | 500000 |           0 | Selamat atas juaranya! |
+------------------+----------------------+----------------------+---------------------+----------+------------+--------+-------------+------------------------+
1 row in set (0.001 sec)

MariaDB [perbankan]> INSERT INTO struk (no_transaksi) VALUES (1672385308570259);
Query OK, 1 row affected (0.009 sec)

MariaDB [perbankan]> SELECT * FROM struk;
+------------------+------------------+
| no_struk         | no_transaksi     |
+------------------+------------------+
| 1672385385650848 | 1672385308570259 |
+------------------+------------------+
1 row in set (0.007 sec)
```

### Melakukan transaksi transfer lagi

```sql
MariaDB [perbankan]> SET
    ->   @no_rekening_pengirim = 8291759182,
    ->   @no_rekening_penerima = 738201928567189,
    ->   @jumlah_transfer = 200000,
    ->   @biaya_admin = 6500;
Query OK, 0 rows affected (0.000 sec)

MariaDB [perbankan]> INSERT INTO transfer (
    ->   no_rekening_pengirim,
    ->   no_rekening_penerima,
    ->   judul,
    ->   status,
    ->   jumlah,
    ->   biaya_admin,
    ->   keterangan
    -> ) VALUES (
    ->   @no_rekening_pengirim,
    ->   @no_rekening_penerima,
    ->   'Transfer dari BSI ke Bank Kalsel',
    ->   'BERHASIL',
    ->   @jumlah_transfer,
    ->   @biaya_admin,
    ->   'Nih buat bayar utang wkwkw'
    -> );
Query OK, 1 row affected (0.017 sec)
```

### Mengubah saldo rekening yang telah melakukan transfer

```sql
MariaDB [perbankan]> UPDATE rekening SET saldo = saldo - @jumlah_transfer - @biaya_admin WHERE no_rekening = @no_rekening_pengirim;
Query OK, 1 row affected (0.003 sec)
Rows matched: 1  Changed: 1  Warnings: 0

MariaDB [perbankan]> UPDATE rekening SET saldo = saldo + @jumlah_transfer WHERE no_rekening = @no_rekening_penerima;
Query OK, 1 row affected (0.002 sec)
Rows matched: 1  Changed: 1  Warnings: 0

MariaDB [perbankan]> SELECT * FROM rekening;
+-----------------+---------+------------+---------+
| no_rekening     | id_bank | id_nasabah | saldo   |
+-----------------+---------+------------+---------+
|      3192648105 |       1 |          2 |  700000 |
|      8291759182 |       1 |          1 | 2793500 |
|   4291028478916 |       3 |          1 |  400000 |
| 738201928567189 |       2 |          3 | 1050000 |
+-----------------+---------+------------+---------+
4 rows in set (0.000 sec)
```

### Membuatkan struk transaksinya

```sql
MariaDB [perbankan]> SELECT * from transfer;
+------------------+----------------------+----------------------+----------------------------------+----------+------------+--------+-------------+----------------------------+
| no_transaksi     | no_rekening_pengirim | no_rekening_penerima | judul                            | status   | tanggal    | jumlah | biaya_admin | keterangan                 |
+------------------+----------------------+----------------------+----------------------------------+----------+------------+--------+-------------+----------------------------+
| 1672385308570259 |           3192648105 |           8291759182 | Transfer sesama BSI              | BERHASIL | 2022-12-30 | 500000 |           0 | Selamat atas juaranya!     |
| 1672385517806663 |           8291759182 |      738201928567189 | Transfer dari BSI ke Bank Kalsel | BERHASIL | 2022-12-30 | 200000 |        6500 | Nih buat bayar utang wkwkw |
+------------------+----------------------+----------------------+----------------------------------+----------+------------+--------+-------------+----------------------------+
2 rows in set (0.001 sec)

MariaDB [perbankan]> INSERT INTO struk (no_transaksi) VALUES (1672385517806663);
Query OK, 1 row affected (0.009 sec)
```

### Membuatkan lagi struk transaksinya

```sql
MariaDB [perbankan]> INSERT INTO struk (no_transaksi) VALUES (1672385517806663);
Query OK, 1 row affected (0.011 sec)

MariaDB [perbankan]> SELECT * FROM struk;
+------------------+------------------+
| no_struk         | no_transaksi     |
+------------------+------------------+
| 1672385385650848 | 1672385308570259 |
| 1672385612198671 | 1672385517806663 |
| 1672385639216364 | 1672385517806663 |
+------------------+------------------+
3 rows in set (0.001 sec)
```

### Menampilkan detail semua struk

```sql
MariaDB [perbankan]> SELECT
    ->   struk.no_struk as 'No. Struk',
    ->   transfer.no_transaksi as 'No. Transaksi',
    ->   transfer.judul as Judul,
    ->   transfer.status as Status,
    ->   transfer.tanggal as Tanggal,
    ->   transfer.no_rekening_pengirim as 'No. Rekening Pengirim',
    ->   transfer.no_rekening_penerima as 'No. Rekening Penerima',
    ->   transfer.biaya_admin as 'Biaya Admin',
    ->   transfer.jumlah as Jumlah,
    ->   transfer.keterangan as Keterangan
    -> FROM
    ->   struk, transfer
    -> WHERE
    ->   struk.no_transaksi = transfer.no_transaksi;
+------------------+------------------+----------------------------------+----------+------------+-----------------------+-----------------------+-------------+--------+----------------------------+
| No. Struk        | No. Transaksi    | Judul                            | Status   | Tanggal    | No. Rekening Pengirim | No. Rekening Penerima | Biaya Admin | Jumlah | Keterangan                 |
+------------------+------------------+----------------------------------+----------+------------+-----------------------+-----------------------+-------------+--------+----------------------------+
| 1672385385650848 | 1672385308570259 | Transfer sesama BSI              | BERHASIL | 2022-12-30 |            3192648105 |            8291759182 |           0 | 500000 | Selamat atas juaranya!     |
| 1672385612198671 | 1672385517806663 | Transfer dari BSI ke Bank Kalsel | BERHASIL | 2022-12-30 |            8291759182 |       738201928567189 |        6500 | 200000 | Nih buat bayar utang wkwkw |
| 1672385639216364 | 1672385517806663 | Transfer dari BSI ke Bank Kalsel | BERHASIL | 2022-12-30 |            8291759182 |       738201928567189 |        6500 | 200000 | Nih buat bayar utang wkwkw |
+------------------+------------------+----------------------------------+----------+------------+-----------------------+-----------------------+-------------+--------+----------------------------+
3 rows in set (0.011 sec)

MariaDB [perbankan]>
```

# F. Kesimpulan
Berdasarkan laporan yang telah dijabarkan, maka di sini saya dapat menarikbeberapa kesimpulan diantaranya:  
- Normalisasi database mencapai tingkat Third Normal Form (3NF).
- Terdapat 5 tabel yaitu bank, nasabah, rekening, transfer, dan struk.
- Terdapat 3 user yaitu admin, customer_service, dan teller.

# G. Saran
Berikut adalah saran sebelum melakukan praktikum studi kasus Transfer Bank:  
- Pahami terlebih dahulu tentang apa itu database
- Pelajari apa itu database relational
- Pelajari bagaimana cara melakukan normalisasi database
- Pahami fungsi dari ERD dan pelajari bagaimana cara mengimplementasikannya
- Pelajari bagaimana cara menggunakan database MySQL
- Pelajari perintah-perintah dasar MySQL seperti CREATE, INSERT, UPDATE, DELETE, SELECT, dll