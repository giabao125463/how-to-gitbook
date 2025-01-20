---
description: This API allows you to delete multiple orders on the platform.
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

# Delete All Orders

#### Prerequisites

Before using this endpoint, ensure you have read the [How to Generate a Signature](../../authentication.md) guide. This guide explains the steps required to create the `signature` parameter needed to authenticate your request.

#### Key Notes

1. The request body must include the required parameters, detailed below.
2. You must provide a valid `timestamp` and `signature` in the request body.
3. The `x-api-key` must be included in the request headers for authentication.

## Delete All Orders

<mark style="color:red;">`DELETE`</mark> `https://nami.exchange/api/v4/spot/all_order`

**Headers**

| Name         | Value               |
| ------------ | ------------------- |
| Content-Type | `application/json`  |
| x-api-key    | `<Your secret key>` |

**Body**

| Name                | Type      | Description                                                                                 | Possible Values                          |
| -------------------- | --------- | ------------------------------------------------------------------------------------------- | ---------------------------------------- |
| `orders`            | array     | An array of objects representing orders to be deleted. Each object contains the following:  | See example below                        |
| `orders[].displayingId` | number | The displaying ID of the order.                                                             | Any valid order ID                       |
| `orders[].symbol`   | string    | The symbol of the order.                                                                    | Any valid trading symbol                 |
| `allowNotification` | boolean   | Whether to send notifications upon deletion.                                                | `true` \| `false`                        |
| `signature`         | string    | The signature is the secret key encoded as ASCII data. It is required for authenticating.   | [How to Generate a Signature](../../authentication.md) |
| `timestamp`         | string    | The timestamp is the time the request was sent. Format must be in milliseconds.             | Millisecond only                         |

#### Example Request Body
```json
{
  "orders": [
    {
      "displayingId": 435372,
      "symbol": "BTCUSDT"
    },
    {
      "displayingId": 435373,
      "symbol": "ETHUSDT"
    }
  ],
  "allowNotification": false,
  "signature": "a1b2c3d4e5f6g7h8i9j0k",
  "timestamp": 1670000000000
}
```
#### Response

{% tabs %} {% tab title="200" %}
```json
{
  "status": "ok",
  "data": [
    {
      "displayingId": 435372,
      "userId": 18,
      "side": "BUY",
      "type": "LIMIT",
      "price": 62877.99,
      "liquidityStatus": 1,
      "quantity": 0.07474,
      "executedQty": 0,
      "quoteQty": 4699.5009726,
      "executedQuoteQty": 0,
      "liquidityUsdtPrice": 1,
      "liquidityTransferPrice": 62877.99,
      "liquiditySymbol": "BTCUSDT",
      "liquidityOrderId": "11779887",
      "feeMetadata": {
        "assetId": 22,
        "asset": "USDT",
        "value": 4.6995009726,
        "feeRatio": 0.001,
        "executed": 0
      },
      "useQuoteQty": false,
      "symbol": "BTCUSDT",
      "baseAsset": "BTC",
      "baseAssetId": 9,
      "quoteAsset": "USDT",
      "quoteAssetId": 22,
      "status": "CANCELED",
      "stopPrice": 0
    },
    {
      "displayingId": 435373,
      "userId": 18,
      "side": "SELL",
      "type": "LIMIT",
      "price": 3500.50,
      "liquidityStatus": 1,
      "quantity": 1.5,
      "executedQty": 0,
      "quoteQty": 5250.75,
      "executedQuoteQty": 0,
      "liquidityUsdtPrice": 1,
      "liquidityTransferPrice": 3500.50,
      "liquiditySymbol": "ETHUSDT",
      "liquidityOrderId": "11779888",
      "feeMetadata": {
        "assetId": 22,
        "asset": "USDT",
        "value": 5.25075,
        "feeRatio": 0.001,
        "executed": 0
      },
      "useQuoteQty": false,
      "symbol": "ETHUSDT",
      "baseAsset": "ETH",
      "baseAssetId": 10,
      "quoteAsset": "USDT",
      "quoteAssetId": 22,
      "status": "CANCELED",
      "stopPrice": 0
    }
  ]
}
```
{% endtab %}

{% tab title="400" %}
```json
{
    "status": "BROKER_ERROR",
    "code": 6104,
    "data": {
        "requestId": "6ff66697-2742-4caf-acad-f97e9cc3596d"
    },
    "message": null
}
```
{% endtab %} {% endtabs %}
