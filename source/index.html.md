---
title: API 文档

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

includes:

search: true

meta:
  - name: description
    content: Documentation for the mexc global API
---

# 介绍

## API Key 设置

- 很多接口需要API Key才可以访问. 请参考[这个页面](https://www.mexc.com/user/openapi)来设置API Key.
- 设置API Key的同时，为了安全，建议设置IP访问白名单(未添加白名单有效期为90天).
- 永远不要把你的API key/secret告诉给任何人
  
<aside class="warning">如果不小心泄露了API key，请立刻删除此Key, 并可以另外生产新的Key.</aside>
 
## API Key 权限设置

在创建API Key时勾选所需要的权限

## API 代码库

我们为开发者提供了Python,DotNET,Java,Javascript,Go五种语言的SDK,提供用户直接通过SDK调用API的方法。目前支持现货所有接口。

[https://github.com/mxcdevelop/mexc-api-sdk](https://github.com/mxcdevelop/mexc-api-sdk)

<aside class="notice">
使用中遇到问题请通过<a href="https://github.com/mxcdevelop/mexc-api-sdk/issues" target="_blank">提交问题</a>反馈
</aside>

## 联系我们

- MEXC API电报群 [MEXC API Support Group](https://t.me/MEXCAPIsupport)
  - 咨询文档中没有提及的API问题
  - 咨询API或者websocket性能方面的问题
  - 咨询做市相关的问题
- MEXC 客服 *官网、app中在线客服*
  -  咨询关于钱包、短信、2FA等问题

# 更新日志

| 时间       | 接口 | 更新类型 | 说明            |
| ---------- | ---- | -------- | --------------- |
| 2022-02-08 | *    | 新增     | REST API V3发布 |


# 基本信息

## 接入URL

请选用以下的baseurl进行API请求：

- ```https://api.mexc.com```

## HTTP 返回代码

- HTTP 4XX 错误码用于指示错误的请求内容、行为、格式。问题在于请求者。
- HTTP 401 表示身份认证、权限错误。
- HTTP 403 错误码表示违反WAF限制(Web应用程序防火墙)。
- HTTP 429 错误码表示警告访问频次超限，即将被封IP。
- HTTP 5XX 错误码用于指示MEXC服务端的问题。

## 请求格式

相应API接受GET，POST或DELETE类型的请求

- GET 方法的接口, 参数必须在 query string中发送。
- POST, PUT, 和 DELETE 方法的接口,参数可以在内容形式为application/x-www-form-urlencoded的 query string 中发送，也可以在 request body 中发送。如果你喜欢，也可以混合这两种方式发送参数。
- 对参数的顺序不做要求。但如果同一个参数名在query string和request body中都有，query string中的会被优先采用。

## 返回格式

所有接口的返回数据均为JSON形式

## 签名
- 调用SIGNED 接口时，除了接口本身所需的参数外，还需要在query string 或 request body中传递 signature, 即签名参数。
- 签名使用HMAC SHA256算法. API-KEY所对应的API-Secret作为 HMAC SHA256 的密钥，其他所有参数作为HMAC SHA256的操作对象，得到的输出即为签名。
- 签名 **大小写不敏感.**
- "totalParams"定义为与"request body"串联的"query string"。

### 时间安全

> 伪代码示例

```
 if (timestamp < (serverTime + 1000) && (serverTime - timestamp) <= recvWindow)
  {
    // process request
  } 
  else 
  {
    // reject request
  }
```

- 签名接口均需要传递timestamp参数，其值应当是请求发送时刻的unix时间戳(毫秒)。
- 服务器收到请求时会判断请求中的时间戳，如果是5000毫秒之前发出的，则请求会被认为无效。这个时间空窗值可以通过发送可选参数recvWindow来定义。

关于交易时效性互联网状况并不完全稳定可靠,因此你的程序本地到MEXC服务器的时延会有抖动。这是我们设置recvWindow的目的所在，如果你从事高频交易，对交易时效性有较高的要求，可以灵活设置recvWindow以达到你的要求。

<aside class="notice">推荐使用5秒以下的 recvWindow! 最多不能超过 60秒!</aside>

### POST /api/v3/order 举例

>  Example 1

```shell
HMAC SHA256 signature:

    $ echo -n "symbol=BTCUSDT&side=BUY&type=LIMIT&quantity=1&price=11&recvWindow=5000&timestamp=1644489390087" | openssl dgst -sha256 -hmac "45d0b3c26f2644f19bfb98b07741b2f5"
    (stdin)= ddbaf78eaf7abc69ce44d7781cc9e53b5aaee48c890a20d606fd825c9ee2a285
```

```shell
curl command:

    (HMAC SHA256)
    $ curl -H "X-MEXC-APIKEY: mx0aBYs33eIilxBWC5" -X POST 'https://api.mexc.com/api/v3/order' -d 'symbol=BTCUSDT&side=BUY&type=LIMIT&quantity=1&price=11&recvWindow=5000&timestamp=1644489390087&signature=ddbaf78eaf7abc69ce44d7781cc9e53b5aaee48c890a20d606fd825c9ee2a285'

```

>  Example 2

```shell
HMAC SHA256 signature:

    $ echo -n "symbol=BTCUSDT&side=BUY&type=LIMIT&quantity=1&price=11&recvWindow=5000&timestamp=1644489390087" | openssl dgst -sha256 -hmac "45d0b3c26f2644f19bfb98b07741b2f5"
    (stdin)= ddbaf78eaf7abc69ce44d7781cc9e53b5aaee48c890a20d606fd825c9ee2a285
```

```shell
curl command:

    (HMAC SHA256)
    $ curl -H "X-MEXC-APIKEY: mx0aBYs33eIilxBWC5" -X POST 'https://api.mexc.com/api/v3/order' -d 'symbol=BTCUSDT&side=BUY&type=LIMIT&quantity=1&price=11&recvWindow=5000&timestamp=1644489390087&signature=ddbaf78eaf7abc69ce44d7781cc9e53b5aaee48c890a20d606fd825c9ee2a285'

```


>  Example 3

```shell
HMAC SHA256 signature:

    $ echo -n "symbol=BTCUSDT&side=BUY&type=LIMITquantity=1&price=11&recvWindow=5000&timestamp=1644489390087" | openssl dgst -sha256 -hmac "45d0b3c26f2644f19bfb98b07741b2f5"
    (stdin)= ddbaf78eaf7abc69ce44d7781cc9e53b5aaee48c890a20d606fd825c9ee2a285
```

```shell
curl command:

    (HMAC SHA256)
    $ curl -H "X-MEXC-APIKEY: mx0aBYs33eIilxBWC5" -X POST 'https://api.mexc.com/api/v3/order?symbol=BTCUSDT&side=BUY&type=LIMIT' -d 'quantity=1&price=11&recvWindow=5000&timestamp=1644489390087&signature=ddbaf78eaf7abc69ce44d7781cc9e53b5aaee48c890a20d606fd825c9ee2a285'

```

以下是在linux bash环境下使用 echo openssl 和curl工具实现的一个调用接口下单的示例 apikey、secret仅供示范

| Key       | Value                                                            |
| --------- | ---------------------------------------------------------------- |
| apiKey    | mx0aBYs33eIilxBWC5                                               |
| secretKey | 45d0b3c26f2644f19bfb98b07741b2f5 |



| 参数       | 取值          |
| ---------- | ------------- |
| symbol     | BTCUSDT       |
| side       | BUY           |
| type       | LIMIT         |
| quantity   | 1             |
| price      | 11            |
| recvWindow | 5000          |
| timestamp  | 1644489390087 |

**示例 1: 所有参数通过 request body 发送**

- requestBody:
symbol=BTCUSDT
&side=BUY
&type=LIMIT
&quantity=1
&price=11
&recvWindow=5000
&timestamp=1644489390087

**所有参数通过 query string 发送**

- queryString:
symbol=BTCUSDT
&side=BUY
&type=LIMIT
&quantity=1
&price=11
&recvWindow=5000
&timestamp=1644489390087

**示例 3: 混合使用 query string 和 request body**

- queryString:
symbol=BTCUSDT&side=BUY&type=LIMIT

- requestBody:
quantity=1&price=11&recvWindow=5000&timestamp=1644489390087

请注意，签名与示例3不同。 "LIMIT"和"quantity = 1"之间没有＆。
## 限频规则

对REST API的访问有频率限制，当超出限制时，返回状态429：请求过于频繁

需要携带access key进行访问的接口，以账号作为限速的基本单位；不需要携带access key进行访问的接口，以IP作为限速的基本单位

未说明限速规则的接口默认为20次/秒

# 接入说明

## 签名操作的组成

请求Header中签名相关参数

| 组成部分            | 说明                   |
| ------------------- | ---------------------- |
| ```X-MEXC-APIKEY``` | API key中的access key  |
| ```Content-Type```  | ```application/json``` |

## 签名方法 

1. 对于公共接口,不需要签名。

2. 对于私有接口,需要在header中传入X-MEXC-APIKEY、Signature、Content-Type 必须指定为application/json，Signature为签名字符串

* 签名规则如下:
    1. 签名时需要先获得请求参数字符串，无参时为""：<br />对于GET/DELETE请求，按Querystring拼接业务参数以&间隔，并最终获得签名目标串（在批量操作的API中，若参数值中有逗号等特殊符号，这些符号在签名时需要做URL encode）。<br />对于POST请求，签名参数为json字符串（无需进行字典排序）。
    2. 获得参数字符串后，再拼接签名目标串，规则为：accessKey+时间戳+获取到的参数字符串
    3. 使用HMAC SHA256算法对目标串用SecretKey进行签名，并最终将签名作为参数携带到header中

注意：

  1)参与签名的业务参数为null时，不参与签名；注意get请求将参数拼接至url上时，如果参数为null， 后台解析时，会解析成""，POST请求，参数为null时，不要传该参数，或者签名时，将该参数的值设置为""，否则会出现验签失败。

  2)请求时将签名时用到的Request-Time的值放入header的Request-Time参数中，获得的签名字符串放入header的Signature参数中，将APIKEY的Access Key放在header的ApiKey参数中，其余业务参数按正常传递即可。

  3)获得的签名字符串不需要进行base64进行编码。

# 行情接口

## 测试服务器连通性

> 响应示例

```json
{}
```

- **GET** ```/api/v3/ping```

测试能否联通 Rest API。

参数：

NONE

## 获取服务器时间

> 响应示例

```json
{
    "serverTime" : 1645539742000
}
```

- **GET** ```/api/v3/time ```
  
参数：

NONE

## 交易规范信息

> 响应示例

```json
{
  "timezone": "UTC",
  "serverTime": 1642403250139,
  "rateLimits": [],
  "exchangeFilters": [],
  "symbols": [{
      "symbol": "ABCDEFGSSSUSDT",
      "status": "DISABLED",
      "baseAsset": "ABCDEFGSSS",
      "baseAssetPrecision": 1,
      "quoteAsset": "USDT",
      "quotePrecision": 1,
      "quoteAssetPrecision": 1,
      "baseCommissionPrecision": 1,
      "quoteCommissionPrecision": 1,
      "orderTypes": ["LIMIT", "LIMIT_MAKER"],
      "icebergAllowed": false,
      "ocoAllowed": false,
      "quoteOrderQtyMarketAllowed": false,
      "isSpotTradingAllowed": true,
      "isMarginTradingAllowed": false,
      "permissions": ["SPOT"],
      "filters": []
  }]
}

```

- **GET** ```/api/v3/exchangeInfo```

获取交易规则和交易对信息。


参数：

三种用法

| 用法         | 举例                                                                          |
| ------------ | ----------------------------------------------------------------------------- |
| 不需要交易对 | curl -X GET "https://api.mexc.com/api/v3/exchangeInfo"                        |
| 单个交易对   | curl -X GET "https://api.mexc.com/api/v3/exchangeInfo?symbol=MXUSDT"          |
| 多个交易对   | curl -X GET "https://api.mexc.com/api/v3/exchangeInfo?symbols=MXUSDT,BTCUSDT" |


## 深度信息

> 响应示例

```json
{
  "lastUpdateId": 1112416,
  "bids": [
      ["15.00000", "49999.00000"]
  ],
  "asks": [
    ["14.0000", "1.0000"]
  ]
}
```

- **GET** ```/api/v3/depth```

参数：

| 参数名 | 数据类型 | 是否必须 | 说明       | 取值范围            |
| ------ | -------- | -------- | ---------- | ------------------- |
| symbol | string   | 是       | 交易对名称 |                     |
| limit  | integer  | 否       | 返回的条数 | 默认 100; 最大 5000 |

响应：

| 参数名       | 数据类型 | 说明                |
| ------------ | -------- | ------------------- |
| lastUpdateId | long     | 成交时间            |
| bids         | list     | 买盘 [价位, 挂单量] |
| asks         | list     | 卖盘 [价位, 挂单量] |

## 近期成交列表

> 响应示例

```json
[
  {
    "id": null,
    "price": "23",
    "qty": "0.478468",
    "quoteQty": "11.004764",
    "time": 1640830579240,
    "isBuyerMaker": true,
    "isBestMatch": true
  }
]
```

- **GET** ```/api/v3/trades```

参数：

| 参数名 | 数据类型 | 是否必须 | 说明       | 取值范围            |
| ------ | -------- | -------- | ---------- | ------------------- |
| symbol | string   | 是       | 交易对名称 |                     |
| limit  | integer  | 否       | 返回的条数 | 默认 500; 最大 1000 |


响应：

| 参数名       | 说明           |
| ------------ | -------------- |
| id           | 成交id         |
| price        | 价格           |
| qty          | 数量           |
| quoteQty     | 成交额         |
| time         | 成交时间       |
| isBuyerMaker | 是否为maker单  |
| isBestMatch  | 是否为最佳匹配 |

## 近期成交列表

> 响应示例

```json
[
  {
    "id": null,
    "price": "23",
    "qty": "0.478468",
    "quoteQty": "11.004764",
    "time": 1640830579240,
    "isBuyerMaker": true,
    "isBestMatch": true
  }
]
```

- **GET** ```/api/v3/historicalTrades```

参数：

| 参数名 | 数据类型 | 是否必须 | 说明                                             | 取值范围            |
| ------ | -------- | -------- | ------------------------------------------------ | ------------------- |
| symbol | string   | 是       | 交易对名称                                       |                     |
| limit  | integer  | 否       | 返回的条数                                       | 默认 500; 最大 1000 |
| fromId | integer  | 否       | 从哪一条成交id开始返回. 缺省返回最近的成交记录。 |                     |


响应：

| 参数名       | 说明           |
| ------------ | -------------- |
| id           | 成交id         |
| price        | 价格           |
| qty          | 数量           |
| quoteQty     | 成交额         |
| time         | 成交时间       |
| isBuyerMaker | 是否为maker单  |
| isBestMatch  | 是否为最佳匹配 |

## 近期成交(归集)

> 响应示例

```json
[
  {
    "a": null,
    "f": null,
    "l": null,
    "p": "46782.67",
    "q": "0.0038",
    "T": 1641380483000,
    "m": false,
    "M": true
  }
]
```

- **GET** ```/api/v3/aggTrades```
  
归集交易与逐笔交易的区别在于，同一价格、同一方向、同一时间的trade会被聚合为一条

参数：

| 参数名    | 数据类型 | 是否必须 | 说明                               | 取值范围            |
| --------- | -------- | -------- | ---------------------------------- | ------------------- |
| symbol    | string   | 是       | 交易对名称                         |                     |
| fromId    | long     | 否       | 从包含fromId的成交id开始返回结果   |                     |
| startTime | long     | 否       | 从该时刻之后的成交记录开始返回结果 |                     |
| endTimne  | long     | 否       | 返回该时刻为止的成交记录           |                     |
| limit     | integer  | 否       | 返回的条数                         | 默认 500; 最大 1000 |


响应：

| 参数名 | 说明                                       |
| ------ | ------------------------------------------ |
| a      | 归集成交ID                                 |
| f      | 被归集的首个成交ID                         |
| l      | 被归集的末个成交ID                         |
| p      | 成交价                                     |
| q      | 成交量                                     |
| T      | 成交时间                                   |
| m      | 是否为主动卖出单                           |
| M      | 是否为最优撮合单(可忽略，目前总为最优撮合) |

## K线数据

> 响应示例

```json
[
  [
    1640804880000, 
    "47482.36", 
    "47482.36", 
    "47416.57", 
    "47436.1", 
    "3.550717", 
    1640804940000, 
    "168387.3"
  ]
]
```

- **GET** ```/api/v3/kline```
  
每根K线代表一个交易对。
每根K线的开盘时间可视为唯一ID

参数：

| 参数名    | 数据类型 | 是否必须 | 说明                |
| --------- | -------- | -------- | ------------------- |
| symbol    | string   | 是       | 交易对名称          |
| interval  | ENUM     | 是       | 见枚举定义：K线间隔 |
| startTime | long     | 否       |                     |
| endTimne  | long     | 否       |                     |
| limit     | integer  | 否       | 默认 500; 最大 1000 |


响应：

| 索引 | 说明     |
| ---- | -------- |
| 0    | 开盘时间 |
| 1    | 开盘价   |
| 2    | 最高价   |
| 3    | 最低价   |
| 4    | 收盘价   |
| 5    | 成交量   |
| 6    | 收盘时间 |
| 7    | 成交额   |

## 当前平均价格


> 响应示例

```json
{
  "mins": 5,
  "price": "9.35751834"
}
```

- **GET** ```/api/v3/avgPrice```

参数：

| 参数名 | 数据类型 | 是否必须 | 说明       |
| ------ | -------- | -------- | ---------- |
| symbol | string   | 是       | 交易对名称 |


响应：

| 参数名 | 说明         |
| ------ | ------------ |
| mins   | 均价时间范围 |
| price  | 价格         |

## 24小时价格滚动情况


> 响应示例

```json
{
    "symbol": "BTCUSDT",
    "priceChange": "184.34",
    "priceChangePercent": "0.00400048",
    "prevClosePrice": "46079.37",
    "lastPrice": "46263.71",
    "lastQty": "",
    "bidPrice": "46260.38",
    "bidQty": "",
    "askPrice": "46260.41",
    "askQty": "",
    "openPrice": "46079.37",
    "highPrice": "47550.01",
    "lowPrice": "45555.5",
    "volume": "1732.461487",
    "quoteVolume": null,
    "openTime": 1641349500000,
    "closeTime": 1641349582808,
    "count": null
}
or
[
  {
    "symbol": "BTCUSDT",
    "priceChange": "184.34",
    "priceChangePercent": "0.00400048",
    "prevClosePrice": "46079.37",
    "lastPrice": "46263.71",
    "lastQty": "",
    "bidPrice": "46260.38",
    "bidQty": "",
    "askPrice": "46260.41",
    "askQty": "",
    "openPrice": "46079.37",
    "highPrice": "47550.01",
    "lowPrice": "45555.5",
    "volume": "1732.461487",
    "quoteVolume": null,
    "openTime": 1641349500000,
    "closeTime": 1641349582808,
    "count": null
  },
  {
    "symbol": "ETHUSDT",
    "priceChange": "184.34",
    "priceChangePercent": "0.00400048",
    "prevClosePrice": "46079.37",
    "lastPrice": "46263.71",
    "lastQty": "",
    "bidPrice": "46260.38",
    "bidQty": "",
    "askPrice": "46260.41",
    "askQty": "",
    "openPrice": "46079.37",
    "highPrice": "47550.01",
    "lowPrice": "45555.5",
    "volume": "1732.461487",
    "quoteVolume": null,
    "openTime": 1641349500000,
    "closeTime": 1641349582808,
    "count": null
  }
]
```

- **GET** ```/api/v3/ticker/25hr```

参数：

| 参数名 | 数据类型 | 是否必须 | 说明                              |
| ------ | -------- | -------- | --------------------------------- |
| symbol | string   | 否       | 交易对名称 不传查全部（谨慎使用） |


响应：

| 参数名             | 说明       |
| ------------------ | ---------- |
| symbol             | 交易对     |
| priceChange        | 价格变化   |
| priceChangePercent | 价格变化比 |
| prevClosePrice     | 前一收盘价 |
| lastPrice          | 最新价     |
| lastQty            | 最新量     |
| bidPrice           | 买盘价格   |
| bidQty             | 买盘数量   |
| askPrice           | 卖盘价格   |
| askQty             | 卖盘数量   |
| openPrice          | 开始价     |
| highPrice          | 最高价     |
| lowPrice           | 最低价     |
| volume             | 成交量     |
| quoteVolume        | 成交额     |
| openTime           | 开始时间   |
| closeTime          | 结束时间   |
| count              |            |

## 最新价格

> 响应示例

```json
{
    "symbol": "BTCUSDT",
    "price": "184.34"
}
or
[
  {
    "symbol": "BTCUSDT",
    "price": "6.65"
  },
  {
    "symbol": "ETHUSDT",
    "price": "5.65"
  }
]
```

- **GET** ```/api/v3/price```

参数：

| 参数名 | 数据类型 | 是否必须 | 说明                  |
| ------ | -------- | -------- | --------------------- |
| symbol | string   | 否       | 交易对名称 不传查全部 |


响应：

| 参数名 | 说明     |
| ------ | -------- |
| symbol | 交易对   |
| price  | 最新价格 |

## 当前最优挂单

> 响应示例

```json
{
  "symbol": "AEUSDT",
  "bidPrice": "0.11001",
  "bidQty": "115.59",
  "askPrice": "0.11127",
  "askQty": "215.48"
}
OR
[
  {
    "symbol": "AEUSDT",
    "bidPrice": "0.11001",
    "bidQty": "115.59",
    "askPrice": "0.11127",
    "askQty": "215.48"
  },
  {
    "symbol": "AEUSDT",
    "bidPrice": "0.11001",
    "bidQty": "115.59",
    "askPrice": "0.11127",
    "askQty": "215.48"
  }
]
```

- **GET** ```/api/v3/ticker/bookTicker```


返回当前最优的挂单(最高买单，最低卖单)

参数：

| 参数名 | 数据类型 | 是否必须 | 说明                  |
| ------ | -------- | -------- | --------------------- |
| symbol | string   | 否       | 交易对名称 不传查全部 |


响应：

| 参数名   | 说明         |
| -------- | ------------ |
| symbol   | 交易对       |
| bidPrice | 最高买盘价   |
| bidQty   | 最高买盘数量 |
| askPrice | 最低卖盘价   |
| askQty   | 最低卖盘数量 |
# 现货账户和交易接口

## 测试下单

> 响应示例

```json
{}
```

- **POST** ```/api/v3/order/test```

用于测试订单请求，但不会提交到撮合引擎

参数：

同于 POST /api/v3/order

## 下单

> 响应示例

```json
{
    "symbol": "BTCUSDT",
    "orderId": "1196315350023612316",
    "orderListId": -1
}
```

- **POST** ```/api/v3/order```

参数：

| 名称             | 类型    | 是否必需 | 描述                   |
| ---------------- | ------- | -------- | ---------------------- |
| symbol           | STRING  | YES      | 交易对                 |
| side             | ENUM    | YES      | 详见枚举定义：订单方向 |
| type             | ENUM    | YES      | 详见枚举定义：订单类型 |
| quantity         | DECIMAL | NO       | 委托数量               |
| price            | DECIMAL | NO       | 委托价格               |
| newClientOrderId | STRING  | NO       | 客户自定义的唯一订单ID |
| recvWindow       | LONG    | NO       | 赋值不能大于 60000     |
| timestamp        | LONG    | YES      |                        |

枚举值
|名称||

## 撤销订单
> 响应示例

```json
{
  "symbol": "LTCBTC",
  "origClientOrderId": "myOrder1",
  "orderId": 4,
  "orderListId": -1, // OCO订单ID，否则为 -1
  "clientOrderId": "cancelMyOrder1",
  "price": "2.00000000",
  "origQty": "1.00000000",
  "executedQty": "0.00000000",
  "cummulativeQuoteQty": "0.00000000",
  "status": "CANCELED",
  "timeInForce": "GTC",
  "type": "LIMIT",
  "side": "BUY"
}
```

- **DELETE** ```/api/v3/order```

取消有效订单。

参数：

| 参数名            | 数据类型 | 是否必须 | 说明                   |
| ----------------- | -------- | -------- | ---------------------- |
| symbol            | string   | 是       | 交易对名称             |
| orderId           | string   | 否       | 订单Id                 |
| origClientOrderId | string   | 否       | 订单Id                 |
| newClientOrderId  | string   | NO       | 客户自定义的唯一订单ID |
| recvWindow        | long     | 否       |                        |
| timestamp         | long     | 是       |                        |

orderId 或 origClientOrderId 必须至少发送一个

响应：

| 参数名              | 说明             |
| ------------------- | ---------------- |
| symbol              | 交易对           |
| origClientOrderId   | 原始客户端订单id |
| orderId             | 订单id           |
| clientOrderId       | 客户端id         |
| price               | 价格             |
| origOty             | qi shi           |
| executedQty         | 交易的订单数量   |
| cummulativeQuoteQty | 累计交易金额     |
| status              | 状态             |
| timeInForce         | 订单有效方式     |
| type                | 订单类型         |
| side                | 订单方向         |
## 撤销单一交易对所有订单
> 响应示例

```json
[
  {
    "symbol": "BTCUSDT",
    "origClientOrderId": "E6APeyTJvkMvLMYMqu1KQ4",
    "orderId": 11,
    "orderListId": -1,
    "clientOrderId": "pXLV6Hz6mprAcVYpVMTGgx",
    "price": "0.089853",
    "origQty": "0.178622",
    "executedQty": "0.000000",
    "cummulativeQuoteQty": "0.000000",
    "status": "CANCELED",
    "timeInForce": "GTC",
    "type": "LIMIT",
    "side": "BUY"
  },
  {
    "symbol": "BTCUSDT",
    "origClientOrderId": "A3EF2HCwxgZPFMrfwbgrhv",
    "orderId": 13,
    "orderListId": -1,
    "clientOrderId": "pXLV6Hz6mprAcVYpVMTGgx",
    "price": "0.090430",
    "origQty": "0.178622",
    "executedQty": "0.000000",
    "cummulativeQuoteQty": "0.000000",
    "status": "CANCELED",
    "timeInForce": "GTC",
    "type": "LIMIT",
    "side": "BUY"
  }
]
```

- **DELETE** ```/api/v3/openOrders```

撤销单一交易对下所有挂单, 包括OCO的挂单。

参数：

| 参数名     | 数据类型 | 是否必须 | 说明   |
| ---------- | -------- | -------- | ------ |
| symbol     | string   | 是       | 交易对 |
| recvWindow | long     | 否       |        |
| timestamp  | long     | 是       |        |


响应：

| 参数名              | 说明             |
| ------------------- | ---------------- |
| symbol              | 交易对           |
| origClientOrderId   | 原始客户端订单id |
| orderId             | 订单id           |
| clientOrderId       | 客户端id         |
| price               | 价格             |
| origOty             | qi shi           |
| executedQty         | 交易的订单数量   |
| cummulativeQuoteQty | 累计交易金额     |
| status              | 状态             |
| timeInForce         | 订单有效方式     |
| type                | 订单类型         |
| side                | 订单方向         |

## 查询订单
> 响应示例

```json
{
  "symbol": "LTCBTC", // 交易对
  "orderId": 1, // 系统的订单ID
  "orderListId": -1, // OCO订单的ID，不然就是-1
  "clientOrderId": "myOrder1", // 客户自己设置的ID
  "price": "0.1", // 订单价格
  "origQty": "1.0", // 用户设置的原始订单数量
  "executedQty": "0.0", // 交易的订单数量
  "cummulativeQuoteQty": "0.0", // 累计交易的金额
  "status": "NEW", // 订单状态
  "timeInForce": "GTC", // 订单的时效方式
  "type": "LIMIT", // 订单类型， 比如市价单，现价单等
  "side": "BUY", // 订单方向，买还是卖
  "stopPrice": "0.0", // 止损价格
  "icebergQty": "0.0", // 冰山数量
  "time": 1499827319559, // 订单时间
  "updateTime": 1499827319559, // 最后更新时间
  "isWorking": true, // 订单是否出现在orderbook中
  "origQuoteOrderQty": "0.000000" // 原始的交易金额
}
```

- **GET** ```/api/v3/order```

查询订单状态。

参数：

| 参数名            | 数据类型         | 是否必须 | 说明 |
| ----------------- | ---------------- | -------- | ---- |
| symbol            | 交易对           | 是       |      |
| origClientOrderId | 原始客户端订单id | 否       |      |
| orderId           | 订单id           | 否       |      |
| recvWindow        | long             | 否       |      |
| timestamp         | long             | 是       |      |


响应：

| 参数名              | 说明              |
| ------------------- | ----------------- |
| symbol              | 交易对            |
| origClientOrderId   | 原始客户端订单id  |
| orderId             | 系统订单id        |
| clientOrderId       | 客户自定义id      |
| price               | 价格              |
| origOty             | 原始订单数量      |
| executedQty         | 交易的订单数量    |
| cummulativeQuoteQty | 累计订单金额      |
| status              | 订单状态          |
| timeInForce         | 订单的时效方式    |
| type                | 订单类型          |
| side                | 订单方向          |
| stopPrice           | 止损价格          |
| icebergQty          | 冰山数量          |
| time                | 订单时间          |
| updateTime          | 最后更新时间      |
| isWorking           | 是否在orderbook中 |
| origQuoteOrderQty   | 原始的交易金额    |

## 当前挂单

> 响应示例

```json
[
  {
    "symbol": "LTCBTC",
    "orderId": 1,
    "orderListId": -1, 
    "clientOrderId": "myOrder1",
    "price": "0.1",
    "origQty": "1.0",
    "executedQty": "0.0",
    "cummulativeQuoteQty": "0.0",
    "status": "NEW",
    "timeInForce": "GTC",
    "type": "LIMIT",
    "side": "BUY",
    "stopPrice": "0.0",
    "icebergQty": "0.0",
    "time": 1499827319559,
    "updateTime": 1499827319559,
    "isWorking": true,
    "origQuoteOrderQty": "0.000000"
  }
]
```

- **GET** ```/api/v3/openOrders```

获取交易对的所有当前挂单

参数：

| 参数名     | 数据类型 | 是否必须 | 说明   |
| ---------- | -------- | -------- | ------ |
| symbol     | string   | 是       | 交易对 |
| recvWindow | long     | 否       |        |
| timestamp  | long     | 是       |        |


响应：

| 参数名              | 说明              |
| ------------------- | ----------------- |
| symbol              | 交易对            |
| origClientOrderId   | 原始客户端订单id  |
| orderId             | 系统订单id        |
| clientOrderId       | 客户自定义id      |
| price               | 价格              |
| origOty             | 原始订单数量      |
| executedQty         | 交易的订单数量    |
| cummulativeQuoteQty | 累计订单金额      |
| status              | 订单状态          |
| timeInForce         | 订单的时效方式    |
| type                | 订单类型          |
| side                | 订单方向          |
| stopPrice           | 止损价格          |
| icebergQty          | 冰山数量          |
| time                | 订单时间          |
| updateTime          | 最后更新时间      |
| isWorking           | 是否在orderbook中 |
| origQuoteOrderQty   | 原始的交易金额    |

## 查询所有订单

> 响应示例

```json
[
  {
    "symbol": "LTCBTC",
    "orderId": 1,
    "orderListId": -1, 
    "clientOrderId": "myOrder1",
    "price": "0.1",
    "origQty": "1.0",
    "executedQty": "0.0",
    "cummulativeQuoteQty": "0.0",
    "status": "NEW",
    "timeInForce": "GTC",
    "type": "LIMIT",
    "side": "BUY",
    "stopPrice": "0.0",
    "icebergQty": "0.0",
    "time": 1499827319559,
    "updateTime": 1499827319559,
    "isWorking": true,
    "origQuoteOrderQty": "0.000000"
  }
]
```

- **GET** ```/api/v3/allOrders```

获取所有帐户订单； 有效，已取消或已完成。

参数：

| 参数名     | 数据类型 | 是否必须 | 说明                 |
| ---------- | -------- | -------- | -------------------- |
| symbol     | string   | 是       | 交易对               |
| orderId    | string   | 否       | 订单id               |
| startTime  | long     | 否       |                      |
| endTime    | long     | 否       |                      |
| limit      | int      | 否       | 默认 500; 最大 1000; |
| recvWindow | long     | 否       |                      |
| timestamp  | long     | 是       |                      |


响应：

| 参数名              | 说明              |
| ------------------- | ----------------- |
| symbol              | 交易对            |
| origClientOrderId   | 原始客户端订单id  |
| orderId             | 系统订单id        |
| clientOrderId       | 客户自定义id      |
| price               | 价格              |
| origOty             | 原始订单数量      |
| executedQty         | 交易的订单数量    |
| cummulativeQuoteQty | 累计订单金额      |
| status              | 订单状态          |
| timeInForce         | 订单的时效方式    |
| type                | 订单类型          |
| side                | 订单方向          |
| stopPrice           | 止损价格          |
| icebergQty          | 冰山数量          |
| time                | 订单时间          |
| updateTime          | 最后更新时间      |
| isWorking           | 是否在orderbook中 |
| origQuoteOrderQty   | 原始的交易金额    |
## 账户信息

> 响应示例

```json
{
    "makerCommission": 20,
    "takerCommission": 20,
    "buyerCommission": 0,
    "sellerCommission": 0,
    "canTrade": true,
    "canWithdraw": true,
    "canDeposit": true,
    "updateTime": null,
    "accountType": "SPOT",
    "balances": [{
        "asset": "NBNTEST",
        "free": "1111078",
        "locked": "33"
    }, {
        "asset": "MAIN",
        "free": "1020000",
        "locked": "0"
    }],
    "permissions": ["SPOT"]
}
```

- **GET** ```/api/v3/account```

获取当前账户信息

参数：

| 参数名     | 数据类型 | 是否必须 | 说明 |
| ---------- | -------- | -------- | ---- |
| recvWindow | long     | 否       |      |
| timestamp  | long     | 是       |      |


响应：

| 参数名           | 说明       |
| ---------------- | ---------- |
| makerCommission  | maker 费率 |
| takerCommission  | taker 费率 |
| buyerCommission  |            |
| sellerCommission |            |
| canTrade         | 是否可交易 |
| canWithdraw      | 是否可提现 |
| canDeposit       | 是否可充值 |
| updateTime       | 更新时间   |
| accountType      | 账户类型   |
| balances         | 余额       |
| asset            | 资产币种   |
| free             | 可用数量   |
| locked           | 冻结数量   |
| permissions      | 权限       |
## 账户成交历史

> 响应示例

```json
[
  {
    "symbol": "BNBBTC", // 交易对
    "id": 28457, // trade ID
    "orderId": 100234, 
    "orderListId": -1, 
    "price": "4.00000100", 
    "qty": "12.00000000", 
    "quoteQty": "48.000012", 
    "commission": "10.10000000", 
    "commissionAsset": "BNB", 
    "time": 1499865549590, 
    "isBuyer": true, 
    "isMaker": false, 
    "isBestMatch": true
  }
]
```

- **GET** ```/api/v3/myTrades```


获取账户指定交易对的成交历史

参数：

| 参数名     | 数据类型 | 是否必须 | 说明                   |
| ---------- | -------- | -------- | ---------------------- |
| symbol     | string   | 是       | 交易对                 |
| orderId    | string   | 否       | 必须和symbol一起使用   |
| startTime  | long     | 否       |                        |
| endTime    | long     | 否       |                        |
| fromId     | long     | 否       | 起始Id默认查询最新交易 |
| limit      | int      | 否       | 默认 500; 最大 1000;   |
| recvWindow | long     | 否       |                        |
| timestamp  | long     | 是       |                        |


响应：

| 参数名          | 说明              |
| --------------- | ----------------- |
| symbol          | 交易对            |
| id              | 成交id            |
| orderId         | 订单id            |
| price           | 价格              |
| qty             | 数量              |
| quoteQty        | 成交金额          |
| time            | 成交时间          |
| commission      | 交易费金额        |
| commissionAsset | 交易类资产类型    |
| time            | 交易时间          |
| isBuyerMaker    | 是否为买方maker单 |
| isBestMatch     | 是否为最佳匹配    |


# 公开API参数

## 枚举定义

### 订单方向

- BUY 买入
- SELL 卖出

### 订单类型

- LIMIT 限价单
- LIMIT_MAKER 限价只挂单
