## Authentication

### Login

#### Endpoint
```http
POST /auth/login
```

#### Headers
| Key           | Value            | Description |
|--------------|----------------|-------------|
| Authorization |  {token}  | JWT access token |
| App-Id       | {app_id}        | Unique identifier for the application |

#### Request Body
```json
{
  "userId": "string",
  "nickname": "string",
  "profileImageUrl": "string"
}
```

#### Response
```json
{
  "status": 200,
  "message": "success",
  "userId": "string",
  "expiresAt": "date"
}
```
