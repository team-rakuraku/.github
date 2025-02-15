## Chat Room List

### Create Chat Room

#### Endpoint
```http
POST /chatrooms
```

#### Headers
| Key           | Value            | Description |
|--------------|----------------|-------------|
| Authorization | {token}  | JWT access token |
| App-Id       | {app_id}        | Unique identifier for the application |

#### Request Body
```json
{
  "userId": "string",
  "name": "string"
}
```

#### Response
```json
{
  "status": 201,
  "message": "Chat room created successfully"
}
```

<br/>
<br/>

### Get Chat Room List

#### Endpoint
```http
GET /chatrooms?page={page}&size={size}
```

#### Response
```json
{
  "status": 200,
  "message": "Chat room list retrieved successfully",
  "data": [
    {
      "roomId": "long",
      "lastMessage": "string",
      "lastMessageTimestamp": "date"
    }
  ]
}
```

