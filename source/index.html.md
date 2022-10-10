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
- 永远不要把你的API key/secret告诉给任何人.
  
<aside class="warning">如果不小心泄露了API key，请立刻删除此Key, 并可以另外生产新的Key.</aside>

## API Key 权限设置

在创建API Key时勾选所需要的权限

## API 代码库

我们为开发者提供了Python,DotNET,Java,Javascript,Go五种语言的SDK,提供用户直接通过SDK调用API的方法。目前支持现货所有接口。

[https://github.com/mxcdevelop/mexc-api-sdk](https://github.com/mxcdevelop/mexc-api-sdk)

<aside class="notice">
使用中遇到问题请通过<a href="https://github.com/mxcdevelop/mexc-api-sdk/issues" target="_blank">提交问题</a>反馈
</aside>
## Demo示例

我们提供了5种语言的demo，用户可以参考，目前支持了现货，推送等示例，后续会持续更新。

https://github.com/mxcdevelop/mexc-api-demo

使用中遇到问题请通过[提交问题](https://github.com/mxcdevelop/mexc-api-demo/issues)反馈

### Postman Collections

现在你可以通过`Postman collection`来快速体验、使用API接口。
如果想了解更多如何使用Postman，请访问: [Mexc API Postman](https://github.com/mxcdevelop/mexc-api-postman)

## 联系我们

- MEXC API电报群 [MEXC API Support Group](https://t.me/MEXCAPIsupport)
  - 咨询文档中没有提及的API问题
  - 咨询API或者websocket性能方面的问题
  - 咨询做市相关的问题
- MEXC 客服 *官网、app中在线客服*
  -  咨询关于钱包、短信、2FA等问题

# 更新日志

## **（更新预告）2022-10-14 16:00(UTC+8)**

- 更新部分[钱包接口](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#ec5249e068)，具体如下，请提前做好准备：

  1、[提币接口](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#096be69702)：提币时，参数address和memo需要分别正确传入（原memo在address后以冒号拼接）；

  2、[获取提币历史](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#66382f2bd0)：参数address和memo分别正确返回（原memo在address后以冒号拼接）；

  3、[获取充值地址](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#aba7aa7a08)：返回参数tag改为memo，且充值所需memo会在memo参数中返回；

  4、[获取充值历史](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#70f3430304)：返回参数addressTag改为memo，且充值所需memo会在memo参数中返回；

## **2022-09-06**

- 新增邀请返佣相关接口：

  1、[获取邀请返佣记录](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#8254d412a1)：获取您邀请的好友以及从他们进行的交易产生的返佣；

  2、[获取返佣记录明细 （奖励记录）](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#72fbc63aa1)：您可查看您的好友以及好友的子账户进行合约和现货（非杠杆)交易产生的每笔返佣记录；

  3、[获取自返记录明细 （奖励记录）](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#26b3666f08)：您可查看您以被邀請的好友身份进行的每笔合約和现货（无保证金）及从中产生的自返佣记录。

## **2022-09-02**

- 新增v3 websocket：

  1、Websocket 行情推送：包括[逐笔交易（实时）](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#2947d06b59)、[K线 Streams](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#k-streams)、[增量深度信息（实时）](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#efff33c875);

  2、Websocket账户信息推送:包括[成交推送（实时）](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#444af6a5fa)和[订单推送（实时）](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#ef28329b2a)；

## **2022-08-26**

- [获取杠杆ETF基础信息](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#etf-2)接口新增返回参数：

| 字段名称       | 数据类型 | 描述          |
| :------------- | :------- | :------------ |
| preBasket      | string   | 再平衡前篮子  |
| preLeverage    | string   | 再平衡前杠杆  |
| basket         | string   | 再平衡后篮子  |

## **2022-08-15**

- 新增部分母子账户接口：

  1、[母子用户万向划转](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#b588d84077)

  2、[查询母子万向划转历史](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#47ebdabc00)

  3、[开通子账户合约业务](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#e5e82cdf39)

  4、[开通子账户杠杆业务接口](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#6d1ec37c49)

## **2022-08-03**

- 新增部分钱包接口：
  1、[查询币种信息](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#2a7110133d)
  2、[提币](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#096be69702)
  3、[获取充值历史(支持多网络)](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#70f3430304)

  4、[获取提币历史(支持多网络)](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#66382f2bd0)

  5、[获取充值地址 (支持多网络)](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#aba7aa7a08)

  6、[用户万向划转](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#2e7fe13169)
  7、[查询用户万向划转历史](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#7a4f3b3457)

## **2022-07-27**

- 现货[下单](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#fd6ce2a756)接口新增订单类型：IOC和FOK

## **2022-07-15**

- [账户成交历史](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#1c077e2313)接口新增返回参数：

| 参数名          | 说明              |
| :-------------- | :---------------- |
| isSelfTrade     | 是否自成交        |

## **2022-07-08**

- 新增[批量下单](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#de93fae07b)接口：支持单次批量下20单；

## **2022-07-03**

- 钱包接口模块下新增：[查询币种信息](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#2a7110133d)接口，该接口可返回币种是否可充提/提币限额以及智能合约地址等。

## **2022-06-16**

- 新增[杠杆账户和交易](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#34a848ad3d)相关接口；


## **2022-05-22**

- 交易规范信息接口优化
- 下单接口优化，统一返回order id

## **2022-04-25**

- [交易规范信息](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#e7746f7d60)接口新增返回参数：

| 参数名                     | 数据类型 | 说明                |
| :------------------------- | :------- | :------------------ |
| isSpotTradingAllowed       | Boolean  | 是否允许api现货交易 |
| isMarginTradingAllowed     | Boolean  | 是否允许api杠杆交易 |


- [当前挂单](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#066ca582c9)接口优化：支持多交易对查询，每次最多可以传5个symbol。

## **2022-03-29**

- 新增[母子账户](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#86382eac44)相关接口：

  1、[创建子账户](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#c6789f6fd9)

  2、[查看子账户列表](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#efa0aed0d6)

  3、[创建子账户的APIkey](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#apikey)

  4、[查询子账户的APIKey](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#apikey-2)

  5、[删除子账户的APIKey](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#apikey-3)

  6、[母子用户万向划转](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#b588d84077)

  7、[查询母子万向划转历史](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#47ebdabc00)

  8、[开通子账户的合约业务](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#e5e82cdf39)

  9、[开通子账户的杠杆业务](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#6d1ec37c49)

## **2022-03-25**

- 新增[API代码库](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#api)：Postman Collections，可以通过`Postman collection`来快速体验、使用API接口。

## **2022-03-24**

- 新增市价订单详细说明

## **2022-03-21**

- 新增订单状态枚举

## **2022-03-18**

- 新增[订单类型](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#8c6d51826c)：市价单（现货）
- 新增分页说明：startTime和endTime需同时使用

## **2022-03-09**

- 新增枚举类型

## **2022-02-19**

- 新增[ETF接口](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#etf)：包括[获取杠杆ETF基础信息](https://mxcdevelop.github.io/apidocs/spot_v3_cn/#etf-2)

## **2022-02-11**
- 新版API


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

## Header操作的组成

请求Header中签名相关参数

| 组成部分            | 说明                   |
| :------------------- | :---------------------- |
| ```X-MEXC-APIKEY``` | API key中的access key  |
| ```Content-Type```  | ```application/json``` |

## 签名
- 调用SIGNED 接口时，除了接口本身所需的参数外，还需要在query string 或 request body中传递 signature, 即签名参数（在批量操作的API中，若参数值中有逗号等特殊符号，这些符号在签名时需要做URL encode）。
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
    (stdin)= 323c96ab85a745712e95e63cad28903dd8292e4a905e99c4ee3932023843a117
```

```shell
curl command:

    (HMAC SHA256)
    $ curl -H "X-MEXC-APIKEY: mx0aBYs33eIilxBWC5" -X POST 'https://api.mexc.com/api/v3/order' -d 'symbol=BTCUSDT&side=BUY&type=LIMIT&quantity=1&price=11&recvWindow=5000&timestamp=1644489390087&signature=323c96ab85a745712e95e63cad28903dd8292e4a905e99c4ee3932023843a117'

```

>  Example 2

```shell
HMAC SHA256 signature:

    $ echo -n "symbol=BTCUSDT&side=BUY&type=LIMIT&quantity=1&price=11&recvWindow=5000&timestamp=1644489390087" | openssl dgst -sha256 -hmac "45d0b3c26f2644f19bfb98b07741b2f5"
    (stdin)= fd3e4e8543c5188531eb7279d68ae7d26a573d0fc5ab0d18eb692451654d837a
```

```shell
curl command:

    (HMAC SHA256)
    $ curl -H "X-MEXC-APIKEY: mx0aBYs33eIilxBWC5" -X POST 'https://api.mexc.com/api/v3/order' -d 'symbol=BTCUSDT&side=BUY&type=LIMIT&quantity=1&price=11&recvWindow=5000&timestamp=1644489390087&signature=fd3e4e8543c5188531eb7279d68ae7d26a573d0fc5ab0d18eb692451654d837a'

```


>  Example 3

```shell
HMAC SHA256 signature:

    $ echo -n "symbol=BTCUSDT&side=BUY&type=LIMITquantity=1&price=11&recvWindow=5000&timestamp=1644489390087" | openssl dgst -sha256 -hmac "45d0b3c26f2644f19bfb98b07741b2f5"
    (stdin)= d1a676610ceb39174c8039b3f548357994b2a34139a8addd33baadba65684592
```

```shell
curl command:

    (HMAC SHA256)
    $ curl -H "X-MEXC-APIKEY: mx0aBYs33eIilxBWC5" -X POST 'https://api.mexc.com/api/v3/order?symbol=BTCUSDT&side=BUY&type=LIMIT' -d 'quantity=1&price=11&recvWindow=5000&timestamp=1644489390087&signature=d1a676610ceb39174c8039b3f548357994b2a34139a8addd33baadba65684592'

```

以下是在linux bash环境下使用 echo openssl 和curl工具实现的一个调用接口下单的示例 apikey、secret仅供示范

| Key       | Value                            |
| :--------- | :-------------------------------- |
| apiKey    | mx0aBYs33eIilxBWC5               |
| secretKey | 45d0b3c26f2644f19bfb98b07741b2f5 |



| 参数       | 取值          |
| :---------- | :------------- |
| symbol     | BTCUSDT       |
| side       | BUY           |
| type       | LIMIT         |
| quantity   | 1             |
| price      | 11            |
| recvWindow | 5000          |
| timestamp  | 1644489390087 |

**示例 1: 所有参数通过 request body 发送**

- requestBody:
symbol=BTCUSDT&side=BUY&type=LIMIT&quantity=1&price=11&recvWindow=5000&timestamp=1644489390087

**所有参数通过 query string 发送**

- queryString:
symbol=BTCUSDT&side=BUY&type=LIMIT&quantity=1&price=11&recvWindow=5000&timestamp=1644489390087

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

## 错误码

以下为接口可能返回的错误码信息

| 错误码     | 说明                    |
|---------|-----------------------|
| 400     | 请求参数无效                |
| 401     | 签名验证失败                |
| 429     | 请求过于频繁                |
| 10072   | 无效的access key         |
| 10073   | 无效的请求时间               |
| 30000   | 当前交易对已暂停交易            |
| 30001   | 当前交易方向不允许下单           |
| 30002   | 小于最小交易金额              |
| 30003   | 大于最大交易金额              |
| 30004   | 持仓不足                  |
| 30005   | 卖出超额                  |
| 30010   | 下单价格超过范围              |
| 30016   | 暂停交易                  |
| 30019   | API市价单未开启             |
| 30020   | 受限制的交易对，暂不支持API访问     |
| 30021   | 无效的交易对                |
| 700001  | API密钥格式无效             |
| 700002  | 请求的签名无效               |
| 700003  | 此请求的时间戳在 recvWindow 之外 |
| 700004  | 必要参数未传或格式错误           |
| 700005  | recvWindow 必须小于 60000 |
| 700006  | IP非白名单                |
| 700007  | 没有访问端点的权限             |
| 700008  | 参数格式不符合验证规则           |
| 730001  | 交易对不存在                |
| 730002  | 参数不合法                 |
| 730000  | 请求失败,请联系客服人员          |
| 730001  | 用户信息错误                |
| 730002  | 参数错误,请检查              |
| 730003  | 不支持的操作,请联系客服人员        |
| 730100  | 用户状态异常                |
| 730600  | 子账户名称不能为空             |
| 730601  | 子账户必须是8-32位字母和数字组合    |
| 730602  | 子账户备注不能为空             |
| 730700  | 备注不能为空                |
| 730701  | 权限不能为空                |
| 730702  | API KEY权限不存在          |
| 730703  | IP信息错误,超过最大绑定IP数量     |
| 730704  | 绑定的IP格式错误,请重新填写       |
| 730705  | 最多允许创建30组Api Key      |
| 730706  | API KEY 信息不存在         |
| 730707  | accessKey不能为空         |
| 730101  | 用户名已存在                |



# 行情接口

## 测试服务器连通性

测试能否联通 Rest API。

> 请求示例

```
GET /api/v3/ping
```
> 返回示例

```json
{}
```
**HTTP请求**
- **GET** ```/api/v3/ping```



**请求参数**

NONE

**返回参数**

NONE
## 获取服务器时间

获得服务器当前时间戳

> 请求示例

```
GET /api/v3/time
```

> 返回示例

```json
{
    "serverTime" : 1645539742000
}
```
**HTTP请求**

- **GET** ```/api/v3/time ```
  

**请求参数**

NONE


## 交易规范信息

获取交易规则和交易对信息。

> 请求示例

```
GET /api/v3/exchangeInfo?symbol=BTCUSDT
```


> 返回示例

```json
{
    "timezone": "CST",
    "serverTime": 1657256965785,
    "rateLimits": [],
    "exchangeFilters": [],
    "symbols": 
{
            "symbol": "TOMO3LUSDT",
            "status": "ENABLED",
            "baseAsset": "TOMO3L",
            "baseAssetPrecision": 2,
            "quoteAsset": "USDT",
            "quotePrecision": 3,
            "quoteAssetPrecision": 3,
            "baseCommissionPrecision": 2,
            "quoteCommissionPrecision": 3,
            "orderTypes": [
                "LIMIT",
                "LIMIT_MAKER"
            ],
            "quoteOrderQtyMarketAllowed": false,
            "isSpotTradingAllowed": false,
            "isMarginTradingAllowed": false,
            "quoteAmountPrecision": "5",
            "baseSizePrecision": "0.0001",
            "permissions": [
                "SPOT",
                "MARGIN"
            ],
            "filters": [],
            "maxQuoteAmount": "5000000",
            "makerCommission": "0.002",
            "takerCommission": "0.002"
        }
}

```
**HTTP请求**

- **GET** ```/api/v3/exchangeInfo```



**请求参数**

三种用法

| 用法         | 举例                                                                          |
| :------------ | :----------------------------------------------------------------------------- |
| 不需要交易对 | curl -X GET "https://api.mexc.com/api/v3/exchangeInfo"                        |
| 单个交易对   | curl -X GET "https://api.mexc.com/api/v3/exchangeInfo?symbol=MXUSDT"          |
| 多个交易对   | curl -X GET "https://api.mexc.com/api/v3/exchangeInfo?symbols=MXUSDT,BTCUSDT" |

**返回参数**

| 参数名       | 数据类型 | 说明                       |
| :------------ | :-------- |:-------------------------|
| timezone | string | 时区                       |
| serverTime | long | 服务器时间                    |
| rateLimits | Array | 频率限制                     |
| exchangeFilters | Array | 过滤器                      |
| symbol | String | 交易对                      |
| status | String | 状态                       |
| baseAsset | String | 交易币                      |
| baseAssetPrecision | Int | 交易币精度                    |
| quoteAsset | String | 计价币                      |
| quotePrecision | Int | 计价币价格精度                  |
| quoteAssetPrecision | Int | 计价币资产精度                  |
| baseCommissionPrecision | Int | 交易币手续费精度                 |
| quoteCommissionPrecision | Int | 计价币手续费精度                 |
| orderTypes | Array | <a href="#order_type">订单类型</a> |
| quoteOrderQtyMarketAllowed | Boolean | 是否允许市价委托                 |
| isSpotTradingAllowed | Boolean | 是否允许api现货交易              |
| isMarginTradingAllowed | Boolean | 是否允许api杠杆交易              |
| permissions | Array | 权限                       |
| maxQuoteAmount | String | 最大委托数量                   |
| makerCommission | String | marker手续费                |
| takerCommission | String | taker手续费                 |
|quoteAmountPrecision|string| 最小下单金额                   |
|baseSizePrecision|string| 最小下单数量                   |



## 深度信息
获取指定交易对的深度信息，默认返回买卖盘各100条信息

> 请求示例

```
GET /api/v3/depth?symbol=BTCUSDT&limit=200
```

> 返回示例

```json
{
 
  "lastUpdateId": 1377043284,
  "bids": [
        ["30225.77","2.132868"],
        ],
  "asks": [
        ["30225.80","1.130244"],
        ],
}
```
**HTTP请求**

- **GET** ```/api/v3/depth```

**请求参数**


| 参数名 | 数据类型 | 是否必须 | 说明       | 取值范围            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
| symbol | string   | 是       | 交易对名称 |     如：BTCUSDT      |
| limit  | integer  | 否       | 返回的条数 | 默认 100; 最大 5000 |

**返回参数**

| 参数名       | 数据类型 | 说明                |
| :------------ | :-------- | :------------------- |
| lastUpdateId | long     | 最新更新ID            |
| bids         | list     | 买盘 [价位, 挂单量] |
| asks         | list     | 卖盘 [价位, 挂单量] |

## 近期成交列表
获取指定交易对的近期成交信息，默认返回最近500条成交信息。

> 请求示例

```
GET /api/v3/trades?symbol=BTCUSDT&limit=600
```

> 返回示例

```json
[
  {
    "id": null,
    "price": "29919.62",
    "qty": "1.292918",
    "quoteQty": "38683.61525116",
    "time": 1652848049876,
    "isBuyerMaker": true,
    "isBestMatch": true
  },
]
```
**HTTP请求**
- **GET** ```/api/v3/trades```

**请求参数**

| 参数名 | 数据类型 | 是否必须 | 说明       | 取值范围            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
| symbol | string   | 是       | 交易对名称 |  如：BTCUSDT         |
| limit  | integer  | 否       | 返回的条数 | 默认 500; 最大 1000 |


**返回参数**

| 参数名       | 说明           |
| :------------ | :-------------- |
| id           | 成交id         |
| price        | 价格           |
| qty          | 数量           |
| quoteQty     | 成交额         |
| time         | 成交时间       |
| isBuyerMaker | 是否为maker单  |
| isBestMatch  | 是否为最佳匹配 |

<!-- ## 近期成交列表

> 返回示例

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

**请求参数**

| 参数名 | 数据类型 | 是否必须 | 说明       | 取值范围            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
| symbol | string   | 是       | 交易对名称 |                     |
| limit  | integer  | 否       | 返回的条数 | 默认 500; 最大 1000 |


**返回参数**

| 参数名       | 说明           |
| :------------ | :-------------- |
| id           | 成交id         |
| price        | 价格           |
| qty          | 数量           |
| quoteQty     | 成交额         |
| time         | 成交时间       |
| isBuyerMaker | 是否为maker单  |
| isBestMatch  | 是否为最佳匹配 | :-->

## 近期成交(归集)
归集交易与逐笔交易的区别在于，同一价格、同一方向、同一时间的trade会被聚合为一条

> 请求示例

```
GET /api/v3/aggTrades?symbol=BTCUSDT
```

> 返回示例

```json
[
  {
    "a": null,
    "f": null,
    "l": null,
    "p": "29881.4",
    "q": "0.010068",
    "T": 1652848230000,
    "m": false,
    "M": true
  },
]
```
**HTTP请求**

- **GET** ```/api/v3/aggTrades```


**请求参数**


| 参数名    | 数据类型 | 是否必须 | 说明                               | 取值范围            |
| :--------- | :-------- | :-------- | :---------------------------------- | :------------------- |
| symbol    | string   | 是       | 交易对名称   如：BTCUSDT          |                     |
| startTime | long     | 否       | 从该时刻之后的成交记录开始返回结果 |                     |
| endTime   | long     | 否       | 返回该时刻为止的成交记录           |                     |
| limit     | integer  | 否       | 返回的条数                         | 默认 500; 最大 1000 |

注意：startTime和endTime需同时使用

**返回参数**

| 参数名 | 说明                                       |
| :------ | :------------------------------------------ |
| a      | 归集成交ID                                 |
| f      | 被归集的首个成交ID                         |
| l      | 被归集的末个成交ID                         |
| p      | 成交价                                     |
| q      | 成交量                                     |
| T      | 成交时间                                   |
| m      | 是否为主动卖出单                           |
| M      | 是否为最优撮合单(可忽略，目前总为最优撮合) |

## K线数据
获取指定交易对的k线数据，每根K线代表一个交易对。每根K线的开盘时间可视为唯一ID。

> 请求示例

```
GET /api/v3/klines?symbol=BTCUSDT&interval=1m&startTime=1652848049876&endTimne=1652848650458
```

> 返回示例

```json
[
  [
    1652818380000,
    "30082.28",
    "30105.66",
    "30082.28",
    "30084.65",
    "5.838067",
    1652818440000,
    "175741.13"
  ],
]
```
**HTTP请求**

- **GET** ```/api/v3/klines```
  

**请求参数**

| 参数名    | 数据类型 | 是否必须 | 说明                                   |
| :--------- | :-------- | :-------- |:-------------------------------------|
| symbol    | string   | 是       | 交易对名称  如：BTCUSDT                     |
| interval  | ENUM     | 是       | 见枚举定义：<a href="#kline">k线间隔</a> 如：1m |
| startTime | long     | 否       | 如：1652848049876                      |
| endTime  | long     | 否       | 如：1652848650458                      |
| limit     | integer  | 否       | 默认 500; 最大 1000                      |

注意：startTime和endTime需同时使用

**返回参数**

| 索引 | 说明     |
| :---- | :-------- |
| 0    | 开盘时间 |
| 1    | 开盘价   |
| 2    | 最高价   |
| 3    | 最低价   |
| 4    | 收盘价   |
| 5    | 成交量   |
| 6    | 收盘时间 |
| 7    | 成交额   |

## 当前平均价格
获取指定交易对在一定时间范围内的平均价格。

> 请求示例

```
GET /api/v3/avgPrice?symbol=BTCUSDT
```

> 返回示例

```json
{
  "mins": 5,
  "price": "29869.882"
}
```
**HTTP请求**

- **GET** ```/api/v3/avgPrice```

**请求参数**

| 参数名 | 数据类型 | 是否必须 | 说明       |
| :------ | :-------- | :-------- | :---------- |
| symbol | string   | 是       | 交易对名称。如：BTCUSDT  |


**返回参数**

| 参数名 | 说明         |
| :------ | :------------ |
| mins   | 均价时间范围 |
| price  | 价格         |

## 24小时价格滚动情况
获取指定交易对或者所有交易对在24小时内的价格滚动（5分钟为单位）

> 请求示例

```
GET /api/v3/ticker/24hr?symbol=BTCUSDT
```


> 返回示例

```json
{
    "symbol": "BTCUSDT",
    "priceChange": "1588.47",
    "priceChangePercent": "0.07791949",
    "prevClosePrice": "20386.04",
    "lastPrice": "21974.51",
    "bidPrice": "21974.48",
    "bidQty": "0.645732",
    "askPrice": "21974.51",
    "askQty": "5.801688",
    "openPrice": "20386.04",
    "highPrice": "22508.06",
    "lowPrice": "20269.12",
    "volume": "6381.884246",
    "quoteVolume": "135594952.21",
    "openTime": 1657258200000,
    "closeTime": 1657258407860,
    "count": null
}
```
**HTTP请求**

- **GET** ```/api/v3/ticker/24hr```

**请求参数**

| 参数名 | 数据类型 | 是否必须 | 说明                              |
| :------ | :-------- | :-------- | :--------------------------------- |
| symbol | string   | 否       | 交易对名称 不传查全部（谨慎使用） 如：BTCUSDT |


**返回参数**

| 参数名             | 说明       |
| :------------------ | :---------- |
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
获取指定交易对或者所有交易对的最新价格

> 请求示例

```
GET /api/v3/ticker/price?symbol=BTCUSDT
```

> 返回示例

```json
{
    "symbol": "BTCUSDT",
    "price": "29805.02"
}
```
**HTTP请求**

- **GET** ```/api/v3/ticker/price```

**请求参数**

| 参数名 | 数据类型 | 是否必须 | 说明                  |
| :------ | :-------- | :-------- | :--------------------- |
| symbol | string   | 否       | 交易对名称 不传查全部 如：BTCUSDT|


**返回参数**

| 参数名 | 说明     |
| :------ | :-------- |
| symbol | 交易对   |
| price  | 最新价格 |

## 当前最优挂单
获取当前最优的挂单(最高买单，最低卖单)

> 请求示例

```
GET /api/v3/ticker/bookTicker?symbol=BTCUSDT
```

> 返回示例

```json
{
    "symbol": "BTCUSDT",
    "bidPrice": "29820.79",
    "bidQty": "2.241948",
    "askPrice": "29820.82",
    "askQty": "2.301948"
}
```
**HTTP请求**

- **GET** ```/api/v3/ticker/bookTicker```



**请求参数**

| 参数名 | 数据类型 | 是否必须 | 说明                  |
| :------ | :-------- | :-------- | :--------------------- |
| symbol | string   | 否       | 交易对名称 不传查全部 如：BTCUSDT |


**返回参数**

| 参数名   | 说明         |
| :-------- | :------------ |
| symbol   | 交易对       |
| bidPrice | 最高买盘价   |
| bidQty   | 最高买盘数量 |
| askPrice | 最低卖盘价   |
| askQty   | 最低卖盘数量 |


# 母子账户接口

## 创建子账户
获取您的母账户生成一个虚拟子账户

> 请求示例

```
POST /api/v3/sub-account/virtualSubAccount?subAccount=subAccount1&note=1&timestamp={{timestamp}}&signature={{signature}}
```

> 返回示例

```
{
    "subAccount":"subAccount1",
    "note":"1"
}

```

**HTTP请求**

- **POST** ```/api/v3/sub-account/virtualSubAccount```

**请求参数**

| 参数名       | 数据类型   | 是否必需 | 说明       |
| :--------- | :----- | :------- | :--------- |
| subAccount | string | 是      | 子账户名称（8-32个字母加数字）如：subAccount1 |
| note       | string | 是      | 备注  如：1     |
| recvWindow | long   | 否       |            |
| timestamp  | long   | 是      |     |

**返回参数**

| 参数名       | 数据类型 | 说明                |
| :------------ | :-------- | :------------------- |
| subAccount | string | 子账户名称（8-32个字母加数字）如：subAccount1 |
| note       | string | 备注  如：1     |

## 查看子账户列表
获取您的母账户下所有子账户信息

> 请求示例

```
GET /api/v3/sub-account/list?timestamp={{timestamp}}&signature={{signature}}
```

> 返回示例

```
{
    "subAccounts":[
        {
            "subAccount":"subAccount1",
            "isFreeze":false,//是否冻结
            "createTime":1544433328000
        },
        {
            "subAccount":"subAccount2",
            "isFreeze":false,
            "createTime":1544433328000
        }
    ]
}

```

 **HTTP请求**

- **GET**  ```/api/v3/sub-account/list```

**请求参数**

| 名称       | 类型   | 是否必需 | 说明                |
| :--------- | :----- | :------- | :------------------ |
| subAccount | string | 否       | 子账户名称 如：subAccount1          |
| isFreeze   | string | 否       | true or false       |
| page       | int    | 否       | 默认: 1             |
| limit      | int    | 否       | 默认: 10, 最大: 200 |
| timestamp  | long   | 是      |                     |
| recvWindow | long   | 否       |                     |

**返回参数**

| 参数名       | 数据类型 | 说明                |
| :------------ | :-------- | :------------------- |
| subAccount | string | 子账户名称 |
| isFreeze | string | 是否冻结 |
| createTime | long | 创建时间 |


## 创建子账户的APIkey
为子账户创建APIkey

> 请求示例

```
POST /api/v3/sub-account/apiKey
body
[
        {
            "subAccount":"subAccount1",
            "permissions":"SPOT_ACCOUNT_READ",
            "ip":"135.181.193",
            "note":"1"
        }
]
```
> 返回示例

```
    {
        "subAccount": "subAccount1",
        "note": "1",
        "apiKey": "arg13sdfgs",
        "secretKey": "nkjwn21973ihi",
        "permissions": "SPOT_ACCOUNT_READ",
        "ip": "135.181.193",
        "creatTime": 1597026383085
    }

```
**HTTP请求**

- **POST** ```/api/v3/sub-account/apiKey```



**请求参数**

| 参数名      | 类型   | 是否必须 | 说明                                                         |
| :----------- | :------ | :-------- | :------------------------------------------------------------ |
| subAccount  | string | 是       | 子账户名称 如：subAccount1                                   |
| note        | string | 是       | APIKey的备注                                                 |
| permissions | string | 是       | APIKey权限:<br/>账户读/SPOT_ACCOUNT_READ,<br/>账户写/SPOT_ACCOUNT_WRITE,<br/>现货交易信息读/SPOT_DEAL_READ,<br/>现货交易信息写/SPOT_DEAL_WRITE,<br/>杠杆账户信息读/ISOLATED_MARGIN_ACCOUNT_READ,<br/>杠杆账户信息写/ISOLATED_MARGIN_ACCOUNT_WRITE,<br/>杠杆交易信息读/ISOLATED_MARGIN_DEAL_READ,<br/>杠杆交易信息写/ISOLATED_MARGIN_DEAL_WRITE,<br/>合约账户信息读/CONTRACT_ACCOUNT_READ,<br/>合约账户信息写/CONTRACT_ACCOUNT_WRITE,<br/>合约交易信息读/CONTRACT_DEAL_READ,<br/>合约交易信息写/CONTRACT_DEAL_WRITE,<br/>资金划转读/SPOT_TRANSFER_READ,<br/>资金划转写/SPOT_TRANSFER_WRITE|
| ip          | string | 否       | 绑定ip地址，多个ip用半角逗号隔开，最多支持20个ip。    如：135.181.193    |
| recvWindow  | long   | 否       |                                                              |
| timestamp   | long   | 是       |                                                              |



**返回参数**

| 参数名      | 类型   | 说明               |
| :----------- | :------ | :------------------ |
| subAccount  | string | 子账户名称         |
| note        | string | APIKey的备注       |
| apiKey      | string | API公钥            |
| secretKey   | string | API的私钥          |
| permissions | string | APIKey权限         |
| ip          | string | APIKey绑定的ip地址 |
| creatTime   | long   | 创建时间           |



## 查询子账户的APIKey
获取指定子账户的APIkey信息

> 请求示例

```
GET/api/v3/sub-account/apiKey?subAccount=subAccount1&timestamp=1597026383085
```

> 返回示例

```
{
  "subAccount":[
    {
      "note":"v5",
      "apiKey":"arg13sdfgs",
      "permissions":"SPOT_ACCOUNT_READ,SPOT_ACCOUNT_WRITE",
      "ip":"135.181.193",
      "creatTime":1597026383085
    },
    {
      "note":"v5.1",
      "apiKey":"arg13sdfgs",
      "permissions":"read_only",
      "ip":"135.181.193",
      "creatTime":1597026383085
    }
   ]
}
```
**HTTP请求**

- **GET** ```/api/v3/sub-account/apiKey```

**请求参数**

| 参数名     | 类型   | 是否必须 | 说明       |
| :--------- | :----- | :------- | :--------- |
| subAccount | string | 是       | 子账户名称 如：subAccount1|
| recvWindow | long   | 否       |            |
| timestamp  | long   | 是       |            |


**返回参数**

| 参数名  | 类型 | 说明          |
| :---------- | :------- | :----------------- |
| note        | string   | APIKey的备注       |
| apiKey      | string   | API公钥            |
| permissions | string   | APIKey权限         |
| ip          | string   | APIKey绑定的ip地址 |
| creatTime   | long     | 创建时间           |



## 删除子账户的APIKey

> 请求示例

```
DELETE /api/v3/sub-account/apiKey
body
[
        {
            "subAccount":"subAccount1",
            "apiKey":"ghytfugy2168hjksaj"
        }
]
```
> 返回示例

```
{
           "subAccount":"subAccount1"
}

```
**HTTP请求**

- **DELETE** ```/api/v3/sub-account/apiKey```



**请求参数**

| 参数名     | 类型   | 是否必须 | 说明       |
| :--------- | :----- | :------- | :--------- |
| subAccount | string | 是       | 子账户名称 如：subAccount1|
| apiKey     | string | 是       | API的公钥 如：ghytfugy2168hjksaj |
| recvWindow | long   | 否       |            |
| timestamp  | long   | 是       |            |



**返回参数**

| 参数名   | 类型   | 说明    |
| :--------- | :------- | :--------- |
| subAccount | string   | 子账户名称 |

## 母子用户万向划转

> 请求示例

```
post /api/v3/capital/sub-account/universalTransfer
```
> 返回示例

```json
[
  {
    "tranId":11945860693 
  }
]
```
**HTTP请求**

- **POST** ```/api/v3/capital/sub-account/universalTransfer```

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明                                                                 | 
| :------ | :-------- | :-------- |:-------------------------------------------------------------------|
|fromAccount|string|否| 母子账户，可填subAccout账户名，不填默认母账户                                        |
|toAccount|string|否| 母子账户，可填subAccout账户名，不填默认母账户                                        |
|fromAccountType|string|是| 划出账户类型，现货/合约/杠杆，枚举值："SPOT","FUTURES","ISOLATED_MARGIN"，划转规则见上描述 |
|toAccountType|string|是| 划出账户类型，现货/合约/杠杆，枚举值："SPOT","FUTURES","ISOLATED_MARGIN"，划转规则见上描述 |
|symbol|string|否| 币对，当fromAccountType为逐仓杠杆（ISOLATED_MARGIN）时必传，eg：ETHUSDT            |
|asset|string|是| 资产，eg：USDT                                                         |
|amount|string|是| 数量，eg：1.82938475                                                   |
|timestamp|string|是| 时间戳                                                                |
|signature|string|是| 签名                                                                 |



**返回参数**

| 参数名  |类型 | 说明|
| :------------ | :-------- | :--------|
|tranId|string|划转ID|

## 查询母子万向划转历史

> 请求示例

```
get /api/v3/capital/sub-account/universalTransfer
```
> 返回示例

```json
[
  {
    "tranId":"11945860693",
    "fromAccount":"master@test.com",
    "toAccount":"subaccount1@test.com",
    "clientTranId":"test",
    "asset":"BTC",
    "amount":"0.1",
    "fromAccountType":"SPOT",
    "toAccountType":"FUTURE",
    "fromSymbol":"SPOT",
    "toSymbol":"FUTURE",
    "status":"SUCCESS",
    "timestamp":1544433325000
  }
]
```
**HTTP请求**

- **GET** ```/api/v3/capital/sub-account/universalTransfer```

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
|fromAccount|string|否|母子账户，可填subAccout账户名，不填默认母账户|
|toAccount|string|否|母子账户，可填subAccout账户名，不填默认母账户|
|fromAccountType|string|是|划出账户类型，现货/合约/杠杆，枚举值："SPOT","FUTURES","ISOLATED_MARGIN"，划转规则见上描述|
|toAccountType|string|是|划出账户类型，现货/合约/杠杆，枚举值："SPOT","FUTURES","ISOLATED_MARGIN"，划转规则见上描述|
|startTime|string|否|起始时间|
|endTime|string|否|截止时间|
|page|string|否|默认 1|
|limit|string|否|默认 500, 最大 500|
|timestamp|string|是|时间戳|
|signature|string|是|签名|


**返回参数**

| 参数名  |类型 | 说明|
| :------------ | :-------- | :--------|
|tranId|string|划转ID|
|fromAccount|string|划出账户|
|toAccount|string|划入账户|
|clientTranId|string|客户自定义划转ID|
|asset|string|币种|
|amount|string|划转数量|
|fromAccountType|string|转出业务账户|
|toAccountType|string|划入业务账户|
|fromSymbol|string|杠杆转入交易对|
|toSymbol|string|杠杆转出交易对|
|status|string|划转状态:成功，失败，划转中，中断|
|timestamp|number|划转时间|
|totalCount|number||

## 开通子账户的合约业务

> 请求示例

```
post /api/v3/sub-account/futures
```
> 返回示例

```json
[
  {
    "code": "0",
    "message": "",
    "data": [{
        "subAccount": "mexc1",
        "isFuturesEnabled": true,
        "timestamp": "1597026383085"
    }]
  }
]
```
**HTTP请求**

- **POST** ```/api/v3/sub-account/futures```

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
|subAccount|string|是|子账户|
|timestamp|string|是|时间戳|
|signature|string|是|签名|


**返回参数**

| 参数名  |类型 | 说明|
| :------------ | :-------- | :--------|
|subAccount|string|子账户名称|
|isFuturesEnabled|boolean|开通合约业务，开通：true|
|timestamp|string|返回时间|



## 开通子账户的杠杆业务

> 请求示例

```
post /api/v3/sub-account/margin
```
> 返回示例

```json
[
  {
    "code": "0",
    "message": "",
    "data": [{
        "subAccount": "mexc1",
        "isMarginEnabled": true,
        "timestamp": "1597026383085"
    }]
  }
]
```
**HTTP请求**

- **POST** ```/api/v3/sub-account/margin```

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
|subAccount|string|是|子账户名称|
|timestamp|string|是|时间戳|
|signature|string|是|签名|


**返回参数**

| 参数名  |类型 | 说明|
| :------------ | :-------- | :--------|
|subAccount|string|子账户名称|
|isMarginEnabled|boolean|是否开通杠杆业务：true or false|
|timestamp|string|返回时间|


# 现货账户和交易接口

## 测试下单
用于测试订单请求，但不会提交到撮合引擎

> 请求示例

```
POST /api/v3/order/test
```
> 返回示例

```json
{}
```
**HTTP请求**
- **POST** ```/api/v3/order/test```

**请求参数**

同于 POST /api/v3/order

## 下单
只有当您的账户有足够的资金才能下单。

> 请求示例

```
POST /api/v3/order?symbol=BTCUSDT&side=BUY&type=LIMIT&quantity=0.0003&price=20000&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
    "symbol": "BTCUSDT",
    "orderId": "0a3b6af38f7a4f2e9bea9a5782321ddc",
    "orderListId": -1
}
```
**HTTP请求**

- **POST** ```/api/v3/order```

**请求参数**

| 名称             | 类型    | 是否必需 | 说明                   |
| :---------------- | :------- | :-------- | :---------------------- |
| symbol           | string  | 是      | 交易对                 |
| side             | ENUM    | 是      | 详见枚举定义：<a href="#order_side">订单方向</a> |
| type             | ENUM    | 是      | 详见枚举定义：<a href="#order_type">订单类型</a> |
| quantity         | decimal | 否       | 委托数量               |
| quoteOrderQty    | decimal | 否       | 委托总额               |
| price            | decimal | 否       | 委托价格               |
| newClientOrderId | string  | 否       | 客户自定义的唯一订单ID |
| recvWindow       | long    | 否       | 赋值不能大于 60000     |
| timestamp        | long    | 是      |                        |

基于订单 `type`不同，强制要求某些参数:

| 类型     | 强制要求的参数                |
| :------- | :---------------------------- |
| `LIMIT`  | `quantity`, `price`           |
| `MARKET` | `quantity` or `quoteOrderQty` |

其他说明：

MARKET：当type是market时，若为买单，则quoteOrderQty，为必填参数。
若为卖单，quantity为必填参数，

- 比如在`BTCUSDT`上下一个市价买单, 明确的是买入时想要花费的计价资产数量。此时的报单数量将会以市场流动性和`quoteOrderQty`被计算出来（实际成交数量以最终订单详情为准）。
  以`BTCUSDT`为例，`quoteOrderQty=100`:下买单的时候, 订单会尽可能的买进价值100USDT的BTC.

- 比如在`BTCUSDT`上下一个市价卖单, `quantity`为用户指明能够卖出多少BTC。

**返回参数**


| 参数名       | 数据类型 | 说明                |
| :------------ | :-------- | :------------------- |
| symbol | string | 交易对 |
| orderId | string | 订单id |
| orderListId|客户端订单列表          |          |

## 批量下单
支持单次批量下20单,要求必须是同一交易对，限频2次/秒。

> 请求示例

```
POST /api/v3/batchOrders?batchOrders=[{"type": "LIMIT_ORDER","price": "40000","quantity": "0.0002","symbol": "BTCUSDT","side": "BID","newClientOrderId": 9588234},{"type": "LIMIT_ORDER","price": "4005","quantity": "0.0003","symbol": "BTCUSDT","side": "ASK"}]
```
> 返回示例

```json
{ //成功返回：
  [
    {   
      "symbol": "BTCUSDT",   
      "orderId": "1196315350023612316",   
      "orderListId": -1 
    },
    {   
      "symbol": "BTCUSDT",   
      "orderId": "1196315350023612318",   
      "orderListId": -1 
    }
  ],
  //有失败的返回：
  [
    { 
      "symbol": "BTCUSDT", 
      "orderId": "1196315350023612316", 
      "newClientOrderId": "hio8279hbdsds", 
      "orderListId": -1 
    },
    { 
      "newClientOrderId": "123456",
      "msg": "The minimum transaction volume cannot be less than：0.5USDT", 
      "code": 30002
    },
    { 
      "symbol": "BTCUSDT", 
      "orderId": "1196315350023612318", 
      "orderListId": -1 
    }
  ] 
}
```
**HTTP请求**

- **POST** ```/api/v3/batchOrders```

**请求参数**


| 名称             | 类型    | 是否必需 | 说明                   |
| :--------------- | :------ | :------- | :--------------------- |
| batchOrders      | LIST  | 是      | 订单列表，最多支持20个订单(list of JSON格式填写订单参数,参考请求示例) |
| symbol           | string  | 是      | 交易对                 |
| side             | ENUM    | 是      | 详见枚举定义：<a href="#order_side">订单方向</a> |
| type             | ENUM    | 是      | 详见枚举定义：<a href="#order_type">订单类型</a> |
| quantity         | decimal | 否       | 委托数量               |
| quoteOrderQty    | decimal | 否       | 委托总额               |
| price            | decimal | 否       | 委托价格               |
| newClientOrderId | string  | 否       | 客户自定义的唯一订单ID |
| recvWindow       | long    | 否       | 赋值不能大于 60000     |
| timestamp        | long    | 是      |                        |

基于订单 `type`不同，强制要求某些参数:

| 类型     | 强制要求的参数                |
| :------- | :---------------------------- |
| `LIMIT`  | `quantity`, `price`           |
| `MARKET` | `quantity` or `quoteOrderQty` |

**返回参数**

| 参数名       | 数据类型 | 说明                |
| :------------ | :-------- | :------------------- |
| symbol | string | 交易对 |
| orderId | string | 订单id |

## 撤销订单

取消有效订单。

> 请求示例

```
DELETE /api/v3/order?symbol=BTCUSDT&orderId=135598325645746176&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
  "symbol": "BTCUSDT",
  "origClientOrderId": "myOrder1",
  "orderId": 4,
  "orderListId": -1, // OCO订单ID，否则为 -1
  "clientOrderId": "cancelMyOrder1",
  "price": "29000.0000",
  "origQty": "1.00000000",
  "executedQty": "0.00000000",
  "cummulativeQuoteQty": "0.00000000",
  "status": "CANCELED",
  "timeInForce": "GTC",
  "type": "LIMIT",
  "side": "BUY"
}
```
**HTTP请求**

- **DELETE** ```/api/v3/order```



**请求参数**

| 参数名            | 数据类型 | 是否必须 | 说明                   |
| :----------------- | :-------- | :-------- | :---------------------- |
| symbol            | string   | 是       | 交易对名称             |
| orderId           | string   | 否       | 订单Id                 |
| origClientOrderId | string   | 否       | 初始自定义订单Id       |
| newClientOrderId  | string   | 否     | 客户自定义的唯一订单ID |
| recvWindow        | long     | 否       |                        |
| timestamp         | long     | 是       |                        |


<aside class="notice">orderId 或 origClientOrderId 必须至少发送一个.</aside>


**返回参数**

| 参数名                 | 说明             |
|:--------------------| :---------------- |
| symbol              | 交易对           |
| origClientOrderId   | 原始客户端订单id |
| orderId             | 订单id           |
| clientOrderId       | 客户端id         |
| price               | 价格             |
| origOty             | 初始数量         |
| executedQty         | 已成交数量   |
| cummulativeQuoteQty | 已成交金额     |
| status              | 当前状态       |
| timeInForce         | 订单有效方式     |
| type                | <a href="#order_type">订单类型</a>         |
| side                | <a href="#order_side">订单方向</a>         |

## 撤销单一交易对所有订单
撤销单一交易对下所有挂单, 包括OCO的挂单。
> 请求示例

```
DELETE /api/v3/openOrders?symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

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
**HTTP请求**

- **DELETE** ```/api/v3/openOrders```



**请求参数**

| 参数名     | 数据类型 | 是否必须 | 说明   |
| :---------- | :-------- | :-------- | :------ |
| symbol     | string   | 是       | 交易对 |
| recvWindow | long     | 否       |        |
| timestamp  | long     | 是       |        |


**返回参数**

| 参数名              | 说明           |
| :------------------- |:-------------|
| symbol              | 交易对          |
| origClientOrderId   | 原始客户端订单id    |
| orderId             | 订单id         |
| clientOrderId       | 客户端id        |
| price               | 价格           |
| origOty             | 初始数量         |
| executedQty         | 已成交数量        |
| cummulativeQuoteQty | 已成交金额        |
| status              | 状态           |
| timeInForce         | 订单有效方式       |
| type                | <a href="#order_type">订单类型</a>          |
| side                | <a href="#order_side">订单方向</a>          |

## 查询订单

查询指定交易对订单状态，最多查询7天内的订单记录，超过7天的可在web客户端查看和导出。

> 请求示例

```
GET /api/v3/order?symbol=BTCUSDT&orderId=129402018493145088&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

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
**HTTP请求**

- **GET** ```/api/v3/order```


**请求参数**

| 参数名            | 数据类型         | 是否必须 | 说明 |
| :----------------- | :---------------- | :-------- | :---- |
| symbol            | 交易对           | 是       |      |
| origClientOrderId | 原始客户端订单id | 否       |      |
| orderId           | 订单id           | 否       |      |
| recvWindow        | long             | 否       |      |
| timestamp         | long             | 是       |      |


**返回参数**

| 参数名              | 说明                               |
| :------------------- |:---------------------------------|
| symbol              | 交易对                              |
| origClientOrderId   | 原始客户端订单id                        |
| orderId             | 系统订单id                           |
| clientOrderId       | 客户自定义id                          |
| price               | 价格                               |
| origOty             | 原始订单数量                           |
| executedQty         | 交易的订单数量                          |
| cummulativeQuoteQty | 累计订单金额                           |
| status              | <a href="#order_status">订单状态</a> |
| timeInForce         | 订单的时效方式                          |
| type                | <a href="#order_type">订单类型</a>   |
| side                | <a href="#order_side">订单方向</a>   |
| stopPrice           | 止损价格                             |
| icebergQty          | 冰山数量                             |
| time                | 订单时间                             |
| updateTime          | 最后更新时间                           |
| isWorking           | 是否在orderbook中                    |
| origQuoteOrderQty   | 原始的交易金额                          |

## 当前挂单
获取当前挂单支持查询多交易对，每次最多可以传5个symbol。  
若批量查5个交易对，最多也只返回1000条挂单

> 请求示例

```
GET /api/v3/openOrders?symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

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
**HTTP请求**

- **GET** ```/api/v3/openOrders```


**请求参数**

| 参数名     | 数据类型 | 是否必须 | 说明   |
| :---------- | :-------- | :-------- | :------ |
| symbol     | string   | 是       | 交易对,【最多可以传5个symbol, 由","分隔的字符串表示. e.g. "BTCUSDT,MXUSDT,ADAUSDT"】 |
| recvWindow | long     | 否       |        |
| timestamp  | long     | 是       |        |


**返回参数**

| 参数名              | 说明                                                             |
| :------------------- |:---------------------------------------------------------------|
| symbol              | 交易对                                                            |
| origClientOrderId   | 原始客户端订单id                                                      |
| orderId             | 系统订单id                                                         |
| clientOrderId       | 客户自定义id                                                        |
| price               | 价格                                                             |
| origOty             | 原始订单数量                                                         |
| executedQty         | 交易的订单数量                                                        |
| cummulativeQuoteQty | 累计订单金额                                                         |
| status              | <a href="#order_status">订单状态</a>                                                           |
| timeInForce         | 订单的时效方式                                                        |
| type                | <a href="#order_type">订单类型</a>                                 |
| side                | <a href="#order_side">订单方向</a>                                    |
| stopPrice           | 止损价格                                                           |
| icebergQty          | 冰山数量                                                           |
| time                | 订单时间                                                           |
| updateTime          | 最后更新时间                                                         |
| isWorking           | 是否在orderbook中                                                  |
| origQuoteOrderQty   | 原始的交易金额                                                        |

## 查询所有订单
获取所有有效，已取消或已完成的帐户订单(查询时间段默认最近24小时)，最多查询最近7天数据。

> 请求示例

```
GET /api/v3/allOrders?symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

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
**HTTP请求**

- **GET** ```/api/v3/allOrders```



**请求参数**

| 参数名     | 数据类型 | 是否必须 | 说明                 |
| :---------- | :-------- | :-------- | :-------------------- |
| symbol     | string   | 是       | 交易对               |
| startTime  | long     | 否       |                      |
| endTime    | long     | 否       |                      |
| limit      | int      | 否       | 默认 500; 最大 1000; |
| recvWindow | long     | 否       |                      |
| timestamp  | long     | 是       |                      |

<aside class="notice">startTime和endTime需同时使用.</aside>



**返回参数**

| 参数名              | 说明                                     |
| :------------------- |:---------------------------------------|
| symbol              | 交易对                                    |
| origClientOrderId   | 原始客户端订单id                              |
| orderId             | 系统订单id                                 |
| clientOrderId       | 客户自定义id                                |
| price               | 价格                                     |
| origOty             | 原始订单数量                                 |
| executedQty         | 交易的订单数量                                |
| cummulativeQuoteQty | 累计订单金额                                 |
| status              | <a href="#order_status">订单状态</a>                                    |
| timeInForce         | 订单的时效方式                                |
| type                | <a href="#order_type">订单类型</a>         |
| side                | <a href="#order_side">订单方向</a>         |
| stopPrice           | 止损价格                                   |
| icebergQty          | 冰山数量                                   |
| time                | 订单时间                                   |
| updateTime          | 最后更新时间                                 |
| isWorking           | 是否在orderbook中                          |
| origQuoteOrderQty   | 原始的交易金额                                |

## 账户信息
获取当前账户信息，限速2次每秒。

> 请求示例

```
GET /api/v3/account?timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

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
    "balances": [
        {
            "asset": "MX",
            "free": "3",
            "locked": "0"
        },
        {
            "asset": "BTC",
            "free": "0.0003",
            "locked": "0"
        }
    ],
    "permissions": [
        "SPOT"
    ]
}
```
**HTTP请求**

- **GET** ```/api/v3/account```


**请求参数**

| 参数名     | 数据类型 | 是否必须 | 说明 |
| :---------- | :-------- | :-------- | :---- |
| recvWindow | long     | 否       |      |
| timestamp  | long     | 是       |      |


**返回参数**

| 参数名           | 说明       |
| :---------------- | :---------- |
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
获取账户指定交易对的成交历史


> 请求示例

```
GET /api/v3/myTrades?symbol=MXUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  {
      "symbol": "MXUSDT",
      "id": "fad2af9e942049b6adbda1a271f990c6",
      "orderId": "bb41e5663e124046bd9497a3f5692f39",
      "orderListId": -1,
      "price": "2.044",
      "qty": "3",
      "quoteQty": "6.132",
      "commission": "0.012264",
      "commissionAsset": "USDT",
      "time": 1651980451000,
      "isBuyer": true,
      "isMaker": false,
      "isBestMatch": true,
      "isSelfTrade": null,
      "clientOrderId": null
  }
]
```
**HTTP请求**

- **GET** ```/api/v3/myTrades```


**请求参数**

| 参数名     | 数据类型 | 是否必须 | 说明                 |
| :---------- | :-------- | :-------- | :-------------------- |
| symbol     | string   | 是       | 交易对               |
| orderId    | string   | 否       | 必须和symbol一起使用 |
| startTime  | long     | 否       |                      |
| endTime    | long     | 否       |                      |
| limit      | int      | 否       | 默认 500; 最大 1000; |
| recvWindow | long     | 否       |                      |
| timestamp  | long     | 是       |                      |


**返回参数**

| 参数名          | 说明              |
| :--------------- | :----------------- |
| symbol          | 交易对            |
| id              | 成交id            |
| orderId         | 订单id            |
| price           | 价格              |
| qty             | 数量              |
| quoteQty        | 成交金额           |
| time            | 成交时间           |
| commission      | 手续费             |
| commissionAsset | 手续费币种          |
| isBuyerMaker    | 是否为买方maker单    |
| isBestMatch     | 是否为最佳匹配       |
| isSelfTrade     | 是否自成交           |
| clientOrderId   | 用户自定义id|


# 钱包接口

## 查询币种信息
返回币种详细信息以及智能合约地址

> 请求示例

```
Get /api/v3/capital/config/getall
```
> 返回示例

```json
[
  {
    "coin": "BTC",
    "name": "Bitcoin",
    "networkList": [
      {
          "coin": "BTC",
          "depositDesc": null,
          "depositEnable": true,
          "minConfirm": 0,
          "name": "BTC-TRX",
          "network": "TRC20",
          "withdrawEnable": false,
          "withdrawFee": "0.000100000000000000",
          "withdrawIntegerMultiple": null,
          "withdrawMax": "40.000000000000000000",
          "withdrawMin": "0.001000000000000000",
          "sameAddress": false,
          "contract": "TN3W4H6rK2ce4vX9YnFQHwKENnHjoxb3m9"
      },
      {
          "coin": "BTC",
          "depositDesc": null,
          "depositEnable": true,
          "minConfirm": 0,
          "name": "BTC-BSC",
          "network": "BEP20(BSC)",
          "withdrawEnable": true,
          "withdrawFee": "0.000010000000000000",
          "withdrawIntegerMultiple": null,
          "withdrawMax": "100.000000000000000000",
          "withdrawMin": "0.000100000000000000",
          "sameAddress": false,
          "contract": "0x7130d2a12b9bcbfae4f2634d864a1ee1ce3ead9c"
      }
    ]
  },
]
```
**HTTP请求**

- **GET** ```/api/v3/capital/config/getall```

**请求参数**

无


**返回参数**

| 参数名 | 说明  | 
| :------------ | :------------ |
|depositEnable|是否可充值|
|network|币种所支持的网络| 
|withdrawEnable|是否可提币|
|withdrawFee|提币手续费| 
|withdrawMax|最大提币限额|
|withdrawMin|最小提币限额|
|contract|币种智能合约地址|

## 提币

> 请求示例

```
post /api/v3/capital/withdraw/apply?coin=USDT&network=TRC20&address=TPb5qT9ZikopzCUD4zyieSEfwbjdjUPVb&amount=3&signature={{signature}}&timestamp={{timestamp}}
```
> 返回示例

```json
[
  {
    "id":"7213fea8e94b4a5593d507237e5a555b"
  }
]
```
**HTTP请求**

- **POST** ```/api/v3/capital/withdraw/apply```

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
|coin|string|是|币种|
|withdrawOrderId|string|否|自定义提币ID(目前不支持)|
|network|string|否|提币网络|
|address|string|是|提币地址(memo请使用:进行拼接)|
|amount|string|是|数量|
|remark|string|否|备注|
|timestamp|string|是|时间戳|
|signature|string|是|签名|
 
1. 如果不发送`network`,将按该币种默认网络返回结果;
2. 可以在接口 `Get /api/v3/capital/config/getall`的返回值中某币种的`networkList`获取`network`网络字段和`isDefault`是否为默认网络。
3. 提币地址只支持web端添加到提币地址管理中的地址。

**返回参数**

| 参数名 | 说明  |
| :------------ | :-------- | 
|id|提币ID|

## 获取充值历史(支持多网络)

> 请求示例

```
get /api/v3/capital/deposit/hisrec?coin=USDT-BSC&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  {
        "amount": "128",
        "coin": "USDT-BSC",
        "network": "BSC",
        "status": 5,
        "address": "0xebe4804f7ecc22d5011c42e6ea1f22e6c891d9b",
        "addressTag": null,
        "txId": "0xd8ff2e4e87ba64454039b62f6fcd456cb8afdbd21352a94b2b115b70212d97d:0",
        "insertTime": 1657952043000,
        "unlockConfirm": "16",
        "confirmTimes": "24"
  }
]
```
**HTTP请求**

- **GET** ```/api/v3/capital/deposit/hisrec```

**请求参数**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| :------ | :-------- |:-----| :---------- |
|coin|string| 否    |币种|
|status|string| 否    |状态|
|startTime|string| 否    |默认当前时间90天前的时间|
|endTime|string| 否    |默认当前时间戳，13位|
|limit|string| 否    |默认：1000，最大1000|
|timestamp|string| 是    |时间戳|
|signature|string| 是    |签名|

请注意`startTime` 与 `endTime` 的默认时间戳，保证请求时间间隔不超过90天.

**返回参数**

| 参数名 | 说明  |
| :------------ | :-------- |
|amount|数量|
|coin|币种|
|network|链类型|
|status|充值状态，1:小额充值，2:延遲到賬，3:大額充值，4:等待中，5:入账成功，6:审核中，7:驳回|
|address|地址|
|addressTag|地址标签|
|txId|交易编号|
|insertTime|插入时间/创建时间|
|unlockConfirm| 解锁需要的网络确认次数|
|confirmTimes|已解锁次数|

## 获取提币历史 (支持多网络)

> 请求示例

```
get /api/v3/capital/withdraw/history?coin=USDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  {
        "id": "17bc9f68c3b740c5947c074748d42c3",
        "txId": "0xaa61d7a5b51580ec4e4e56b3f49e4c8f2f9d0665995f0652dfeeb5007f8fbf9",
        "coin": "USDT-BSC",
        "network": "BSC",
        "address": "0x2c7471e7F4A841b591460F431D9A3B1DEF6E5EC",
        "amount": "1501",
        "transferType": 0,
        "status": 7,
        "transactionFee": "1",
        "confirmNo": null,
        "applyTime": 1658625828000,
        "remark": ""
  }
]
```
**HTTP请求**

- **GET** ```/api/v3/capital/withdraw/history```

**请求参数**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| :------ | :-------- |:-----| :---------- |
|coin|string| 否    |币种|
|status|string| 否    |提币状态|
|limit|string| 否    |默认：1000， 最大：1000|
|startTime|string| 否    |默认当前时间90天前的时间戳|
|endTime|string| 否    |默认当前时间戳|
|timestamp|string| 是    |时间戳|
|signature|string| 是    |签名|

1. 支持多网络提币前的历史记录可能不会返回`network`字段.
2. 请注意`startTime` 与 `endTime` 的默认时间戳，保证请求时间间隔不超过90天.

**返回参数**

| 参数名 | 说明  |
| :------------ | :-------- | 
|address|地址|
|amount| 提现转出金额|
|applyTime| 申请时间|
|coin|币种|
|id|该笔提现的id|
|withdrawOrderId| 自定义ID，如果没有则不返回该字段|
|network|链类型|
|transferType| 0: 站外转账，1: 站内转账  |
|status|提币状态，1:提交申请，2:审核中，3:等待处理，4:处理中，5:等待打包，6:等待确认，7:提现成功，8:提现失败，9:已取消，10:手动入账|
|transactionFee| 手续费|
|confirmNo| 提现确认数|
|txId| 提现交易id|
|remark|提现记录备注|

## 获取充值地址 (支持多网络)

> 请求示例

```
get /api/v3/capital/deposit/address?coin=USDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  {
      "coin": "USDT",
      "network": "TRC20",
      "address": "TXobiKkdciupZrhdvZyTSSLjE8CmZAufS",
      "tag": null
  },
  {
      "coin": "USDT",
      "network": "BEP20(BSC)",
      "address": "0xebe4804f7ecc22d5011c42e6ea1f2e6c891d89b",
      "tag": null
  },
  {
      "coin": "USDT",
      "network": "ERC20",
      "address": "0x3f4d1f43761b52fd594e5a77cd83cab6955e85b",
      "tag": null
  }
]
```
**HTTP请求**

- **GET** ```/api/v3/capital/deposit/address```

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
|coin|string|是|币种|
|network|string|否||
|timestamp|string|是|时间戳|
|signature|string|是|签名|

**返回参数**

| 参数名 | 说明  |
| :------------ | :-------- |
|address|地址|
|coin|币种|
|tag|标签|
|network||

## 用户万向划转【母母账户】

> 请求示例

```
post /api/v3/capital/transfer?fromAccountType=FUTURES&toAccountType=SPOT&asset=USDT&amount=1&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  {
    "tranId": "c45d800a47ba4cbc876a5cd29388319"
  }
]
```
**HTTP请求**

- **POST** ```/api/v3/capital/transfer```

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
|timestamp|string|是|时间戳|
|signature|string|是|签名|
|fromAccountType|string|是|划出账户类型，现货/合约/杠杆，枚举值："SPOT","FUTURES","ISOLATED_MARGIN"|
|toAccountType|string|是|划入账户类型，现货/合约/杠杆，枚举值："SPOT","FUTURES","ISOLATED_MARGIN"|
|asset|string|是|资产|
|amount|string|是|数量|
|symbol|string|否|交易对，当fromAccountType为逐仓杠杆（ISOLATED_MARGIN）时必传，eg：ETHUSDT|

当类型为 `ISOLATEDMARGIN`,`fromSymbol`和`toSymbol` 必须要发送.

**返回参数**

| 参数名 | 说明  |
| :------------ | :-------- | 
|tranId|划转ID|

## 查询用户万向划转历史

> 请求示例

```
get /api/v3/capital/transfer
```
> 返回示例

```json
[
  {
    "rows":[
    {
      "tranId":"11945860693",//划转ID
      "clientTranId":"test",//client ID
      "asset":"BTC",//币种
      "amount":"0.1",//划转数量
      "fromAccountType":"SPOT",//转出业务账户
      "toAccountType":"FUTURE",//划入业务账户
      "fromSymbol":"SPOT",//转出交易对
      "toSymbol":"FUTURE",//划入交易对
      "status":"SUCCESS",//划转状态
      "timestamp":1544433325000//划转时间
    },
    {
      "tranId":"11945860693",//划转ID
      "clientTranId":"test",//client ID
      "asset":"BTC",//币种
      "amount":"0.1",//划转数量
      "fromAccountType":"SPOT",//转出业务账户
      "toAccountType":"FUTURE",//划入业务账户
      "fromSymbol":"SPOT",//转出交易对
      "toSymbol":"FUTURE",//划入交易对
      "status":"SUCCESS",//划转状态
      "timestamp":1544433325000//划转时间
    }],
    "total": 2,//总数
  }
]
```
**HTTP请求**

- **GET** ```/api/v3/capital/transfer```

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
|timestamp|string|是|时间戳|
|signature|string|是|签名|
|fromAccountType|string|是|划出账户类型，现货/合约/杠杆，枚举值："SPOT","FUTURES","ISOLATED_MARGIN"|
|toAccountType|string|是|划入账户类型，现货/合约/杠杆，枚举值："SPOT","FUTURES","ISOLATED_MARGIN"|
|startTime|string|否||
|endTime|string|否||
|page|string|否|默认1|
|size|string|否|默认 10, 最大 100|
|symbol|string|是|交易对，当fromAccountType为逐仓杠杆（ISOLATED_MARGIN）时必传，如:ETHUSDT|

1. 仅支持查询最近半年（6个月）数据
2. 若`startTime`和`endTime`没传，则默认返回最近7天数据
**返回参数**

| 参数名 | 说明  |
| :------------ | :-------- | 
|total|总数|
|tranId|划转ID|
|clientTranId|client ID|
|asset|币种|
|amount|划转数量|
|fromAccountType|转出业务账户|
|toAccountType|划入业务账户|
|symbol|转出交易对|
|status|划转状态|
|timestamp|划转时间|

# ETF接口

## 获取杠杆ETF基础信息
获取ETF的基础信息，如可交易币对、最新净值和管理费率。

> 请求示例

```
GET /api/v3/etf/info
```
> 返回示例

```json
{
  "symbol": "OP3SUSDT",
  "netValue": "0.332",
  "feeRate": "0.00001",
  "timestamp": 1661494588543,
  "leverage": -3,
  "realLeverage": 2.9126,
  "mergedTimes": 3,
  "lastMergedTime": 1659063531000,
  "preBasket": 18827.8361,
  "preLeverage": 2.2888,
  "basket": 24678.0916
}

```
**HTTP请求**

- **GET** ```api/v3/etf/info```


**请求参数**

| 参数   | 数据类型 | 是否必须 | 默认值 | 描述                    |
| :------ | :-------- | :-------- | :------ | :----------------------- |
| symbol | string   | 否       | NA     | ETF交易对，不填返回所有 |



**返回参数**

| 字段名称  | 数据类型 | 描述          |
| :--------- | :-------- | :------------- |
| symbol     | string   | 杠杆ETF交易对 |
| netValue   | string   | 最新净值      |
| feeRate    | string   | 管理费率      |
| timestamp  | long     | 系统时间      |
|leverage    |string    | 目标杠杆      |
|realLeverage|string    | 当前杠杆      |
|mergedTimes |string    | 合并次数      |
|lastMergedTime|long   | 最近合并时间   |
|preBasket  |string    | 再平衡前篮子   |
|preLeverage|string    | 再平衡前杠杆   |
|basket     |string    | 再平衡后篮子   |


# 杠杆账户和交易接口

## 切换杠杆账户模式
切换杠杆账户的交易模式

> 请求示例

```
POST /api/v3/margin/tradeMode?tradeMode=0&symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  {
  "tradeMode": 0,
  "symbol": "BTCUSDT"
  }
]
```

**HTTP请求**

- **POST** ```/api/v3/margin/tradeMode```

**请求参数**

| 参数名 | 说明| 是否必须  | 数据类型 |  示例            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
| timestamp | 时间戳 | 是| string|1655143087012|
| signature | 签名 |是|string|
| tradeMode | 交易模式 |是|int|0: 手动模式  1:自动借还模式|
| symbol | 交易对 |是|string|BTCUSDT|


**返回参数**

| 参数名 | 说明  |数据类型 | 示例|
| :------------ | :-------- | :-------| :------ |
|tradeMode|交易模式|int|0|
|symbol|交易对|string|BTCUSDT|



## 下单

进行杠杆账户下单操作

<aside class="warning">杠杆账户下单暂时不支持市价单</aside>


> 请求示例

```
POST /api/v3/margin/order?symbol=BTCUSDT&side=BUY&type=LIMIT&quantity=0.0003&price=20000&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  {
  "symbol": "BTCUSDT",
  "orderId": "693471305432961024",
  "clientOrderId": "6gCrw2kRUAF9CvJDGP16IP",
  "isIsolated": true,       
  "transactTime": 1507725176595
  }
]
```
**HTTP请求**

- **POST** ```/api/v3/margin/order```

**请求参数**

| 参数名 | 说明| 是否必须  | 数据类型 |  示例  | 
| :------ | :-------- | :-------- | :---------- | :------------------- |
|timestamp|时间 |是|string|1507725176595|
|signature|签名 |是|string|signature|
|symbol| 交易对 |是|string|BTCUSDT|
|isIsolated|是否逐仓杠杆|否|string|"TRUE", "FALSE", 默认 "TRUE"|
|side|方向|是|string|BUY|
|type|详见枚举定义：<a href="#order_type">订单类型</a>  (暂不支持市价单)|是|string|LIMIT| 
|quantity|订单数量|否|string|10| 
|quoteOrderQty|订单总额|否|string|200000| 
|price|下单价格买入价|否|string|20000| 
|newClientOrderId|客户自定义的唯一订单ID|否|string|6gCrw2kRUAF9CvJDGP16IP| 
|recvWindow|同步时间 |否|string|6000| 


**返回参数**

| 参数名 | 说明  |数据类型 | 示例 |
| :------------ | :-------- | :-------- |:-------------- |
|symbol| 交易对|string|BTCUSDT|
|orderId|订单id |string|693471305432961024|
|clientOrderId|客户自定义订单id |string|6gCrw2kRUAF9CvJDGP16IP|
|isIsolated| 是否是逐仓|boolean|true|
|transactTime| 下单时间|number|1507725176595|


## 借贷 

> 请求示例

```
post /api/v3/margin/loan?asset=BTC&amount=0.002&symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  {
    "tranId": 746784754145301480
  }
]
```
**HTTP请求**

- **POST** ```/api/v3/margin/loan```

**请求参数**

| 参数名 | 说明| 是否必须  | 数据类型 |  示例 |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|timestamp|时间 |是|string|1507725176595|
|signature|签名 |是|string|signature|
|asset|资产|是|string|BTC| 
|isIsolated|是否逐仓杠杆|否|string|"TRUE", "FALSE", 默认 "TRUE"| 
|symbol|交易对|是|string|BTCUSDT| 
|amount| 数量|是|string|10| 
|recvWindow|同步时间 |否|string|6000| 


**返回参数**

| 参数名 | 说明  |数据类型 | 示例 |
| :------------ | :-------- | :-------- | :------------------- |
| tranId | 借款记录id |number|746784754145301480|

**详细说明**：

如果 isIsolated = “TRUE”, 表示逐仓借贷，此时 symbol 必填。


## 归还借贷

> 请求示例

```
post /api/v3/margin/repay?asset=BTC&symbol=BTCUSDT&isAllRepay=true&borrowId=746784754145300480&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  {
    "tranId": 2597392
  }
]
```
**HTTP请求**

- **POST** ```/api/v3/margin/repay```

**请求参数**

| 参数名 | 说明| 是否必须  | 数据类型 |  示例            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|timestamp|时间 |是|string|1507725176595|
|signature|签名 |是|string|signature|
|asset|资产|是|string|BTC|
|isIsolated|是否逐仓杠杆|否|string|"TRUE", "FALSE", 默认 "TRUE"|
|symbol|交易对|是|string|BTCUSDT|
|amount|amount和isAllRepay，二选一|否|string|10|
|borrowId|借款订单id|是|string|746784754145301480|
|isAllRepay|全不全还|否|string|true or false|
|recvWindow|同步时间 |否|string|6000|

**返回参数**

| 参数名 | 说明  |数据类型 | 示例|
| :------------ | :-------- | :--------| :------------------- |
|tranId|还款id|number|2597392|

**详细说明**：

如果 isIsolated = “TRUE”, 表示逐仓还款，此时 symbol 必填。


## 撤销单一交易对的所有挂单

> 请求示例

```
delete /api/v3/margin/openOrders?symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  [
    {
      "symbol": "BTCUSDT",
          "orderId": "746779360689786880",
          "orderListId": "-1",
          "clientOrderId": null,
          "price": "20000",
          "origQty": "0.0003",
          "executedQty": "0",
          "cummulativeQuoteQty": "0",
          "status": "NEW",
          "type": "LIMIT",
          "side": "BUY",
          "isIsolated": true,
          "isWorking": true,
          "time": 1658212540000,
          "updateTime": 1658212540000
    }
  ]
]
```
**HTTP请求**

- **DELETE** ```/api/v3/margin/openOrders```

**请求参数**

| 参数名 | 说明| 是否必须  | 数据类型 |  示例            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|timestamp|时间 |是|string|1507725176595|
|signature|签名 |是|string|signature|
|symbol|交易对|是|string|BTCUSDT|
|isIsolated|是否逐仓杠杆|否|string|"TRUE", "FALSE", 默认 "TRUE"|
|recvWindow|同步时间|否|string|6000|

**返回参数**

| 参数名 | 说明  |数据类型 | 示例|
| :------------ | :-------- | :--------| :------------------- |
|symbol|交易对 |string|BTCUSDT|
|isIsolated| 是否是逐仓 |boolean|true|
|clientOrderId|客户自定义订单id|string|pXLV6Hz6mprAcVYpVMTGgx|
|price|下单价格|string|0.089853|
|origQty|下单数量 |string|0.178622|
|executedQty|成交数量|string|0.000000|
|cummulativeQuoteQty|累计成交金额 |string|0.000000|
|status|<a href="#order_status">订单状态</a> |string|CANCELED|
|type|<a href="#order_type">订单类型</a> |string|LIMIT|
|side|方向 |string|BUY|
|orderId|订单id|string| |
|orderListId|客户端订单列表|string||



## 撤销订单

> 请求示例

```
delete /api/v3/margin/order?symbol=BTCUSDT&orderId=746777776866070528&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  {
    "symbol": "BTCUSDT",
    "orderId": "746777776866070528",
    "orderListId": "-1",
    "clientOrderId": null,
    "price": "20000",
    "origQty": "0.0003",
    "executedQty": "0",
    "cummulativeQuoteQty": "0",
    "status": "NEW",
    "type": "LIMIT",
    "side": "BUY",
    "isIsolated": true,
    "isWorking": true,
    "time": 1658212162000,
    "updateTime": 1658212162000
  }

]
```
**HTTP请求**

- **DELETE** ```/api/v3/margin/order```

**请求参数**

| 参数名 | 说明| 是否必须  | 数据类型 |  示例            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|timestamp|时间 |是|string|1507725176595|
|signature|签名 |是|string|signature|
|isIsolated|是否逐仓杠杆|否|string|"TRUE", "FALSE", 默认 "TRUE"|
|symbol|交易对|是|string|BTCUSDT|
|orderId|订单id |是|string|746777776866070528|
|origClientOrderId|下单时，用户传入的自定义id|否|string|
|recvWindow|同步时间 |否|string|6000|

**返回参数**

| 参数名 | 说明 |数据类型 | 示例|
| :------------ | :------ | :--------| :------------------- |
|symbol| 交易对|string|LTCBTC|
|orderId|订单id |string|693471305432961024|
|clientOrderId|客户自定义订单id |string|cancelMyOrder1|
|price|下单价格 |string|1.00000000|
|origQty|下单数量 |string|10.00000000|
|executedQty|成交数量 |string|8.00000000|
|cummulativeQuoteQty|累计成交金额累计成交金额|string|8.00000000|
|status| <a href="#order_status">订单状态</a>     |string|CANCELED|
|type|<a href="#order_type">订单类型</a>  |string|LIMIT|
|side| 方向        |string|SELL|
|isIsolated| 是否是逐仓     |boolean|true|

**详细说明**：

必须发送 orderId 或 origClientOrderId 其中一个。


## 查询借贷记录

> 请求示例

```
get /api/v3/margin/loan?asset=BTC&symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  {
    "symbol": "BTCUSDT",
    "tranId": "746784754145300480",
    "asset": "BTC",
    "principal": "0.002",
    "remainAmount": "0",
    "remainInterest": "0",
    "repayAmount": "0.002",
    "repayInterest": "0.00000001",
    "status": "REPAID",
    "timestamp": 1658213826000
  }
]
```
**HTTP请求**

- **GET** ```/api/v3/margin/loan```

**请求参数**

| 参数名 | 说明| 是否必须  | 数据类型 |  示例            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|timestamp|时间 |是|string|1507725176595|
|signature|签名 |是|string|signature|
|asset|资产|是|string|BTC|
|symbol|逐仓symbol|是|string|BTCUSDT|
|tranId|`借贷id` in POST /api/v3/margin/loan|否|string|746784754145300480|
|startTime|开始时间 |否|string|
|endTime|截止时间 |否|string|
|current|当前查询页|否|string|开始值 1, 默认:1|
|size||否|string|默认:10 最大:100|
|recvWindow|同步时间 |否|string|6000|

**返回参数**

| 参数名 | 说明  |数据类型 | 示例|
| :------------ | :-------- | :--------| :------------------- |
|symbol| 逐仓借贷 返回逐仓symbol; 若是全仓不会返回此字段|string|BTCUSDT|
|tranId|借贷id |number|12807067523|
|asset|资产 |string|BTC|
|principal|借款金额|string|0.84624403|
|timestamp|时间 |number|1555056425000|
|remainAmount|待还金额|string| |
|remainInterest|待还利息|string| |
|repayAmount|已还金额|string|300|
|repayInterest|已还利息|string|1.96249686|
|status|订单状态: PENDING (等待执行), CONFIRMED (成功借贷), FAILED (执行失败);|string|CONFIRMED|
|total|总数 |number|1|

**详细说明**：

必须发送tranId 或 startTime，tranId 优先。响应返回为降序排列。如果发送isolatedSymbol，返回指定逐仓symbol指定asset的借贷记录。


## 查询历史委托记录

> 请求示例

```
get /api/v3/margin/allOrders?symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  {
      "symbol": "BTCUSDT",
      "orderId": "746779360689786880",
      "orderListId": "-1",
      "clientOrderId": null,
      "price": "20000",
      "origQty": "0.0003",
      "executedQty": "0",
      "cummulativeQuoteQty": "0",
      "status": "CANCELED",
      "type": "LIMIT",
      "side": "BUY",
      "isIsolated": true,
      "isWorking": true,
      "time": 1658212540000,
      "updateTime": 1658212551000
  },
]
```
**HTTP请求**

- **GET** ```/api/v3/margin/allOrders```

**请求参数**

| 参数名 | 说明| 是否必须  | 数据类型 |  示例            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|timestamp|时间 |是|string|1507725176595|
|signature|签名 |是|string|signature|
|symbol|交易对|是|string|BTCUSDT|
|isIsolated|是否逐仓杠杆|否|string|"TRUE", "FALSE", 默认 "TRUE"|
|orderId|订单id|否|string|746779360689786880|
|startTime|开始时间 |否|string|
|endTime|截止时间 |否|string|
|limit|默认 500;最大500.|否|string|

**返回参数**

| 参数名 | 说明       |数据类型 | 示例|
| :------------ |:---------| :--------| :------------------- |
|clientOrderId| 客户自定义订单id|string|D2KDy4DIeS56PvkM13f8cP|
|cummulativeQuoteQty| 累计成交金额   |string|0.00000000|
|executedQty| 成交数量     |string|0.00000000|
|isWorking| 是否正常工作   |boolean|false|
|orderId| 订单id     |number|41295|
|origQty| 下单数量     |string|5.31000000|
|price| 下单价格     |string|0.22500000|
|side| 方向       |string|SELL|
|status| <a href="#order_status">订单状态</a>     |string|CANCELED|
|symbol| 交易对      |string|MXBTC|
|isIsolated| 是否是逐仓    |boolean|false|
|time| 下单时间     |number|1565769338806|
|type| <a href="#order_type">订单类型</a>      |string|TAKE_PROFIT_LIMIT|
|updateTime| 更新时间     |number|1565769342148|

**详细说明**：

如果设置 orderId , 获取订单 &gt;= orderId， 否则返回近期订单历史。一些历史订单的 cummulativeQuoteQty &lt; 0, 是指当前数据不存在。



## 查询历史成交记录

> 请求示例

```
get /api/v3/margin/myTrades?symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[

]
```
**HTTP请求**

- **GET** ```/api/v3/margin/myTrades```

**请求参数**

| 参数名 | 说明| 是否必须  | 数据类型 |  示例            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|timestamp|时间 |是|string|1507725176595|
|signature|签名 |是|string|signature|
|symbol|交易对|是|string|BTCUSDT|
|isIsolated|是否逐仓杠杆|否|string|"TRUE", "FALSE", 默认 "TRUE"|
|startTime|开始时间 |否|string|
|endTime|截止时间 |否|string|
|fromId|获取TradeId，默认获取近期交易历史。|否|string|
|limit|默认 500; 最大 1000.|否|string|

**返回参数**

| 参数名 | 说明  |数据类型 | 示例|
| :------------ | :-------- | :--------| :------------------- |
|commission|手续费|string|0.00006000|
|commissionAsset|手续费币种|string|BTC|
|id|trade-id|number|34|
|isBuyer| 是否自成交|boolean|false|
|orderId|订单id |number|39324|
|price|下单价格 |string|0.02000000|
|qty|数量 |string|3.00000000|
|symbol|交易对 |string|MXBTC|
|isIsolated| 是否是逐仓|boolean|false|
|time|下单时间 |number|1561973357171|

**详细说明**：

如果设置 fromId , 获取订单 id &gt;= fromId， 否则返回近期订单历史。


## 查询当前挂单记录

> 请求示例

```
get /api/v3/margin/openOrders?symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  {
  "rows": [
    {
        "isolatedSymbol": "MXUSDT", // 逐仓借贷 返回逐仓symbol; 【统一参数】
        "id": "12807067523",//order id 
        "asset": "MX",
        "timestamp": 1555056425000,
        "amount": "315.53307675",
        "dealAmount": "319.26088158",//成交金额
        "dealQuantity": "23768.97",//成交数量
        "fee": "0",
        "feeCurrency": "USDT",
        "orderType": "STOP_OUT",
        "price": "0.013275",
        "quantity": "23768.97",
				"remainQuantity": "0",//未成交数量
        "remainAmount": "300",//未成交金额
				"side": "SELL",
				"status": "FILLED"
    }
  ],
  "total": 1
  }
]
```
**HTTP请求**

- **GET** ```/api/v3/margin/openOrders```

**请求参数**

| 参数名 | 说明| 是否必须  | 数据类型 |  示例            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|timestamp|时间 |是|string|1507725176595|
|signature|签名 |是|string|signature|
|symbol|交易对|是|string|BTCUSDT|
|isIsolated|是否逐仓杠杆|否|string|"TRUE", "FALSE", 默认 "TRUE"|


**返回参数**

| 参数名 | 说明 |数据类型 | 示例|
| :------------ | :------ | :--------| :------------------- |
|clientOrderId|客户自定义订单id |string|qhcZw71gAkCCTv0t0k8LUK|
|cummulativeQuoteQty|累计成交金额成交金额|string|0.00000000|
|executedQty| 成交数量     |string|0.00000000|
|isWorking| 是否正常工作   |boolean|true|
|orderId| 订单id     |number|211842552|
|origQty| 下单数量     |string|0.30000000|
|price| 下单价格     |string|0.00475010|
|side| 方向       |string|SELL|
|status| <a href="#order_status">订单状态</a>     |string|NEW|
|symbol| 交易对      |string|MXBTC|
|isIsolated| 是否是逐仓    |boolean|true|
|time| 下单时间     |number|1562040170089|
|timeInForce| 生效时间     |string|GTC|
|type| <a href="#order_type">订单类型</a>         |string|LIMIT|
|updateTime| 更新时间     |number|1562040170089|

**详细说明**：

如未发送symbol，返回所有 symbols 订单记录。如果 isIsolated = “TRUE”, symbol 为必填



## 查询最大可转出额

> 请求示例

```
get /api/v3/margin/maxTransferable?asset=BTC&symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  {
    "amount": "0.00022998"
  } 
]
```
**HTTP请求**

- **GET** ```/api/v3/margin/maxTransferable```

**请求参数**

| 参数名 | 说明| 是否必须  | 数据类型 |  示例            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|timestamp|时间 |是|string|1507725176595|
|signature|签名 |是|string|signature|
|asset|资产|是|string|BTC|
|symbol|交易对|是|string|BTCUSDT|

**返回参数**

| 参数名 | 说明  |数据类型 | 示例|
| :------------ | :-------- | :--------| :------------------- |
|amount| 可转出数额|string|0.00022998|


## 查询杠杆价格指数
说明
> 请求示例

```
get /api/v3/margin/priceIndex?symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  {
    "price": "21823.45",
    "symbol": "BTCUSDT",
    "calcTime": 1658215048128
  }
]
```
**HTTP请求**

- **GET** ```/api/v3/margin/priceIndex```

**请求参数**

| 参数名 | 说明| 是否必须  | 数据类型 |  示例            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|timestamp|时间 |是|string|1507725176595|
|signature|签名 |是|string|signature|
|symbol|交易对|是|string|BTCUSDT| 

**返回参数**

| 参数名 | 说明  |数据类型 | 示例|
| :------------ | :-------- | :--------| :------------------- |
|calcTime| 查询时间|number|1562046418000|
|price|下单价格 |string|21823.45|
|symbol| 交易对|string|BTCUSDT|



## 查询杠杆账户订单详情

> 请求示例

```
get /api/v3/margin/order?symbol=BTCUSDT&orderId=746779360689786880&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  {
    "symbol": "BTCUSDT",
    "orderId": "746779360689786880",
    "orderListId": "-1",
    "clientOrderId": null,
    "price": "20000",
    "origQty": "0.0003",
    "executedQty": "0",
    "cummulativeQuoteQty": "0",
    "status": "CANCELED",
    "type": "LIMIT",
    "side": "BUY",
    "isIsolated": true,
    "isWorking": true,
    "time": 1658212540000,
    "updateTime": 1658212551000
  }
]
```
**HTTP请求**

- **GET** ```/api/v3/margin/order```

**请求参数**

| 参数名 | 说明| 是否必须  | 数据类型 |  示例            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|timestamp|时间 |是|string|1507725176595|
|signature|签名 |是|string|signature|
|symbol|交易对|是|string|BTCUSDT|
|isIsolated|是否逐仓杠杆|否|string|"TRUE", "FALSE", 默认 "TRUE"|
|orderId|订单id|否|string| 746779360689786880|

**返回参数**

| 参数名 | 说明                               |数据类型 | 示例|
| :------------ |:---------------------------------| :--------| :------------------- |
|clientOrderId| 客户自定义订单id                        |string|ZwfQzuDIGpceVhKW5DvCmO|
|cummulativeQuoteQty| 累计成交金额累计交易货币数量？？                 |string|0.00000000|
|executedQty| 成交数量实际数量                         |string|0.00000000|
|isWorking| 是否正常工作                           |boolean|true|
|orderId| 订单id                             |number|213205622|
|origQty| 下单数量原始数量                         |string|0.30000000|
|price| 下单价格                             |string|0.00493630|
|side| 方向                               |string|SELL|
|status| <a href="#order_status">订单状态</a>                                 |string|NEW|
|symbol| 交易对                              |string|MXBTC|
|isIsolated| 是否是逐仓                            |boolean|true|
|time| 下单时间                             |number|1562133008725|
|type| <a href="#order_type">订单类型</a>   |string|LIMIT|
|updateTime| 更新时间                             |number|1562133008725|

**详细说明**：

必须发送 orderId 或 origClientOrderId 其中一个。一些历史订单的 cummulativeQuoteQty &lt; 0, 是指当前数据不存在。


## 查询杠杆逐仓账户信息

> 请求示例

```
get /api/v3/margin/isolated/account?symbols=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  {
    "assets": [
        {
            "baseAsset": {
                "asset": "BTC",
                "borrowEnabled": true,
                "borrowed": "0",
                "free": "0.00022998",
                "interest": "0",
                "locked": "0",
                "netAsset": "0.00022998",
                "netAssetOfBtc": "0.00022998",
                "repayEnabled": true,
                "totalAsset": "0.00022998"
            },
            "quoteAsset": {
                "asset": "USDT",
                "borrowEnabled": true,
                "borrowed": "0",
                "free": "10",
                "interest": "0",
                "locked": "0",
                "netAsset": "10",
                "netAssetOfBtc": "0.000458278339932541",
                "repayEnabled": true,
                "totalAsset": "10"
            },
            "symbol": "BTCUSDT",
            "isolatedCreated": true,
            "enabled": true,
            "marginLevel": "1.00006882",
            "marginRatio": "9",
            "indexPrice": "21804.199655172413793103",
            "liquidatePrice": "--",
            "liquidateRate": "--",
            "tradeEnabled": true
        }
    ]
  }  
]
```
**HTTP请求**

- **GET** ```/api/v3/margin/isolated/account```

**请求参数**

| 参数名 | 说明| 是否必须  | 数据类型 |  示例            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|timestamp|时间 |是|string|1507725176595|
|signature|签名 |是|string|signature|
|symbols|最多可以传5个symbol; 由","分隔的字符串表示. e.g. "BTCUSDT,MXUSDT,ADAUSDT"|是|string|

**返回参数**

| 参数名 | 说明  |数据类型 | 示例|
| :------------ | :-------- | :--------| :------------------- |
|asset|资产|string|BTC|
|borrowEnabled|是否可借 |boolean|true|
|borrowed| 已借金额|string|0|
|free| 可用金额|string|1|
|interest|利息金额 |string|0|
|locked|冻结金额 |string|0|
|netAsset| 净资产|string|1|
|netAssetOfBtc|净资产折合BTC |string|0.0002|
|repayEnabled|是否可还 |boolean|true|
|totalAsset|总资产 |string|1|
|symbol|交易对 |string|BTCUSDT|
|isolatedCreated| 该逐仓账户创建状态|boolean|true|
|enabled| 账户是否启用，true-启用，false-停用|boolean|true|
|marginLevel| 实际杠杆倍数|string|1|
|marginRatio| 支持杠杠倍数|string|9|
|indexPrice| 指数价格|string|10000.00000000|
|liquidatePrice| 强平价|string|1000.00000000|
|liquidateRate|强平率 |string|1.00000000|
|tradeEnabled| 是否可交易|boolean|true|


**详细说明**：

传”symbols”, 将只会返回制定symbol的杠杆逐仓资产


<!-- ## 查询止盈止损订单
说明

> 请求示例

```
get /api/v3/margin/trigerOrder
```
> 返回示例

```json
[

]
```
**HTTP请求**

- **GET** ```/api/v3/margin/trigerOrder```

**请求参数**

| 参数名 | 说明| 是否必须  | 数据类型 |  示例            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|timestamp|时间 |是|string|1507725176595|
|signature|签名 |是|string|signature|

**返回参数**

| 参数名 | 说明  |数据类型 | 示例|
| :------------ | :-------- | :--------| :------------------- |

 -->

## 查询账户最大可借贷额度

> 请求示例

```
get /api/v3/margin/maxBorrowable?asset=BTC&symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  {
    "amount": "0.00618914",
    "borrowLimit": "30"
  }
]
```
**HTTP请求**

- **GET** ```/api/v3/margin/maxBorrowable```

**请求参数**

| 参数名 | 说明| 是否必须  | 数据类型 |  示例            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|timestamp|时间 |是|string|1507725176595|
|signature|签名 |是|string|signature|
|asset|资产|是|string|BTC|
|symbol|交易对|是|string|BTCUSDT| 

**返回参数**

| 参数名 | 说明  |数据类型 | 示例|
| :------------ | :-------- | :--------| :------------------- |
|amount| 系统可借充足情况下，用户账户当前最大可借额度|string|1.69248805|
|borrowLimit| 平台限制的用户当前等级可以借的额度|string|60|


## 查询还贷记录

> 请求示例

```
get /api/v3/margin/repay?asset=BTC&symbol=BTCUSDT&tranId=2597392&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[

]
```
**HTTP请求**

- **GET** ```/api/v3/margin/repay```

**请求参数**

| 参数名 | 说明| 是否必须  | 数据类型 |  示例            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|timestamp|时间 |是|string|1507725176595|
|signature|签名 |是|string|signature|
|asset|资产|是|string|BTC|
|symbol|交易对|是|string|BTCUSDT|
|tranId|还款id|是|string| |
|startTime|开始时间 |否|string| |
|endTime|截止时间 |否|string| |
|current|当前查询页。开始值 1. 默认:1|否|string| |
|size|默认:10 最大:100|否|string| |
|recvWindow|同步时间 |否|string|6000 |

**返回参数**

| 参数名 | 说明  |数据类型 | 示例|
| :------------ | :-------- | :--------| :------------------- |
|symbol| 逐仓还款 返回逐仓symbol; 若是全仓不会返回此字段|string|MXUSDT|
|amount| 还款总额|string|14.00000000|
|asset|资产 |string|MX|
|interest| 支付的利息|string|0.01866667|
|principal| 支付的本金|string|13.98133333|
|timestamp|时间 |number|1563438204000|
|tranId| 还款id|number|2970933056|
|total|总数 |number|1|

**详细说明**：

必须发送tranId 或 startTime，tranId 优先。响应返回为降序排列。如果发送symbol，返回指定逐仓symbol指定asset的还贷记录。



## 查询逐仓杠杆交易对

> 请求示例

```
get /api/v3/margin/isolated/pair?symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  {
   "symbol":"BTCUSDT",
   "base":"BTC",
   "quote":"USDT",
   "isMarginTrade":true
  }
]
```
**HTTP请求**

- **GET** ```/api/v3/margin/isolated/pair```

**请求参数**

| 参数名 | 说明| 是否必须  | 数据类型 |  示例            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|timestamp|时间 |是|string|1507725176595|
|signature|签名 |是|string|signature|
|symbol|交易对|是|string|BTCUSDT|

**返回参数**

| 参数名 | 说明  |数据类型 | 示例|
| :------------ | :-------- | :--------| :------------------- |
|symbol| 交易对|string|BTCUSDT|
|base|交易币种 |string|BTC|
|quote| 计价币种|string|USDT|
|isMarginTrade|能不能杠杆交易 |boolean|true|



## 获取账户强制平仓记录

> 请求示例

```
get /api/v3/margin/forceLiquidationRec?symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[

]
```
**HTTP请求**

- **GET** ```/api/v3/margin/forceLiquidationRec```

**请求参数**

| 参数名 | 说明| 是否必须  | 数据类型 |  示例            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|timestamp|时间 |是|string|1507725176595|
|signature|签名 |是|string|signature|
|startTime|开始时间 |否|string| |
|endTime|截止时间 |否|string|| 
|symbol|交易对|是|string|BTCUSDT|
|current|当前查询页。 开始值 1. 默认:1|否|string|| 
|size|默认:10 最大:100|否|string|| 

**返回参数**

| 参数名 | 说明  |数据类型 | 示例|
| :------------ | :-------- | :--------| :------------------- |
|avgPrice| |string|0.00388359|
|executedQty|成交数量 |string|31.39000000|
|orderId|订单id没有order id 为系统还|string|180015097|
|price|下单价格没有price 为直接还|string|0.00388110|
|qty| 数量|string|31.39000000|
|side|方向 |string|SELL|
|symbol| 交易对|string|MXBTC|
|isIsolated| 是否是逐仓|boolean|true|
|updatedTime| 更新时间|number|1558941374745|
|total|总数 |number|1|

**详细说明**：

响应返回为降序排列。



## 获取逐仓杠杆利率及限额

> 请求示例

```
get /api/v3/margin/isolatedMarginData?symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  [
    {
        "symbol": "BTCUSDT",
        "leverage": "10",
        "data": [
            {
                "coin": "BTC",
                "hourInterest": "0.00026125",
                "borrowLimit": "270"
            },
            {
                "coin": "USDT",
                "hourInterest": "0.000475",
                "borrowLimit": "2100000"
            }
        ]
    }
] 

]
```
**HTTP请求**

- **GET** ```/api/v3/margin/isolatedMarginData```

**请求参数**

| 参数名 | 说明| 是否必须  | 数据类型 |  示例            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|timestamp|时间 |是|string|1507725176595|
|signature|签名 |是|string|signature|
|symbol|交易对|是|string|BTCUSDT|

**返回参数**

| 参数名 | 说明  |数据类型 | 示例|
| :------------ | :-------- | :--------| :------------------- |
|symbol| 交易对|string|BTCUSDT|
|leverage| 杠杆倍率|string|10|
|coin|币种 |string|BTC|
|hourInterest|小时利息|string|0.00026125|
|borrowLimit|借贷限额|string|270|



## 获取逐仓档位信息

> 请求示例

```
get /api/v3/margin/isolatedMarginTier?symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  [
    {
        "symbol": "BTCUSDT",
        "tier": 1,
        "effectiveMultiple": "10",
        "initialRiskRatio": "1.111",
        "liquidationRiskRatio": "1.05",
        "baseAssetMaxBorrowable": "9",
        "quoteAssetMaxBorrowable": "70000"
    }
  ]
]
```
**HTTP请求**

- **GET** ```/api/v3/margin/isolatedMarginTier```

**请求参数**

| 参数名 | 说明| 是否必须  | 数据类型 |  示例            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|timestamp|时间 |是|string||1507725176595|
|signature|签名 |是|string|signature|
|symbol|交易对|是|string|BTCUSDT|
|tier|不传则返回所有逐仓杠杆档位|否|string|| 

**返回参数**

| 参数名 | 说明  |数据类型 | 示例|
| :------------ | :-------- | :--------| :------------------- |
|symbol|交易对 |string|BTCUSDT|
|tier|仓位等级|number|1|
|effectiveMultiple|有效倍数|string|10|
|initialRiskRatio|初始风险比|string|1.111|
|liquidationRiskRatio|清算风险比|string|1.05|
|baseAssetMaxBorrowable|基础货币最大可借|string|9|
|quoteAssetMaxBorrowable|计价货币最大可借|string|70000|

# Websocket 行情推送

- 本篇所列出的所有wss接口的baseurl为: **wss://wbs.mexc.com/ws**
- 每个到 **wbs.mexc.com** 的链接有效期不超过24小时，请妥善处理断线重连
- symbol名称中所有交易对均为**大写**，如：`spot@public.deals.v3.api@<symbol>`</br>实例：`spot@public.deals.v3.api@BTCUSDT`
- websocket没有有效订阅的话，服务器会在**30秒**时主动断开连接，如果订阅成功但是没有流量，服务器会在**一分钟**时主动断开，客户端可以发送ping来保持链接
- 1个 ws 连接最多30个订阅
- 请按照文档返回的参数进行处理数据，文档没有返回的参数近期将进行优化处理，请勿使用

## 实时订阅/取消数据流

- 以下数据可以通过websocket发送以实现订阅或取消订阅数据流。示例如下。
- 响应内容中的`id`是无符号整数，作为往来信息的唯一标识。
- 如果相应内容中的 `msg` 为相应的请求字段，表示请求发送成功。

### 订阅一个信息流

> **订阅频道响应**

```
 {
  "id":0,
  "code":0,
  "msg":"spot@public.deals.v3.api@BTCUSDT"
 }
```

- **请求**


{
 "method":"SUBSCRIPTION",
 "params":["spot@public.deals.v3.api@BTCUSDT"]
}

### 取消订阅一个信息流

> **取消订阅响应**

```
 {
  "id":0,
  "code":0,
  "msg":"spot@public.increase.depth.v3.api@BTCUSDT,spot@public.deals.v3.api@BTCUSDT"
 }
```

- **请求**

{
 "method":"UNSUBSCRIPTION",
 "params":["spot@public.deals.v3.api@BTCUSDT","spot@public.increase.depth.v3.api@BTCUSDT"]
}

### PING/PONG机制

> **PING/PONG响应**

```
 {
  "id":0,
  "code":0,
  "msg":"PONG"
 }
```

- **请求**

{"method":"PING"}

## 逐笔交易(实时)

>**request:**

```
{
    "method": "SUBSCRIPTION",
    "params": [
        "spot@public.deals.v3.api@BTCUSDT"
    ]
}
```
> **response:**

```
{
	"c":"spot@public.deals.v3.api@BTCUSDT",    
	"d":{
			"deals":[{
					"S":2,                             //交易类型tradeType
					"p":"20233.84",                    //成交价格price
					"t":1661927587825,  				       //成交时间dealTime
					"v":"0.001028"}],  						     //成交数量quantity
			"e":"spot@public.deals.v3.api"},        //事件类型eventType			         
	"s":"BTCUSDT",  								           //交易对symbol
	"t":1661927587836                          //事件时间eventTime
} 								         
```

**请求参数：**   `spot@public.deals.v3.api@<symbol>`

逐笔交易推送每一笔成交的信息。**成交**，或者说交易的定义是仅有一个吃单者与一个挂单者相互交易

**返回参数:**

| 参数名      | 数据类型   | 说明 |
| :-------- | :----- | :--- |
| deals | array | 成交信息  |
| > S | int | 交易类型 1:买 2:卖 |
| > p | string | 成交价格 |
| > t | long | 成交时间 |
| > v | string | 成交数量 |
| e | string | 事件类型 |
| s | string | 交易对 |
| t | long | 事件时间 |

## K线 Streams

>**request:**

```
{
    "method": "SUBSCRIPTION",
    "params": [
        "spot@public.kline.v3.api@BTCUSDT@Min15"
    ]
}
```

> **response:**

```
{
	"c":"spot@public.kline.v3.api@BTCUSDT@Min15",  
	"d":{
			"k":{
				"T":1661931900,      //这根K线的结束时间                      
				"a":29043.48804658,	 //这根K线期间成交额
				"c":20279.43,				 //这根K线期间末一笔成交价
				"h":20284.93,				 //这根K线期间最高成交价
				"i":"Min15",				 //K线间隔
				"l":20277.52,				 //这根K线期间最低成交价
				"o":20284.93,				 //这根K线期间第一笔成交价
				"s":"BTCUSDT",			 //交易对
				"t":1661931000,			 //这根K线的起始时间
				"v":1.43211},				 //这根K线期间成交量
			"e":"spot@public.kline.v3.api"},					 //事件类型
	"s":"BTCUSDT",						 //交易对
	"t":1661931016878					 //事件时间
}

```

K线逐秒推送所请求的K线种类(最新一根K线)的更新。

**请求参数：** `spot@public.kline.v3.api@<symbol>@<interval>`

**返回参数:**

| 参数名      | 数据类型   | 说明 |
| :-------- | :----- | :--- |
| e | string | 事件类型 |
| k | object| k线信息 |
| > T | long | 这根K线的结束时间 |
| > a | bigDecimal | 这根K线期间成交额 |
| > c | bigDecimal | 这根K线期间末一笔成交价 |
| > h | bigDecimal | 这根K线期间最高成交价 |
| > i | interval | K线间隔 |
| > l | bigDecimal | 这根K线期间最低成交价 |
| > o | bigDecimal | 这根K线期间第一笔成交价 |
| > t | long | 这根K线的起始时间 |
| > v | bigDecimal | 这根K线期间成交量 |
| s | string | 交易对 |
| t | long | 事件时间 |

**K线图间隔参数:**

Min -> 分钟; Hour -> 小时; Day -> 天; Week -> 周, M -> 月

- Min1
- Min5
- Min15
- Min30
- Min60
- Hour4
- Hour8
- Day1
- Week1
- Month1

## 增量深度信息(实时)

>**request:**

```
{
    "method": "SUBSCRIPTION",
    "params": [
        "spot@public.increase.depth.v3.api@BTCUSDT"
    ]
}
```

> **response:**

```

{
	"c":"spot@public.increase.depth.v3.api@BTCUSDT",  
	"d":{
		"asks":[{									//bids:买单,asks:卖单
			"p":"20290.89",		//变动的价格档位
			"v":"0.000000"}], //数量
		"e":"spot@public.increase.depth.v3.api", },	 //事件类型
	"s":"BTCUSDT",							//交易对
	"t":1661932660144						//事件时间
}
```

如果某个价格对应的挂单量(v)为0，表示该价位的挂单已经撤单或者被吃，应该移除这个价位。

**请求参数:** `spot@public.increase.depth.v3.api@<symbol>`

**返回参数:**

| 参数名      | 数据类型   | 说明 |
| :-------- | :----- | :--- |
| p | string | 变动的价格档位 |
| v | string | 数量 |
| e | string | 事件类型 |
| s | string | 交易对 |
| t | long | 事件时间 |



<!-- ## 如何正确在本地维护一个orderbook副本

1. 通过订阅 **spot@public.increase.depth.v3.api@<symbol>**获取全量深度信息，保存当前version。
2. 订阅ws深度信息，收到更新后，如果收到的数据version>当前version,同一个价位，后收到的更新覆盖前面的。
3. 访问Rest接口 **https://api.mexc.com/api/v3/depth?symbol=MXBTC&limit=1000** 获得一个1000档的深度快照
4. 将目前缓存的深度信息中同一价格，version<步骤3获取到的快照中的version的数据丢弃。
5. 将深度快照中的内容更新至本地缓存，并从ws接收到的event开始继续更新。
6. 每一个新event的version应该恰好等于上一个event的version+1，否则可能出现了丢包，如出现丢包或者获取到的event的version不连续,请从步骤3重新进行初始化。
7. 每一个event中的挂单量代表这个价格目前的挂单量**绝对值**，而不是相对变化。
8. 如果某个价格对应的挂单量为0，表示该价位的挂单已经撤单或者被吃，应该移除这个价位。

注意: 因为深度快照对价格档位数量有限制，初始快照之外的价格档位并且没有数量变化的价格档位不会出现在增量深度的更新信息内。因此，即使应用来自增量深度的所有更新，这些价格档位也不会在本地 order book 中可见，所以本地的 order book 与真实的 order book 可能会有一些差异。 不过对于大多数用例，5000 的深度限制足以有效地了解市场和交易。 -->



# Websocket账户信息推送

- 本篇所列出API接口的base url : **https://api.mexc.com**
- 用于订阅账户数据的 `listenKey` 从创建时刻起有效期为60分钟
- 可以通过 `PUT` 一个 `listenKey` 延长60分钟有效期
- 可以通过`DELETE`一个 `listenKey` 立即关闭当前数据流，并使该`listenKey` 无效
- 在具有有效`listenKey`的帐户上执行`POST`将返回当前有效的`listenKey`并将其有效期延长60分钟
- websocket接口的baseurl: **wss://wbs.mexc.me/ws**
- 订阅账户数据流的stream名称为 **/ws?listenKey=listenKey** <br/>  如：**wss://wbs.mexc.me/ws?listenKey=pqia91ma19a5s61cv6a81va65sd099v8a65a1a5s61cv6a81va65sdf19v8a65a1**
- 每个链接有效期不超过24小时，请妥善处理断线重连
- 每个UID，最多申请60个listen key（不包含已失效listen key）
- ws链接数的数量限制：每个listen key最多5个ws链接（即：每个uid最多申请的60个listen key，300个ws链接）

## Listen Key(现货账户) 

### 生成 Listen Key 

> **响应**

```
{
  "listenKey": "pqia91ma19a5s61cv6a81va65sdf19v8a65a1a5s61cv6a81va65sdf19v8a65a1"
}
```

**HTTP请求**

- **POST**  ` /api/v3/userDataStream`

开始一个新的数据流。除非发送 keepalive，否则数据流于60分钟后关闭。如果该帐户具有有效的`listenKey`，则将返回该`listenKey`并将其有效期延长60分钟。 

**参数:**

NONE

### 延长 Listen Key 有效期 

> **响应**

```
{
    "listenKey": "pqia91ma19a5s61cv6a81va65sdf19v8a65a1a5s61cv6a81va65sdf19v8a65a1"
}
```

**HTTP请求**

- **PUT**  ` /api/v3/userDataStream`

有效期延长至本次调用后60分钟,建议每30分钟发送一次请求。

**请求参数:**

| 参数名    | 数据类型 | 是否必需 | 说明 |
| :-------- | :------- | :------- | :--- |
| listenKey | string   | 是      |      |

### 关闭 Listen Key  

> **响应**

```
{
    "listenKey": "pqia91ma19a5s61cv6a81va65sdf19v8a65a1a5s61cv6a81va65sdf19v8a65a1"
}
```

**HTTP请求**

- **DELETE**  ` /api/v3/userDataStream`

关闭用户数据流。

**请求参数:**

| 参数名    | 数据类型 | 是否必需 | 说明 |
| :-------- | :------- | :------- | :--- |
| listenKey | string   | 是      |      |

## 账户成交(实时)

>**request:**

```
{
    "method": "SUBSCRIPTION",
    "params": [
        "spot@private.deals.v3.api"
    ]
}
```

> **response:**

```
{
    "c": "spot@private.deals.v3.api",
    "d": {
        "S": 1,
        "T": 1661938980268,
        "c": "",
        "i": "c079b0fcb80a46e8b128b281ce4e4f38",
        "m": 1,
        "p": "1.008",
        "st": 0,
        "t": "4079b1522a0b40e7919f609e1ea38d44",
        "v": "5"
    },
    "s": "MXUSDT",
    "t": 1661938980285
}
```

**请求参数：** `spot@private.deals.v3.api`

**返回参数:**

| 参数名      | 数据类型   | 说明 |
| :-------- | :----- | :--- |
| d | json | 账户成交信息 |
| > S | int | 交易类型 1:买 2:卖 |
| > T | long | 成交时间 |
| > c | string | 用户自定义订单id: clientOrderId |
| > i | string | 订单id: orderId |
| > m | int | 是否是挂单: isMaker |
| > p | string | 交易价格 |
| > st | byte | 是否自成交：isSelfTrade |
| > t | string | 成交id: tradeId |
| > v | string | 交易数量 |
| s | string | 交易对 |
| t | long | 事件时间 |

## 账户订单(实时)

>**request:**

```
{
  "method": "SUBSCRIPTION",
  "params": [
      "spot@private.orders.v3.api"
  ]
}
```

**请求参数：** `spot@private.orders.v3.api`

### a.限价/市价订单 (实时)

> **response:**

```
{
  "c": "spot@private.orders.v3.api",
  "d": {
        "A":8.0,
        "O":1661938138000,
        "S":1,
        "V":10,
        "a":8,
        "c":"",
        "i":"e03a5c7441e44ed899466a7140b71391",
        "m":0,
        "o":1,
        "p":0.8,
        "s":1,
        "v":10
  },
  "s": "MXUSDT",
  "t": 1661938138193
}
```

**返回参数:**

| 参数名      | 数据类型   | 说明 |
| :-------- | :----- | :--- |
| d | json | 账户订单信息 |
| > A | bigDecimal | 实际剩余金额: remainAmount |
| > O | long | 订单创建时间 |
| > S | int | 交易类型 1:买 2:卖 |
| > V | bigDecimal | 实际剩余数量: remainQuantity |
| > a | bigDecimal | 下单总金额 |
| > c | string | 用户自定义订单id: clientOrderId |
| > i | string | 订单id |
| > m | int | 是否是挂单: isMaker |
| > o | int | 订单类型LIMIT_ORDER(1),POST_ONLY(2),IMMEDIATE_OR_CANCEL(3),<br />FILL_OR_KILL(4),MARKET_ORDER(5); 止盈止损（100） |
| > p | bigDecimal | 下单价格 |
| > s | int | 订单状态 1:未成交 2:已成交 3:部分成交 4:已撤单 5:部分撤单 |
| > v | bigDecimal | 下单数量 |
| t | long | 事件时间 |
| s | string | 交易对 |

### b.账户止盈止损订单(实时)

> **response:**

```
{
  "c": "spot@private.orders.v3.api",
  "d": {
        "N":"USDT",
        "O":1661938853715,
        "P":0.9,
        "S":1,
        "T":"LE",
        "i":"f6d82e5f41d745f59fe9d3cafffd80b5",
        "o":100,
        "p":1.01,
        "s":"NEW",
        "v":6
  },
  "s": "MXUSDT",
  "t": 1661938853727
}
```

**返回参数:**

|  参数名      | 数据类型   | 说明 |
| :-------- | :----- | :--- |
| d            | json | 账户订单信息 |
| > N | string | 手续费资产类别 |
|  > O | long | 订单创建时间 |
|  > P | bigDecimal | 触发价格 |
|  > S | int | 交易类型 1: 买 2: 卖 |
|  > T | int | 0: GE(买入价大过触发价) 1: LE(买入价小于触发价) |
|  > i | string | 订单id |
| >  o | int | 订单类型 LIMIT_ORDER(1),POST_ONLY(2),IMMEDIATE_OR_CANCEL(3),<br />FILL_OR_KILL(4),MARKET_ORDER(5); 止盈止损（100） |
|  > p | bigDecimal | 下单价格 |
| > s | string | 订单状态  NEW ,CANCELED ,EXECUTED, FAILED |
|  > v | bigDecimal | 下单数量 |
| s | string | 交易对 |
| t | long | 事件时间 |


# 邀请返佣接口

## 获取邀请返佣记录

> 请求示例

```
get /api/v3/rebate/taxQuery?timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
    "page": 1,  //当前页
    "totalRecords": 1,  //总记录数
    "totalPageNum": 1,  //总页数
    "data": [
        {
            "spot": "0.00082273",  // 现货返佣，以usdt计
            "futures":"0.00022487",        // 合约返佣，以usdt计
            "total": "0.00012126",  //累积奖励金额，以usdt计
            "uid": "221827",  // 受邀人UID
            "account": "154****291@qq.com",  // 受邀人账号
            "inviteTime": 1637651320000//邀请时间
        },
        ...
        {
            "spot": "0.00082273",  // 现货返佣，以usdt计
            "futures":"0.00022487",        // 合约返佣，以usdt计
            "total": "0.00012126",  //累积奖励金额，以usdt计
            "uid": "82937",  // 受邀人UID
            "account": "338****291@qq.com",  // 受邀人账号
            "inviteTime": 1637651320000//邀请时间
        }
    ]
}
```
**HTTP请求**

- **GET** ```/api/v3/rebate/taxQuery```

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
| startTime  | long | 否       |        |
| endTime    | long | 否       |        |
| page       | int  | 否       | 默认 1  |
| recvWindow | long | 否       |        |
| timestamp  | long | 是       |        |
| signature  | string | 是     |        |

**返回参数**

| 参数名  |类型 | 说明|
| :------------ | :-------- | :--------|
| spot |string|现货返佣，以usdt计|
| futures |string|合约返佣，以usdt计|
| total |string|累积奖励金额，以usdt计|
| uid |string|受邀人UID|
| account |string|受邀人账号|
| inviteTime |long|邀请时间|

若startTime和endTime均未发送,返回最近一年的数据。

## 获取返佣记录明细 （奖励记录）

> 请求示例

```
get /api/v3/rebate/detail?timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
     "page": 1, //当前页
     "totalRecords": 1, //总记录数
     "totalPageNum": 1, //总页数
     "data": [
         {
             "asset": "USDT", // 返佣资产，币种
             "type": "spot",       // 返佣类型：现货，杠杆，合约
             "rate": "0.3", // 返佣比例
             "amount": "0.0001126", // 返佣金额
             "uid": "2293729101827", // 受邀人UID
             "account": "154****291@qq.com", // 受邀人账号
             "tradeTime": 1637651320000,//用户交易时间
             "updateTime": 1637651320000//获取返佣时间
         },
         ...
         {
             "asset": "ETH", // 返佣资产，币种
             "type": "margin", // 返佣类型：现货，杠杆，合约
             "rate": "0.3", // 返佣比例
             "amount": "0.00000056",// 返佣金额
             "uid": "22937291018263", // 受邀人UID
             "account": "154****291@qq.com", // 受邀人账号
             "tradeTime": 1637651320000,//用户交易时间
             "updateTime": 1637928379000//获取返佣时间
         }
     ]
}
​
```
**HTTP请求**

- **GET** ```/api/v3/rebate/detail```

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
| startTime  | long | 否       |        |
| endTime    | long | 否       |        |
| page       | int  | 否       | 默认 1  |
| recvWindow | long | 否       |        |
| timestamp  | long | 是       |        |
| signature  | string | 是     |        |


**返回参数**

| 参数名  |类型 | 说明|
| :------------ | :-------- | :--------|
|asset|string|返佣资产，币种|
|type|string|返佣类型：现货，杠杆，合约|
|rate|string|返佣比例|
|amount|string|返佣金额|
|uid|string|受邀人UID|
|account|string|受邀人账号|
|tradeTime|long|用户交易时间|
|updateTime|long|获取返佣时间|

若startTime和endTime均未发送,返回最近一年的数据。

## 获取自返记录明细 （奖励记录）


> 请求示例

```
get /api/v3/rebate/detail/kickback?timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
    "page": 1,  //当前页
    "totalRecords": 27,  //总记录数
    "totalPageNum": 3,  //总页数
    "data": [
        {
            "asset": "USDT",  // 返佣资产，币种
            "type": "spot",        // 返佣类型：现货，杠杆，合约
            "rate": "0.3", // 返佣比例
            "amount": "0.0001126",  // 返佣金额
            "uid": "2293729101827",  // 受邀人UID
            "account": "154****291@qq.com",  // 受邀人账号
            "tradeTime": 1637651320000,//用户交易时间
            "updateTime": 1637651320000//获取返佣时间
        },
        ...
        {
            "asset": "ETH", // 返佣资产，币种
            "type": "margin", // 返佣类型：现货，杠杆，合约
            "rate": "0.3", // 返佣比例
            "amount": "0.00000056",// 返佣金额
            "uid": "22937291018263",  // 受邀人UID
            "account": "154****291@qq.com",  // 受邀人账号
            "tradeTime": 1637651320000,//用户交易时间
            "updateTime": 1637928379000//获取返佣时间
        }
    ]
}
```
**HTTP请求**

- **GET** ```/api/v3/rebate/detail/kickback```

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
| startTime  | long | 否       |        |
| endTime    | long | 否       |        |
| page       | int  | 否       | 默认 1  |
| recvWindow | long | 否       |        |
| timestamp  | long | 是       |        |
| signature  | string | 是     |        |


**返回参数**

| 参数名  |类型 | 说明|
| :------------ | :-------- | :--------|
|asset|string|返佣资产，币种|
|type|string|返佣类型：现货，杠杆，合约|
|rate|string|返佣比例|
|amount|string|返佣金额|
|uid|string|受邀人UID|
|account|string|受邀人账号|
|tradeTime|long|用户交易时间|
|updateTime|long|获取返佣时间|

若startTime和endTime均未发送,返回最近一年的数据。


# 公开API参数

## 枚举定义

### <a id="order_side">订单方向</a>

- BUY 买入
- SELL 卖出


### <a id="order_type">订单类型</a>

- LIMIT 限价单
- MARKET 市价单
- LIMIT_MAKER 限价只挂单
- IMMEDIATE_OR_CANCEL IOC单 (无法立即成交的部分就撤销,订单在失效前会尽量多的成交。)
- FILL_OR_KILL FOK单 (无法全部立即成交就撤销,如果无法全部成交,订单会失效。)

### <a id="order_status">订单状态</a>

- NEW 未成交
- FILLED 已成交
- PARTIALLY_FILLED 部分成交
- CANCELED 已撤销
- PARTIALLY_CANCELED 部分撤销

### <a id="kline">K线间隔</a>

- 1m  1分钟
- 5m  5分钟
- 15m  15分钟
- 30m  30分钟
- 60m  1小时
- 4h  4小时
- 1d  1天
- 1M  1月



