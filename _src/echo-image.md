# echo-image #

Contoh ini akan mendemonstrasikan cara untuk membuat sebuah aplikasi bot dengan **Spring framework** dan terintegrasi dengan **LINE Messaging API**, **LINE Bot SDK** dan **Cloudinary image storage** untuk mengembalikan gambar yang dikirimkan oleh pengguna via LINE Chat ke aplikasi bot anda. Aplikasi ini dijalankan di **Heroku**.

### Langkah Untuk Membuat ###
* Pertama, anda harus membuat akun LINE@, mengaktifkan Messaging API, memasukkan URL dari Webhook anda dengan [cara ini](Integration.html), dan [membuat akun Cloudinary](cloudinary-overview.html).

* Selanjutnya, tambah file  `application.properties` di direktori *src/main/resources*, dan isi dengan nama cloud, api key, dan api secret dari Cloudinary anda, serta channel secret dan channel access token anda, seperti berikut:

	```ini
com.cloudinary.cloud_name=<your_cloud_name>
com.cloudinary.api_key=<your_api_key>
com.cloudinary.api_secret=<your_api_secret>
com.linecorp.channel_secret=<your_channel_secret>
com.linecorp.channel_access_token=<your_channel_access_token>
```

* Untuk mendapatkan konten yang dikirimkan oleh pengguna, anda dapat menggunakan **Get Content API**. Pada contoh ini akan didapatkan gambar yang dikirim pengguna.

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

* Konten yang didapatkan dari Get Content API merupakan *binary data*, maka dari itu, anda perlu menyimpannya terlebih dahulu pada sebuah storage, sebelum dapat dikirimkan kembali ke pengguna.

	```java
	Map uploadResult = cloudinary.uploader().upload(path.toFile(), ObjectUtils.emptyMap());
    System.out.println(uploadResult.toString());
    JSONObject jUpload = new JSONObject(uploadResult);
    uploadURL = jUpload.getString("secure_url");
	```
	**INFO** Gambar perlu disimpan karena LINE Messaging API membutuhkan URL gambar untuk mengirimkan gambar ke pengguna.<br>
	**INFO** URL harus aman **(HTTPS)**, Maka dari itu, *secure_url* dari Objek JSON yang didapatkan dari respon Cloudinary digunakan.

* Untuk mengirim kembali ke pengguna, maka digunakan **Push Message API**. Pada contoh ini, digunakan Java SDK.

	```java
	Response<BotApiResponse> response = LineMessagingServiceBuilder
            .create(lChannelAccessToken)
            .build()
            .pushMessage(pushMessage)
            .execute();
   	System.out.println(response.code() + " " + response.message());
	```
	Dari source code diatas, terkomposisi data JSON dibawah. Untuk mengirimkan pesan ini, digunakan metode pengiriman dengan **Push Message API** maka dari itu, anda membutuhkan **id** dari target pengiriman.
	
	```JSON
	{
		"to":<target's_id>,
		"messages":
		[
			{
				"type":"image",
				"originalContentUrl":<secure_url>,
				"previewImageUrl":<secure_url>
			}
		]
	}
	```
* Setelah selesai membuat aplikasi anda, anda dapat menjalankan aplikasi anda dengan [cara ini](heroku-overview.html).

### Tautan ke git repository ###

[echo-image](https://github.com/line-indonesia/echo-image)
