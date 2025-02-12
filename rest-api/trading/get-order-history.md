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

| Name           | Type      | Description                                                                                           | Required | Example               |
| -------------- | --------- | ----------------------------------------------------------------------------------------------------- | -------- | --------------------- |
| `side`         | string    | Side of the order (buy/sell)                                                                          | No       | BUY                   |
| `symbol`       | string    | Trading pair symbol                                                                                   | No       | ETHUSDT               |
| `hideCanceled` | boolean   | Hide canceled orders                                                                                  | No       | true                  |
| `pageSize`     | integer   | Number of orders per page                                                                             | No       | 10                    |
| `page`         | integer   | Page number                                                                                           | No       | 1                     |
| `timeFrom`     | date-time | Filter orders from this time                                                                          | No       | 2024-01-01T00:00:00Z  |
| `timeTo`       | date-time | Filter orders up to this time                                                                         | No       | 2024-12-31T23:59:59Z  |
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
      "price": 200,
      "stopPrice": null,
      "executedPrice": 0,
      "quantity": 1000,
      "executedQty": 1000,
      "quoteQty": 200000,
      "executedQuoteQty": 200000,
      "useQuoteQty": null,
      "liquidityStatus": 0,
      "liquiditySymbol": null,
      "liquidityUsdtPrice": 0,
      "liquidityTransferPrice": 0,
      "liquidityOrderId": null,
      "liquidityTransferFee": 0,
      "limitPrice": null,
      "internalError": false,
      "_id": "678e12e7a679c0c007d3b315",
      "displayingId": 453079,
      "baseAsset": "NAMI",
      "baseAssetId": 1,
      "createdAt": "2025-01-20T09:09:59.066Z",
      "executedType": null,
      "feeMetadata": {
        "feeMode": 0,
        "originBaseQty": 1000,
        "assetId": 39,
        "value": 80,
        "feeRatio": 0.0004
      },
      "limitOrderId": null,
      "ocoOrderId": null,
      "priceToCalLockAndFee": null,
      "quoteAsset": "VNST",
      "quoteAssetId": 39,
      "side": "BUY",
      "status": "FILLED",
      "stopLimitOrderId": null,
      "symbol": "NAMIVNST",
      "type": "LIMIT",
      "updatedAt": "2025-01-20T09:09:59.066Z",
      "userId": 583344
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

{% endtab %}
{% endtabs %}
