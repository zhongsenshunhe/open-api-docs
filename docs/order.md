# Order API

## Get exist order by id

请求格式：`GET /v1/trade/orders/<orderId>`

请求参数：

- orderId: INTEGER, REQUIRED, order id in the request URI.

请求示例：

```bash
GET https://api.thdax.com/v1/trade/orders/12800178
```

响应示例：

```json
{
    "id": 12800178,
    "userId": 903821,
    "type": "SELL_LIMIT",
    "symbol": "BTC_USDT",
    "status": "FULLY_FILLED",
    "price": 5200.00,
    "amount": 1.02,
    "filledAmount": 1.02,
    "features": 1,
    "triggerOn": 0,
    "feeCurrency": "USDT",
    "fee": 3.20,
    "makerFeeRate": -0.001,
    "takerFeeRate": 0.002,
    "chargeQuote": true,
    "source": "iPhoneXR",
    "createdAt": 1543659847880,
    "updatedAt": 1543659850143
}
```

响应参数：

- id: INTEGER, order id.
- userId: INTEGER, user id who own this order.
- type: STRING, order type.
- symbol: STRING, symbol for trade.
- status: STRING, order status as enumeration, see explaination below.
- price: NUMBER, limit price or market spent.
- amount: NUMBER, order amount.
- filledAmount: NUMBER, filled amount at current time.
- features: INTEGER, combined with constants, see explaination below.

order status enumeration:

- SUBMITTED: just submitted, waiting for sequencing
- SEQUENCED: waiting for processing or processing now. Order with this status may partially filled if filledAmount is positive.
- FULLY_FILLED: completely filled
- FULLY_CANCELLED: completely cancelled (nothing bought or sold)
- PARTIAL_CANCELLED: partial cancelled (not fully bought or sold)

order features bit set:

- FILL_OR_KILL = 1 (0b0001)
- POST_ONLY = 2 (0b0010)
- HIDDEN = 4 (0b0100)
- IMMEDIATE_OR_CANCEL = 8 (0b1000)
- TRAILING_STOP = 1024 (0b10000000000)

Features Example:

If features = 6, it combined with POST_ONLY (2) and HIDDEN (4).

### Get exist orders

### Create Order

URL: POST /v1/trade/orders

Parameters:

- type: STRING, REQUIRED, OrderType enum: `"BUY_LIMIT"`, `"SELL_LIMIT"`, `"BUY_MARKET"`, `"SELL_MARKET"`.

- symbol: STRING, REQUIRED, symbol for trade, e.g. `"BTC_USDT"`.

- price: NUMBER, REQUIRED when type is "BUY_LIMIT", "SELL_LIMIT", "BUY_MARKET", order price, e.g. `5506.99`.

- amount: NUMBER, REQUIRED when type is "BUY_LIMIT", "SELL_LIMIT", "SELL_MARKET", order amount, e.g. `1.25`.

- triggerOn: NUMBER, OPTIONAL, the trigger price if set, e.g. `5800.00`.

- fillOrKill: BOOLEAN, OPTIONAL, set true for fill-or-kill flag, only works for limit order. Default to `false`.

- immediateOrCancel: BOOLEAN, OPTIONAL, set true for immediate-or-cancel flag, only works for limit order. Default to `false`.

- postOnly: BOOLEAN, OPTIONAL, set true for post-only flag, only works for limit order. Default to `false`.

- hidden: BOOLEAN, OPTIONAL, set true for hidden flag, only works for limit order. Default to `false`.

- trailingStop: BOOLEAN, OPTIONAL, set true for trailing-stop flag, only works for market order with triggerOn. If trailingStop is true, the triggerOn is not the trigger price, but the trigger price distance. Default to `false`.

- source: STRING, OPTIONAL, any string with `0~9`, `a-z`, `A-Z` and `_`. e.g. `"APP"`, `"WEB"`. The maximum length is 32. Default to empty string `""`.

Request example:

```bash
POST https://api.thdax.com/v1/trade/orders

{
    "type": "BUY_LIMIT",
    "symbol": "BTC_USDT",
    "price": 5521.05,
    "amount": 1.06,
    "postOnly": true,
    "source": "iPhoneXR"
}
```

响应示例：

```json
{
    "id": 12800178,
    "userId": 903821,
    "status": "SUBMITTED",
    ...
}
```

响应字段含义与Get exist order by id完全一致。

错误响应示例：

```json
{
    "error": "ACCOUNT_FREEZE_FAILED",
    "data": null,
    "message": "No enough balance to freeze"
}
```

错误码`ACCOUNT_FREEZE_FAILED`表示冻结失败，原因是没有足够可用的金额。
