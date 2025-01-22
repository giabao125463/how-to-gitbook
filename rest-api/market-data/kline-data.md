---
description: >-
  This API retrieves historical chart data for a specified trading pair, including price and volume information over a specified time range.
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

## Get Chart History

<mark style="color:green;">`GET`</mark> `https://nami.exchange/api/v1/chart/history`

**Headers**

| Name         | Value               |
| ------------ | ------------------- |
| Content-Type | `application/json`  |

**Query Parameters**

| Name        | Type    | Description                                             | Required | Example   |
| ----------- | ------- | ------------------------------------------------------- | -------- | --------- |
| `from`      | integer | Start timestamp (in seconds) of the data range          | Yes      | 1715889600 |
| `to`        | integer | End timestamp (in seconds) of the data range            | Yes      | 1715893200 |
| `resolution`| string  | Resolution of the data (e.g. 1m, 5m, 1h)                | Yes      | `1h`      |
| `broker`    | string  | Broker name (e.g. NAMI_SPOT)                            | No       | `NAMI_SPOT` |
| `symbol`    | string  | Trading pair symbol                                     | No       | `BTCUSDT` |

**Response**

{% tabs %}
{% tab title="200" %}
```json
[
  [
    1715889600,
    65144.26,
    65289.99,
    65054.24,
    65273.9,
    6.946629999999999,
    452728
  ]
]
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