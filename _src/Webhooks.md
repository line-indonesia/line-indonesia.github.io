#Webhooks
Saat sebuah event terjadi , seperti saat pengguna mengirimkan pesan, permintaan HTTP POST dikirmkan ke URL webhook yang telah terkonfigurasi di Channel Console.<br>
Server bot anda akan menerima dan menangani permintaan iniuntuk event tersebut.

####Request Headers
Request Header |	Deskripsi
--- | ---
X-Line-Signature | Digunakan untuk validasi *signature*

####Request body
Request body mengandung objek JSON dengan array yang berisi objek event webhook.

Field | Type | Description
---|---|---
events	| Array dari objek event webhook | Informasi mengenai event tersebut

####Respon
Server Anda seharusnya mengembalikan kode status 200 untuk permintaan HTTP POST yang dikirimkan oleh webhook.

**INFO** Permintaan HTTP POST yang dikirimkan oleh webhook tidak akan dikirim ulang jika gagal.

#### Validasi Signature
*Signature* pada header request "X-Line-Signature" harus diverifikasi dan dikonfirmasi bahwa permintaan tersebut dikirim dari Platform LINE.

Autentikasi dijalankan sebagai berikut:

1. Dengan "Channel secret" sebagai kunci, aplikasi anda menerima nilai yang telah diolah menggunakan algoritma HMAC-SHA256 di request body.
2. Server mengonfirmasi bahwa *signature* pada request header sesuai dengan nilai yang telah diolah menggunakan Base64.
