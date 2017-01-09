#LINE Messaging API
Messaging API dapat membuat kamu untuk membuat sebuah bot yang berinteraksi dengan pengguna lewat LINE chats.

###Komponen LINE Messaging API:

1. **Webhooks:** Menerima notifikasi secara _real-time_ saat pengguna mengirim pesan atau berteman dengan akun anda.
2. **Reply Messaging API:** Membalas pesan pengguna.
3. **Push Messaging API:** Mengirimkan pesan ke pengguna saat anda inginkan.
4. **Get Content API:** Mengambil gambar, video, atau audio yang dikirimkan oleh pengguna.
5. **Get Profile API:** Mendapatkan informasi profil pengguna.
6. **Leave API:** Meninggalkan grup atau room.

###Spesifikasi Umum:
* Limit Request: 

Paket | Limit
------------ | -------------
Developer Trial | 1.000/min
Paket lain | 10.000/min

* Kode Status:

Kode Error | Deskripsi
------------ | -------------
200 OK | Request berhasil
400 Bad Request | Masalah dengan request
401 Unauthorized | Channel access token yang valid belum ditentukan
403 Forbidden | Tidak memiliki wewenang untuk menggunakan API. Pastikan bahwa akun anda atau paket dapat menggunakan API
429 Too Many Request | Melebihi batas untuk pemanggilan API
500 Internal Server Error | Error di server internal

* Header Respon:

Header Respon | Deskripsi
------------ | -------------
X-Line-Request-Id | ID dihasilkan untuk setiap request

* Respon Error: Data JSON ini dikembalikan saat terjadi error

Label | Tipe  | Deskripsi
------------ | ------------ | -------------
message | String | Ringkasan dari error
details[].message | String | detail dari error

ATAU

Label | Tipe  | Deskripsi
------------ | ------------ | -------------
message | String | Detail dari error

#####LINE Bot SDK

LINE Bot SDK disediakan dalam beberapa bahasa pemrograman untuk memudahkan pengembangan aplikasi bot anda dengan Mesaaging API. 

* [Java](https://github.com/line/line-bot-sdk-java)
* [PHP](https://github.com/line/line-bot-sdk-php)
* [Go](https://github.com/line/line-bot-sdk-go)
* [Perl](https://github.com/line/line-bot-sdk-perl)
* [Ruby](https://github.com/line/line-bot-sdk-ruby)
* [Python](https://github.com/line/line-bot-sdk-python)