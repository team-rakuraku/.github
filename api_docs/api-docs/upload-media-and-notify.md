
### **1. Request S3 Upload URL **

사용자가 업로드할 파일을 위한 **S3 서명된 URL**을 요청하는 REST API입니다.

**Method:**  
<mark style="color:green;">`POST`</mark> `/media/upload-url`

**Headers**

| Name            | Value              |
| --------------- | ------------------ |
| `Content-Type`  | `application/json` |
| `Authorization` | `{ access token }` |
| `App-Id`        | `{ app id }`       |

**Body**

| Name       | Type   | Description                |
| ---------- | ------ | -------------------------- |
| `fileName` | string | 업로드할 파일 이름 (예: `image123.jpg`) |
| `fileType` | string | 파일 형식 (예: `image/jpeg`) |

**Response**

| Status Code | Body                                                                                     |
| ----------- | ---------------------------------------------------------------------------------------- |
| `200`       | ```json { "uploadUrl": "https://your-s3-bucket.s3.amazonaws.com/uploads/image123.jpg?AWSAccessKeyId=...", "fileUrl": "https://cdn.example.com/uploads/image123.jpg" }``` |
| `400`       | ```json { "error": "Invalid request" }```                                               |

---

### **2. Notify Uploaded Media**

파일 업로드 후 클라이언트가 서버로 업로드 완료를 알립니다.  
이벤트는 채팅 메시지 전송으로 이어집니다.

**Event**

- **Event Name:** `notify_uploaded_media`

**Headers**

| Name            | Type               | Description     |
| --------------- | ------------------ | --------------- |
| `App-Id`        | `{ app id }`       | 앱 식별자       |
| `Authorization` | `{ access token }` | 사용자 인증 토큰 |

**Payload**

| Name        | Type   | Description                           |
| ----------- | ------ | ------------------------------------- |
| `channelId` | string | 메시지가 전송될 채널 ID                        |
| `userId`    | string | 메시지를 보낸 사용자 ID                        |
| `fileUrl`   | string | S3 또는 CloudFront URL                       |
| `fileType`  | string | 파일 형식 (`image/jpeg`, `video/mp4`) |
| `caption`   | string | 파일에 대한 설명 (선택)                         |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "event": "media_message_notified",
  "data": {
    "status": "success",
    "messageId": "msg-12345",
    "channelId": "channel-67890",
    "fileUrl": "https://cdn.example.com/uploads/image123.jpg",
    "fileType": "image/jpeg",
    "caption": "Check this out!",
    "timestamp": "2025-01-18T12:15:00Z"
  }
}
```
{% endtab %}
{% tab title="400" %}
```json
{
  "error": "Invalid request"
}
```
{% endtab %}
{% endtabs %}

---

### **3. Broadcast Media Message**

다른 사용자에게 업로드된 파일 정보를 포함한 메시지를 실시간으로 브로드캐스트합니다.

**Event**

- **Event Name:** `received_message`

**Headers**

| Name            | Type               | Description     |
| --------------- | ------------------ | --------------- |
| `App-Id`        | `{ app id }`       | 앱 식별자       |
| `Authorization` | `{ access token }` | 사용자 인증 토큰 |

**Payload**

| Name         | Type   | Description                             |
| ------------ | ------ | --------------------------------------- |
| `messageId`  | string | 메시지 ID                               |
| `senderId`   | string | 메시지 보낸 사용자 ID                           |
| `receiverId` | string | 메시지 받는 사용자 ID                           |
| `fileUrl`    | string | S3 또는 CloudFront URL                        |
| `fileType`   | string | 파일 형식 (`image/jpeg`, `video/mp4`)  |
| `caption`    | string | 파일 설명 (텍스트 메시지일 경우 `null`)              |
| `timestamp`  | string | 메시지 전송 시간                            |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "event": "media_message_broadcast",
  "data": {
    "messageId": "msg-12345",
    "senderId": "user-67890",
    "receiverId": "user-12345",
    "fileUrl": "https://cdn.example.com/uploads/image123.jpg",
    "fileType": "image/jpeg",
    "caption": "Check this out!",
    "timestamp": "2025-01-18T12:15:00Z"
  }
}
```
{% endtab %}
{% tab title="400" %}
```json
{
  "error": "Invalid request"
}
```
{% endtab %}
{% endtabs %}
