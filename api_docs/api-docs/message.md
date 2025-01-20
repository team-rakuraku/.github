# Message

***

## Send Message

사용자가 텍스트 메시지를 채널에 전송합니다.



**Event**

* **Event Name:** `send_message`&#x20;



**Header**

| Name            | Type               | Descriptoin |
| --------------- | ------------------ | ----------- |
| `App-Id`        | `{ app id }`       |             |
| `Authorization` | `{ access token }` |             |

**Payload**

| Name        | Type   | Description     |
| ----------- | ------ | --------------- |
| `userId`    | string | 메시지를 보내는 사용자 ID |
| `channelId` | string | 메시지가 전송될 채널 ID  |
| `message`   | string | 텍스트 메시지 내용      |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "status": "sent",
  "messageId": "msg-12345",
  "channelId": "channel-67890",
  "userId": "user-abc123",
  "timestamp": "2025-01-18T12:00:00Z"
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

***




## Retrieve Messages

특정 채널의 메시지 목록을 조회합니다.



**Event**

* **Event Name:** `retrieve_messages`



**Header**

| Name            | Type               | Descriptoin |
| --------------- | ------------------ | ----------- |
| `App-Id`        | `{ app id }`       |             |
| `Authorization` | `{ access token }` |             |

**Payload**

| Name        | Type   | Description          |
| ----------- | ------ | -------------------- |
| `channelID` | string | 조회할 채널 ID            |
| `limit`     | int    | 가져올 메시지 수 (기본값: 20)  |
| `before`    | string | 특정 메시지 ID 이전 메시지를 조회 |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "event": "messages_retrieved",
  "data": {
    "channelId": "channel-67890",
    "messages": [
      {
        "messageId": "msg-12345",
        "userId": "12345",
        "content": "Hello, World!",
        "mediaUrl": null,
        "mediaType": null,
        "timestamp": "2025-01-18T12:09:00Z"
      },
      {
        "messageId": "msg-67890",
        "userId": "54321",
        "content": null,
        "mediaUrl": "https://cdn.example.com/uploads/image12345.jpg",
        "mediaType": "image/jpeg",
        "timestamp": "2025-01-18T12:10:00Z"
      }
    ]
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

***

## Receive real-time messages

친구가 메시지를 보낼 때마다 실시간으로 메시지를 수신합니다.



**Event**

* **Name**: `received_message`



**Header**

| Name            | Type               | Descriptoin |
| --------------- | ------------------ | ----------- |
| `App-Id`        | `{ app id }`       |             |
| `Authorization` | `{ access token }` |             |

**Payload**

| Name         | Type   | Description                            |
| ------------ | ------ | -------------------------------------- |
| `messageId`  | string |                                        |
| `senderId`   | string |                                        |
| `receiverId` | string |                                        |
| `content`    | string | 텍스트 메시지 내용 (미디어 메시지일 경우 `null`).       |
| `mediaUrl`   | string | 미디어 파일 URL (텍스트 메시지일 경우 `null`).       |
| `mediaType`  | string | 미어 파일 형식 (`image/jpeg`, `video/mp4`).다 |
| `timestamp`  | string |                                        |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "event": "received_message",
  "data": {
    "messageId": "msg-12345",
    "senderId": "user-67890",
    "receiverId": "user-12345",
    "content": "Hey, how are you?",
    "mediaUrl": null,
    "mediaType": null,
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
