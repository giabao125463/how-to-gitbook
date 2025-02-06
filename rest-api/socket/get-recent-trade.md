---
description: >-
  This WebSocket API provides real-time updates for recent trades on Nami Exchange.
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

## Get Recent Trades Realtime By Socket

**Overview**
This WebSocket API provides real-time updates for recent trades on Nami Exchange.

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

### 2. Subscribe to Recent Trades
- **Event:** `subscribe:recent_trade`
- **Description:** Subscribes to real-time recent trade updates for a specific trading pair.
- **Payload:** `string` (trading pair, e.g., `"BTCUSDT"`)
- **Example:**

  ```javascript
  socket.emit("subscribe:recent_trade", "BTCUSDT");
  ```

### 3. Receive Recent Trade Updates
- **Event:** `spot:recent_trade:add`
- **Description:** Provides real-time recent trade updates for the subscribed trading pair.
- **Payload:** JSON object containing trade details.
- **Example Response:**
  
  ```json
  {
    "S": "SELL",
    "s": "BTCUSDT",
    "p": 97548.08,
    "q": 0.000002,
    "Q": 0,
    "t": 1738817372945
  }
  ```

#### **Response Fields:**
| Field | Type | Description |
|-------|------|-------------|
| `S` | `string` | Trade side (`BUY` or `SELL`) |
| `s` | `string` | Trading pair (e.g., `BTCUSDT`) |
| `p` | `number` | Trade price |
| `q` | `number` | Trade quantity |
| `Q` | `number` | Unknown field (may represent extra trade metadata) |
| `t` | `number` | Trade timestamp (Unix time in milliseconds) |

- **Example Handling:**
  
  ```javascript
  socket.on("spot:recent_trade:add", (data) => {
    console.log("Recent trade update:", data);
  });
  ```

## Disconnection & Reconnection
- The WebSocket client automatically attempts to reconnect with exponential backoff.
- If disconnected, it will retry indefinitely with a delay between **100ms - 500ms**.

## Notes
- Ensure your WebSocket client supports reconnection strategies to maintain a stable connection.
- Data is subject to market fluctuations and should be handled accordingly.
