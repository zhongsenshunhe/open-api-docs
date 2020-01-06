# one orders API 获取单个委托信息

请求格式：GET /v1/spots/orders/{orderId}`

请求参数

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|orderId |是  |string |订单编号   |

请求示例：

```bash
GET https://api.zssh.com/v1/spots/orders/{orderId}
```

响应示例：

```json
{
	"code": 0,
	"msg": "success",
	"ts": 1577511919567,
	"data": {
		"id": 1160001912,
		"userId": 10000,
		"features": 0,
		"price": 39,
		"fee": 0,
		"fillPrice": 0.0,
		"marginTrade": false,
		"chargeQuote": false,
		"quantity": 34,
		"unfilledQuantity": 34,
		"makerFeeRate": 0.002,
		"takerFeeRate": 0.002,
		"type": "LIMIT",
		"status": "PENDING",
		"direction": "LONG",
		"triggerDirection": "LONG",
		"triggerOn": 0,
		"trailingBasePrice": 0,
		"trailingDistance": 0,
		"createdAt": 1577448907960,
		"updatedAt": 1577448907960,
		"symbol": "LTC_USDT",
		"trailing": false
	}
```

响应参数：

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|code |int   |处理结果code  |
|msg |String   |处理结果描述信息  |
|ts |long   |请求结果生成时间戳  |
|userId |String   |用户id  |
|price |Decimal   |订单价格  |
|fee |Decimal   |手续费  |
|fillPrice |Decimal   |平均成交价  |
|quantity |Decimal   |委托数量  |
|unfilledQuantity |String   |未成交数量  |
|makerFeeRate |double   |maker手续费  |
|takerFeeRate |double   |taker手续费  |
|type |String   |委托类型  |
|status |String   |状态  |
|direction |String   |方向  |
|symbol |String   |币对  |

