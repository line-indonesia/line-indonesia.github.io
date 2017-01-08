# Heroku
Heroku adalah PaaS (Platform as a Service) yang menyediakan layanan bagi para pengembang aplikasi web service untuk menempatkan aplikasi mereka di ruang publik agar semua orang dapat mengaksesnya.

## Mengapa Heroku?
- Heroku memiliki paket gratis yang dapat digunakan para pengembang dengan batasan-batasan teknis tertentu.
- Layanan gratis Heroku dapat dinikmati selamanya.
- Heroku mendukung penempatan service yang ditulis dalam beragam bahasa pemrograman populer: Node.js, Ruby, Java, PHP, Python, Go, Scala, dan Clojure. 
- Memiliki dukungan add-on yang banyak, meliputi beberapa servis populer seperti: Kafka, Redis, Memcached, PostgreSQL, Cloudinary, dan banyak lagi.
- Pemasangan aplikasi dilakukan lewat git. Heroku secara internal memiliki repository git untuk tiap service yang ditempatkan. Dengan demikian penempatan bisa dilakukan secara aman dan sejarah modifikasi terhadap proyek dapat terpantau.

## Registrasi
Registrasi dapat dilakukan di [sini](https://devcenter.heroku.com/).
Anda dapat memilih menjadi pengguna gratis tanpa diminta kartu kredit.

## Instalasi
Heroku memiliki tool yang dapat digunakan lewat CLI (Command Line Interface).
Tool ini bernama Heroku CLI dan dapat digunakan dengan memanggil `heroku` pada CLI.


## Heroku CLI
Sebelum melakukan berbagai operasi menggunakan Heroku CLI, anda harus login terlebih dahulu dengan mengetikan perintah berikut:

``` bash
$ heroku login
```

Masukkan email yang anda gunakan saat melakukan registrasi.

```bash
$ heroku login
Enter your Heroku credentials.
Email:
```

Masukkan password anda.

```bash
$ heroku login
Enter your Heroku credentials.
Email: moon@line.me
Password (typing will be hidden):
```

Setelah anda memasukkan username dan password yang valid, anda sudah siap menggunakan Heroku CLI.

```bash
$ heroku login
Enter your Heroku credentials.
Email: moon@line.me
Password (typing will be hidden):
Logged in as moon@line.me
```

Heroku diciptakan untuk berhubungan erat dengan git. Setelah anda melakukan `git clone` untuk mendapatkan source code aplikasi anda, ketikkan perintah berikut:

```bash
$ heroku create
```
Perintah tersebut akan melakukan hal-hal berikut:

- Menciptakan sebuah container dengan nama yang random untuk anda berikut dengan repository git dengan nama yang sama (pada contoh di bawah ini adalah _sheltered-caverns-85393_).

```bash
$ heroku create
Creating sheltered-caverns-85393... done, stack is cedar-14
http://sheltered-caverns-85393.herokuapp.com/ | https://git.heroku.com/sheltered-caverns-85393.git
Git remote heroku added
```

- Menambahkan sebuah remote repository pada git anda. Remote repository ini bisa anda lihat dengan mengetikkan perintah:

```bash
$ git remote -v
```

Perintah tersebut akan mencetak daftar repository yang tersedia dan digunakan saat melakukan `git push` dan `git fetch`.

```bash
$ git remote -v
heroku  https://git.heroku.com/sheltered-caverns-85393.git (fetch)
heroku  https://git.heroku.com/sheltered-caverns-85393.git (push)
origin  https://git.line.me/moon/spring-line (fetch)
origin  https://git.line.me/moon/spring-line (push)
```

Setiap kali anda ingin memasang aplikasi anda ke heroku, anda dapat memanggil perintah:

```bash
$ git push heroku master
```

**Note**: Perintah di atas tidak melakukan push ke repository anda, melainkan hanya ke repository Heroku, untuk kemudian dilakukan pemasangan ke container heroku anda.
Anda tetap harus memanggil perintah `git push` seperti biasa untuk melakukan push ke repository anda.

Setiap pengguna gratis Heroku akan mendapatkan satu worker default bernama `web`. Untuk memastikan aplikasi anda berjalan, panggil perintah berikut:

```bash
$ heroku ps:scale web=1
```

Heroku menghitung kuota waktu yang anda gunakan setiap bulan. Oleh sebab itu, jika anda tidak berniat menghidupkan worker anda, anda dapat menghentikannya dengan menggunakan perintah berikut:

```bash
$ heroku ps:stop web.1
```

## Penutup
Demikian penjelasan dasar tentang bagaimana menggunakan Heroku sebagai PaaS untuk aplikasi anda.

Untuk lebih jelasnya anda dapat mengikuti tutorial Heroku di [sini](https://devcenter.heroku.com/start) dengan memilih bahasa pemrograman yang anda ingin gunakan.