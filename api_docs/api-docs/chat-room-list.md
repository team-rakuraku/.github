# Chat Room List

## Create Chat Room

### Endpoint
```http
POST /chatrooms
```

### Headers
| Key           | Value            |
|--------------|----------------|
| Authorization | Bearer {token}  |
| App-Id       | {app_id}        |

### Request Body
```json
{
  "userId": "string",
  "name": "string"
}
```

### Response
```json
{
  "status": 201,
  "message": "방 생성 성공"
}
```


<br/>

## Get Chat Room List

### Endpoint
```http
GET /chatrooms?page={page}&size={size}
```

### Response
```json
{
  "status": 200,
  "message": "방 목록 가져오기 성공",
  "data": [
    {
      "roomId": "long",
      "lastMessage": "string",
      "lastMessageTimestamp": "date"
    }
  ]
}
```
