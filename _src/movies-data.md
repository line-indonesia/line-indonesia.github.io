# movies-data #

Contoh ini akan mendemonstrasikan cara untuk membuat sebuah aplikasi bot dengan **Spring framework** dan terintegrasi dengan **LINE Messaging API** dan **LINE Bot SDK** untuk memerlihaktkan kegunaan dari fitur LINE Messaging API. Data film diambil dari [OMDb API](https://www.omdbapi.com/). Aplikasi ini dijalankan di **Heroku**.

### Langkah Untuk Membuat ###
* Pertama, anda harus membuat akun LINE@, mengaktifkan Messaging API, dan memasukkan URL dari Webhook anda dengan [cara ini](Integration.html).

* Selanjutnya, tambah file  `application.properties` di direktori *src/main/resources*, dan isi dengan channel secret dan channel access token anda, seperti berikut:

	```ini
com.linecorp.channel_secret=<your_channel_secret>
com.linecorp.channel_access_token=<your_channel_access_token>
	```
* Pada saat anda menerima sebuah event, maka anda akan mendapatkan data JSON:

	```JSON
	{
		"events":
		[
			{
				"type":"message",
				"replyToken":"610147d637dc4ef091cb47ca45289ba6",
				"source":
				{
					"userId":<target's_user_id>,
					"type":"user"
				},
				"timestamp":1484622624865,
				"message":
				{
					"type":"text",
					"id":"5513240775730",
					"text":"title \"Iron Man\""
				}
			}
		]
	}
	```
	Dari data ini anda bisa mendapatkan tipe dari event, replyToken, siapa yang melakukan event tersebut, dan detail lainnya dari event.

* Untuk membalas sebuah event pesan dari pengguna, anda dapat menggunakan **Reply Message API**. Pada contoh ini, digunakan Java SDK.

	```java
	TextMessage textMessage = new TextMessage(messageToUser);
   	ReplyMessage replyMessage = new ReplyMessage(rToken, textMessage);
   	try {
   		Response<BotApiResponse> response = LineMessagingServiceBuilder
                .create(lChannelAccessToken)
                .build()
                .replyMessage(replyMessage)
                .execute();
      	System.out.println("Reply Message: " + response.code() + " " + response.message());
     } catch (IOException e) {
        	System.out.println("Exception is raised ");
            e.printStackTrace();
        }
	```
	Dari source code diatas, terkomposisi data JSON dibawah. Anda hanya memerlukan **replyToken** untuk membalas pesan, tidak perlu menggunakan id dari target.
	
	```JSON
	{
		"replyToken":"<replyToken>",
		"messages":
		[
			{
				"type":"text",
				"text":"Plot: After being held captive in an Afghan cave, billionaire engineer Tony Stark creates a unique weaponized suit of armor to fight evil."
			}
		]
	}
	```

* Untuk mengirim pesan ke pengguna tertentu, anda dapat menggunakan **Push Message API**. Pada contoh ini, digunakan Java SDK.

	```java
	TextMessage textMessage = new TextMessage(txt);
    PushMessage pushMessage = new PushMessage(sourceId,textMessage);
    try {
    	Response<BotApiResponse> response = LineMessagingServiceBuilder
            .create(lChannelAccessToken)
            .build()
            .pushMessage(pushMessage)
            .execute();
        System.out.println(response.code() + " " + response.message());
    } catch (IOException e) {
            System.out.println("Exception is raised ");
            e.printStackTrace();
        }
	```
	Dari source code diatas, terkomposisi data JSON dibawah. Untuk mengirimkan pesan ini, anda membutuhkan **id** dari target pengiriman.
	
	```JSON
	{
		"to":"<target's_id>",
		"messages":
		[
			{
				"type":"text",
				"text":"plot \"iron man\" - user\uDBC0\uDC8D"
			}
		]
	}
	```

* Pada Messaging API terdapat sebuah jenis pesan yang disebut **Template Message**. Pada contoh ini, digunakan salah satu template message yaitu **Carousel Template**. Cara membuat carousel template message:

	```java
	CarouselTemplate carouselTemplate = new CarouselTemplate(
                    Arrays.asList(new CarouselColumn
                                    (poster_url, title, "Select one for more info", Arrays.asList
                                        (new MessageAction("Full Data", "Title \"" + title + "\""),
                                         new MessageAction("Summary", "Plot \"" + title + "\""),
                                         new MessageAction("Poster", "Poster \"" + title + "\""))),
                                  new CarouselColumn
                                    (poster_url, title, "Select one for more info", Arrays.asList
                                        (new MessageAction("Released Date", "Released \"" + title + "\""),
                                         new MessageAction("Actors", "Actors \"" + title + "\""),
                                         new MessageAction("Awards", "Awards \"" + title + "\"")))));
   TemplateMessage templateMessage = new TemplateMessage("Your search result", carouselTemplate);
    PushMessage pushMessage = new PushMessage(sourceId,templateMessage);
	```
	Dari source code diatas, terkomposisi data JSON dibawah. Untuk mengirimkan pesan ini, digunakan metode pengiriman dengan **Push Message API** maka dari itu, anda membutuhkan **id** dari target pengiriman.
	
	```JSON
	{
		"to":"<target's_id>",
		"messages":
		[
			{
				"type":"template",
				"altText":"Your search result",
				"template":
				{
					"type":"carousel",
					"columns":
					[
						{
							"thumbnailImageUrl":"https://images-na.ssl-images-amazon.com/images/M/MV5BMTczNTI2ODUwOF5BMl5BanBnXkFtZTcwMTU0NTIzMw@@._V1_SX300.jpg",
							"title":"Iron Man",
							"text":"Select one for more info",
							"actions":
							[
								{
									"type":"message",
									"label":"Full Data",
									"text":"Title \"Iron Man\""
								},
								{
									"type":"message",
									"label":"Summary",
									"text":"Plot \"Iron Man\""
								},
								{
									"type":"message",
									"label":"Poster",
									"text":"Poster \"Iron Man\""
								}
							]
						},
						{
							"thumbnailImageUrl":"https://images-na.ssl-images-amazon.com/images/M/MV5BMTczNTI2ODUwOF5BMl5BanBnXkFtZTcwMTU0NTIzMw@@._V1_SX300.jpg",
							"title":"Iron Man",
							"text":"Select one for more info",
							"actions":
							[
								{
									"type":"message",
									"label":"Released Date",
									"text":"Released \"Iron Man\""
								},
								{
									"type":"message",
									"label":"Actors",
									"text":"Actors \"Iron Man\""
								},
								{
									"type":"message",
									"label":"Awards",
									"text":"Awards \"Iron Man\""
								}
							]
						}
					]
				}
			}
		]
	}

	```

* Salah satu fitur dari Messaging API adalah anda dapat meninggalkan group atau room dengan menggunakan **Leave API**. Pada contoh di bawah, digunakan Java SDK.

	```java
	Response<BotApiResponse> response = LineMessagingServiceBuilder
                    .create(lChannelAccessToken)
                    .build()
                    .leaveGroup(id)
                    .execute();
    System.out.println(response.code() + " " + response.message());
	```
	Leave API hanya akan mengirimkan JSON kosong saat berhasil.
* Contoh ini menggunakan `CloseableHttpAsyncClient` untuk mengambil data dari **OMDb API** karena saat menggunakan protokol `HttpClient` hanya dua request ke OMDb API yang dilayani, dan selebihnya akan menghasilkan "Request Timeout". 

	```java
	CloseableHttpAsyncClient c = HttpAsyncClients.createDefault();
        
	try{
   		c.start();
       	//Use HTTP Get to retrieve data
       HttpGet get = new HttpGet(URI);
            
       Future<HttpResponse> future = c.execute(get, null);
       HttpResponse responseGet = future.get();
       System.out.println("HTTP executed");
       System.out.println("HTTP Status of response: " + responseGet.getStatusLine().getStatusCode());
            
       // Get the response from the GET request
       BufferedReader brd = new BufferedReader(new InputStreamReader(responseGet.getEntity().getContent()));
            
       StringBuffer resultGet = new StringBuffer();
       String lineGet = "";
       while ((lineGet = brd.readLine()) != null) {
       		resultGet.append(lineGet);
       }
       System.out.println("Got result");
            
       // Change type of resultGet to JSONObject
       jObjGet = resultGet.toString();
       System.out.println("OMDb responses: " + jObjGet);
	} catch (InterruptedException | ExecutionException e) {
		System.out.println("Exception is raised ");
       	e.printStackTrace();
   } finally {
       	c.close();
   }

	```

* Setelah selesai membuat aplikasi anda, anda dapat menjalankan aplikasi anda dengan [cara ini](heroku-overview.html).

### Tautan ke git repository ###

[movies-data](https://github.com/line-indonesia/movies-data)
