# Message

## Send Message

### WebSocket Endpoint
```ws
/ws/{roomId}
```

### Message Payload
```json
{
  "appId": "string",
  "usersId": "string",
  "content": "string",
  "roomId": "string",
  "type": "CHAT"
}
```

### Receive Message
```json
{
  "roomId": "string",
  "userId": "string",
  "content": "string",
  "time": "string",
  "type": "CHAT"
}
