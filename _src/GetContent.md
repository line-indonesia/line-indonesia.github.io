#Mendapatkan Content
Mengambil gambar, video, dan audio yang dikirimkan oleh pengguna.

####HTTP request

```GET https://api.line.me/v2/bot/message/{messageId}/content```

####Request headers

Request header | Deskripsi
--- | ---
Authorization | "Bearer "{Channel Access Token}

####Parameter URL

Parameter | Deskripsi
--- | ---
messageId | ID pesan

####Respon
Mengembalikan kode status 200 OK dan konten dalam biner.

**INFO** Konten akan secara otomatis dihapus setelah beberapa waktu tertentu. Tidak ada waktu pasti seberapa lama konten akan disimpan.