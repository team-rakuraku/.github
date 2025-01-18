# Chat Room List

***

## Retrieve Chat Room List

특정 사용자가 참여 중인 채팅방 목록을 조회합니다.



**Event**

* **Event Name:** `retrieve_chat_rooms`



**Header**

| Name            | Type               | Descriptoin |
| --------------- | ------------------ | ----------- |
| `App-Id`        | `{ app id }`       |             |
| `Authorization` | `{ access token }` |             |

**Payload**

| Name     | Type   | Description     |
| -------- | ------ | --------------- |
| `userId` | string | 메시지를 보내는 사용자 ID |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "event": "chat_rooms_retred",
  "data": {
    "userId": "user-12345",
    "chatRooms": [
      {
        "roomId": "room-67890",
        "roomName": "Team Chat",
        "lastMessage": "See you tomorrow!",
        "lastMessageTimestamp": "2025-01-18T12:00:00Z",
        "unreadMessages": 2
      },
      {
        "roomId": "room-54321",
        "roomName": "Project Discussion",
        "lastMessage": "Meeting at 3 PM.",
        "lastMessageTimestamp": "2025-01-18T11:00:00Z",
        "unreadMessages": 5
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
