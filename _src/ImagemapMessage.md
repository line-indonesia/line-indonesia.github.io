#Pesan Imagemap

Imagemaps adalah gambar dengan satu atau lebih tautan. Anda dapat menentukan sebuah tautan untuk seluruh gambar atau beberapa tautan yang berhubungan dengan area yang berbeda di gambar.

Contoh JSON dari Imagemap dengan duah buah daerah yang dapat diketuk, kiri dan kanan.

```json
{
  "type": "imagemap",
  "baseUrl": "https://example.com/bot/images/rm001",
  "altText": "this is an imagemap",
  "baseSize": {
      "height": 1040,
      "width": 1040
  },
  "actions": [
      {
          "type": "uri",
          "linkUri": "https://example.com/",
          "area": {
              "x": 0,
              "y": 0,
              "width": 520,
              "height": 1040
          }
      },
      {
          "type": "message",
          "text": "hello",
          "area": {
              "x": 520,
              "y": 0,
              "width": 520,
              "height": 1040
          }
      }
  ]
}
```

Label | Tipe | Deskripsi
--- | --- | ---
type | String | "imagemap"
baseUrl | String | URL untuk gambar dasar<br>(Max: 1000 karakter)<br>**HTTPS**
altText | String | Teks Alternatif<br>Max: 400 karaketer
baseSize.width | Number | Lebar dari gambar dasar (Atur ke 1040px）
baseSize.height | Number | Tinggi dari gambar dasar (Atur untuk sesuai dengan lebar 1040px）
actions | Array dari objek Imagemap action object | Aksi saat diketuk<br>Max: 50

####Base URL
Untuk menggunakan imagemap, anda harus memasukkan URL dengan lebar gambar(px) di akhir URL dasar, sehingga klien dapat mengunduh gambar sesuai resolusi yang dibutuhkan.

Sebagai contoh, jika URL dasar adalah,
`https://example.com/images/cats`<br>
URL untuk devais klien untuk mengunduh gambar sebesar 700px adalah
`https://example.com/images/cats/700`

Dibawah ini adalah resolusi gambar yang dibutuhkan oleh devais klien.
Lebar: 240px, 300px, 460px, 700px, 1040px

Gambar yang digunakan untuk imagemap harus memenuhi spesifikasi:

* Image format: JPEG or PNG
* File size: Up to 1 MB

#####Imagemap action object
Objek yang menspesifikasikan aksi dan area yang dapat di ketuk dari sebuah imagemap.

Saat sebuah area diketuk, pengguna diarahkan ke URI yang ditentukan di "uri" dan pesan yang ditentukan di "message" akan dikirimkan.

####URI action

Label | Tipe | Deskripsi
--- | --- | ---
type | String | "uri"
linkUri | String | Webpage URL<br>Max: 1000 characters
area | Objek imagemap area | Pendefinisian area yang dapat diketuk

####Message action

Label | Tipe | Deskripsi
type | String | "message"
text | String | Pesan yang akan dikirim<br>Max: 400 characters
area | Objek imagemap | Pendefinisian area yang dapat diketuk

####Objek imagemap area
Mendefinikan besar dari imagemap secara keseluruhan dengan lebas 1040px. Pojok kiri atas adalah titik origin dari area.

Label | Tipe | Deskripsi
--- | --- | ---
x | Number | Posisi horisontal dari area yang bisa diketuk
y | Number | Posisi vertical dari area yang dapat diketuk
width | Number | Lebar dari area yang dapat diketuk
height | Number | Tinggi dari area yang dapat diketuk
