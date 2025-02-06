---
description: >-
  This WebSocket API provides real-time updates for tickers on Nami Exchange.
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
