# bot-phonebook #

Contoh ini akan mendemonstrasikan cara untuk membuat sebuah aplikasi bot dengan **Spring framework** dan terintegrasi dengan **LINE Messaging API** dan **Line Bot SDK**, **PostgreSQL** untuk registrasi dan mendapatkan data dari bot yang layaknya sebuah buku telepon yang dikirimkan oleh pengguna via LINE Chat ke aplikasi bot anda. Aplikasi ini dijalankan di **Heroku**.

### Langkah Untuk Membuat ###
* Buat LINE@ Account dengan mengaktifkan Messaging API
> [LINE Business Center](https://business.line.me/en/)

* Register Webhook URL anda
	1. Buka [LINE Developer](https://developers.line.me/)
	2. Pilih channel anda
	3. Edit "Basic Information"
* Buat akun Cloudinary
> [Cloudinary](http://cloudinary.com)

* Tambah file  `application.properties` di direktori *src/main/resources*, dan isi dengan channel secret dan channel access token anda, seperti berikut:

	```ini
com.linecorp.channel_secret=<your_channel_secret>
com.linecorp.channel_access_token=<your_channel_access_token>
	```
	
* Buka Heroku Postgres

	```bash
	$ heroku psql
	```

* Siapkan tabel `phonebook`

	```sql
	CREATE TABLE IF NOT EXISTS phonebook
	(
		id BIGSERIAL PRIMARY KEY,
		name TEXT,
		phone_number TEXT
	);
	```	

* Compile
 
    ```bash
    $ gradle clean build
    ```
* Deploy
 	
 	```bash
	$ git push heroku master
	```  

* Run Server

    ```bash
    $ heroku ps:scale web=1
    ```

* Penggunaan
    
    Ada dua kata kunci yang bisa digunakan dengan bot ini, yaitu **find** dan **reg**

Template pesan untuk find:
> find "Your_Name"<br><br>
> **INFO** Tanda kutip dua (") harus digunakan. Jika tidak digunakan, maka katakunci tidak akan dikenali oleh bot.
    
Template pesan untuk reg:
> reg "Your_Name" #Your_Phone_Number<br><br>
> **INFO** Tanda kutip dua (") dan tanda pagar (#) harus digunakan. Jika tidak digunakan, maka kata kunci tidak akan dikenali oleh bot.


### Tautan ke git repository ###

[bot-phonebook](https://github.com/line-indonesia/bot-phonebook)
