---
description: >-
  This API retrieves the spot config defail for all currencies.
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
## Get Spot Config

<mark style="color:green;">`GET`</mark> `https://nami.exchange/api/v3/spot/config`

**Headers**

| Name         | Value               |
| ------------ | ------------------- |
| Content-Type | `application/json`  |

**Query Parameters**

| Name        | Type      | Description | Required | Example               |
| ----------- | --------- | ----------- | -------- | --------------------- |
| `symbol`  | string   | Token | No       | `BTCUSDT`                     |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "status": "ok",
  "data": [
    {
      "symbol": "ZRXVNDC",
      "status": "TRADING",
      "baseAsset": "ZRX",
      "baseAssetPrecision": 8,
      "quoteAsset": "VNDC",
      "quotePrecision": 8,
      "baseCommissionPrecision": 8,
      "quoteCommissionPrecision": 8,
      "orderTypes": ["LIMIT", "MARKET", "STOP_LIMIT", "OCO"],
      "icebergAllowed": true,
      "ocoAllowed": true,
      "quoteOrderQtyMarketAllowed": true,
      "isSpotTradingAllowed": true,
      "isMarginTradingAllowed": true,
      "filters": [
        {
          "filterType": "PRICE_FILTER",
          "minPrice": 0.0001,
          "maxPrice": 1000,
          "tickSize": 0.0001
        }
      ],
      "permissions": ["SPOT", "MARGIN"],
      "baseAssetId": 123,
      "quoteAssetId": 456,
      "liquidityBroker": "NamiBroker",
      "createdAt": "2023-07-01T12:00:00Z",
      "updatedAt": "2023-07-02T12:00:00Z"
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
{% endtab %}
{% endtabs %}
