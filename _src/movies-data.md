# movies-data #

Contoh ini akan mendemonstrasikan cara untuk membuat sebuah aplikasi bot dengan **Spring framework** dan terintegrasi dengan **LINE Messaging API** dan **LINE Bot SDK** untuk memerlihaktkan kegunaan dari fitur LINE Messaging API. Data film diambil dari [OMDb API](https://www.omdbapi.com/). Aplikasi ini dijalankan di **Heroku**.

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

* Membalas pesan pengguna

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

* Mengirim pesan ke pengguna

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

* Membuat carousel template message

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

* Meninggalkan group atau room

	```java
	Response<BotApiResponse> response = LineMessagingServiceBuilder
                    .create(lChannelAccessToken)
                    .build()
                    .leaveGroup(id)
                    .execute();
    System.out.println(response.code() + " " + response.message());
	```

* Compile

`gradle clean build`

* Menambahkan ke Git Repositories

`git add .`

* Commit changes

`git commit -m "Your Messages"`

* Deploy

`git push heroku master`

* Run Server

`$ heroku ps:scale web=1`

* Open logs

`heroku logs --tail`


### Tautan ke git repository ###

[movies-data](https://github.com/line-indonesia/movies-data)
