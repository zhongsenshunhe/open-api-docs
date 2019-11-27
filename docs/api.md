# API

支持 REST API 和 WebSocket API 两种。

## REST API

Request Method: 仅支持GET和POST，GET为只读请求，POST为创建、修改、删除等请求。

Request URI: 以`/v1`开头的URI。

Request Parameter:

- 如果请求为GET，所有参数均以URL参数传递，例如：`symbol=BTC_USDT&limit=100`，URL参数总是以`&`分隔，参数需要正确的URL编码。

- 如果请求为POST，参数以JSON作为BODY传递，且必须指定`Content-Type: application/json`。例如：

```json
{
    "type": "BUY_LIMIT",
    "symbol": "BTC_USDT",
    "price": 5601.02,
    "amount": 1.05,
    "fillOrKill": true
}
```

### JSON参数类型

- STRING: 字符串参数，必须以`"..."`括起来；
- NUMBER: 浮点数，例如`1.23`，`456`，`-0.001`；（注：整数也是浮点数）
- INTEGER: 整数，例如`1099`，但不可为浮点数；
- BOOLEAN: 布尔值，必须为`true`或`false`；
- NULL: 空值，`null`。

如果是必须参数，则必须传递，如果是可选参数，则不必传递。

可选参数如果不传，后台视作默认值。默认值请参考具体的API文档。
