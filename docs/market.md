# Market API

## trades

获取当前所有交易信息。

请求格式：`GET /v1/market/trades`

请求参数：无

请求示例：

```bash
GET https://api.thdax.com/v1/market/trades
```

响应示例：

```json
{
    "currencies": [
        {
            "name": "BTC",
            "depositEnabled": true,
            "withdrawEnabled": true
        },
        {
            "name": "USDT",
            "depositEnabled": true,
            "withdrawEnabled": true
        },
        ...
    ],
    "symbols": [
        {
            "name": "BTC_USDT",
            "baseName": "BTC",
            "quoteName": "USDT",
            "baseScale": 4,
            "quoteScale": 2,
            "baseMinimum": 0.01,
            "quoteMinimum": 0.01,
            "startTime": 0,
            "endTime": 5000000000000
        },
        ...
    ]
}
```

响应说明：

- currencies: ARRAY，所有货币列表
  - 数组元素: 每个元素表示一种货币
    - name: 货币名称（唯一标识）
    - depositEnabled: 当前是否允许存款
    - withdrawEnabled: 当前是否允许取款
- symbols: ARRAY，所有交易对列表
  - 数组元素: 每个元素表示一个交易对
    - name: 交易对名称（唯一标识）
    - baseName: 交易货币名称，例如`"BTC"`
    - quoteName: 计价货币名称，例如`"USDT"`
    - baseScale: 交易货币的最小交易单位，例如`4`表示`0.0001`，即4位小数
    - quoteScale: 计价货币的最小交易单位，例如`2`表示`0.01`，即2位小数
    - baseMinimum: 卖出时的最小数量
    - quoteMinimum: 买入时的最小数量
    - startTime: 开始交易时间戳
    - endTime: 结束交易时间戳

如果当前时间戳小于`startTime`，则交易尚未开始，如果如果当前时间戳大于`endTime`，则交易已结束。

## prices

获取当前所有交易对的24小时价格数据。

请求格式：`GET /v1/market/prices`

请求参数：无

请求示例：

```bash
GET https://api.thdax.com/v1/market/prices
```

响应示例：

```json
{
    "BTC_USDT": [ 1556163658073, 5458.17, 5479.88, 5451.41, 5459.88, 10.2637 ],
    "ETH_USDT": [ 1555048079711, 152.33, 156.73, 144.01, 147.82, 181.93 ]
}
```

响应说明：

- key: 每个key是symbol名称.
- value: 每个value是以array`[INTEGER, NUMBER, NUMBER, NUMBER, NUMBER, NUMBER]`表示的bar数据:
  - index 0: 当前时间戳.
  - index 1: Open price.
  - index 2: High price.
  - index 3: Low price.
  - index 4: Close price (latest price).
  - index 5: 成交量.

## depth

获取当前交易对的盘口深度数据。

请求格式：`GET  https://api.thdax.com/v1/market/depth/<symbol>`

请求参数：

- symbol: 交易对名称

请求示例：

```bash
GET  https://api.thdax.com/v1/market/depth/BTC_USDT
```

响应示例：

```json
{
    "symbol": "BTC_USDT",
    "sequenceId": 9700676,
    "timestamp": 1556163666773,
    "price": 5459.88,
    "buyOrders": [
        {
            "price": 5459.54,
            "amount": 0.1184
        },
        {
            "price": 5456.41,
            "amount": 0.1125
        },
        ...
    ],
    "sellOrders": [
        {
            "price": 5459.88,
            "amount": 0.1514
        },
        {
            "price": 5460.82,
            "amount": 0.1048
        },
        ...
    ]
}
```

响应说明：

- symbol: 当前交易对名称
- sequenceId: 当前深度快照的交易序列号
- timestamp: 当前深度快照的时间戳
- buyOrders: 价格从高到低的买盘：
  - 数组元素: 每个元素代表一个盘口深度
    - price: 盘口价格
    - amount: 该价格的累加数量
- sellOrders: 价格从低到高的卖盘，数组结构与买盘一致。

## bars

获取当前K线图

请求格式：`GET /v1/market/bars/<symbol>/<barType>`

请求参数：

- symbol: 当前交易对名称
- barType: K线类型
  - K_1_SEC: 秒K
  - K_1_MIN: 分钟K
  - K_1_HOUR: 小时K
  - K_1_DAY: 日K

请求示例：

```bash
GET https://api.thdax.com/v1/market/bars/BTC_USDT/K_1_DAY
```

响应示例：

```json
{
    "bars": [
        [ 1551888000000, 3911.03, 3940.96, 3892.35, 3925.86, 157.84 ],
        [ 1551974400000, 3924.81, 3947.92, 3907.86, 3932.43, 161.41 ],
        ...
    ]
}
```

响应说明：

- bars: ARRAY，包含K线的数组
  - 数组元素: 每个元素都是一个包含6个元素的数组，分别是：`[时间戳, 开盘价, 最高价, 最低价, 收盘价, 成交量]`，时间戳是整数，毫秒值，价格和成交量是NUMBER类型。

示例：

```json
[ 1551888000000, 3911.03, 3940.96, 3892.35, 3925.86, 157.84 ]
```

表示：该K线开始时间戳`1551888000000` = `2019-03-07 00:00 GMT+8:00`，开盘价`3911.03`，最高`3940.96`，最低`3892.35`，收盘价`3925.86`，成交量`157.84`。

注意：

只能获取秒K、分钟K、小时K和日K的数据，没有10分钟K、2小时K、周K的数据。

若需要获取周K的数据，必须首先获取日K数据，然后进行聚合计算。

秒K、分钟K、小时K仅返回最近的若干条历史记录，具体返回数量取决于交易所配置。日K将返回所有历史数据。

## feeRates

获取当前费率信息。

请求格式：`GET /v1/market/feeRates`

请求参数：无

请求示例：

```bash
GET https://api.thdax.com/v1/market/feeRates
```

响应示例：

```json
{
    "timestamp": 1556688883709,
    "alwaysChargeQuote": true,
    "defaultFeeRates": {
        "takerFeeRate": 0.002,
        "makerFeeRate": 0.002
    }
    "symbolFeeRates": {
        "BTC_USDT": {
            "takerFeeRate": 0.002,
            "makerFeeRate": -0.001
        },
        "ETH_USDT": {
            "takerFeeRate": 0.002,
            "makerFeeRate": 0
        },
        ...
    }
}
```

响应说明：

- timestamp: INTEGER，请求时刻服务器的当前时间戳，毫秒
- alwaysChargeQuote: BOOLEAN，是否总是收取Quote费用。例如，对`BTC_USDT`交易对，如果为`true`，表示买卖双方均收取`USDT`手续费，若为`false`，则买方收取`BTC`，卖方收取`USDT`作为手续费。
- defaultFeeRates: 系统默认手续费率
  - takerFeeRate: 吃单手续费率，例如`0.002`表示千分之二
  - makerFeeRate: 挂单手续费率，例如`0.001`表示千分之一
- symbolFeeRates: 各交易对设定的手续费率
  - KEY: 交易对名称
  - VALUE: 交易对手续费
    - takerFeeRate: 吃单手续费率，例如`0.002`表示千分之二
    - makerFeeRate: 挂单手续费率，例如`0.001`表示千分之一

注：

手续费率可以为0，表示零手续费。

手续费率可以为负，表示交易时不但不收取手续费，还将补贴手续费给用户。对maker设置负费率表示将用taker的部分手续费补贴maker，以鼓励用户提供流动性。

未列出的交易对，表示使用默认手续费率。

## timestamp

获取服务器当前时间戳。

请求格式：`GET /v1/market/timestamp`

请求参数：无

请求示例：

```bash
GET https://api.thdax.com/v1/market/timestamp
```

响应示例：

```json
{
    "timestamp": 1556613212712
}
```

响应说明：

- timestamp: INTEGER，服务器当前时间戳，毫秒
