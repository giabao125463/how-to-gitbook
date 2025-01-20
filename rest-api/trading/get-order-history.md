---
description: This API allows you to retrieve the history of orders placed on the platform.
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

# Get Order History

#### Prerequisites

Before using this endpoint, ensure you have read the [How to Generate a Signature](../../authentication.md) guide. This guide explains the steps required to create the `signature` parameter needed to authenticate your request.

#### Key Notes

1. The request requires specific query parameters to filter results. See details below.
2. You must provide a valid `timestamp` and `signature` in the query parameters.
3. The `x-api-key` must be included in the request headers for authentication.

## Get Order History

<mark style="color:green;">`GET`</mark> `https://nami.exchange/api/v4/spot/history`

**Headers**

| Name         | Value               |
| ------------ | ------------------- |
| Content-Type | `application/json`  |
| x-api-key    | `<Your secret key>` |

**Query Parameters**

| Name            | In    | Type      | Description                                      | Required | Example            |
| --------------- | ----- | --------- | ------------------------------------------------ | -------- | ------------------ |
| `side`          | query | string    | Side of the order (buy/sell)                    | No       | BUY                |
| `symbol`        | query | string    | Trading pair symbol                             | No       | ETHUSDT            |
| `hideCanceled`  | query | boolean   | Hide canceled orders                            | No       | true               |
| `pageSize`      | query | integer   | Number of orders per page                       | No       | 10                 |
| `page`          | query | integer   | Page number                                     | No       | 1                  |
| `timeFrom`      | query | date-time | Filter orders from this time                    | No       | 2024-01-01T00:00:00Z |
| `timeTo`        | query | date-time | Filter orders up to this time                   | No       | 2024-12-31T23:59:59Z |
| `signature`     | query | string    | The signature is the secret key encoded as ASCII data. It is required for authenticating the request. | Yes      | a1b2c3d4e5f6g7h8i9j0k |
| `timestamp`     | query | date-time | The timestamp is the time the request was sent. | Yes      | 1670000000000      |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "status": "ok",
  "data": [
    {
      "price": 0,
      "stopPrice": null,
      "executedPrice": 3394.3322747747743,
      "quantity": 0.222,
      "executedQty": 0.222,
      "quoteQty": 753.541765,
      "executedQuoteQty": 753.541765,
      "useQuoteQty": false,
      "liquidityStatus": 0,
      "liquiditySymbol": "ETHUSDT",
      "liquidityUsdtPrice": 1,
      "liquidityTransferPrice": 0,
      "liquidityOrderId": null,
      "liquidityTransferFee": 0,
      "limitPrice": 0,
      "internalError": false,
      "displayingId": 434256,
      "userId": 18,
      "side": "SELL",
      "type": "MARKET",
      "symbol": "ETHUSDT",
      "baseAsset": "ETH",
      "baseAssetId": 2,
      "quoteAsset": "USDT",
      "quoteAssetId": 22,
      "status": "FILLED",
      "createdAt": "2024-06-24T04:09:24.324Z",
      "updatedAt": "2024-06-24T04:09:24.324Z"
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
