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

<mark style="color:blue;">`GET`</mark> `https://nami.exchange/api/v4/spot/trade`

**Headers**

| Name         | Value               |
| ------------ | ------------------- |
| Content-Type | `application/json`  |
| x-api-key    | `<Your secret key>` |

**Query Parameters**

| Name           | Type      | Description                                                                                           | Required | Example               |
| -------------- | --------- | ----------------------------------------------------------------------------------------------------- | -------- | --------------------- |
| `side`         | string    | The side of the order (buy/sell).                                                                     | No       | buy                   |
| `symbol`       | string    | Trading pair symbol.                                                                                  | No       | BTC/USD               |
| `hideCanceled` | boolean   | Whether to hide canceled orders.                                                                      | No       | true                  |
| `pageSize`     | integer   | Number of orders per page.                                                                            | No       | 50                    |
| `page`         | integer   | Page number.                                                                                          | No       | 1                     |
| `timeFrom`     | date-time | Filter orders from this time.                                                                         | No       | 2025-01-01T00:00:00Z  |
| `timeTo`       | date-time | Filter orders up to this time.                                                                        | No       | 2025-01-10T00:00:00Z  |
| `signature`    | string    | The signature is the secret key encoded as ASCII data. It is required for authenticating the request. | Yes      | a1b2c3d4e5f6g7h8i9j0k |
| `timestamp`    | date-time | The timestamp is the time the request was sent.                                                       | Yes      | 1670000000000         |

**Response**

{% tabs %}
{% tab title="200" %}

```json
{
  "status": "ok",
  "data": [
    {
      "_id": "6790d15914c0436561b54463",
      "symbol": "NAMIVNST",
      "side": "SELL",
      "displayingId": "8415",
      "orderId": 453017,
      "feeMetadata": {
        "feeValue": 0.30000000000000004,
        "feeAssetId": 1,
        "feeAsset": "NAMI",
        "feeRatio": 0.0003,
        "quoteQty": 200000
      },
      "createdAt": "2025-01-22T11:07:05.042Z",
      "flag": "BUY_ORDER_FILL",
      "baseQty": 1000,
      "quoteQty": 200000,
      "price": 200,
      "baseAssetId": 1,
      "quoteAssetId": 39
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
