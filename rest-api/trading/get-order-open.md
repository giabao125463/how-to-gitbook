---
description: This API retrieves the list of open orders on the platform.
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

# Get Open Orders

#### Prerequisites

Before using this endpoint, ensure you have read the [How to Generate a Signature](../../authentication.md) guide. This guide explains the steps required to create the `signature` parameter needed to authenticate your request.

#### Key Notes

1. The request requires specific query parameters to filter results. See details below.
2. You must provide a valid `timestamp` and `signature` in the query parameters.
3. The `x-api-key` must be included in the request headers for authentication.

## Get Open Orders

<mark style="color:green;">`GET`</mark> `https://nami.exchange/api/v4/spot/open`

**Headers**

| Name         | Value               |
| ------------ | ------------------- |
| Content-Type | `application/json`  |
| x-api-key    | `<Your secret key>` |

**Query Parameters**

| Name           | Type      | Description                                                                                           | Required | Example               |
| -------------- | --------- | ----------------------------------------------------------------------------------------------------- | -------- | --------------------- |
| `filterByPair` | string    | Filter open orders by a specific trading pair (e.g., BTC/USD).                                        | No       | BTC/USD               |
| `signature`    | string    | The signature is the secret key encoded as ASCII data. It is required for authenticating the request. | Yes      | a1b2c3d4e5f6g7h8i9j0k |
| `timestamp`    | date-time | The timestamp is the time the request was sent.                                                       | Yes      | 1670000000000         |

**Response**

{% tabs %}
{% tab title="200" %}

```json
{
  "status": "ok",
  "data": {
    "orders": [
      {
        "price": 200,
        "stopPrice": null,
        "executedPrice": 0,
        "quantity": 10000,
        "executedQty": 0,
        "quoteQty": 2000000,
        "executedQuoteQty": 0,
        "useQuoteQty": null,
        "liquiditySymbol": null,
        "liquidityUsdtPrice": 0,
        "liquidityTransferPrice": 0,
        "liquidityTransferFee": 0,
        "limitPrice": null,
        "displayingId": 453021,
        "baseAsset": "NAMI",
        "baseAssetId": 1,
        "createdAt": "2025-01-14T08:41:17.032Z",
        "executedType": null,
        "feeMetadata": {
          "feeMode": 0,
          "originBaseQty": 10000,
          "assetId": 39,
          "value": 0,
          "feeRatio": 0.0004
        },
        "limitOrderId": null,
        "ocoOrderId": null,
        "priceToCalLockAndFee": null,
        "quoteAsset": "VNST",
        "quoteAssetId": 39,
        "side": "SELL",
        "status": "NEW",
        "stopLimitOrderId": null,
        "symbol": "NAMIVNST",
        "type": "LIMIT",
        "updatedAt": "2025-01-14T08:41:17.032Z",
        "userId": 583344,
        "metadata": {}
      }
    ]
  }
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
