# history orders API  历史委托

请求格式：GET /v1/spots/orders/open`

请求参数：无

请求示例：

```bash
GET https://api.zssh.com/v1/spots/orders/open
```

响应示例：

```json
{
	"code": 0,
	"msg": "success",
	"ts": 1576769173591,
	"data": {
		"results": [{
			"id": 1632621912,
			"userId": 10000,
			"symbolId": 100105,
			"symbol": null,
			"features": 0,
			"price": 7129.00,
			"fee": 0,
			"fillPrice": 0.0,
			"marginTrade": false,
			"chargeQuote": true,
			"quantity": 112.00,
			"unfilledQuantity": 112.00,
			"makerFeeRate": -0.001,
			"takerFeeRate": 0.002,
			"type": "LIMIT",
			"status": "PENDING",
			"direction": "SHORT",
			"triggerDirection": "LONG",
			"triggerOn": 0,
			"trailingBasePrice": 0,
			"trailingDistance": 0,
			"createdAt": 1576767605063,
			"updatedAt": 1576767605063,
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
|status |String   |FULLY_FILLED-完成成交,PENDING-待成交，PARTIAL_FILLED-部分成交  |
|makerFeeRate |String   |maker费率  |
|takerFeeRate |String   |taker费率  |
|quantity |String   |数量  |
|price |String   |单价  |

