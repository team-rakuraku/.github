# Authentication

## Login

### Endpoint
```http
POST /auth/login
```

### Headers
| Key           | Value            |
|--------------|----------------|
| Authorization | {token}     |
| App-Id       | {app_id}        |

### Request Body
```json
{
  "userId": "string",
  "nickname": "string",
  "profileImageUrl": "string"
}
```

### Response
```json
{
  "status": 200,
  "message": "success",
  "userId": "string",
  "expiresAt": "date"
}
```

