# Heroku + Spring
Artikel ini membahas tentang bagaimana memasang sebuah aplikasi Java yang dikembangkan menggunakan framework Spring pada Heroku. Contoh source code yang digunakan adalah proyek _spring-hello_ dari Github LINE Indonesia.

## spring-hello
Aplikasi contoh ini membuka endpoint `/hello` yang hanya menerima method `GET`.

- Tanpa parameter akan menampilkan salam diikuti 'hoo-man' sebagai nama anda.
- Jika anda menambahkan parameter `name`, maka aplikasi akan mencetak salam sesuai waktu lokal server diikuti nama yang dimasukkan di parameter.

## Unduh spring-hello
Pertama, unduh source code ini dari repository LINE Indonesia dengan memanggil perintah berikut:

```bash
$ git clone https://github.com/line-indonesia/spring-hello
```

Anda akan menemukan directory _spring-hello_ di tempat anda memanggil perintah tersebut

```bash
$ ls
spring-hello
```

Masuk ke dalam directory tersebut dengan mengetikkan perintah:

```bash
$ cd spring-hello
```

Anda sekarang berada pada root directory dari proyek _spring-hello_.

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

## Menguji endpoint

Setelah container Heroku anda terbuat, anda dapat mengakses container tersebut dari web browser favorit anda dengan memasukkan URL:

```bash
https://sheltered-caverns-85393.herokuapp.com/hello?name=Moon
```

Anda akan mendapatkan tampilan sebagai berikut:

```bash
Good evening, Moon!
```

