#Objek Send Message
Objek JSON yang berisi konten dari pesan yang akan dikirim.

####Text (Teks)
Contoh text (teks)

```json
{
    "type": "text",
    "text": "Hello, world"
}
```

Label | Tipe | Deskripsi
--- | --- | ---
type | String | "text"
text | String | 	Teks pesan, Max: 2000 karakter

####Image (Gambar)
Contoh image (gambar)

```json
{
    "type": "image",
    "originalContentUrl": "https://example.com/original.jpg",
    "previewImageUrl": "https://example.com/preview.jpg"
}
```

Label | Tipe | Deskripsi
--- | --- | ---
type | String | "image"
originalContentUrl | String | Image URL<br>(Max: 1000 karakter)<br>**HTTPS**<br>JPEG<br>Max: 1024 x 1024<br>Max: 1 MB
previewImageUrl | String | Preview image URL<br>(Max: 1000 karakter)<br>**HTTPS**<br>JPEG<br>Max: 240 x 240<br>Max: 1 MB

####Video
Contoh video

```json
{
    "type": "video",
    "originalContentUrl": "https://example.com/original.mp4",
    "previewImageUrl": "https://example.com/preview.jpg"
}
```

Label | Tipe | Deskripsi
--- | --- | ---
type | String | "video"
originalContentUrl | String | URL dari file video<br>(Max: 1000 karakter)<br>**HTTPS**<br>mp4 <br>Less than 1 minute<br>Max: 10 MB
previewImageUrl | String | URL dari preview image<br>(Max: 1000 karakter)<br>**HTTPS**<br>JPEG <br>Max: 240 x 240<br>Max: 1 MB

####Audio
Contoh audio

```json
{
    "type": "audio",
    "originalContentUrl": "https://example.com/original.m4a",
    "duration": 240000
}
```


Label | Type | Deskripsi
--- | --- | ---
type | String | "audio"
originalContentUrl | String | URL dari file audio (Max: 1000 karakter)<br>**HTTPS**<br>m4a<br>Less than 1 minute<br>Max 10 MB
duration | Number | Durasi dari file audio (milisekon)

####Location (Lokasi)
Contoh location (lokasi)

```json
{
    "type": "location",
    "title": "my location",
    "address": "〒150-0002 東京都渋谷区渋谷２丁目２１−１",
    "latitude": 35.65910807942215,
    "longitude": 139.70372892916203
}
```
Label | Tipe | Deskripsi
--- | --- | ---
type | String | "location"
title | String | Judul, Max: 100 karakter
address | String | Alamat, Max: 100 karakter
latitude | Decimal | Latitude
longitude | Decimal | Longitude

####Sticker (Stiker)
Contoh sticker (stiker)

```json
{
  "type": "sticker",
  "packageId": "1",
  "stickerId": "1"
}
```
Untuk daftar ID stiker yang dikirim melalui Messaging API, lihat [Daftar Stiker](https://devdocs.line.me/files/sticker_list.pdf).

Label | Tipe | Deskripsi
--- | --- | ---
type | String | "sticker"
packageId | String | ID Paket
stickerId | String | ID Stiker