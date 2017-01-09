#Template messages
Template messages adalah pesan dengan layout yang telah didefinisikan terlebih dahulu dan dapat anda sesuaikan. Ada tiga tipe template yang tersedia dan dapat digunakan untuk berinteraksi dengan pengguna melalui bot anda.

Label | Tipe | Deskripsi
--- | --- | ---
type | String | "template"
altText | String | Teks alternatif untuk perangkat yang tidak mendukung<br>Max: 400 karakter
template | Buttons<br>Confirm<br>Carousel | Objek dengan konten sebuah template
**INFO** Template messages hanya didukung pada LINE iOS/Android versi 6.7.0 ke atas.

####Buttons
Contoh buttons template message

```json
{
  "type": "template",
  "altText": "this is a buttons template",
  "template": {
      "type": "buttons",
      "thumbnailImageUrl": "https://example.com/bot/images/image.jpg",
      "title": "Menu",
      "text": "Please select",
      "actions": [
          {
            "type": "postback",
            "label": "Buy",
            "data": "action=buy&itemid=123"
          },
          {
            "type": "postback",
            "label": "Add to cart",
            "data": "action=add&itemid=123"
          },
          {
            "type": "uri",
            "label": "View detail",
            "uri": "http://example.com/page/123"
          }
      ]
  }
}
```

Buttons adalah template message dengan gambar, judul, teks, dan beberapa tombol aksi.

![Gambar buttons template](https://devdocs.line.me/images/buttons.png)

Label | Tipe | Deskripsi
--- | --- | ---
type | String | "buttons"
thumbnailImageUrl | String | URL gambar (Max: 1000 karakter)<br>**HTTPS**<br>JPEG or PNG<br>Aspect ratio: 1:1.51<br>Lebar max: 1024px<br>Max: 1 MB
title | String | Judul<br>Max: 40 karakter
text | String | Pesan teks<br>Max: 160 karakter (tanpa gambar dan judul)<br>Max: 60 characters (dengan gambar dan judul)
actions | Array dari template actions | Aksi saat diketuk<br>Max: 4
Label "thumbnailImageUrl" and "title" opsional

**INFO** Karena terbatasnya tinggi pesan buttons template, bagian bawah dari area yang menampilkan "text" akan dipotong jika melebihi batas. Untuk alasan ini, tergantung dengan lebar karakter, pesan teks mungkin tidak ditampilkan seluruhnya walaupun belum melebihi batas karakter maksimal.

####Confirm

Contoh confirm template message

```json
{
  "type": "template",
  "altText": "this is a confirm template",
  "template": {
      "type": "confirm",
      "text": "Are you sure?",
      "actions": [
          {
            "type": "message",
            "label": "Yes",
            "text": "yes"
          },
          {
            "type": "message",
            "label": "No",
            "text": "no"
          }
      ]
  }
}
```

Template message dengan dua tombol aksi.

![Gammbar confirm template](https://devdocs.line.me/images/confirm.png)

Field | Type | Description
--- | --- | ---
type | String | "confirm"
text | String | Pesan teks<br>Max: 240 karakter
actions | Array dari template actions | Aksi saat diketuk<br>Max: 2
**INFO** Karena terbatasnya tinggi pesan confirm template, bagian bawah dari area yang menampilkan "text" akan dipotong jika melebihi batas. Untuk alasan ini, tergantung dengan lebar karakter, pesan teks mungkin tidak ditampilkan seluruhnya walaupun belum melebihi batas karakter maksimal.

####Carousel

Contoh carousel template message

```json
{
  "type": "template",
  "altText": "this is a carousel template",
  "template": {
      "type": "carousel",
      "columns": [
          {
            "thumbnailImageUrl": "https://example.com/bot/images/item1.jpg",
            "title": "this is menu",
            "text": "description",
            "actions": [
                {
                    "type": "postback",
                    "label": "Buy",
                    "data": "action=buy&itemid=111"
                },
                {
                    "type": "postback",
                    "label": "Add to cart",
                    "data": "action=add&itemid=111"
                },
                {
                    "type": "uri",
                    "label": "View detail",
                    "uri": "http://example.com/page/111"
                }
            ]
          },
          {
            "thumbnailImageUrl": "https://example.com/bot/images/item2.jpg",
            "title": "this is menu",
            "text": "description",
            "actions": [
                {
                    "type": "postback",
                    "label": "Buy",
                    "data": "action=buy&itemid=222"
                },
                {
                    "type": "postback",
                    "label": "Add to cart",
                    "data": "action=add&itemid=222"
                },
                {
                    "type": "uri",
                    "label": "View detail",
                    "uri": "http://example.com/page/222"
                }
            ]
          }
      ]
  }
}
```
Template message dengan beberapa kolom yang dapat berputar seperti carousel.

![Gambar carousel template](https://devdocs.line.me/images/carousel.png)

Label | Tipe | Deskripsi
--- | --- | ---
type | String | "carousel"
columns | Array dari column objects | Array of kolom<br>Max: 5

#####Column object

Label | Tipe | Deskripsi
--- | --- | ---
thumbnailImageUrl | String | URL gambar (Max: 1000 karakter)<br>**HTTPS**<br>JPEG or PNG<br>Aspect ratio: 1:1.51<br>Lebar max: 1024px<br>Max: 1 MB
title | String | Judul<br>Max: 40 karakter
text | String | Teks pesan<br>Max: 120 karakter (tanpa gambar atau judul)<br>Max: 60 karakter (dengan gambar atau judul)
actions | Array dari template actions | Aksi saat diketuk<br>Max: 3

"thumbnailImageUrl" dan "title"untuk setiap kolom opsional.

**INFO** Karena terbatasnya tinggi pesan carousel template, bagian bawah dari area yang menampilkan "text" akan dipotong jika melebihi batas. Untuk alasan ini, tergantung dengan lebar karakter, pesan teks mungkin tidak ditampilkan seluruhnya walaupun belum melebihi batas karakter maksimal.

**INFO** Banyaknya aksi untuk semua kolom harus sama. Jika anda menggunakan gambar atau judul untuk sebuah kolom, pastikan seluruh kolom juga menggunakannya.

####Template action
Aksi yang dapat dimasukkan ke template message anda.

#####Postback action
Saat aksi ini dipilih, sebuah postback event akan dikembalikan via webhook dengan string spesifik dalam label "data".

Jika anda mengisi pada label "text", string akan dikirim sebagai pesan dari pengguna.

Label | Tipe | Deskripsi
--- | --- | ---
type | String | "postback"
label | String | Label untuk aksi<br>Max: 20 karakter
data | String | String dikembalikan via webhook pada postback.data di event postback<br>Max: 300 karakter
text | String | Teks dikirim saat aksi dilakukan<br>Max: 300 karakter
"text" opsional.

#####Message Action
Saat aksi ini dipilih, teks akan dikirimkan sebagai pesan dari pengguna.

Label | Tipe | Deskripsi
--- | --- | ---
type | String | "message"
label | String | Label untuk aksi<br>Max: 20 karakter
text | String | Teks dikirim saat aksi dilakukan<br>Max: 300 karakter

#####URI Action
Saat aksi ini dipilih, URI yang ditentukan akan dibuka.

Label | Tipe | Deskripsi
--- | --- | ---
type | String | "uri"
label | String | Label untuk aksi<br>Max: 20 karakter
uri | String | URI akan dibuka ketika aksi dilakukan (Max: 1000 karakter)<br>**http, https, tel**