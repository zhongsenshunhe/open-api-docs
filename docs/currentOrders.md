# create orders API  当前委托

请求格式：GET /v1/spots/orders/closed`

请求参数

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|range |是  |string |查询月份：201912   |
|symbol |是  |string |币对名称：BTC_USDT   |
|offsetId |是  |decimal | 起始订单id默认0    |
|limit     |是  |decimal | 每页条数    |

请求示例：

```bash
GET https://api.zssh.com/v1/spots/orders/closed
```

响应示例：

```json
{
	"code": 0,
	"msg": "success",
	"ts": 1576767979458,
	"data": {
		"range": "201912",
		"hasMore": true,
		"nextOffsetId": 1633501912,
		"results": [{
			"id": 1633871912,
			"sequenceId": 163387,
			"userId": 10000,
			"symbolId": 100105,
			"type": "LIMIT",
			"status": "FULLY_FILLED",
			"direction": "LONG",
			"features": 0,
			"fillPrice": 7127.0,
			"price": 7130.000000000000000000,
			"makerFeeRate": -0.001000000000000000,
			"takerFeeRate": 0.002000000000000000,
			"fee": 1.425400000000000000,
			"triggerDirection": "LONG",
			"triggerOn": 0E-18,
			"trailingBasePrice": 0E-18,
			"trailingDistance": 0E-18,
			"createdAt": 1576767962250,
			"updatedAt": 1576767962250,
			"baseCurrencyId": 100,
			"quoteCurrencyId": 105,
			"chargeQuote": true,
			"marginTrade": false,
			"quantity": 0.100000000000000000,
			"unfilledQuantity": 0E-18,
			"trailing": false
		}...]
	}
}
```

响应参数：

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|code |int   |处理结果code  |
|msg |String   |处理结果描述信息  |
|ts |long   |请求结果生成时间戳  |
|range |String   |查询月份  |
|hasMore |boolean   |是否有更多  |
|nextOffsetId |int   |下一页id  |
|results |T   |数组头  |
|baseCurrencyId |String   |基本币  |
|quoteCurrencyId |String   |计价币  |
|chargeQuote |String   |费用  |
|marginTrade |boolean   |是保证金交易  |
|fee |String   |手续费  |
|type |String   |LIMIT-限价单  |
|status |String   |FULLY_FILLED-完成成交  |
|makerFeeRate |String   |maker费率  |
|takerFeeRate |String   |taker费率  |
|quantity |String   |数量  |
|price |String   |单价  |

