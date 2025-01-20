---
description: This API allows you to delete an order on the platform.
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

# Delete Order

#### Prerequisites

Before using this endpoint, ensure you have read the [How to Generate a Signature](../../authentication.md) guide. This guide explains the steps required to create the `signature` parameter needed to authenticate your request.

#### Key Notes

1. The request body must include the required parameters, detailed below.
2. You must provide a valid `timestamp` and `signature` in the request body.
3. The `x-api-key` must be included in the request headers for authentication.

## Delete Order

<mark style="color:red;">`DELETE`</mark> `https://nami.exchange/api/v4/spot/order`

**Headers**

| Name         | Value               |
| ------------ | ------------------- |
| Content-Type | `application/json`  |
| x-api-key    | `<Your secret key>` |

**Body**

| Name                | Type      | Description                                                                                 | Possible Values                          |
| -------------------- | --------- | ------------------------------------------------------------------------------------------- | ---------------------------------------- |
| `symbol`            | string    | The trading symbol                                                                          | Read [Spot Config](../market-data/exchange-info.md) to get symbols available |
| `displayingId`      | string    | The unique ID of the order to be deleted                                                    | Any valid order ID                       |
| `allowNotification` | boolean   | Whether to send notifications upon deletion.                                                | `true` \| `false`                        |
| `signature`         | string    | The signature is the secret key encoded as ASCII data. It is required for authenticating.   | [How to Generate a Signature](../../authentication.md) |
| `timestamp`         | string    | The timestamp is the time the request was sent. Format must be in milliseconds.             | Millisecond only                         |

#### Example Request Body
```json
{
  "symbol": "BTCUSDT",
  "displayingId": "435372",
  "allowNotification": false,
  "signature": "a1b2c3d4e5f6g7h8i9j0k",
  "timestamp": 1670000000000
}