# Authentication

## Login

### Endpoint

```http
POST /auth/login
```

### Headers

| Key           | Value     | Description                           |
| ------------- | --------- | ------------------------------------- |
| Authorization | {token}   | JWT access token                      |
| App-Id        | {app\_id} | Unique identifier for the application |

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



### **JWT Access Token**&#x20;

**Access Token Payload**

```json
{
  "sub": "user123",  // 사용자 고유 ID
  "app_id": "rakuraku3",  // 애플리케이션 ID
  "iat": 1705080000,  // 발급 시간 (Issued At, Unix timestamp)
  "exp": 1705086400  // 만료 시간 (Expiration, Unix timestamp)
}
```

| **Key** | **Type** | **설명**                    |
| ------- | -------- | ------------------------- |
| **sub** | string   | 사용자 고유 ID                 |
| **iat** | int      | 토큰 발급 시간 (Unix timestamp) |
| **exp** | int      | 토큰 만료 시간 (Unix timestamp) |

***

**JWT 알고리즘**

* **알고리즘**: `HS256` (HMAC-SHA256)
*   **Signature 생성 방식**:

    ```
    HMACSHA256(
      base64UrlEncode(header) + "." + base64UrlEncode(payload), 
      secretKey
    )
    ```
