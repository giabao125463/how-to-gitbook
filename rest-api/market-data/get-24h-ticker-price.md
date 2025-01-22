---
description: >-
  This API retrieves the market watch details for a specified trading pair or all available pairs.
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

## Get Spot Market Watch

<mark style="color:green;">`GET`</mark> `https://nami.exchange/api/v3/spot/market_watch`

**Headers**

| Name         | Value               |
| ------------ | ------------------- |
| Content-Type | `application/json`  |

**Query Parameters**

| Name        | Type      | Description                     | Required | Example     |
| ----------- | --------- | ------------------------------- | -------- | ----------- |
| `symbol`    | string    | Trading pair symbol (optional). | No       | `BTCUSDT`   |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "status": "ok",
  "data": [
    {
      "a": 0,
      "b": "ETH",
      "p": 3437.59,
      "ld": 3490.58,
      "h": 3498.99,
      "l": 3426.67,
      "hh": 3451.74,
      "lh": 3434.53,
      "vb": 57771.715600000025,
      "vq": 200279763.829316,
      "s": "ETHUSDT",
      "qi": 22,
      "bi": 2,
      "q": "USDT",
      "u": false,
      "lq": 0.024,
      "lQ": 83,
      "t": 1719906507691,
      "ph": 3450.36,
      "av": 25050.38146000001,
      "hy": 4092.36,
      "ly": 1522,
      "vc": 0,
      "pw": 3394.91,
      "p1m": 3780.91,
      "p3m": 3278.23,
      "py": 1937.48,
      "lbl": "top_view"
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