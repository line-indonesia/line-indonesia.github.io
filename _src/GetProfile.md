#Mendapatkan Profil
Mendapatkan informasi pengguna.

####HTTP request

```GET https://api.line.me/v2/bot/profile/{userId}```

####Request headers
Request header | Deskripsi
--- | ---
Authorization | "Bearer "{Channel Access Token}

####Parameter URL
Parameter | Deskripsi
--- | ---
userId | ID pengguna

**INFO** Untuk parameter "userId", gunakan ID yang dikembalikan via webhook dari pengguna. Janggan menggunakan LINE ID yang ditemukan pada LINE app.

####Respon
```
Response body example
{
    "displayName":"LINE taro",
    "userId":"Uxxxxxxxxxxxxxx...",
    "pictureUrl":"http://obs.line-apps.com/...",
    "statusMessage":"Hello, LINE!"
}
```
Mengembalikan kode status 200 OK dan objek JSON dengan parameter sebagai berikut.

Label | Tipe | Deskripsi
--- | --- | ---
displayName | String | Nama yang ditampilkan
userId | String | ID pengguna
pictureUrl | String | URL gambar yang ditampilkan
statusMessage | String | Pesan status