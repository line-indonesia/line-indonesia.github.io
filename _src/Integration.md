#Integrasi Dengan LINE Messaging API

####Buat akun LINE@ dengan mengaktifkan Messaging API
1. Buka [LINE Business Center](https://business.line.me/en/), pilih **Messaging API** di dalam kategori **Service** di bagian atas halaman. Pilih **Start Messaging API** atau **Start Developer Trial**.
2. Masukkan informasi yang dibutuhkan untuk akun LINE@ anda yang baru. Pastikan informasi yang anda berikan.
3. Klik tombol **LINE@ MANAGER** di bagian bawah halaman konfirmasi untuk melanjutkan ke halaman **Bot Settings** di LINE@ Manager.
4. Di halaman **Bot Settings**, klik **Enable API**. Konfigurasi bot anda.

####Konfigurasi Bot Anda
1. Pada LINE@ Manager, buka halaman Bot Settings, yang dapat ditemukan pada pilhan "Settings" pada menu di samping.
2. Untuk menggunakan "reply message API", pilih "Allow" untuk “Use webhooks” di bawah “Request Settings”.
3. Pengaturan tambahan:
	1. Untuk bergabung dengan chat grup, pilih "Allow" untuk pilihan “Allow bots to join group chats”.
	2. Untuk mengirimkan respon pesan yang disesuaikan ke pesan yang dikirimkan pengguna, pilih "Allow" untuk pilihan “Auto Reply Message”.
	3. Untuk mengirimkan pesan sapaan saat pengguna menjadikan akun anda temannya, pilih "Allow" untuk pilihan “Greeting Message”.

####Integrasi Dengan Messaging API
1. Buka [LINE Developers](https://developers.line.me/) dan pilih **Channels** pada pojok kanan atas halaman.
2. Pilih channel yang anda ingin integrasi dengan Messaging API.
3. Pilih menu "Basic information" pada menu disamping dan klik "Edit" di bagian bawah halaman.
4. Masukkan alamat webhook anda, dan klik "Save"
5. Klik "Issue" pada kolom "Channel Access Token"
6. Klik "Show" pada kolom "Channel Secret"
7. Channel Access Token dan Channel Secret akan digunakan untuk proses autentikasi saat anda mengirimkan request.