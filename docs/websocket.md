# WebSocket API

WebSocket API用于接收WebSocket推送事件。

## 如何连接

WebSocket的URL是: `wss://<ws-domain-name>/v1/market/notification`

使用JavaScript连接示例代码：

```javascript
var ws = new WebSocket('wss://wss.thdax.com/v1/market/notification');
```

连接成功后，所有消息均以JSON格式收发。

## 如何订阅

连接成功后，客户端首先需要订阅某个交易对。

示例代码：

```javascript
var msg = JSON.stringify({"action": "subscribe", "symbol": "BTC_USDT"});
ws.send(msg);
```

说明：

通过WebSocket只能发送String，因此必须手动使用`JSON.stringify`将消息序列化为JSON字符串。

没有主动发送订阅消息时，客户端接收不到任何消息。

消息内容：

```javascript
{
    "action": "subscribe",
    "symbol": "BTC_USDT"
}
```

参数说明：

- action: STRING，使用`"subscribe"`表示订阅
- symbol: STRING，待订阅的交易对名称

订阅成功后，所有BTC_USDT相关的事件将被推送。

## 接收消息

当收到消息后，该消息总是一个JSON字符串。解析后获得一个包含两个元素的数组，第一个STRING表示消息类型，第二个对象表示消息本身。

示例代码：

```javascript
ws.onmessage = function (event) {
    // 第一步：解析JSON字符串:
    var data = JSON.parse(event.data);
    // 第二步：解析消息类型和消息对象
    if (Array.isArray(data) && data.length==2) {
        var
            topic = data[0], // 第一个元素是消息类型，例如`"topic_bar"`
            message = data[1]; // 第二个元素是消息对象本身
        // 打印消息类型和消息本身便于调试:
        console.log(topic);
        console.log(JSON.stringify(message, null, '  '));
        if (topic === 'topic_snapshot') {
            // process snapshot:
        } else if (topic === 'topic_prices') {
            // process prices:
        } else if (topic === 'topic_tick') {
            // process tick:
        } else if (topic === 'topic_bar') {
            // process bar:
        } else if (topic === 'topic_order') {
            // process order:
        }
    }
};
```

消息类型：

- topic_snapshot: 盘口深度快照
- topic_tick: 最新成交信息
- topic_prices: 所有Symbol的最新价格信息
- topic_bar: 新的K线图信息
- topic_order: 订单成交信息

### 如何绘制K线图

第一步：使用REST API一次性获取历史数据；

第二步：通过WebSocket接收最新的K线。
