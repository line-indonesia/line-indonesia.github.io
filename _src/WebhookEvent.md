#Objek Event Webhook

```json
{
  "events": [
    {
      "replyToken": "nHuyWiB7yP5Zw52FIkcQobQuGDXCTA",
      "type": "message",
      "timestamp": 1462629479859,
      "source": {
        "type": "user",
        "userId": "U206d25c2ea6bd87c17655609a1c37cb8"
      },
      "message": {
        "id": "325708",
        "type": "text",
        "text": "Hello, world"
      }
    },
    {
      "replyToken": "nHuyWiB7yP5Zw52FIkcQobQuGDXCTA",
      "type": "follow",
      "timestamp": 1462629479859,
      "source": {
        "type": "user",
        "userId": "U206d25c2ea6bd87c17655609a1c37cb8"
      }
    }
  ]
}
```

##Label Umum
Label | Tipe | Deskripsi
---- | ---- | ---
type | String | Indefikator tipe event
timestamp | Number | Waktu saat event terjadi (milisekon)
source | String | Objek JSON yang mengandung source dari event
##Source (Sumber)
Event memiliki beberapa source, yaitu:

* User (1-on-1 Chat)
* Group
* Room (Multiperson Chat)

####Source User (1-on-1 Chat)
Objek JSON yang mengandung pengguna sebagai source event.

Label | Tipe | Deskripsi
---- | ---- | ---
type | String | "user"
userId | String | ID Pengguna

####Source Group
Objek JSON yang mengandung group sebagai source event.

Label | Tipe | Deskripsi
---- | ---- | ---
type | String | "group"
groupId | String | ID Grup

**INFO** Anda tidak bisa mendapatkan ID dari setiap pengguna di grup.

####Source Room (Multiperson Chat)
Objek JSON yang mengandung room sebagai source event.

Label | Tipe | Deskripsi
---- | ---- | ---
type | String | "room"
roomId | String | ID Room

**INFO** Anda tidak bisa mendapatkan ID dari setiap pengguna di grup.

##Tipe Event
Event memiliki beberapa tipe, yaitu:

* Message Event
* Follow Event
* Unfollow Event
* Join Event
* Leave Event
* Postback Event

###Message Event
-----
Objek event yang mengandung pesan yang dikirmkan. Label "message" mengandung objek pesan yang berhubungan dengan tipe pesan. Anda dapat membalas event pesan.

Label | Tipe | Deskripsi
---- | ---- | ---
type | String | "message"
replyToken | String | Token untuk membalas event ini
message | Text<br>Image<br>Video<br>Audio<br>Location<br>Sticker | Konten dari pesan

####Text Message (Pesan Teks)
Objek Pesan yang mengandung teks yang dikirimkan dari source.

Label | Tipe | Deskripsi
---- | ---- | ---
id | String | ID Pesan
type | String | "text"
text | String | Isi pesan

####Image Message (Pesan Gambar)
Objek pesan yang mengandung gambar yang dikirimkan dari source. Data biner dari gambar bisa didapatkan menggunakan Content API.

Label | Tipe | Deskripsi
---- | ---- | ---
id | String | ID Pesan
type | String | "image"

####Video Message (Pesan Video)
Objek pesan yang mengandung video yang dikirimkan dari source. Data biner dari video bisa didapatkan menggunakan Content API.

Label | Tipe | Deskripsi
---- | ---- | ---
id | String | ID Pesan
type | String | "video	"

####Audio Message (Pesan Audio)
Objek pesan yang mengandung audio yang dikirimkan dari source. Data biner dari audio bisa didapatkan menggunakan Content API.

Label | Tipe | Deskripsi
---- | ---- | ---
id | String | ID Pesan
type | String | "audio"

####Location Message (Pesan Lokasi)
Objek pesan yang mengandung lokasi yang dikirimkan dari source.

Label | Tipe | Deskripsi
---- | ---- | ---
id | String | ID Pesan
type | String | "location"
title | String | Judul
address | String | Alamat
latitude | Decimal | Latitude
longitude | Decimal | Longitude

####Sticker Message (Pesan Stiker)
Objek pesan yang mengandung stiker yang dikirimkan dari source.

Label | Tipe | Deskripsi
---- | ---- | ---
id | String | ID Pesan
type | String | "sticker"
packageId | String | ID Paket Stiker
stickerId | String | ID Stiker

###Follow Event
-----
Objek event saat akun anda dijadikan teman atau tidak diblokir lagi. Anda dapat membalas ke event ini.

Label | Tipe | Deskripsi
---- | ---- | ---
type | String | "follow"
replyToken | String | Token untuk membalas event ini.

###Unfollow Event
-----
Objek event saat akun anda diblokir.

Label | Tipe | Deskripsi
---- | ---- | ---
type | String | "unfollow"

###Join Event
-----
Objek event saat akun anda bergabung sebuah grup atau room. Anda dapat membalas event ini.

Label | Tipe | Deskripsi
---- | ---- | ---
type | String | "join"
replyToken | String | Token untuk membalas event ini.

###Leave Event
-----
Objek event saat akun anda meninggalkan sebuah grup.

Label | Tipe | Deskripsi
---- | ---- | ---
type | String | "leave"

**INFO** Tidak ada event yg dihasilkan saat anda meninggalkan sebuah room.<br>
**INFO** Event ini tidak akan dihasilkan jika anda menggunakan Leave API untuk keluar sendiri dari grup atau room.

###Postback Event
-----
Objek event saat pengguna melakukan aksi pada "Template Message" yang menginisiasi postback. Anda dapat membalas event ini.

Label | Tipe | Deskripsi
---- | ---- | ---
type | String | "postback"
replyToken | String | Token untuk membalas event ini.
postback.data | String | Postback data