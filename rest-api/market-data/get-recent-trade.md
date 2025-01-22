---
description: >-
  This API retrieves recent trade data for a specified trading pair, including details about the trade type, symbol, price, and quantity.
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

## Get Recent Trades

<mark style="color:green;">`GET`</mark> `https://nami.exchange/api/v3/spot/recent_trade`

**Headers**

| Name         | Value               |
| ------------ | ------------------- |
| Content-Type | `application/json`  |

**Query Parameters**

| Name     | Type   | Description           | Required | Example  |
| -------- | ------ | --------------------- | -------- | -------- |
| `symbol` | string | Trading pair symbol   | No       | `BTCUSDT` |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "status": "ok",
  "data": [
    {
      "S": "SELL",
      "s": "BTCUSDT",
      "p": 62948,
      "q": "0.00027000",
      "Q": 17,
      "t": 1721117625675
    },
    {
      "S": "BUY",
      "s": "BTCUSDT",
      "p": 62950,
      "q": "0.00100000",
      "Q": 10,
      "t": 1721117625676
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