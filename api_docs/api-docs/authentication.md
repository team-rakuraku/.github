# Authentication

***

## User Login

<mark style="color:green;">`POST`</mark> `/auth/login`

사용자를 인증하고 고유한 사용자 ID와 액세스 토큰을 반환합니다.



**Headers**

| Name            | Value              |
| --------------- | ------------------ |
| `Content-Type`  | `application/json` |
| `Authorization` | `{ access token }` |
| `App-Id`        | `{ app id }`       |

**Body**

| Name            | Type           | Description |
| --------------- | -------------- | ----------- |
| userId          | string         |             |
| nickname        | string         |             |
| profileImageUrl | string         | AWS S3 URL  |
| friends         | Array\<string> | uuid array  |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "status": "success",
  "userId": "string",
  "expiresAt": "timestamp"
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

## Connect the Chat

WebSocket 핸드셰이크 중에 토큰과 userId가 검증됩니다



**Event**

**Event Name:** `connect`



**Header**

| Name            | Type               | Descriptoin |
| --------------- | ------------------ | ----------- |
| `App-Id`        | `{ app id }`       |             |
| `Authorization` | `{ access token }` |             |

**Payload**

| Name     | Type   | Description |
| -------- | ------ | ----------- |
| `userId` | string |             |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "event": "connected",
  "data": {
    "status": "success",
    "userId": "user-12345",
    "timestamp": "2025-01-18T12:00:00Z"
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



## Disconnect From Chat

연결 종료 시 모든 캐시 데이터가 클리어됩니다. 이 API는 사용자가 더 이상 채팅 연결이 필요하지 않을 때 호출됩니다.



**Event**&#x20;

**Event Name**: disconnect



**Headers**

| Name            | Value              |
| --------------- | ------------------ |
| `Authorization` | `{ access Token }` |
| `App-Id`        | `{ app id }`       |

**Payload**

| Name     | Type   | Description |
| -------- | ------ | ----------- |
| `userId` | string |             |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "event": "disconnected",
  "data": {
    "status": "disconnected",
    "userId": "user-12345",
    "timestamp": "2025-01-18T12:10:00Z"
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
