---
description: >-
  This API retrieves the order book for a specified trading pair, including the current bids and asks.
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

## Get Spot Depth

<mark style="color:green;">`GET`</mark> `https://nami.exchange/api/v3/spot/depth`

**Headers**

| Name         | Value              |
| ------------ | ------------------ |
| Content-Type | `application/json` |

**Query Parameters**

| Name     | Type   | Description         | Required | Example   |
| -------- | ------ | ------------------- | -------- | --------- |
| `symbol` | string | Trading pair symbol | No       | `BTCUSDT` |

**Response**

{% tabs %}
{% tab title="200" %}

```json
{
  "status": "ok",
  "bid": [
    [43000.5, 1.5],
    [42950.0, 2.0]
  ],
  "asks": [
    [43050.5, 1.0],
    [43100.0, 2.5]
  ]
}
```

{% endtab %}

{% tab title="400" %}

```json
{
  "statusCode": 400,
  "message": "Invalid query parameters",
  "error": "Bad Request"
}
```

{% endtab %} {% endtabs %}

## Get Real Time Spot Depth By WebSocket

**Overview**
This WebSocket API provides real-time order book depth updates on Nami Exchange.

- **Base URL:** `wss://stream-asia2.nami.exchange`
- **Path:** `/ws`
- **Transport:** WebSocket
- **Reconnection:** Enabled with exponential backoff

**Connection**
To establish a connection, use the following WebSocket client configuration:

```javascript
const socket = socketIO("https://stream-asia2.nami.exchange", {
  path: "/ws",
  upgrade: false,
  reconnection: true,
  reconnectionDelay: 100,
  reconnectionDelayMax: 500,
  reconnectionAttempts: Infinity,
  transports: ["websocket"],
});
```

**Events**

### 1. Connect
- **Event:** `connect`
- **Description:** Triggered when the client successfully connects to the WebSocket server.
- **Example:**
  
  ```javascript
  socket.on("connect", () => {
    console.log("Connected to WebSocket server");
  });
  ```

### 2. Subscribe to Market Depth
- **Event:** `subscribe:depth`
- **Description:** Subscribes to real-time order book depth updates for a specific trading pair.
- **Payload:** `string` (trading pair, e.g., `"BTCUSDT"`)
- **Example:**

  ```javascript
  socket.emit("subscribe:depth", "BTCUSDT");
  ```

### 3. Receive Market Depth Updates
- **Event:** `spot:depth:update`
- **Description:** Provides real-time order book depth updates for the subscribed trading pair.
- **Payload:** JSON object containing bid and ask order book data.
- **Example Response:**
  
  ```json
  {
    "symbol": "BTCUSDT",
    "bids": [
      [ 97638.22, 2.66402 ],
      [ 97638.2, 0.00018 ]
    ],
    "asks": [
      [ 97638.23, 1.9828 ],
      [ 97638.27, 0.00018 ]
    ]
  }
  ```

#### **Response Fields:**
| Field | Type | Description |
|-------|------|-------------|
| `symbol` | `string` | Trading pair (e.g., `BTCUSDT`) |
| `bids` | `array` | List of bid prices and quantities |
| `asks` | `array` | List of ask prices and quantities |

- **Example Handling:**
  
  ```javascript
  socket.on("spot:depth:update", (data) => {
    console.log("Order book update:", data);
  });
  ```

## Disconnection & Reconnection
- The WebSocket client automatically attempts to reconnect with exponential backoff.
- If disconnected, it will retry indefinitely with a delay between **100ms - 500ms**.

## Notes
- Ensure your WebSocket client supports reconnection strategies to maintain a stable connection.
- Data is subject to market fluctuations and should be handled accordingly.