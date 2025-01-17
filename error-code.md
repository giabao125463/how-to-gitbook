---
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

# Error Code

#### Example Error Response

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

## Error Codes

<table><thead><tr><th width="347">Error Status</th><th width="134">Error Code</th><th>Description</th></tr></thead><tbody><tr><td>UNKNOWN</td><td>1000</td><td>Unknown error</td></tr><tr><td>INVALID_ORDER_TYPE</td><td>1110</td><td>Invalid order type</td></tr><tr><td>INVALID_SIDE</td><td>1111</td><td>Invalid side</td></tr><tr><td>BAD_SYMBOL</td><td>1112</td><td>Bad symbol</td></tr><tr><td>INVALID_REQUEST_ID</td><td>1112</td><td>Invalid request ID</td></tr><tr><td>NO_SUCH_ORDER</td><td>2013</td><td>No such order</td></tr><tr><td>TRADE_NOT_ALLOWED</td><td>3004</td><td>Trade not allowed</td></tr><tr><td>ACCOUNT_BAN_TRADE</td><td>3005</td><td>Account banned from trading</td></tr><tr><td>NOT_FOUND_ORDER</td><td>6101</td><td>Order not found</td></tr><tr><td>NOT_ENOUGH_BASE_ASSET</td><td>6102</td><td>Not enough base asset</td></tr><tr><td>NOT_ENOUGH_QUOTE_ASSET</td><td>6103</td><td>Not enough quote asset</td></tr><tr><td>BROKER_ERROR</td><td>6104</td><td>Broker error</td></tr><tr><td>NOT_ENOUGH_FEE_ASSET</td><td>6106</td><td>Not enough fee asset</td></tr><tr><td>STOP_LIMIT_INVALID_STOP_PRICE</td><td>6107</td><td>Stop limit invalid stop price</td></tr><tr><td>STOP_LIMIT_UNKNOWN_LAST_PRICE</td><td>6108</td><td>Stop limit unknown last price</td></tr><tr><td>STOP_LIMIT_INVALID_MIN_TOTAL</td><td>6109</td><td>Stop limit invalid minimum total</td></tr><tr><td>ORDER_TYPE_NOT_SUPPORT</td><td>6110</td><td>Order type not supported</td></tr></tbody></table>

