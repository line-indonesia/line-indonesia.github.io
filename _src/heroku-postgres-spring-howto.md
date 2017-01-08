# Heroku Postgres + Spring
Artikel ini membahas tentang bagaimana memasang sebuah aplikasi Java yang dikembangkan menggunakan framework Spring pada Heroku dengan menggunakan PostgreSQL sebagai database. Contoh source code yang digunakan adalah proyek _spring-phonebook_ dari Github LINE Indonesia.

## spring-phonebook
Aplikasi contoh ini membuka endpoint `/phonebook` yang menerima dua method:

### `GET /phonebook`
Ada dua alternatif hasil jika request dikirim dengan menggunakan method GET:

- Tanpa parameter akan menampilkan semua isi dari tabel `phonebook`.
- Dengan menambahkan parameter `name`, maka akan dikembalikan isi dari tabel `phonebook` yang namanya terkandung pada parameter tersebut.

### `POST /phonebook`
Request dengan mehod POST harus dikirimkan dengan body berisi JSON dengan format sebagai berikut:

|Key|Keterangan|
|---|---|
|name|Nama|
|phoneNumber|Nomer telepon|


## Unduh spring-phonebook
Pertama, unduh source code ini dari repository LINE Indonesia dengan memanggil perintah berikut:

```bash
$ git clone https://github.com/line-indonesia/spring-phonebook
```

Anda akan menemukan directory _spring-phonebook_ di tempat anda memanggil perintah tersebut

```bash
$ ls
spring-phonebook
```

Masuk ke dalam directory tersebut dengan mengetikkan perintah:

```bash
$ cd spring-phonebook
```

Anda sekarang berada pada root directory dari proyek _spring-phonebook_.

## Gabungkan dengan Heroku
Lakukan login jika anda belum login dengan akun Heroku anda dengan memanggil perintah:

```bash
$ heroku login
```

Setelah anda berhasil login, ketikkan perintah:

```bash
$ heroku create
```

Tampilan di bawah ini menunjukkan bahwa container anda telah terbuat.

```bash
$ heroku create
Creating sheltered-caverns-85393... done, stack is cedar-14
http://sheltered-caverns-85393.herokuapp.com/ | https://git.heroku.com/sheltered-caverns-85393.git
Git remote heroku added
```
Pada contoh di atas, nama container anda adalah _sheltered-caverns-85393_.

## Menambahkan add-on

Tambahkan add-on Heroku Postgres pada container anda, dengan mengetikkan perintah berikut:

```bash
$ heroku addons:create heroku-postgresql:hobby-dev
```

Tampilan berikut menunjukkan bahwa add-on Heroku Postgres telah berhasil ditambahkan.

```bash
$ heroku addons:create heroku-postgresql:hobby-dev
Database has been created and is available
 ! This database is empty. If upgrading, you can transfer
 ! data from another database with pg:copy
Created postgresql-shaped-95386 as DATABASE_URL
```

## Membuat dan mengisi tabel

Masuk ke PostgreSQL dengan mengetikkan perintah berikut:

```bash
$ heroku psql
```

Selanjutnya masuklah ke dalam database anda dengan mengetikkan perintah berikut:

```bash
sheltered-caverns-85393::DATABASE=> \c <nama_database_anda>
```
**Note**: Untuk mengetahui nama database anda, silakhan lihat di pembahasan sebelumnya, _Heroku Postgres_.

Tambahkan tabel `phonebook` di dalam database, dengan memasukkan SQL berikut:

```sql
CREATE TABLE IF NOT EXISTS phonebook
(
	id BIGSERIAL PRIMARY KEY,
	name TEXT,
	phone_number TEXT
);
```
Isi tabel tersebut dengan menambahkan SQL berikut:

```sql
INSERT INTO phonebook VALUES(default, 'Leonard', '0213456789');
```

Pastikan tabel anda telah terisi dengan mencoba SQL berikut:

```sql
SELECT * FROM phonebook;
```

Jika benar, maka anda akan melihat isi tabel anda seperti ini:

```bash
 id |  name   | phone_number 
----+---------+--------------
  1 | Leonard | 0213456789
(1 row)
```

Setelah tabel terisi, saatnya keluar dari PostgreSQL dengan mengetikkan:

```bash
sheltered-caverns-85393::DATABASE=> \q
```

## Menguji endpoint

Untuk menguji method GET, masukkan perintah berikut:

```bash
$ curl https://sheltered-caverns-85393.herokuapp.com/phonebook/
```

Maka anda akan mendapatkan pesan balasan dalam bentuk JSON:

```json
[
 {
  "id":1,
  "name":"Leonard",
  "phoneNumber":"0213456789"
 }
]
```

Untuk menguji method POST, masukkan perintah berikut:

```bash
$ curl -X POST -d'{ "name":"Brown", "phoneNumber":"909090" }' -H "Content-Type: application/json;charset=UTF-8" https://fast-dusk-99392.herokuapp.com/phonebook/
```

Setelah anda melakukan GET lagi, anda akan mendapatkan hasil berikut:

```json
[
 {
  "id":1,
  "name":"Leonard",
  "phoneNumber":"0213456789"
 },
 {
  "id":2,
  "name":"Brown",
  "phoneNumber":"909090"
 }
]
```

Untuk mencari berdasarkan nama, anda bisa melakukan GET dengan mencantumkan keyword nama yang ingin anda cari. Contoh:

```bash
$ curl https://sheltered-caverns-85393.herokuapp.com/phonebook?name=own
```

Anda akan mendapatkan JSON berikut sebagai responsnya:

```json
[
 {
  "id":2,
  "name":"Brown",
  "phoneNumber":"909090"
 }
]
```

