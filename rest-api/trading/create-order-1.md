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

Prerequisites

Before using this endpoint, ensure you have read the [How to Generate a Signature](../../authentication.md) guide. This guide explains the steps required to create the `signature` parameter needed to authenticate your request.

#### Key Notes

1. The request body must include the required parameters, detailed below.
2. You must provide a valid `timestamp` and `signature` in the request body.
3. The `x-api-key` must be included in the request headers for authentication.

## Place Order

<mark style="color:green;">`POST`</mark> `https://nami.exchange/api/v4/spot/order`

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| x-api-key     | `<Your secret key>`|

**Body**

| Name        | Type   | Description      |
| --------    | ------ | ---------------- |
| `symbol`    | string | Name of the user |
| `price`     | number | Age of the user  |
| `stopPrice` | number | Age of the user  |
| `side`      | number | Age of the user  |
| `type`      | number | Age of the user  |
| `quantity`      | number | Age of the user  |
| `quoteOrderQty`      | number | Age of the user  |
| `useQuoteQty`      | number | Age of the user  |
| `signature`      | number | Age of the user  |
| `timestamp`      | number | Age of the user  |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "id": 1,
  "name": "John",
  "age": 30
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

