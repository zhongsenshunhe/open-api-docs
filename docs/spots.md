# Spots API  获取spots资产

请求格式：`GET /v1/spots/accounts`

请求参数：无

请求示例：

```bash
GET https://api.zssh.com/v1/spots/accounts
```

响应示例：

```json
{
	"code": 0,
	"msg": "success",
	"ts": 1576765080477,
	"data": {
		"BTC": [9282608.000000000000000000, 0, 0],
		"USDT": [9282558.000000000000000000, 0E-18, 0],
		"ARM": [70.000000000000000000, 0, 0]
	}
}
```

响应参数：

|参数名|类型|说明|
|:-----  |:-----|-----                           |
|code |int   |处理结果code  |
|msg |String   |处理结果描述信息  |
|ts |long   |请求结果生成时间戳  |
|data |T   |处理结果数据信息  |

内容：币种:[可用,冻结,锁定]

