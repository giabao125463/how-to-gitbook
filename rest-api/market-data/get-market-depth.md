---
description: >-
  This API retrieves the order book for a specified trading pair, including the current bids and asks.
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

## Get Spot Depth

<mark style="color:green;">`GET`</mark> `https://nami.exchange/api/v3/spot/depth`

**Headers**

| Name         | Value              |
| ------------ | ------------------ |
| Content-Type | `application/json` |

**Query Parameters**

| Name     | Type   | Description         | Required | Example   |
| -------- | ------ | ------------------- | -------- | --------- |
| `symbol` | string | Trading pair symbol | No       | `BTCUSDT` |

**Response**

{% tabs %}
{% tab title="200" %}

```json
{
  "status": "ok",
  "bid": [
    [43000.5, 1.5],
    [42950.0, 2.0]
  ],
  "asks": [
    [43050.5, 1.0],
    [43100.0, 2.5]
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