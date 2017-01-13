#Servis Pendukung

LINE Messaging API merupakan sebuah antarmuka pemrograman aplikasi yang memungkinkan sebuah program untuk menerima pesan, mengirim dan membalas pesan, dan mendapatkan profil pengguna dari LINE Chat.

LINE Messaging API sendiri tidak dapat digunakan sendiri. Dibutuhkan pula komponen-komponen berikut pada implementasi dasarnya: 

* **Framework** untuk membangun aplikasi dimana API diimplementasikan.
* **PaaS** sebagai platform untuk mengembangkan, mengelola, dan menjalankan aplikasi tanpa membangun dan memelihara infrastruktur.
* **Database** untuk menyimpan informasi.
* **Storage** untuk menyimpan file yang didapatkan dari aplikasi.

Servis Pendukung yang digunakan dalam pembuatan contoh aplikasi dengan LINE Messaging API kali ini adalah:

1. **Framework** Spring
2. **PaaS** Heroku
3. **Database** PostgreSQL
4. **Storage** Cloudinary

Pada pembahasan kali ini, akan dibahas lebih jauh mengenai **PaaS** dan **Storage** yang digunakan, dan bagaimana cara untuk mengintegrasikan aplikasi dengan kedua komponen tersebut.