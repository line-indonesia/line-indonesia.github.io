# Cloudinary + Spring
Artikel ini membahas tentang bagaimana memasang sebuah aplikasi Java yang dikembangkan menggunakan framework Spring dan terintegrasi dengan Cloudinary. Contoh source code yang digunakan adalah proyek _spring-cloudinary_ dari Github LINE Indonesia.

## spring-cloudinary
Aplikasi contoh ini membuka endpoint `/cloud/image` yang menerima dua method:

### `GET /cloud/image`
Menampilkan seluruh gambar dan video yang pernah diupload ke Cloudinary.

### `POST /cloud/image`
Request dengan method POST harus dikirimkan dengan body berisi file gambar/video dengan format multi-part dengan parameter `upload`.

## Unduh spring-cloudinary
Pertama, unduh source code ini dari repository LINE Indonesia dengan memanggil perintah berikut:

```bash
$ git clone https://github.com/line-indonesia/spring-cloudinary
```

Anda akan menemukan directory _spring-cloudinary_ di tempat anda memanggil perintah tersebut

```bash
$ ls
spring-hello
```

Masuk ke dalam directory tersebut dengan mengetikkan perintah:

```bash
$ cd spring-hello
```

Anda sekarang berada pada root directory dari proyek _spring-cloudinary_.

Masuk ke dalam directory _src/main/resources_ dengan mengetikkan perintah:

```bash
$ cd src/main/resources
```

Buat file `application.properties`, dan isi dengan informasi cloud name, api key, dan api secret yang anda dapatkan saat melakukan registrasi di Cloudinary.

Isi file `application.properties` ini adalah:

```ini
com.cloudinary.cloud_name=<cloud_name_anda>
com.cloudinary.api_key=<api_key_anda>
com.cloudinary.api_secret=<api_secret_anda>
```

## Compile
Lakukan compile dengan kembali ke root directory proyek dengan mengetikkan perintah:

```bash
$ gradle clean build
```

## Jalankan aplikasi
Gradle menmiliki embedded Tomcat yang mengijinkan aplikasi untuk berjalan tanpa harus dipasang di webserver khusus. Jalankan aplikasi ini dengan mengetikkan perintah:

```bash
$ gradle bootRun
```

## Menguji endpoint

Setelah aplkasi anda berjalan, anda dapat mengujinya menggunakan tool `curl`.

Misalkan anda ingin mendapatkan file-file yang ada di penyimpanan Cloudinary anda, anda dapat melakukannya dengan cara:

```bash
curl http://localhost:8000/cloud/image/
```

Anda akan mendapatkan balasan sebagai berikut:

```json
["http://res.cloudinary.com/mrexmelle/image/upload/v1483870054/sample.jpg"]
```

Berikutnya jika anda ingin menambahkan/upload file gambar/video anda, bisa juga anda lakukan lewat `curl` dengan cara:

```bash
curl -X POST -F"upload=@<file_yang_mau_diupload>" "http://localhost:8080/cloud/image/"
``` 

Pada source code contoh telah disediakan gambar yang dapat anda uji untuk diupload. Gambar tersebut terletak di _res/peluk.png_. Sehingga anda dapat mencoba mengupload gambar tersebut dengan cara:

```bash
curl -X POST -F"upload=@res/peluk.png" "http://localhost:8080/cloud/image/"
``` 
Jika anda berhasil mengirimkan gambar tersebut ke Cloudinary, anda akan mendapatkan respons sebagai berikut:

```json
{"status":"OK", "url":"http://res.cloudinary.com/moon/image/upload/v1483879780/tozlsndd56awfcf6xaem.png"}
```

Di mana _http://res.cloudinary.com/moon/image/upload/v1483879780/tozlsndd56awfcf6xaem.png_ merupakan lokasi URL yang diberikan Cloudinary bagi siapapun untuk mengambil gambar anda.
