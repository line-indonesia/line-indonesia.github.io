# PostgreSQL
PostgreSQL adalah sebuah sistem database open-source yang ampuh dan telah dikembangkan selama lebih dari 15 tahun terakhir. Database ini dapat berjalan di beragam OS populer seperti: Linux, UNIX (AIX, BSD, HP-UX, SGI IRIX, Mac OS X, Solaris, Tru64), dan Windows.

PostgreSQL digunakan oleh banyak perusahaan teknologi terkemuka di dunia, termasuk: Apple, Fujitsu, Cisco, Red Hat, Skype, Telstra, termasuk LINE.

# Heroku Postgres

Karena kepopuleran dan kehandalannya ini, Heroku membangun sebuah add-on database yang menggunakan PostgreSQL bernama _Heroku Postgres_.

## Arsitektur
Dengan menggunakan add-on ini, Heroku secara otomatis akan membangun sebuah tempat penyimpanan database bagi anda menggunakan Amazon AWS dan mengijinkan aplikasi anda mengakses URL Postgres hanya melalui environment variable. Sehingga source code aplikasi anda akan menjadi loosely-coupled dengan add-on Heroku Postgres.

## Menambahkan add-on
Ketikkan perintah berikut untuk menambahkan add-on Heroku Postgres ke container anda:

```bash
$ heroku addons:create heroku-postgresql:hobby-dev
```

## Environment Variable
Daftar Environment variable yang ditambahkan oleh Heroku adalah:

- JDBC\_DATABASE\_USERNAME
- JDBC\_DATABASE\_PASSWORD
- JDBC\_DATABASE\_URL
- DATABASE\_URL

Anda dapat melihat daftar environment variable anda dengan mengetikkan perintah:

```bash
$ heroku run printenv
```

## Nama database
Untuk mendapatkan nama database anda, anda dapat melihat environment variable `DATABASE_URL`.

Database URL pada PostgreSQL, memiliki pola

```bash
postgres://<username>:<password>@<url_database><nama_database>
```

Sehingga jika `DATABASE_URL` anda adalah:

```bash
postgres://moon:19851006@abc-12-345-678-90.defghi-14.amazonaws.com:5432/a1b2c3d4e5
```
Maka informasi yang dapat diambil dari database anda adalah sebagai berikut:

- Username: _moon_
- Password: _19851006_
- URL database: _abc-12-345-678-90.defghi-14.amazonaws.com_
- Port database: _5432_
- Nama database: _a1b2c3d4e5_


## Mengakses database
Untuk mengakses database anda, silakhan anda masuk melalui `psql` dengan memasukkan perintah:

```bash
$ heroku psql
```
Kemudian, di dalam terminal `psql`, silakhan ketik `\c` diikuti nama database anda. Sehingga jika nama database anda adalah _a1b2c3d4e5_, maka perintah yang harus anda masukkan adalah:

```bash
sheltered-caverns-85393::DATABASE=> \c a1b2c3d4e5
```

## Melihat daftar tabel
Untuk melihat daftar tabel pada database anda, anda dapat mengetik:

```bash
sheltered-caverns-85393::DATABASE=> \l
```

## Keluar dari `psql`
Setelah anda selesai melakukan operasi-operasi pada database anda, anda dapat mengetik:

```bash
sheltered-caverns-85393::DATABASE=> \q
```

## Penutup
Untuk pembahasan yang lebih lengkap tentang add-on _Heroku Postgres_, anda dapat membaca [di sini](https://elements.heroku.com/addons/heroku-postgresql).
