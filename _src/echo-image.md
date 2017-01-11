# echo-image #

Contoh ini akan mendemonstrasikan cara untuk membuat sebuah aplikasi bot dengan **Spring framework** dan terintegrasi dengan **LINE Messaging API**, **LINE Bot SDK** dan **Cloudinary image storage** untuk mengembalikan gambar yang dikirimkan oleh pengguna via LINE Chat ke aplikasi bot anda. Aplikasi ini dijalankan di **Heroku**.

### Langkah Untuk Membuat ###
* Buat LINE@ Account dengan mengaktifkan Messaging API
> [LINE Business Center](https://business.line.me/en/)

* Register Webhook URL anda
	1. Buka [LINE Developer](https://developers.line.me/)
	2. Pilih channel anda
	3. Edit "Basic Information"
* Buat akun Cloudinary
> [Cloudinary](http://cloudinary.com)

* Tambah file  `application.properties` di direktori *src/main/resources*, dan isi dengan nama cloud, api key, dan api secret dari Cloudinary anda, serta channel secret dan channel access token anda, seperti berikut:

	```ini
com.cloudinary.cloud_name=<your_cloud_name>
com.cloudinary.api_key=<your_api_key>
com.cloudinary.api_secret=<your_api_secret>
com.linecorp.channel_secret=<your_channel_secret>
com.linecorp.channel_access_token=<your_channel_access_token>
```

* Mendapatkan gambar yang dikirim pengguna

	```java
	Response<ResponseBody> response =
        LineMessagingServiceBuilder
                .create("<channel access token>")
                .build()
                .getMessageContent("<messageId>")
                .execute();
	if (response.isSuccessful()) {
    		ResponseBody content = response.body();
    		InputStream imageStream = content.byteStream();
    		Path path = Files.createTempFile(messageId, ".jpg");
		try (FileOutputStream out = new FileOutputStream(path.toFile())) {
    			byte[] buffer = new byte[1024];
       			int len;
       			while ((len = imageStream.read(buffer)) != -1) {
       				out.write(buffer, 0, len);
       			}
     		} catch (Exception e) {
     		System.out.println("Exception is raised ");
     		}
	} else {
    	System.out.println(response.code() + " " + response.message());
	}
	```

* Menyimpan di Cloudinary

	```java
	Map uploadResult = cloudinary.uploader().upload(path.toFile(), ObjectUtils.emptyMap());
    System.out.println(uploadResult.toString());
    JSONObject jUpload = new JSONObject(uploadResult);
    uploadURL = jUpload.getString("secure_url");
	```
	**INFO** Gambar perlu disimpan karena LINE Messaging API membutuhkan URL gambar untuk mengirimkan gambar ke pengguna.
	**INFO** URL harus aman **(HTTPS)**, Maka dari itu, *secure_url* dari Objek JSON yang didapatkan dari respon Cloudinary digunakan.

* Mengirim gambar ke pengguna

	```java
	Response<BotApiResponse> response = LineMessagingServiceBuilder
            .create(lChannelAccessToken)
            .build()
            .pushMessage(pushMessage)
            .execute();
   	System.out.println(response.code() + " " + response.message());
	```


* Compile

	`gradle clean build`

* Menambahkan ke Git Repositories
	
	`git add .`

* Commit perubahan

	`git commit -m "Your Messages"`

* Deploy

	`git push heroku master`

* Run Server

	`$ heroku ps:scale web=1`

* Open logs

	`heroku logs --tail`


### Tautan ke git repository ###

[echo-image](https://github.com/line-indonesia/echo-image)
