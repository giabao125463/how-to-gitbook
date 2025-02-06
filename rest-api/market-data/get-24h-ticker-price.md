---
description: >-
  This API retrieves the market watch details for a specified trading pair or all available pairs.
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

## Get Spot Market Watch

<mark style="color:green;">`GET`</mark> `https://nami.exchange/api/v3/spot/market_watch`

**Headers**

| Name         | Value              |
| ------------ | ------------------ |
| Content-Type | `application/json` |

**Query Parameters**

| Name     | Type   | Description                     | Required | Example   |
| -------- | ------ | ------------------------------- | -------- | --------- |
| `symbol` | string | Trading pair symbol (optional). | No       | `BTCUSDT` |

**Response**

{% tabs %}
{% tab title="200" %}

```json
{
  "status": "ok",
  "data": [
    {
      "a": 0,
      "b": "ETH",
      "p": 3437.59,
      "ld": 3490.58,
      "h": 3498.99,
      "l": 3426.67,
      "hh": 3451.74,
      "lh": 3434.53,
      "vb": 57771.715600000025,
      "vq": 200279763.829316,
      "s": "ETHUSDT",
      "qi": 22,
      "bi": 2,
      "q": "USDT",
      "u": false,
      "lq": 0.024,
      "lQ": 83,
      "t": 1719906507691,
      "ph": 3450.36,
      "av": 25050.38146000001,
      "hy": 4092.36,
      "ly": 1522,
      "vc": 0,
      "pw": 3394.91,
      "p1m": 3780.91,
      "p3m": 3278.23,
      "py": 1937.48,
      "lbl": "top_view"
    }
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

## Get Ticker Price RealTime By Socket

**Overview**
This WebSocket API provides real-time updates for tickers on Nami Exchange.

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

### 2. Subscribe to Tickers

- **Event:** `subscribe:ticker`
- **Description:** Subscribes to real-time Tickers updates for a specific trading pair.
- **Payload:** `string` (trading pair, e.g., `"BTCUSDT"`)
- **Example:**

  ```javascript
  socket.emit("subscribe:ticker", "BTCUSDT");
  ```

### 3. Receive Tickers Updates

- **Event:** `spot:ticker:update`
- **Description:** Provides real-time Tickers updates for the subscribed trading pair.
- **Payload:** JSON object containing trade details.
- **Example Response:**

  ```json
  {
    "a": 0,
    "b": "BTC",
    "p": 98250.01,
    "ld": 97643.14,
    "h": 99128,
    "l": 96155,
    "hh": 98409.08,
    "lh": 97696.49,
    "vb": 3.868911719999997,
    "vq": 377860.9234310737,
    "s": "BTCUSDT",
    "qi": 22,
    "bi": 9,
    "q": "USDT",
    "u": true,
    "lq": 3e-7,
    "lQ": 0,
    "t": 1738824644102,
    "ph": 97796.25,
    "av": 3.1648889600000083,
    "hy": 109544.14,
    "ly": 42788.01,
    "vc": 0,
    "pw": 101344.15,
    "p1m": 98220.51,
    "p3m": 75571.99,
    "py": 43098.96,
    "lbl": "top_view"
  }
  ```
- **Example Handling:**

  ```javascript
  socket.on("spot:ticker:update", (data) => {
    console.log("Tickers update:", data);
  });
  ```

## Disconnection & Reconnection

- The WebSocket client automatically attempts to reconnect with exponential backoff.
- If disconnected, it will retry indefinitely with a delay between **100ms - 500ms**.

## Notes

- Ensure your WebSocket client supports reconnection strategies to maintain a stable connection.
- Data is subject to market fluctuations and should be handled accordingly.
