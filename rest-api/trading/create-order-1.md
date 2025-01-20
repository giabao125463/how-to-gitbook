---
description: This API allows you to create a new order on the platform.
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

# Create Order

#### Prerequisites

Before using this endpoint, ensure you have read the [How to Generate a Signature](../../authentication.md) guide. This guide explains the steps required to create the `signature` parameter needed to authenticate your request.

#### Key Notes

1. The request body must include the required parameters, detailed below.
2. You must provide a valid `timestamp` and `signature` in the request body.
3. The `x-api-key` must be included in the request headers for authentication.

## Place Order

<mark style="color:green;">`POST`</mark> `https://nami.exchange/api/v4/spot/order`

**Headers**

| Name         | Value               |
| ------------ | ------------------- |
| Content-Type | `application/json`  |
| x-api-key    | `<Your secret key>` |

**Body**

| Name            | Type    | Description                                           | Possible Values                                                                |
| --------------- | ------- | ----------------------------------------------------- | ------------------------------------------------------------------------------ |
| `symbol`        | string  | The trading symbol                                    | Read [Spot Config](../market-data/exchange-info.md) to get symbol available    |
| `price`         | number  | The price at which to place the order.                | Any positive integer                                                           |
| `stopPrice`     | number  | The stop price for a stop order.                      | Any positive integer                                                           |
| `side`          | string  | The side of the order                                 | BUY \| SELL                                                                    |
| `type`          | string  | The type of the order                                 | LIMIT \| MARKET \| STOP\_LIMIT \| OCO                                          |
| `quantity`      | number  | The quantity of the asset to buy or sell.             | Any positive integer                                                           |
| `quoteOrderQty` | number  | The quote order quantity.                             | Any positive integer                                                           |
| `useQuoteQty`   | boolean | Whether to use the quote order quantity.              | <p>True use <code>quoteOrderQty</code>.<br>False use <code>quantity</code></p> |
| `signature`     | string  | The signature is the secret key encoded as ASCII data |   [How to Generate a Signature](../../authentication.md)                                                                             |
| `timestamp`     | number  | The timestamp is the time the request was sent.       | Millisecond only                                                               |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "status": "ok",
  "data": {
    "displayingId": 435372,
    "userId": 18,
    "side": "BUY",
    "type": "LIMIT",
    "price": 62877.99,
    "liquidityStatus": 1,
    "quantity": 0.07474,
    "executedQty": 0,
    "quoteQty": 4699.5009726,
    "executedQuoteQty": 0,
    "liquidityUsdtPrice": 1,
    "liquidityTransferPrice": 62877.99,
    "liquiditySymbol": "BTCUSDT",
    "liquidityOrderId": "11779887",
    "feeMetadata": {
      "assetId": 22,
      "asset": "USDT",
      "value": 4.6995009726,
      "feeRatio": 0.001,
      "executed": 0
    },
    "useQuoteQty": false,
    "symbol": "BTCUSDT",
    "baseAsset": "BTC",
    "baseAssetId": 9,
    "quoteAsset": "USDT",
    "quoteAssetId": 22,
    "status": "NEW",
    "stopPrice": 0
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
{% endtab %}
{% endtabs %}

## Place Order LIMIT

{% tabs %}
{% tab title="Body" %}
```json
{
    "symbol": "NAOVNST",
    "side": "SELL",
    "type": "LIMIT",
    "quantity": 500,
    "quoteOrderQty": 1450000,
    "price": 2900,
    "useQuoteQty": false,
    "timestamp": 1737361908354,
    "signature": "81524e9fbbba63102b98f120d88c907639a09e15534869a782f79dd6a5c1aa29"
}
```
{% endtab %}

{% tab title="200" %}
```json
{
  "status": "ok",
  "data": {
    "displayingId": 435372,
    "userId": 18,
    "side": "BUY",
    "type": "LIMIT",
    "price": 62877.99,
    "liquidityStatus": 1,
    "quantity": 0.07474,
    "executedQty": 0,
    "quoteQty": 4699.5009726,
    "executedQuoteQty": 0,
    "liquidityUsdtPrice": 1,
    "liquidityTransferPrice": 62877.99,
    "liquiditySymbol": "BTCUSDT",
    "liquidityOrderId": "11779887",
    "feeMetadata": {
      "assetId": 22,
      "asset": "USDT",
      "value": 4.6995009726,
      "feeRatio": 0.001,
      "executed": 0
    },
    "useQuoteQty": false,
    "symbol": "BTCUSDT",
    "baseAsset": "BTC",
    "baseAssetId": 9,
    "quoteAsset": "USDT",
    "quoteAssetId": 22,
    "status": "NEW",
    "stopPrice": 0
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
{% endtab %}
{% endtabs %}

## Place Order MARKET

{% tabs %}
{% tab title="Body" %}
```json
{
    "symbol": "NAOVNST",
    "side": "BUY",
    "type": "MARKET",
    "quantity": 1000,
    "quoteOrderQty": 2900000,
    "price": 2900,
    "useQuoteQty": false,
    "timestamp": 1737361908354,
    "signature": "81524e9fbbba63102b98f120d88c907639a09e15534869a782f79dd6a5c1aa29"
}
```
{% endtab %}

{% tab title="200" %}
```json
{
  "status": "ok",
  "data": {
    "displayingId": 435372,
    "userId": 18,
    "side": "BUY",
    "type": "LIMIT",
    "price": 62877.99,
    "liquidityStatus": 1,
    "quantity": 0.07474,
    "executedQty": 0,
    "quoteQty": 4699.5009726,
    "executedQuoteQty": 0,
    "liquidityUsdtPrice": 1,
    "liquidityTransferPrice": 62877.99,
    "liquiditySymbol": "BTCUSDT",
    "liquidityOrderId": "11779887",
    "feeMetadata": {
      "assetId": 22,
      "asset": "USDT",
      "value": 4.6995009726,
      "feeRatio": 0.001,
      "executed": 0
    },
    "useQuoteQty": false,
    "symbol": "BTCUSDT",
    "baseAsset": "BTC",
    "baseAssetId": 9,
    "quoteAsset": "USDT",
    "quoteAssetId": 22,
    "status": "NEW",
    "stopPrice": 0
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
{% endtab %}
{% endtabs %}

## Place Order STOP_LIMIT

{% tabs %}
{% tab title="Body" %}
```json
{
    "symbol": "NAMIVNDC",
    "side": "SELL",
    "type": "STOP_LIMIT",
    "quantity": 300,
    "quoteOrderQty": 270000,
    "price": 280,
    "useQuoteQty": false,
    "stopPrice": 250,
    "timestamp": 1737361908354,
    "signature": "81524e9fbbba63102b98f120d88c907639a09e15534869a782f79dd6a5c1aa29"
}
```
{% endtab %}

{% tab title="200" %}
```json
{
  "status": "ok",
  "data": {
    "displayingId": 435372,
    "userId": 18,
    "side": "BUY",
    "type": "LIMIT",
    "price": 62877.99,
    "liquidityStatus": 1,
    "quantity": 0.07474,
    "executedQty": 0,
    "quoteQty": 4699.5009726,
    "executedQuoteQty": 0,
    "liquidityUsdtPrice": 1,
    "liquidityTransferPrice": 62877.99,
    "liquiditySymbol": "BTCUSDT",
    "liquidityOrderId": "11779887",
    "feeMetadata": {
      "assetId": 22,
      "asset": "USDT",
      "value": 4.6995009726,
      "feeRatio": 0.001,
      "executed": 0
    },
    "useQuoteQty": false,
    "symbol": "BTCUSDT",
    "baseAsset": "BTC",
    "baseAssetId": 9,
    "quoteAsset": "USDT",
    "quoteAssetId": 22,
    "status": "NEW",
    "stopPrice": 0
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
{% endtab %}
{% endtabs %}

## Place Order OCO

{% tabs %}
{% tab title="Body" %}
```json
{
    "symbol": "BTCUSDT",
    "side": "BUY",
    "type": "OCO",
    "quantity": 0.0005,
    "quoteOrderQty": 70,
    "price": 50000,
    "useQuoteQty": false,
    "stopPrice": 63520,
    "limitPrice": 70000,
    "timestamp": 1737361908354,
    "signature": "81524e9fbbba63102b98f120d88c907639a09e15534869a782f79dd6a5c1aa29"
}
```
{% endtab %}

{% tab title="200" %}
```json
{
  "status": "ok",
  "data": {
    "displayingId": 435372,
    "userId": 18,
    "side": "BUY",
    "type": "LIMIT",
    "price": 62877.99,
    "liquidityStatus": 1,
    "quantity": 0.07474,
    "executedQty": 0,
    "quoteQty": 4699.5009726,
    "executedQuoteQty": 0,
    "liquidityUsdtPrice": 1,
    "liquidityTransferPrice": 62877.99,
    "liquiditySymbol": "BTCUSDT",
    "liquidityOrderId": "11779887",
    "feeMetadata": {
      "assetId": 22,
      "asset": "USDT",
      "value": 4.6995009726,
      "feeRatio": 0.001,
      "executed": 0
    },
    "useQuoteQty": false,
    "symbol": "BTCUSDT",
    "baseAsset": "BTC",
    "baseAssetId": 9,
    "quoteAsset": "USDT",
    "quoteAssetId": 22,
    "status": "NEW",
    "stopPrice": 0
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
{% endtab %}
{% endtabs %}