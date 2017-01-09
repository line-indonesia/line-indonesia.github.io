#Leave
####HTTP request
```
POST https://api.line.me/v2/bot/group/{groupId}/leave

POST https://api.line.me/v2/bot/room/{roomId}/leave
```

####Request headers

Request header | Deskripsi
--- | ---
Authorization | "Bearer "{Channel Access Token}

####URL parameters

Parameter | Deskripsi
--- | ---
groupId | ID grup
roomId | ID room

**INFO** Gunakan ID yang dikembalikan via webhook dari source group atau room.

####Respon
Mengembalikan kode status 200 OK dan objek JSON kosong.

