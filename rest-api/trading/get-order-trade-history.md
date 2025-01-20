---
description: This API retrieves the trade details of orders on the platform.
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

# Get Order Trades

#### Prerequisites

Before using this endpoint, ensure you have read the [How to Generate a Signature](../../authentication.md) guide. This guide explains the steps required to create the `signature` parameter needed to authenticate your request.

#### Key Notes

1. The request requires specific query parameters to filter results. See details below.
2. You must provide a valid `timestamp` and `signature` in the query parameters.
3. The `x-api-key` must be included in the request headers for authentication.

## Get Order Trades

<mark style="color:blue;">`GET`</mark> `https://nami.exchange/api/v3/spot/trade`

**Headers**

| Name         | Value               |
| ------------ | ------------------- |
| Content-Type | `application/json`  |
| x-api-key    | `<Your secret key>` |

**Query Parameters**

| Name           | In    | Type      | Description                                              | Required | Example         |
| -------------- | ----- | --------- | -------------------------------------------------------- | -------- | --------------- |
| `side`         | query | string    | The side of the order (buy/sell).                       | No       | buy             |
| `symbol`       | query | string    | Trading pair symbol.                                    | No       | BTC/USD         |
| `hideCanceled` | query | boolean   | Whether to hide canceled orders.                        | No       | true            |
| `pageSize`     | query | integer   | Number of orders per page.                              | No       | 50              |
| `page`         | query | integer   | Page number.                                            | No       | 1               |
| `timeFrom`     | query | date-time | Filter orders from this time.                           | No       | 2025-01-01T00:00:00Z |
| `timeTo`       | query | date-time | Filter orders up to this time.                          | No       | 2025-01-10T00:00:00Z |
| `signature`    | query | string    | The signature is the secret key encoded as ASCII data. It is required for authenticating the request. | Yes      | a1b2c3d4e5f6g7h8i9j0k |
| `timestamp`    | query | date-time | The timestamp is the time the request was sent.         | Yes      | 1670000000000   |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "status": "ok",
  "data": [
    {
      "price": 35000,
      "stopPrice": null,
      "quantity": 1.2,
      "executedQty": 0.6,
      "quoteQty": 42000,
      "executedQuoteQty": 21000,
      "useQuoteQty": false,
      "liquidityStatus": 1,
      "liquiditySymbol": "BTC/USD",
      "liquidityUsdtPrice": 1,
      "liquidityTransferPrice": 35000,
      "liquidityOrderId": "12537485",
      "displayingId": 453672,
      "userId": 25,
      "side": "BUY",
      "type": "LIMIT",
      "symbol": "BTC/USD",
      "baseAsset": "BTC",
      "baseAssetId": 1,
      "quoteAsset": "USD",
      "quoteAssetId": 22,
      "status": "NEW",
      "createdAt": "2025-01-10T14:25:33.524Z",
      "updatedAt": "2025-01-12T16:40:11.124Z"
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