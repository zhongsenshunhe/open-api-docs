# cancel orders API 取消订单

请求格式：POST /v1/spots/orders/<orderId>/cancel`

请求参数：

- orderId: Long, REQUIRED, order id in the request URI.

请求示例：

```bash
POST https://api.zssh.com/v1/spots/orders/12800178/cancel
```

响应示例：

```json
{
	"code": 0,
	"data": {
		"symbolId": 100105,
		"hidden": false,
		"trailingDistance": 0,
		"fee": 0,
		"chargeQuote": true,
		"type": "LIMIT",
		"sequenceId": 92359,
		"triggerDirection": "LONG",
		"features": 0,
		"createdAt": 1576565222406,
		"trailing": false,
		"unfilledQuantity": 1E+1,
		"price": 4E+3,
		"takerFeeRate": 0.002,
		"id": 923591912,
		"direction": "LONG",
		"updatedAt": 1576767049306,
		"triggerOn": 0,
		"quantity": 1E+1,
		"makerFeeRate": -0.001,
		"marginTrade": false,
		"trailingBasePrice": 0,
		"userId": 10005,
		"fillPrice": 0.0,
		"status": "FULLY_CANCELLED"
	},
	"msg": "success",
	"ts": 1576767049313
}
```

响应参数：

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|code |int   |处理结果code  |
|msg |String   |处理结果描述信息  |
|ts |long   |请求结果生成时间戳  |
|data |T   |处理结果数据信息  |
|status |String   |FULLY_CANCELLED-完全取消，PARTIAL_CANCELLED-部分取消  |

