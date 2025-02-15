## Messaging

### Send Message

#### WebSocket Endpoint
```ws
/ws/{roomId}
```

#### Message Payload
```json
{
  "appId": "string",
  "usersId": "string",
  "content": "string",
  "roomId": "string",
  "cloudFrontImageURL": "string",
  "type": "CHAT"
}
```

<br/>
<br/>

### Receive Message

#### Response Payload
```json
{
  "roomId": "string",
  "userId": "string",
  "content": "string",
  "time": "string",
  "cloudFrontImageURL": "string",
  "type": "CHAT"
}
```
