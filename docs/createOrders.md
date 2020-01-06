# current orders API  创建新订单

请求格式：POST /v1/spots/orders`

请求参数：

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|type |是  |string |方向：SHORT-卖，LONG-买   |
|direction |是  |string | LIMIT-限价，MARKET-市价    |
|price |是  |BigDecimal |单价   |
|symbol |是  |string | 币对：BTC_USDT    |
|quantity |是  |BigDecimal |数量   |
|triggerDirection |是  |String | 触发方向：SHORT-卖，LONG-买    |
|triggerOn |是  |BigDecimal |触发价格   |
|trailingDistance |是  |BigDecimal | 终止价格    |
|fillOrKill |是  |boolean |默认false   |
|immediateOrCancel |是  |boolean | 默认false    |
|postOnly |是  |boolean | 默认false    |
|hidden |是  |boolean | 默认false    |

请求示例：

```bash
POST https://api.zssh.com/v1/spots/orders
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
		"quoteCurrencyId": 105,
		"chargeQuote": true,
		"baseCurrencyId": 100,
		"type": "LIMIT",
		"sequenceId": 163177,
		"triggerDirection": "LONG",
		"features": 0,
		"createdAt": 1576767427750,
		"trailing": false,
		"unfilledQuantity": 0.20,
		"price": 7115.00,
		"takerFeeRate": 0.002,
		"id": 1631771912,
		"direction": "LONG",
		"updatedAt": 1576767427750,
		"triggerOn": 0,
		"quantity": 0.20,
		"makerFeeRate": -0.001,
		"marginTrade": false,
		"trailingBasePrice": 0,
		"userId": 10000,
		"fillPrice": 0.0,
		"status": "PENDING"
	},
	"msg": "success",
	"ts": 1576767427757
}
```

响应参数：

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|code |int   |处理结果code  |
|msg |String   |处理结果描述信息  |
|ts |long   |请求结果生成时间戳  |
|data |T   |处理结果数据信息  |
|status |String   |PENDING-待成交，FULLY_FILLED-完全成交，PARTIAL_FILLED-部分成交  |

