---
title: API 文档

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

includes:

search: true

meta:
  - name: description
    content: Documentation for the mexc API
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

[https://github.com/mexcdevelop/mexc-api-sdk](https://github.com/mexcdevelop/mexc-api-sdk)

<aside class="notice">
使用中遇到问题请通过<a href="https://github.com/mexcdevelop/mexc-api-sdk/issues" target="_blank">提交问题</a>反馈
</aside>

## Demo示例

我们提供了5种语言的demo，用户可以参考，目前支持了现货，推送等示例，后续会持续更新。

https://github.com/mexcdevelop/mexc-api-demo

使用中遇到问题请通过[提交问题](https://github.com/mexcdevelop/mexc-api-demo/issues)反馈

### Postman Collections

现在你可以通过`Postman collection`来快速体验、使用API接口。
如果想了解更多如何使用Postman，请访问: [Mexc API Postman](https://github.com/mexcdevelop/mexc-api-postman)

## 经纪商申请

MEXC致力于构建加密货币基础设施，提供有价值服务的API 经纪商合作伙伴是MEXC生态系统中的重要参与部分。MEXC推出了MEXC经纪商权益，包括交易返佣和营销支持，以奖励合作伙伴。

**目前MEXC支持的经纪商模式：**

**1. API 经纪商：**
包括集跟单平台、交易机器人、量化策略平台或其他500人以上资产管理平台等，用户可以将API key授权给API经纪商，API经纪商代替用户发送含有经济商ID的交易订单，获取手续费分润。

**2. 独立经纪商：**
包括钱包商、行情资讯平台、聚合交易平台、券商和股票证券交易平台等，有自己独立用户，MEXC可以提供订单撮合系统、账户管理系统、结算系统以及母子账户系统等，独立经纪商可共享全站流动性和深度，获得高额手续费分润。

合作请联系：institution@mexc.com

## 联系我们

- MEXC API电报群 [MEXC API Support Group](https://t.me/MEXCAPIsupport)
  - 咨询文档中没有提及的API问题
  - 咨询API或者websocket性能方面的问题
  - 咨询做市相关的问题
- MEXC 客服 *官网、app中在线客服*
  - 咨询关于钱包、短信、2FA等问题

# 更新日志

## **2025-02-24**
- 新增Protocol Buffers形式的websocket推送频道

## **2024-10-17**
- 新增查询账户KYC状态接口

## **2024-08-16**
- 交易规范信息接口更新返回参数

## **2024-06-09**
- 查询币种信息接口新增币种网络新参数，旧币种网络参数即将下线
- 新增提币新接口，旧提币接口即将下线

## **2024-05-15**
- 新增获取手续费率接口

## **2024-04-08**
- 获取提币历史接口更新返回参数

## **2024-01-12**
- 新增查询子账户资产接口

## **2024-01-01**
- K线查询支持周线
- 查询充值和提现历史接口调整查询时间窗口

## **2023-12-11**
- 查看子账户列表接口新增返回参数：子账户uid

## **2023-11-10**

- 新增用户站内转账接口、查询用户内部转账历史接口
- 新增miniTicker和miniTickers推送频道

## **2023-10-17**

- 新增查询直客页面数据接口、查询子代理页面数据接口

## **2023-09-27**

- 新增获取代理提现记录接口、获取代理返佣明细接口

## **2023-08-15**

- 新增获取代理邀请返佣记录接口

## **2023-06-13**

- 新增获取有效listenKey接口

## **2023-05-21**

- 新增历史行情数据下载

## **2023-03-16**

- 新增：查询用户万向划转历史（根据tranId）接口
- ws账户成交推送新增“手续费”、“手续费币种”和“交易金额”参数

## **2023-03-12**

- 新增：查询API交易对、用户API交易对、取消提币和获取提币地址接口

## **2023-03-07**

- ws新增频道：现货账户信息推送

## **2023-02-13**

- 新增获取小额资产可兑换列表、小额资产兑换和查询小额资产兑换历史接口

## **2023-02-07**

- ws新增频道：按Symbol的最优挂单信息

## **2023-01-06**

- [新增权重限速模式](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#c1fd2fc5ac)


## **2022-12-28**

- websocket新增有限档深度信息推送

## **2022-12-13**

- websocket `spot@private.orders.v3.api`频道新增：平均成交价，累计成交数量，累计成交金额三个参数。
- 新增获取邀请人接口


## **2022-11-24**

- 新增经纪商申请介绍
- 新增开启MX抵扣接口和查看MX抵扣状态接口

## **2022-10-14**

- 更新部分[钱包接口](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#ec5249e068)，具体如下：

  1、[提币接口](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#096be69702)：提币时，参数address和memo需要分别正确传入（原memo在address后以冒号拼接）；

  2、[获取提币历史](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#66382f2bd0)：参数address和memo分别正确返回（原memo在address后以冒号拼接）；

  3、[获取充值地址](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#aba7aa7a08)：返回参数tag改为memo，且充值所需memo会在memo参数中返回；

  4、[获取充值历史](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#70f3430304)：返回参数addressTag改为memo，且充值所需memo会在memo参数中返回；

  5、新增：[生成充值地址](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#66382f2bd0)

  6、[查询币种信息](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#2a7110133d)：新增withdrawTips和depositTips两个字段。

## **2022-09-06**

- 新增邀请返佣相关接口：

  1、[获取邀请返佣记录](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#8254d412a1)：获取您邀请的好友以及从他们进行的交易产生的返佣；

  2、[获取返佣记录明细 （奖励记录）](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#72fbc63aa1)：您可查看您的好友以及好友的子账户进行合约和现货（非杠杆)交易产生的每笔返佣记录；

  3、[获取自返记录明细 （奖励记录）](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#26b3666f08)：您可查看您以被邀請的好友身份进行的每笔合約和现货（无保证金）及从中产生的自返佣记录。

## **2022-09-02**

- 新增v3 websocket：

  1、Websocket 行情推送：包括[逐笔交易（实时）](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#2947d06b59)、[K线 Streams](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#k-streams)、[增量深度信息（实时）](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#efff33c875);

  2、Websocket账户信息推送:包括[成交推送（实时）](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#444af6a5fa)和[订单推送（实时）](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#ef28329b2a)；

## **2022-08-26**

- [获取ETF基础信息](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#etf-2)接口新增返回参数：

| 字段名称       | 数据类型 | 描述          |
| :------------- | :------- | :------------ |
| preBasket      | string   | 再平衡前篮子  |
| preLeverage    | string   | 再平衡前杠杆  |
| basket         | string   | 再平衡后篮子  |

## **2022-08-15**

- 新增部分母子账户接口：

  1、[母子用户万向划转](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#b588d84077)

  2、[查询母子万向划转历史](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#47ebdabc00)

## **2022-08-03**

- 新增部分钱包接口：

  1、[查询币种信息](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#2a7110133d)

  2、[提币](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#096be69702)

  3、[获取充值历史(支持多网络)](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#70f3430304)

  4、[获取提币历史(支持多网络)](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#66382f2bd0)

  5、[获取充值地址 (支持多网络)](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#aba7aa7a08)

  6、[用户万向划转](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#2e7fe13169)

  7、[查询用户万向划转历史](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#7a4f3b3457)

## **2022-07-27**

- 现货[下单](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#fd6ce2a756)接口新增订单类型：IOC和FOK

## **2022-07-15**

- [账户成交历史](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#1c077e2313)接口新增返回参数：

| 参数名          | 说明              |
| :-------------- | :---------------- |
| isSelfTrade     | 是否自成交        |

## **2022-07-08**

- 新增[批量下单](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#de93fae07b)接口：支持单次批量下20单；

## **2022-07-03**

- 钱包接口模块下新增：[查询币种信息](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#2a7110133d)接口，该接口可返回币种是否可充提/提币限额以及智能合约地址等。


## **2022-05-22**

- 交易规范信息接口优化
- 下单接口优化，统一返回order id

## **2022-04-25**

- [交易规范信息](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#e7746f7d60)接口新增返回参数：

| 参数名                     | 数据类型 | 说明                |
| :------------------------- | :------- | :------------------ |
| isSpotTradingAllowed       | Boolean  | 是否允许api现货交易 |
| isMarginTradingAllowed     | Boolean  | 是否允许api杠杆交易 |


- [当前挂单](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#066ca582c9)接口优化：支持多交易对查询，每次最多可以传5个symbol。

## **2022-03-29**

- 新增[母子账户](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#86382eac44)相关接口：

  1、[创建子账户](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#c6789f6fd9)

  2、[查看子账户列表](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#efa0aed0d6)

  3、[创建子账户的APIkey](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#apikey)

  4、[查询子账户的APIKey](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#apikey-2)

  5、[删除子账户的APIKey](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#apikey-3)

  6、[母子用户万向划转](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#b588d84077)

  7、[查询母子万向划转历史](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#47ebdabc00)

## **2022-03-25**

- 新增[API代码库](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#api)：Postman Collections，可以通过`Postman collection`来快速体验、使用API接口。

## **2022-03-24**

- 新增市价订单详细说明

## **2022-03-21**

- 新增订单状态枚举

## **2022-03-18**

- 新增[订单类型](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#8c6d51826c)：市价单（现货）
- 新增分页说明：startTime和endTime需同时使用

## **2022-03-09**

- 新增枚举类型

## **2022-02-19**

- 新增[ETF接口](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#etf)：包括[获取ETF基础信息](https://mexcdevelop.github.io/apidocs/spot_v3_cn/#etf-2)

## **2022-02-11**

- 新版API

# 常见问题

## Q1:一个用户可以申请多少个API Key？

每个账户最多可以创建30个API Key，未绑定ip地址的API Key有效期只有90天，到期自动失效。每个API Key最多绑定10个ip地址。

## Q2:一个母账户可以申请多少个子账户？

每个母账户最多可以创建30个子账户，子账户会自动继承母账户费率，通过api创建的子账户无法在web端登陆。

## Q3:为什么经常出现断线、超时的情况？

如果不能够稳定的访问，建议使用日本或者新加坡AWS云服务器进行访问。

## Q4:超出限制频率报错后，该怎么做？

超出接口访问频率限制后，无法继续访问接口，10分钟后会恢复正常，要保持低于限制的频率访问接口。

## Q5:一个账户最多可以下多少单？

每个账户最大可以同时拥有500个未完全成交的有效订单。

## Q6:为什么WebSocket总是断开连接？

1.如果没有有效订阅的话，会在30s断开链接。
2.如果订阅成功后，60s内没有流量，会自动断开。
3.需在接收到服务端发送的Ping信息后回复Pong，保证连接的稳定。

## Q7:WebSocket想要订阅多个频道为什么无效？

目前WebSocket单个链接最多可以订阅30个频道，超过30后则订阅无效，若想要订阅更多的频道，推荐建立多个链接。

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
- POST, PUT, 和 DELETE 方法的接口,参数可以在内容形式为application/x-www-form-urlencoded的 query string 中发送，也可以在 request body 中以application/json的形式发送。如果你喜欢，也可以混合这两种方式发送参数。
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
- 调用SIGNED接口时，除了接口本身所需的参数外，还需要在query string 或 request body中传递 signature, 即签名参数（在批量操作的API中，若参数值中有逗号等特殊符号，这些符号在签名时需要做URL encode，注意**encode只支持大写**）。
- 签名使用HMAC SHA256算法. API-KEY所对应的API-Secret作为 HMAC SHA256 的密钥，其他所有参数作为HMAC SHA256的操作对象，得到的输出即为签名。
- 签名 **目前只支持小写**。
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

对REST API的访问有频率限制，当超出限制时，返回状态429：请求过于频繁。

需要携带access key进行访问的接口，以账号作为限速的基本单位；不需要携带access key进行访问的接口，以IP作为限速的基本单位。

### 限频说明

- 每个接口会标明是按照IP或者按照UID统计, 以及相应请求一次的权重值。不同接口拥有不同的权重，越消耗资源的接口权重就会越大。
- **按IP和按UID(account)两种模式分别统计, 两者互相独立。按IP权重限频的接口，所有接口共用500权重/10秒；按UID权重限频的接口，所有接口共用500权重/10秒。**

### 超频报错

- 收到429时，您有责任停止发送请求，不得滥用API。
- **收到429后仍然继续违反访问限制，会被封禁IP。**
- 频繁违反限制，封禁时间会逐渐延长，**从最短2分钟到最长3天**。
- `Retry-After`的头会与带有418或429的响应发送，并且会给出**以秒为单位**的等待时长(如果是429)以防止禁令，或者如果是418，直到禁令结束。

### WEBSOCKET 连接限制
- Websocket服务器访问频率限制为：100次/s。
- 如果用户发送的消息超过限制，连接会被断开连接。反复被断开连接的IP有可能被服务器屏蔽。
- 单个连接最多可以订阅 30 个Streams。

## 错误码

以下为接口可能返回的错误码信息

| 错误码     | 说明                    |
|---------|-----------------------|
| -2011  |  未知订单                                                     |
| 26     |  该操作不允许                                                 |
| 400    |  需要APIKEY                                                   |
| 401    |  未授权                                                       |
| 403    |  访问被拒                                                     |
| 429    |  请求过多                                                     |
| 500    |  内部错误                                                     |
| 503    |  服务不可用，请重试                                           |
| 504    |  网关超时                                                     |
| 602    |  签名认证失败                                                 |
| 10001  |  用户不存在                                                   |
| 10007  |  该交易对不支持api交易                                        |
| 10015  |  用户id不能为空                                               |
| 10072  |  无效的access key                                             |
| 10073  |  无效的请求时间                                               |
| 10095  |  金额不能为空                                                 |
| 10096  |  金额小数位过大                                               |
| 10097  |  金额错误                                                     |
| 10098  |  因风控原因，无法划转，请稍后重试                             |
| 10099  |  子站账号未开通                                               |
| 10100  |  不支持该币种划转                                             |
| 10101  |  资产余额不足                                                 |
| 10102  |  金额不能为零或负数                                           |
| 10103  |  不支持该账户划转                                             |
| 10200  |  转账操作处理中                                               |
| 10201  |  用户资金入账失败                                             |
| 10202  |  用户资金出账失败                                             |
| 10206  |  转账关闭                                                     |
| 10211  |  禁止提现                                                     |
| 10212  |  提币地址不是常用地址或已失效                                 |
| 10216  |  没有可用地址，请稍后再试                                     |
| 10219  |  资产流水写入失败请重新尝试                                   |
| 10222  |  币种不能为空                                                 |
| 10232  |  币种不存在                                                   |
| 10259  |  未配置中间账户错误                                           |
| 10265  |  由于风控原因，暂不支持提币，请稍后再试                       |
| 10268  |  备注长度过大                                                 |
| 20001  |  不支持此子系统                                               |
| 20002  |  内部系统调用错误                                             |
| 22222  |  记录不存在                                                   |
| 30000  |  交易对暂停交易                                               |
| 30001  |  当前交易方向不允许下单                                       |
| 30002  |  最小交易量不能小过                                           |
| 30003  |  最大交易量不能大过                                           |
| 30004  |  持仓不足                                                     |
| 30005  |  卖出超过持仓                                                 |
| 30010  |  无效价格                                                     |
| 30014  | 无效交易对                                                   |
| 30016  |  无法交易                                                     |
| 30018  |  暂不支持市价单                                               |
| 30019  |  暂不支持API市价单                                            |
| 30020  |  该交易对不支持api                                            |
| 30021  |  无效交易对                                                   |
| 30025  |  不存在的对手订单                                             |
| 30026  |  无效的订单id                                                 |
| 30027  |  该货币已达到最大持仓限制，买入暂停                           |
| 30028  |  货币触发平台风控，抛售暂停                                   |
| 30029  | 不能超过最大订单限制                                         |
| 30032  | 不能超过最大仓位                                             |
| 30041  |  目前的订单类型不支持下单                                     |
| 33333  |  参数错误                                                     |
| 44444  | 参数不能为空                                                 |
| 60005  | 您的账号存在异常，暂时无法进行法币交易，请联系客服或稍后再试 |
| 70011  | 交易对不支持api交易                                          |
| 700001 |  apikey格式错误                                               |
| 700002 | 签名无效                                                     |
| 700003 | 此请求的时间戳在 recvWindow 之外                             |
| 700004 | 参数'origClientOrderId' 或 'orderId'至少需要一个             |
| 700005 | recvWindow 必须小于 60000                                    |
| 700006 |  IP非白名单                                                   |
| 700007 | 没有访问端点的权限                                           |
| 700008 | 参数中有无效字节                                             |
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
| 140001 | 子账号不存在         |
| 140002 | 禁止子账号访问      |



# 行情接口

## 历史行情数据下载

提供2023年01月01日以来的K线和交易历史数据下载：[历史行情数据下载](https://www.mexc.co/zh-CN/market-data-download)

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

**权重(IP):** 1

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
  
**权重(IP):** 1

**请求参数**

NONE


## API交易对

获取平台可API交易的交易对

> 请求示例

```
GET /api/v3/defaultSymbols
```

> 返回示例

```json
{
    "code": 200,
    "data": [
        "GENE1USDT",
        "SNTUSDT",
        "SQUAWKUSDT",
        "HEGICUSDT",
        "GUMUSDT"
    ],
    "msg": null
}
```
**HTTP请求**

- **GET** ```/api/v3/defaultSymbols ```
  
**权重(IP):** 1

**请求参数**

NONE

**返回参数**

| 参数名       | 数据类型 | 说明                       |
| :------------ | :-------- |:-------------------------|
| symbol | string | 返回支持API交易的交易对      |


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
                "Limit"
            ],
            "filters": [],
            "maxQuoteAmount": "5000000",
            "makerCommission": "0.002",
            "takerCommission": "0.002",
            "tradeSideType":"1"
        }
}

```
**HTTP请求**

- **GET** ```/api/v3/exchangeInfo```

**权重(IP):** 10

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
| status | String | 状态:1 - 开放， 2 - 暂停， 3 - 下线           |
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
| maxQuoteAmount | String | 最大下单金额                   |
| makerCommission | String | marker手续费                |
| takerCommission | String | taker手续费                 |
| quoteAmountPrecision|string| 最小下单金额                   |
| baseSizePrecision|string| 最小下单数量                   |
| quoteAmountPrecisionMarket |string| 市价最小下单金额                   |
| maxQuoteAmountMarket | String | 市价最大下单金额                   |
| tradeSideType | String | 交易对可交易方向:1 - 全部， 2 - 仅买单， 3 - 仅卖单，4 - 关闭     |




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

**权重(IP):** 基于限制调整

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

**权重(IP):** 5

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

**权重(IP):** 1

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
GET /api/v3/klines?symbol=BTCUSDT&interval=1m&startTime=1652848049876&endTime=1652848650458
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
  
**权重(IP):** 1

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

**权重(IP):** 1

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

**权重(IP):** 1单交易对/40所有交易对

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

**权重(IP):**1 单一交易对;**2** 交易对参数缺失

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

**权重(IP):**1 单一交易对;**2** 交易对参数缺失;

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

**接口权限要求:** 账户读 / SPOT_ACCOUNT_R 

**权重(IP):** 1

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
            "createTime":1544433328000,
            "uid": "49910511"
        },
        {
            "subAccount":"subAccount2",
            "isFreeze":false,
            "createTime":1544433328000,
            "uid": "91921059"
        }
    ]
}

```

 **HTTP请求**

- **GET**  ```/api/v3/sub-account/list```

**接口权限要求:** 账户读 / SPOT_ACCOUNT_R  

**权重(IP):** 1

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
| uid | string | 子账户uid |



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

**接口权限要求:** 账户读 / SPOT_ACCOUNT_R  

**权重(IP):** 1

**请求参数**

| 参数名      | 类型   | 是否必须 | 说明                                                         |
| :----------- | :------ | :-------- | :------------------------------------------------------------ |
| subAccount  | string | 是       | 子账户名称 如：subAccount1                                   |
| note        | string | 是       | APIKey的备注                                                 |
| permissions | string | 是       | APIKey权限:<br/>账户读/SPOT_ACCOUNT_READ,<br/>账户写/SPOT_ACCOUNT_WRITE,<br/>现货交易信息读/SPOT_DEAL_READ,<br/>现货交易信息写/SPOT_DEAL_WRITE,<br/>合约账户信息读/CONTRACT_ACCOUNT_READ,<br/>合约账户信息写/CONTRACT_ACCOUNT_WRITE,<br/>合约交易信息读/CONTRACT_DEAL_READ,<br/>合约交易信息写/CONTRACT_DEAL_WRITE,<br/>资金划转读/SPOT_TRANSFER_READ,<br/>资金划转写/SPOT_TRANSFER_WRITE|
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

**接口权限要求:** 账户读 / SPOT_ACCOUNT_R 

**权重(IP):** 1

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

**接口权限要求:** 账户读 / SPOT_ACCOUNT_R 

**权重(IP):** 1

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

**接口权限要求:** 资金划转写 / SPOT_TRANSFER_W 

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明                                                                 | 
| :------ | :-------- | :-------- |:-------------------------------------------------------------------|
|fromAccount|string|否| 母子账户，可填subAccout账户名，不填默认母账户                                        |
|toAccount|string|否| 母子账户，可填subAccout账户名，不填默认母账户                                        |
|fromAccountType|string|是| 划出账户类型，现货/合约，枚举值："SPOT","FUTURES",划转规则见上描述 |
|toAccountType|string|是| 划出账户类型，现货/合约，枚举值："SPOT","FUTURES",划转规则见上描述 |
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

**接口权限要求:** 资金划转读 / SPOT_TRANSFER_R

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
|fromAccount|string|否|母子账户，可填subAccout账户名，不填默认母账户|
|toAccount|string|否|母子账户，可填subAccout账户名，不填默认母账户|
|fromAccountType|string|是|划出账户类型，现货/合约，枚举值："SPOT","FUTURES",划转规则见上描述|
|toAccountType|string|是|划出账户类型，现货/合约，枚举值："SPOT","FUTURES",划转规则见上描述|
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


## 查询子账户资产

> 请求示例

```
get /api/v3/sub-account/asset?subAccount=account1&accountType=SPOT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
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
    ]
}
```
**HTTP请求**

- **GET** ```/api/v3/sub-account/asset```  

**接口权限要求:** 资金划转读 / SPOT_TRANSFER_R

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
| subAccount | string | 是       | 子账户名称，仅支持单个子账户查询       |
| accountType|string|是|账户类型，现货/合约，枚举值："SPOT","FUTURES",当前仅支持SPOT|
| timestamp|string|是|时间戳|
| signature|string|是|签名|


**返回参数**

| 参数名  |类型 | 说明|
| :------------ | :-------- | :--------|
|balances|string|余额|
|asset|string|币种|
|free|string|可用数量|
|locked|string|冻结数量|



# 现货账户和交易接口

## 查询账户KYC状态

> 请求示例

```
GET /api/v3/kyc/status?timestamp={{timestamp}}&signature={{signature}}
```

> 返回示例

```json
{
"status": "1"
}
```
**HTTP请求**

- **GET** ```/api/v3/kyc/status ```

**接口权限要求:** 账户读 / SPOT_ACCOUNT_READ

**权重(IP):** 1

**请求参数**

| 参数名     | 数据类型 | 是否必须 | 说明                 |
| :---------- | :-------- | :-------- | :-------------------- |
|timestamp    |string     |是         |   时间戳        |
|signature    |string     |是         |签名            |

**返回参数**

| 参数名       | 数据类型 | 说明                       |
| :------------ | :-------- |:-------------------------|
| status | string | 1:未kyc  2:初级kyc  3:高级kyc 4:机构kyc  |


## 用户API交易对

获取用户可API交易的交易对

> 请求示例

```
GET /api/v3/selfSymbols?timestamp={{timestamp}}&signature={{signature}}
```

> 返回示例

```json
{
    "code": 200,
    "data": [
        "GENE1USDT",
        "SNTUSDT",
        "SQUAWKUSDT",
        "HEGICUSDT",
        "GUMUSDT"
    ],
    "msg": null
}
```
**HTTP请求**

- **GET** ```/api/v3/selfSymbols ```

**接口权限要求:** 账户读 / SPOT_ACCOUNT_R

**权重(IP):** 1

**请求参数**

NONE

**返回参数**

| 参数名       | 数据类型 | 说明                       |
| :------------ | :-------- |:-------------------------|
| symbol | string | 返回支持API交易的交易对      |


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

**接口权限要求:** 现货交易信息写 / SPOT_DEAL_W

**权重(IP):** 1

**请求参数**

同于 POST /api/v3/order

## 下单
只有当您的账户有足够的资金才能下单。

> 请求示例

```
POST /api/v3/order?symbol=MXUSDT&side=BUY&type=LIMIT&quantity=50&price=0.1&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
    "symbol": "MXUSDT",
    "orderId": "06a480e69e604477bfb48dddd5f0b750",
    "orderListId": -1,
    "price": "0.1",
    "origQty": "50",
    "type": "LIMIT",
    "side": "BUY",
    "transactTime": 1666676533741
}
```
**HTTP请求**

- **POST** ```/api/v3/order```  

**接口权限要求:** 现货交易信息写 / SPOT_DEAL_W

**权重(IP):** 1/**权重(UID):** 1

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

MARKET：当type是market时，不论是买单或者卖单，quoteOrderQty和quantity参数任选其一。

- 比如在`BTCUSDT`上下一个市价买单, 明确的是买入时想要花费的计价资产数量。此时的报单数量将会以市场流动性和`quoteOrderQty`被计算出来（实际成交数量以最终订单详情为准）。
  以`BTCUSDT`为例，`quoteOrderQty=100`:下买单的时候, 订单会尽可能的买进价值100USDT的BTC.

- 比如在`BTCUSDT`上下一个市价卖单, `quantity`为用户指明能够卖出多少BTC。

**返回参数**


| 参数名       | 数据类型 | 说明                |
| :------------ | :-------- | :------------------- |
| symbol | string | 交易对 |
| orderId | string | 订单id |
| orderListId|string|客户端订单列表 |
| price | string | 订单id |
| origQty | string | 委托数量 |
| type | string | <a href="#order_type">订单类型</a>|
| side | string | <a href="#order_side">订单方向</a> |
| transactTime | long | 下单时间 |


## 批量下单
支持单次批量下30单,要求必须是同一交易对。

> 请求示例

```
POST /api/v3/batchOrders?batchOrders=[{"type": "LIMIT_ORDER","price": "40000","quantity": "0.0002","symbol": "BTCUSDT","side": "BUY","newClientOrderId": 9588234},{"type": "LIMIT_ORDER","price": "4005","quantity": "0.0003","symbol": "BTCUSDT","side": "SELL"}]
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

**接口权限要求:** 现货交易信息写 / SPOT_DEAL_W

**权重(IP):** 1

**请求参数**


| 名称             | 类型    | 是否必需 | 说明                   |
| :--------------- | :------ | :------- | :--------------------- |
| batchOrders      | LIST  | 是      | 订单列表，最多支持30个订单(list of JSON格式填写订单参数,参考请求示例) |
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

**接口权限要求:** 现货交易信息写 / SPOT_DEAL_W

**权重(IP):** 1

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

**接口权限要求:** 现货交易信息写 / SPOT_DEAL_W

**权重(IP):** 1

**请求参数**

| 参数名     | 数据类型 | 是否必须 | 说明   |
| :---------- | :-------- | :-------- | :------ |
| symbol     | string   | 是       | 交易对 |
| recvWindow | long     | 否       |        |
| timestamp  | long     | 是       |        |


**返回参数**

| 参数名                 | 说明           |
|:--------------------|:-------------|
| symbol              | 交易对          |
| origClientOrderId   | 原始客户端订单id    |
| orderId             | 订单id         |
| clientOrderId       | 客户端id        |
| price               | 价格           |
| origQty             | 初始数量         |
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

**接口权限要求:** 现货交易信息读 / SPOT_DEAL_R

**权重(IP):** 2

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

**接口权限要求:** 现货交易信息读 / SPOT_DEAL_R

**权重(IP):** 3

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

**接口权限要求:** 现货交易信息读 / SPOT_DEAL_R

**权重(IP):** 10

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
获取当前账户信息。

> 请求示例

```
GET /api/v3/account?timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
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

**接口权限要求:** 账户读 / SPOT_ACCOUNT_R

**权重(IP):** 10

**请求参数**

| 参数名     | 数据类型 | 是否必须 | 说明 |
| :---------- | :-------- | :-------- | :---- |
| recvWindow | long     | 否       |      |
| timestamp  | long     | 是       |      |


**返回参数**

| 参数名           | 说明       |
| :---------------- | :---------- |
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
获取账户指定交易对的成交历史，仅可查询近1月成交记录，如需查看更多成交记录，请使用web端导出功能，最多支持导出近3年成交记录。


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

**接口权限要求:** 账户读 / SPOT_ACCOUNT_R

**权重(IP):** 10

**请求参数**

| 参数名     | 数据类型 | 是否必须 | 说明                 |
| :---------- | :-------- | :-------- | :-------------------- |
| symbol     | string   | 是       | 交易对               |
| orderId    | string   | 否       | 必须和symbol一起使用 |
| startTime  | long     | 否       |                      |
| endTime    | long     | 否       |                      |
| limit      | int      | 否       | 默认 100; 最大 100; |
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

## 开启MX抵扣
调用该接口，开启或者关闭现货MX抵扣手续费设置

> 请求示例

```
post api/v3/mxDeduct/enable?timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
  "data":{
    "mxDeductEnable":true
  },
  "code":0,
  "msg":"success",
  "timestamp":1669109672280
} 
```
**HTTP请求**

- **POST** ```api/v3/mxDeduct/enable```  

**接口权限要求:** 现货交易信息写 / SPOT_DEAL_W

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
|mxDeductEnable|boolean|yes|是否开启MX抵扣,true:开启, false:关闭|
|recvWindow|long|no|同步时间|
|timestamp|long|yes|时间戳|
|signature|string|yes|签名|

**返回参数**

| 参数名  |类型 | 说明|
| :------------ | :-------- | :--------|
|mxDeductEnable|boolean|是否开启了MX抵扣,true:已开启,false:已关闭.|

<aside class="notice">合约账户的MX抵扣：将MX转入合约账户, 即可使用MX抵扣USDT本位合约手续费, 享受10%手续费折扣</aside>


## 查看MX抵扣状态

> 请求示例

```
get api/v3/mxDeduct/enable?timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
  "data":{
    "mxDeductEnable":false
  },
  "code":0,
  "msg":"success",
  "timestamp":1669109672717
}
```
**HTTP请求**

- **GET** ```api/v3/mxDeduct/enable```  

**接口权限要求:** 现货交易信息读 / SPOT_DEAL_R

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
|recvWindow|long|no|同步时间|
|timestamp|long|yes|时间戳|
|signature|string|yes|签名|


**返回参数**

| 参数名  |类型 | 说明|
| :------------ | :-------- | :--------|
|mxDeductEnable|boolean|是否开启了MX抵扣,true:已开启,false:已关闭.|

## 查看手续费率

> 请求示例

```
get api/v3/tradeFee?symbol=MXUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
  "data":{
    "makerCommission":0.003000000000000000,
    "takerCommission":0.003000000000000000
  },
  "code":0,
  "msg":"success",
  "timestamp":1669109672717
}
```
**HTTP请求**

- **GET** ```api/v3/tradeFee```  

**接口权限要求:** 账户信息读 / SPOT_ACCOUNT_R

**权重(IP):** 20

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
|symbol|string|yes|交易对|
|recvWindow|long|no|同步时间|
|timestamp|long|yes|时间戳|
|signature|string|yes|签名|


**返回参数**

| 参数名  |类型 | 说明|
| :------------ | :-------- | :--------|
|makerCommission|long|用户maker费率|
|takerCommission|long|用户taker费率|


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
    "coin": "EOS",
    "name": "EOS",
    "networkList": [
      {
          "coin": "EOS",
          "depositDesc": null,
          "depositEnable": true,
          "minConfirm": 0,
          "name": "EOS",
          "network": "EOS",
          "withdrawEnable": false,
          "withdrawFee": "0.000100000000000000",
          "withdrawIntegerMultiple": null,
          "withdrawMax": "10000.000000000000000000",
          "withdrawMin": "0.001000000000000000",
          "sameAddress": false,
          "contract": "TN3W4H6rK2ce4vX9YnFQHwKENnHjoxbm9",
          "withdrawTips": "Both a MEMO and an Address are required.",
          "depositTips": "Both a MEMO and an Address are required.",
          "netWork": "EOS"
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
          "contract": "0x7130d2a12b9bcbfae4f2634d864a1ee1ce3ead9c",
          "withdrawTips": null,
          "depositTips": null,
          "netWork": "BTC"
      }
    ]
  },
]
```
**HTTP请求**

- **GET** ```/api/v3/capital/config/getall```  

**接口权限要求:** 钱包提现相关读 / SPOT_WITHDRAW_R

**权重(IP):** 10

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
|timestamp|string|是|时间戳|
|signature|string|是|签名|


**返回参数**

| 参数名 | 说明  | 
| :------------ | :------------ |
|depositEnable|是否可充值|
|withdrawEnable|是否可提币|
|withdrawFee|提币手续费| 
|withdrawMax|最大提币限额|
|withdrawMin|最小提币限额|
|contract|币种智能合约地址|
|network|币种所支持的网络（旧参数，即将下线，建议提币使用提币新接口）| 
|netWork|币种所支持的网络（新参数，适用于提币新接口）| 


## 提币（新增）

> 请求示例

```
post /api/v3/capital/withdraw?coin=EOS&address=zzqqqqqqqqqq&amount=10&network=EOS&memo=MX10086&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
    "id":"7213fea8e94b4a5593d507237e5a555b"
}
```
**HTTP请求**

- **POST** ```/api/v3/capital/withdraw```  

**接口权限要求:** 钱包提现相关写 / SPOT_WITHDRAW_W

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须 | 说明               | 
| :------ | :-------- |:-----|:-----------------|
|coin|string| 是    | 币种               |
|withdrawOrderId|string| 否    | 自定义提币ID   |
|netWork|string| 否    | 提币网络             |
|contractAddress|string| 否    | 币种智能合约地址             |
|address|string| 是    | 提币地址             |
|memo|string| 否    | 如地址中需求memo，则此处必传 |
|amount|string| 是    | 数量               |
|remark|string| 否    | 备注               |
|timestamp|string| 是    | 时间戳              |
|signature|string| 是    | 签名               |
 

可以在接口 `Get /api/v3/capital/config/getall`的返回值中某币种的`networkList`获取`netWork`网络字段。


**返回参数**

| 参数名 | 说明  |
| :------------ | :-------- | 
|id|提币ID|

## 取消提币

> 请求示例

```
delete /api/v3/capital/withdraw?id=ca7bd51895134fb5bd749f1cf875b8af&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
    "id": "ca7bd51895134fb5bd749f1cf875b8af"
}
```
**HTTP请求**

- **DELETE** ```/api/v3/capital/withdraw```  

**接口权限要求:** 钱包提现相关写 / SPOT_WITHDRAW_W

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须 | 说明               | 
| :------ | :-------- |:-----|:-----------------|
|id|string| 是    | 提币ID              |

**返回参数**

| 参数名 | 说明  |
| :------------ | :-------- | 
|id|提币ID|

## 获取充值历史(支持多网络)

> 请求示例

```
get /api/v3/capital/deposit/hisrec?coin=EOS&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  {
        "amount": "50000",
        "coin": "EOS",
        "network": "EOS",
        "status": 5,
        "address": "0x20b7cf77db93d6ef1ab979c49142ec168427fdee",
        "txId": "01391d1c1397ef0a3cbb3c7f99a90846f7c8c2a8dddcdcf84f46b530dede203e1bc804",
        "insertTime": 1659513342000,
        "unlockConfirm": "10",
        "confirmTimes": "241",
        "memo": "xxyy1122"
  }
]
```
**HTTP请求**

- **GET** ```/api/v3/capital/deposit/hisrec```  

**接口权限要求:** 钱包提现相关读 / SPOT_WITHDRAW_R

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| :------ | :-------- |:-----| :---------- |
|coin|string| 否    |币种|
|status|string| 否    |状态|
|startTime|string| 否    |默认当前时间7天前的时间|
|endTime|string| 否    |默认当前时间戳，13位|
|limit|string| 否    |默认：1000，最大1000|
|timestamp|string| 是    |时间戳|
|signature|string| 是    |签名|

1. 默认返回最近7天的记录.
2. `startTime` 与 `endTime` 的默认时间戳，保证请求时间间隔不超过7天.
3. 做多可查询90天内的记录.
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
|memo|memo|

## 获取提币历史 (支持多网络)

> 请求示例

```
get /api/v3/capital/withdraw/history?coin=EOS&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
  {
        "id": "bb17a2d452684f00a523c015d512a341",
        "txId": null,
        "coin": "EOS",
        "network": "EOS",
        "address": "zzqqqqqqqqqq",
        "amount": "10",
        "transferType": 0,
        "status": 3,
        "transactionFee": "0",
        "confirmNo": null,
        "applyTime": 1665300874000,
        "remark": "",
        "memo": "MX10086",
        "transHash": "0x0ced593b8b5adc9f6003a934d0d7335456a7ed772ea5547beda4f33a065c",
        "updateTime": 1712134082000,
        "coinId": "128f589271cb491b03e71e6323eb7be",
        "vcoinId": "af42c6414b9a43869ce30fd51660f"
  }
]
```
**HTTP请求**

- **GET** ```/api/v3/capital/withdraw/history```  

**接口权限要求:** 钱包提现相关读 / SPOT_WITHDRAW_R

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| :------ | :-------- |:-----| :---------- |
|coin|string| 否    |币种|
|status|string| 否    |提币状态|
|limit|string| 否    |默认：1000， 最大：1000|
|startTime|string| 否    |默认当前时间7天前的时间戳|
|endTime|string| 否    |默认当前时间戳|
|timestamp|string| 是    |时间戳|
|signature|string| 是    |签名|

1. 默认返回最近7天的记录.
2. `startTime` 与 `endTime` 的默认时间戳，保证请求时间间隔不超过7天.
3. 做多可查询90天内的记录.
4. 支持多网络提币前的历史记录可能不会返回`network`字段.
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
|memo|memo|
|transHash|交易hash|
|coinId|资产id|
|vcoinId|币种id|

## 生成充值地址 (支持多网络)

> 请求示例

```
post /api/v3/capital/deposit/address?coin=EOS&network=EOS&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
    "coin": "EOS",
    "network": "EOS",
    "address": "zzqqqqqqqqqq",
    "memo": "MX10068"
}
```
**HTTP请求**

- **POST** ```/api/v3/capital/deposit/address```  

**接口权限要求:** 钱包提现相关写 / SPOT_WITHDRAW_W  

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| :------ | :-------- |:-----| :---------- |
|coin|string| 是    |币种|
|network|string| 是    |充值网络|
|timestamp|string| 是    |时间戳|
|signature|string| 是    |签名|


**返回参数**

| 参数名 | 说明  |
| :------------ | :-------- | 
|address|地址|
|coin|币种|
|network|链类型|
|memo|memo值|

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
      "memo": null
  },
  {
      "coin": "USDT",
      "network": "BEP20(BSC)",
      "address": "0xebe4804f7ecc22d5011c42e6ea1f2e6c891d89b",
      "memo": null
  },
  {
      "coin": "USDT",
      "network": "ERC20",
      "address": "0x3f4d1f43761b52fd594e5a77cd83cab6955e85b",
      "memo": null
  }
]
```
**HTTP请求**

- **GET** ```/api/v3/capital/deposit/address```  

**接口权限要求:** 钱包提现相关读 / SPOT_WITHDRAW_R

**权重(IP):** 10

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
|memo|memo|
|network|网络|

## 获取提币地址 (支持多网络)

> 请求示例

```
get /api/v3/capital/withdraw/address?coin=USDT&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
    "data": [
        {
            "coin": "USDT",
            "network": "TRC20",
            "address": "TArGWdTApuuZtiWMjupXqbZqQYsBTy126o",
            "addressTag": "test",
            "memo": null
        },
        {
            "coin": "USDT",
            "network": "BEP20(BSC)",
            "address": "0xa82898C70BeB5E1b1621fdA62fD17Ba27227BBC5",
            "addressTag": "usdt",
            "memo": null
        }
    ],
    "totalRecords": 2,
    "page": 1,
    "totalPageNum": 1
}
```
**HTTP请求**

- **GET** ```/api/v3/capital/withdraw/address```  

**接口权限要求:** 钱包提现相关读 / SPOT_WITHDRAW_R

**权重(IP):** 10

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
|coin|string|否|币种|
|page|number|否|页数，默认1|
|limit|number|否|条数|
|timestamp|string|是|时间戳|
|signature|string|是|签名|

**返回参数**

| 参数名 | 说明  |
| :------------ | :-------- |
|coin|币种|
|network|链名称|
|address|地址|
|addressTag|地址标签|
|memo|memo|
|totalRecords|总条数|
|totalPageNum|总页数|
|page|当前页|

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

**接口权限要求:** 资金划转写 / SPOT_TRANSFER_W

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
|fromAccountType|string|是|划出账户类型，现货/合约，枚举值："SPOT","FUTURES"|
|toAccountType|string|是|划入账户类型，现货/合约，枚举值："SPOT","FUTURES"|
|asset|string|是|资产|
|amount|string|是|数量|
|timestamp|string|是|时间戳|
|signature|string|是|签名|


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

**接口权限要求:** 资金划转读 / SPOT_TRANSFER_R

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
|fromAccountType|string|是|划出账户类型，现货/合约，枚举值："SPOT","FUTURES"|
|toAccountType|string|是|划入账户类型，现货/合约/，枚举值："SPOT","FUTURES"|
|startTime|string|否||
|endTime|string|否||
|page|string|否|默认1|
|size|string|否|默认 10, 最大 100|
|timestamp|string|是|时间戳|
|signature|string|是|签名|

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

## 查询用户万向划转历史（根据tranId）

> 请求示例

```
get /api/v3/capital/transfer/tranId?tranId=cb28c88cd20c42819e4d5148d5fb5742&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
    "tranId": "cb28c88cd20c42819e4d5148d5fb5742",
    "clientTranId": null,
    "asset": "USDT",
    "amount": "10",
    "fromAccountType": "SPOT",
    "toAccountType": "FUTURES",
    "symbol": null,
    "status": "SUCCESS",
    "timestamp": 1678603205000
}
```
**HTTP请求**

- **GET** ```/api/v3/capital/transfer/tranId```  

**接口权限要求:** 资金划转读 / SPOT_TRANSFER_R

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
|tranId|string|是|划转id|
|timestamp|string|是|时间戳|
|signature|string|是|签名|

仅支持查询最近半年（6个月）数据

**返回参数**

| 参数名 | 说明  |
| :------------ | :-------- | 
|tranId|划转ID|
|clientTranId|client ID|
|asset|币种|
|amount|划转数量|
|fromAccountType|转出业务账户|
|toAccountType|划入业务账户|
|symbol|转出交易对|
|status|划转状态|
|timestamp|划转时间|


## 获取小额资产可兑换列表

> 请求示例

```
get {{api_url}}/api/v3/capital/convert/list?timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
[
    {
           "convertMx": "0.000009",
           "convertUsdt": "0.000009",
           "balance": "0.000441",
           "asset": "USDT",
           "code": "30021",
           "message": "xxxxxxx"
 },
{
           "convertMx": "0.000009",
           "convertUsdt": "0.000009",
           "balance": "0.000441",
           "asset": "BTC",
           "code": "30021",
           "message": "xxxxxxx"
 }
]
```
**HTTP请求**

- **GET** ```/api/v3/capital/convert/list```  

**接口权限要求:** 账户读 / SPOT_ACCOUNT_R

**权重(IP):** 1

**请求参数**
  
| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
|timestamp|string|是|时间戳|
|signature|string|是|签名|

**返回参数**

| 参数名 | 说明  |
| :------------ | :-------- | 
| convertMx|余额mx值预估(扣除手续费后)|
| convertUsdt | 余额usdt估值      |
| balance|币种余额|
| asset|币种|
| code    | 无法兑换原因code     |
| message | 无法兑换原因message  |

## 小额资产兑换

> 请求示例

```
post {{api_url}}/api/v3/capital/convert?asset=BTC,FIL,ETH&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
  "successList":["ALGO","OMG"],
  "failedList":[],
  "totalConvert":"0.07085578",
  "convertFee":"0.00071571"
  }
```
**HTTP请求**

- **POST** ```/api/v3/capital/convert```  

**接口权限要求:** 账户写 / SPOT_ACCOUNT_W

**权重(IP):** 10

**请求参数**
  
| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
|asset|string|是|要兑换mx的小额资产(最多可以传15个)如:asset=BTC,FIL,ETH|
|timestamp|string|是|时间戳|
|signature|string|是|签名|

**返回参数**

| 参数名 | 说明  |
| :------------ | :-------- | 
|totalConvert|转换后的mx数量(扣除mx手续费)|
| convertFee  | 扣除mx手续费     |
| successList | 兑换成功币种列表 |
| failedList  | 兑换失败币种列表 |
| -asset     | 资产名称         |
| -message   | 兑换失败错误信息 |
| -code      | 兑换失败错误码   |

## 查询小额资产兑换历史

> 请求示例

```
get {{api_url}}/api/v3/capital/convert?timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
    "data": [
        {
            "totalConvert": "0.00885018",
            "totalFee": "0.000177",
            "convertTime": 1665360563000,
            "convertDetails": [
                {
                    "id": "3e52a99c5c3447b2af2163cd829dca28",
                    "convert": "0.00885018",
                    "fee": "0.000177",
                    "amount": "0.007130464601986065",
                    "time": 1665360563000,
                    "asset": "ETHF"
                }
            ]
        },
        {
            "totalConvert": "0.026782",
            "totalFee": "0.00053562",
            "convertTime": 1663631477000,
            "convertDetails": [
                {
                    "id": "6483bfb1766d41d8a4b6b6315ded6e99",
                    "convert": "0.02098255",
                    "fee": "0.00041965",
                    "amount": "0.00000098",
                    "time": 1663631477000,
                    "asset": "BTC"
                },
                {
                    "id": "f9e886f28c454f5dae45eec6a11f6c6a",
                    "convert": "0.00084019",
                    "fee": "0.0000168",
                    "amount": "2",
                    "time": 1663631477000,
                    "asset": "JAM"
                }
            ]
        }
    ],  
    "totalRecords": 4,
    "page": 1,
    "totalPageNum": 1
}
```
**HTTP请求**

- **GET** ```/api/v3/capital/convert```  

**接口权限要求:** 现货交易信息读 / SPOT_DEAL_R

**权重(IP):** 1

**请求参数**
  
| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
|startTime|long|否|开始时间|
|endTime|long|否|结束时间|
|page|int|否|页数,默认 1|
|limit|int|否|返回的条数,默认 1; 最大 1000|
|timestamp|string|是|时间戳|
|signature|string|是|签名|

**返回参数**

| 参数名 |  数据类型|说明  |
| :------------ | :-------- | :-------- |
|totalConvert|string|转换后的mx数量(扣除mx手续费)|
|totalFee|string|本次兑换的总手续费|
|convertTime|long|本次兑换时间|
|convertDetails|object|本次转换的细节|
|id|string|兑换id|
|convert|string|兑换后的mx|
|fee|string|兑换手续费|
|amount|string|币种数量|
|time|long|兑换时间|
|asset|string|币种|
|page|int|当前页|
|totalRecords|int|总记录数|
|totalPage|int|总页数|


## 用户站内转账接口

> 请求示例

```
post /api/v3/capital/transfer/internal?&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
  {
    "tranId": "c45d800a47ba4cbc876a5cd29388319"
  }

```
**HTTP请求**

- **POST** ```/api/v3/capital/transfer/internal```  

**接口权限要求:** 钱包提现相关写 / SPOT_WITHDRAW_W

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须 | 说明               | 
| :------ | :-------- |:-----|:-----------------|
|toAccountType|string| 是    | 收款账户类型，支持填入手机号/邮箱或者UID  |
|toAccount|string| 是    | 收款账户地址，支持填入手机号/邮箱或者UID   |
|areaCode|string| 否    | 如果toAccount为手机号，该字段为该手机号的必填区号            |
|asset|string| 是    | 资产            |
|amount|string| 是    | 数量           |
|timestamp|string| 是    | 时间戳              |
|signature|string| 是    | 签名               |

**返回参数**

| 参数名 | 说明  |
| :------------ | :-------- | 
|tranId|划转ID|


## 查询用户内部转账历史接口

> 请求示例

```
get /api/v3/capital/transfer/internal?&timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
  {
    "page": 1,  //当前页
    "totalRecords": 1,  //总记录数
    "totalPageNum": 1,  //总页数
    "data": [
             {
      "tranId":"11945860693",//划转ID
      "asset":"BTC",//币种
      "amount":"0.1",//划转数量
      "toAccountType":"EMAIL",//收款账户类型
      "toAccount":"156283619@outlook.com",//收款账户
      "fromAccount":"156283618@outlook.com",//付款账户
      "status":"SUCCESS",//划转状态
      "timestamp":1544433325000//划转时间
    },
    {
      "tranId":"",//划转ID
      "asset":"BTC",//币种
      "amount":"0.8",//划转数量
      "toAccountType":"UID",//收款账户类型
      "fromAccount":"156283619@outlook.com",//付款账户
      "toAccount":"87658765",//收款账户
      "status":"SUCCESS",//划转状态
      "timestamp":1544433325000//划转时间
    }
    ]
}

```
**HTTP请求**

- **GET** ```/api/v3/capital/transfer/internal```  

**接口权限要求:** 钱包提现相关读 / SPOT_WITHDRAW_R

**权重(IP):** 1

**请求参数**

|参数名	|数据类型	|是否必须	|说明|
| :------ | :-------- |:-----|:-----------------|
|startTime|	long|	否	|
|endTime|	long|	否	|
|page	|int|	否|	默认1|
|limit|	int	|否|	默认10|
|tranId|	string|	否	|划转id|
|timestamp|	string|	是|	时间戳|
|signature|	string|	是|	签名|

若startTime和endTime没传，则默认返回最近7天数据 

**返回参数**

| 参数名 | 说明  |
| :------------ | :-------- | 
|page	|当前页|
|totalRecords	|总记录数|
|totalPage	|总页数|
|tranId	|划转ID|
|asset	|币种|
|amount	|划转数量|
|fromAccountType	|转出业务账户|
|toAccountType	|划入业务账户|
|status	|划转状态|
|timestamp	|划转时间|

## 提币（旧接口，即将下线）

> 请求示例

```
post /api/v3/capital/withdraw/apply?coin=EOS&address=zzqqqqqqqqqq&amount=10&network=EOS&memo=MX10086&timestamp={{timestamp}}&signature={{signature}}
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

**接口权限要求:** 钱包提现相关写 / SPOT_WITHDRAW_W

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须 | 说明               | 
| :------ | :-------- |:-----|:-----------------|
|coin|string| 是    | 币种               |
|withdrawOrderId|string| 否    | 自定义提币ID   |
|network|string| 否    | 提币网络             |
|address|string| 是    | 提币地址             |
|memo|string| 否    | 如地址中需求memo，则此处必传 |
|amount|string| 是    | 数量               |
|remark|string| 否    | 备注               |
|timestamp|string| 是    | 时间戳              |
|signature|string| 是    | 签名               |
 

可以在接口 `Get /api/v3/capital/config/getall`的返回值中某币种的`networkList`获取`network`网络字段。


**返回参数**

| 参数名 | 说明  |
| :------------ | :-------- | 
|id|提币ID|


<!-- # ETF接口

## 获取ETF基础信息
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
  "basket": 24678.0916
}

```
**HTTP请求**

- **GET** ```api/v3/etf/info```  

**权重(IP):** 1

**请求参数**

| 参数   | 数据类型 | 是否必须 | 默认值 | 描述                    |
| :------ | :-------- | :-------- | :------ | :----------------------- |
| symbol | string   | 否       | NA     | ETF交易对，不填返回所有 |



**返回参数**

| 字段名称  | 数据类型 | 描述          |
| :--------- | :-------- | :------------- |
| symbol     | string   | ETF交易对 |
| netValue   | string   | 最新净值      |
| feeRate    | string   | 管理费率      |
| timestamp  | long     | 系统时间      |
|leverage    |string    | 目标杠杆      |
|realLeverage|string    | 当前杠杆      |
|mergedTimes |string    | 合并次数      |
|lastMergedTime|long   | 最近合并时间   |
|basket     |string    | 再平衡后篮子   |
 -->

# Websocket 行情推送

- 本篇所列出的所有wss接口的baseurl为: **[ws://wbs-api.mexc.com/ws](http://wbs-api.mexc.com/ws)**
- 每个到 **wbs.mexc.com** 的链接有效期不超过24小时，请妥善处理断线重连
- symbol名称中所有交易对均为**大写**，如：`spot@public.deals.v3.api.pb@<symbol>`</br>实例：`spot@public.deals.v3.api.pb@BTCUSDT`
- websocket没有有效订阅的话，服务器会在**30秒**时主动断开连接，如果订阅成功但是没有流量，服务器会在**一分钟**时主动断开，客户端可以发送ping来保持链接
- 1个 ws 连接最多30个订阅
- 请按照文档返回的参数进行处理数据，文档没有返回的参数近期将进行优化处理，请勿使用

## 实时订阅/取消数据流

- 以下数据可以通过websocket发送以实现订阅或取消订阅数据流。示例如下。
- 响应内容中的`id`是无符号整数，作为往来信息的唯一标识。
- 如果相应内容中的 `msg` 为相应的请求字段，表示请求发送成功。

## protocolbuffers接入方案

当前ws推送采用protobuf的形式，具体接入流程如下：

1.**PB文件定义**
   PB定义文件可以在此连接处获取
   
2.**生成反序列化代码**
   使用[https://github.com/protocolbuffers/protobuf](https://github.com/protocolbuffers/protobuf)工具编译.proto文件，生成反序列化代码

> **Java**

```
//在proto文件夹下执行
protoc *.proto --java_out=java文件输出路径
```

> **python**

```
//在proto文件夹下执行
protoc *.proto --python_out=python文件输出路径
```

> **其他**

```
 支持多种语言，包括 C++,C#, Go, Ruby, PHP, JS等。详见[https://github.com/protocolbuffers/protobuf](https://github.com/protocolbuffers/protobuf)。
```
3.**数据反序列化**
   使用上一步生成的代码，反序列化数据

> **Java**
 引入protobuf-java:

```
  <dependency>
 		<groupId>com.google.protobuf</groupId>
 		<artifactId>protobuf-java</artifactId>	
 		<version>S{protobuf.version}/version><!-- 根据项目实际情况指定版本 -->	
 	</dependency>


 解析示例:

 	// 组装对象
 	PushDataV3ApiWrapper pushDataV3ApiWrapper = PushDataV3ApiWrapper.newBuilder()
 			.setChannel("spot@public.increase.depth.v3.api.pb")
 			.setSymbol("BTCUSDTI)
 			.setSendTime(System.currentTimeMillis())
 			.build();
 	
 	// 序列化为byte数组
 	byte[] serializedData = pushDataV3ApiWrapper.toByteArray();
 	
 	// 反序列化为 PushDataV3ApiWrapper 对象
 	PushDataV3ApiWrapper resultV3 = PushDataV3ApiWrapper.parseFrom(serializedData);
```
> **python**

```
 解析示例:
 	

 	import PushDataV3ApiWrapper_pb2
 	
 	#组装对象
 	PushDataV3ApiWrapper = PushDataV3ApiWrapper_pb2.PushDataV3ApiWrapper()
 	PushDataV3ApiWrapper.channel = 'spot@public.increase.depth.v3.api.pb'
 	PushDataV3ApiWrapper.symbol ='BTCUSDT'
 	
 	#序列化为字符串
 	serializedData = PushDataV3ApiWrapper.SerializeToString()
 	
 	# 反序列化为 PushDataV3ApiWrapper 对象
 	result = PushDataV3ApiWrapper_pb2.PushDataV3ApiWrapper()
 	result.ParseFromString(serializedData)
 	print(result)
```


### 订阅一个信息流

> **订阅频道响应**

```
 {
  "id":0,
  "code":0,
  "msg":"spot@public.deals.v3.api.pb@BTCUSDT"
 }
```

- **请求**


{
 "method":"SUBSCRIPTION",
 "params":["spot@public.deals.v3.api.pb@BTCUSDT"]
}


### 取消订阅一个信息流

> **取消订阅响应**

```
 {
  "id":0,
  "code":0,
  "msg":"spot@public.increase.depth.v3.api.pb@BTCUSDT"
 }
```

- **请求**


{
 "method":"UNSUBSCRIPTION",
 "params":["spot@public.deals.v3.api.pb@BTCUSDT"]
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


## 逐笔交易

>**request:**

```
{
    "method": "SUBSCRIPTION",
    "params": [
        "spot@public.aggre.deals.v3.api.pb@100ms@BTCUSDT"
    ]
}
```

> **response:**

```
 {
  "channel": "spot@public.aggre.deals.v3.api.pb@100ms@BTCUSDT",
  "publicdeals": {
    "dealsList": [
      {
        "price": "93220.00", //成交价格price
        "quantity": "0.04438243", //成交数量quantity
        "tradetype": 2,//交易类型tradeType
        "time": 1736409765051 //成交时间dealTime
      }
    ],
    "eventtype": "spot@public.aggre.deals.v3.api.pb@100ms" //事件类型eventType 
  },
  "symbol": "BTCUSDT", //交易对symbol
  "sendtime": 1736409765052 //事件时间eventTime
}
```

**请求参数：**   `spot@public.aggre.deals.v3.api.pb@(100ms|10ms)@<symbol>`

逐笔交易推送每一笔成交的信息。**成交**，或者说交易的定义是仅有一个吃单者与一个挂单者相互交易

**返回参数:**

| 参数名    | 数据类型 | 说明               |
| :-------- | :------- | :----------------- |
| dealsList | array    | 成交信息           |
| price     | string   | 成交价格           |
| quantity  | string   | 成交数量           |
| tradetype | int      | 交易类型 1:买 2:卖 |
| time      | long     | 成交时间           |
| eventtype | string   | 事件类型           |
| symbol    | string   | 交易对             |
| sendtime  | long     | 事件时间           |

## K线 Streams

>**request:**

```
{
    "method": "SUBSCRIPTION",
    "params": [
        "spot@public.kline.v3.api.pb@BTCUSDT@Min15"
    ]
}
```

> **response:**

```
{
  "channel": "spot@public.kline.v3.api.pb@BTCUSDT@Min15",
  "publicspotkline": {
    "interval": "Min15", //K线间隔
    "windowstart": 1736410500, //这根K线的起始时间
    "openingprice": "92925", //这根K线期间第一笔成交价
    "closingprice": "93158.47", //这根K线期间末一笔成交价
    "highestprice": "93158.47", //这根K线期间最高成交价
    "lowestprice": "92800", //这根K线期间最低成交价
    "volume": "36.83803224", //这根K线期间成交量
    "amount": "3424811.05", //这根K线期间成交额
    "windowend": 1736411400 //这根K线的结束时间   
  },
  "symbol": "BTCUSDT",
  "symbolid": "2fb942154ef44a4ab2ef98c8afb6a4a7",
  "createtime": 1736410707571
}

```

K线逐秒推送所请求的K线种类(最新一根K线)的更新。

**请求参数：** `spot@public.kline.v3.api.pb@<symbol>@<interval>`

**返回参数:**

| 参数名          | 数据类型   | 说明                    |
| :-------------- | :--------- | :---------------------- |
| publicspotkline | object     | k线信息                 |
| interval        | interval   | K线间隔                 |
| windowstart     | long       | 这根K线的起始时间       |
| openingprice    | bigDecimal | 这根K线期间第一笔成交价 |
| closingprice    | bigDecimal | 这根K线期间末一笔成交价 |
| highestprice    | bigDecimal | 这根K线期间最高成交价   |
| lowestprice     | bigDecimal | 这根K线期间最低成交价   |
| volume          | bigDecimal | 这根K线期间成交量       |
| amount          | bigDecimal | 这根K线期间成交额       |
| windowend       | long       | 这根K线的结束时间       |
| symbol          | string     | 交易对                  |
| symbolid        | string     | 交易对id                |
| createtime      | long       | 事件时间                |

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

## 增量深度信息

>**request:**

```
{
    "method": "SUBSCRIPTION",
    "params": [
        "spot@public.aggre.depth.v3.api.pb@100ms@BTCUSDT"
    ]
}
```

> **response:**

```
{
  "channel": "spot@public.aggre.depth.v3.api.pb@100ms@BTCUSDT",
  "publicincreasedepths": {
    "asksList": [], //asks:卖单
    "bidsList": [ //bids:买单
      {
        "price": "92877.58", //变动的价格档位
        "quantity": "0.00000000" //数量
      }
    ],
    "eventtype": "spot@public.aggre.depth.v3.api.pb@100ms", //事件类型
    "version": "36913293511" //版本号
  },
  "symbol": "BTCUSDT", //交易对
  "sendtime": 1736411507002 //事件时间
}
```

如果某个价格对应的挂单量(quantity)为0，表示该价位的挂单已经撤单或者被吃，应该移除这个价位。

**请求参数:** `spot@public.aggre.depth.v3.api.pb@(100ms|10ms)@<symbol>`

**返回参数:**

| 参数名    | 数据类型 | 说明           |
| :-------- | :------- | :------------- |
| price     | string   | 变动的价格档位 |
| quantity  | string   | 数量           |
| eventtype | string   | 事件类型       |
| version   | string   | 版本号         |
| symbol    | string   | 交易对         |
| sendtime  | long     | 事件时间       |


## 增量深度信息(批量聚合)

>**request:**

```
{
    "method": "SUBSCRIPTION",
    "params": [
        "spot@public.increase.depth.batch.v3.api.pb@BTCUSDT"
    ]
}
```

> **response:**

```
{
  "channel" : "spot@public.increase.depth.batch.v3.api.pb@BTCUSDT",
  "symbol" : "BTCUSDT",
  "sendTime" : "1739502064578",
  "publicIncreaseDepthsBatch" : {
    "items" : [ {
      "asks" : [ ],
      "bids" : [ {
        "price" : "96578.48",
        "quantity" : "0.00000000"
      } ],
      "eventType" : "",
      "version" : "39003145507"
    }, {
      "asks" : [ ],
      "bids" : [ {
        "price" : "96578.90",
        "quantity" : "0.00000000"
      } ],
      "eventType" : "",
      "version" : "39003145508"
    }, {
      "asks" : [ ],
      "bids" : [ {
        "price" : "96579.31",
        "quantity" : "0.00000000"
      } ],
      "eventType" : "",
      "version" : "39003145509"
    }, {
      "asks" : [ ],
      "bids" : [ {
        "price" : "96579.84",
        "quantity" : "0.00000000"
      } ],
      "eventType" : "",
      "version" : "39003145510"
    }, {
      "asks" : [ ],
      "bids" : [ {
        "price" : "96576.69",
        "quantity" : "4.88725694"
      } ],
      "eventType" : "",
      "version" : "39003145511"
    } ],
    "eventType" : "spot@public.increase.depth.batch.v3.api.pb"
  }
}
```

批量聚合版本，条数超过5条或者时间超过5ms就推送一次，如果某个价格对应的挂单量(quantity)为0，表示该价位的挂单已经撤单或者被吃，应该移除这个价位。

**请求参数:** `spot@public.increase.depth.batch.v3.api.pb@<symbol>`

**返回参数:**

| 参数名    | 数据类型 | 说明           |
| :-------- | :------- | :------------- |
| price     | string   | 变动的价格档位 |
| quantity  | string   | 数量           |
| eventtype | string   | 事件类型       |
| version   | string   | 版本号         |
| symbol    | string   | 交易对         |
| sendtime  | long     | 事件时间       |

## 有限档位深度信息

推送有限档深度信息，levels表示几档买卖单信息, 可选 5/10/20档。

>**request:**

```
{
    "method": "SUBSCRIPTION",
    "params": [
                "spot@public.limit.depth.v3.api.pb@BTCUSDT@5"

   ]
}
```

> **response:**

```
{
  "channel": "spot@public.limit.depth.v3.api.pb@BTCUSDT@5",
  "publiclimitdepths": {
    "asksList": [ //asks:卖单
      {
        "price": "93180.18", //变动的价格档位
        "quantity": "0.21976424" //数量
      }
    ],
    "bidsList": [ //bids:买单
      {
        "price": "93179.98",
        "quantity": "2.82651000"
      }
    ],
    "eventtype": "spot@public.limit.depth.v3.api.pb", //事件类型
    "version": "36913565463" //版本号 
  },
  "symbol": "BTCUSDT", //交易对
  "sendtime": 1736411838730 //事件时间
}
```


**请求参数:** `spot@public.limit.depth.v3.api.pb@<symbol>@<level>`

**返回参数:**

| 参数名    | 数据类型 | 说明           |
| :-------- | :------- | :------------- |
| price     | string   | 变动的价格档位 |
| quantity  | string   | 数量           |
| eventtype | string   | 事件类型       |
| version   | string   | 版本号         |
| symbol    | string   | 交易对         |
| sendtime  | long     | 事件时间       |

## 按Symbol的最优挂单信息

推送指定交易对最优挂单信息。

>**request:**

```
{
    "method": "SUBSCRIPTION",
    "params": [
                "spot@public.aggre.bookTicker.v3.api.pb@100ms@BTCUSDT"
      ]
}
```

> **response:**

```
{
  "channel": "spot@public.aggre.bookTicker.v3.api.pb@100ms@BTCUSDT",
  "publicbookticker": {
    "bidprice": "93387.28",  // 买单最优挂单价格 
    "bidquantity": "3.73485", //买单最优挂单数量
    "askprice": "93387.29", //卖单最优挂单价格
    "askquantity": "7.669875" //卖单最优挂单数量
  },
  "symbol": "BTCUSDT", //交易对
  "sendtime": 1736412092433 //事件时间
}
```

**请求参数:** `spot@public.aggre.bookTicker.v3.api.pb@(100ms|10ms)@<symbol>`

**返回参数:**

| 参数名      | 数据类型 | 说明             |
| :---------- | :------- | :--------------- |
| bidprice    | string   | 买单最优挂单价格 |
| bidquantity | string   | 买单最优挂单数量 |
| askprice    | string   | 卖单最优挂单价格 |
| askquantity | string   | 卖单最优挂单数量 |
| symbol      | string   | 交易对           |
| sendtime    | long     | 事件时间         |

## 按Symbol的最优挂单信息（批量聚合）

批量聚合版本，推送指定交易对最优挂单信息。

>**request:**

```
{
    "method": "SUBSCRIPTION",
    "params": [
                "spot@public.bookTicker.batch.v3.api.pb@BTCUSDT"
      ]
}
```

> **response:**

```
{
  "channel" : "spot@public.bookTicker.batch.v3.api.pb@BTCUSDT",
  "symbol" : "BTCUSDT",
  "sendTime" : "1739503249114",
  "publicBookTickerBatch" : {
    "items" : [ {
      "bidPrice" : "96567.37",
      "bidQuantity" : "3.362925",
      "askPrice" : "96567.38",
      "askQuantity" : "1.545255"
    } ]
  }
}
```

**请求参数:** `spot@public.bookTicker.batch.v3.api.pb@<symbol>`

**返回参数:**

| 参数名      | 数据类型 | 说明             |
| :---------- | :------- | :--------------- |
| bidprice    | string   | 买单最优挂单价格 |
| bidquantity | string   | 买单最优挂单数量 |
| askprice    | string   | 卖单最优挂单价格 |
| askquantity | string   | 卖单最优挂单数量 |
| symbol      | string   | 交易对           |
| sendtime    | long     | 事件时间         |


## 如何正确在本地维护一个orderbook副本

1. 通过订阅spot@public.aggre.depth.v3.api.pb@(100ms|10ms)@<symbol>获取全量深度信息，保存当前version。
2. 订阅ws深度信息，收到更新后，如果收到的数据version > 当前version,同一个价位，后收到的更新覆盖前面的。
3. 访问Rest接口 **https://api.mexc.com/api/v3/depth?symbol=MXBTC&limit=1000** 获得一个1000档的深度快照
4. 将目前缓存的深度信息中同一价格，version<步骤3获取到的快照中的version的数据丢弃。
5. 将深度快照中的内容更新至本地缓存，并从ws接收到的event开始继续更新。
6. 每一个新event的version应该恰好等于上一个event的version+1，否则可能出现了丢包，如出现丢包或者获取到的event的version不连续,请从步骤3重新进行初始化。
7. 每一个event中的挂单量代表这个价格目前的挂单量**绝对值**，而不是相对变化。
8. 如果某个价格对应的挂单量为0，表示该价位的挂单已经撤单或者被吃，应该移除这个价位。

注意: 因为深度快照对价格档位数量有限制，初始快照之外的价格档位并且没有数量变化的价格档位不会出现在增量深度的更新信息内。因此，即使应用来自增量深度的所有更新，这些价格档位也不会在本地 order book 中可见，所以本地的 order book 与真实的 order book 可能会有一些差异。 不过对于大多数用例，5000 的深度限制足以有效地了解市场和交易。



# Websocket账户信息推送

- 本篇所列出API接口的base url : **https://api.mexc.com**
- 用于订阅账户数据的 `listenKey` 从创建时刻起有效期为60分钟
- 可以通过 `PUT` 一个 `listenKey` 延长60分钟有效期
- 可以通过`DELETE`一个 `listenKey` 立即关闭当前数据流，并使该`listenKey` 无效
- websocket接口的baseurl: **ws://wbs-api.mexc.com/ws**
- 订阅账户数据流的stream名称为 **/ws?listenKey=listenKey** <br/>  如：**ws://wbs-api.mexc.com/ws?listenKey=pqia91ma19a5s61cv6a81va65sd099v8a65a1a5s61cv6a81va65sdf19v8a65a1**
- 每个链接有效期不超过24小时，请妥善处理断线重连
- 每个UID，最多申请60个listen key（不包含已失效listen key）
- ws链接数的数量限制：每个listen key最多5个ws链接（即：每个uid最多申请的60个listen key，300个ws链接）

## Listen Key 

### 生成 Listen Key 

> **响应**

```
{
  "listenKey": "pqia91ma19a5s61cv6a81va65sdf19v8a65a1a5s61cv6a81va65sdf19v8a65a1"
}
```

**接口权限要求:** 账户读 / SPOT_ACCOUNT_R 

**HTTP请求**

- **POST**  ` /api/v3/userDataStream`

开始一个新的数据流。除非发送 keepalive，否则数据流于60分钟后关闭。

**参数:**

NONE

### 获取有效 Listen Key 

> **响应**

```
{
    "listenKey": [
        "c285bc363cfeac6646576b801a2ed1f9523310fcda9e927e509aaaaaaaaaaaaaa",
        "87cb8da0fb150e36c232c2c060bc3848693312008caf3acae73bbbbbbbbbbbb",
        "dc027517ebee2328b75268461a9df4d21addfac6ebebab8f5a6cccccccccccccc"
    ]
}
```

**接口权限要求:** 账户读 / SPOT_ACCOUNT_R 

**HTTP请求**

- **GET**  ` /api/v3/userDataStream`

获取当前所有有效的listenKey

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
| listenKey | string   | 是       |      |

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
| listenKey | string   | 是       |      |

## 现货账户信息 

在订阅成功后，每当账户余额发生变动或可用余额发生变动时，服务器将推送账户资产的更新。  

>**request:**

```
{
    "method": "SUBSCRIPTION",
    "params": [
    "spot@private.account.v3.api.pb"
    ]
}
```

> **response:**

```
{
	channel: "spot@private.account.v3.api.pb"
	createTime: 1736417034305
	sendTime: 1736417034307
	privateAccount {
  	vcoinName: "USDT"
  	coinId: "128f589271cb4951b03e71e6323eb7be"
  	balanceAmount: "21.94210356004384"
  	balanceAmountChange: "10"
  	frozenAmount: "0"
  	frozenAmountChange: "0"
  	type: "CONTRACT_TRANSFER"
  	time: 1736416910000
	}
}
```

**请求参数：** `spot@private.account.v3.api.pb`

**返回参数:**

| 参数名              | 数据类型 | 说明                                     |
| :------------------ | :------- | :--------------------------------------- |
| privateAccount      | json     | 账户信息                                 |
| vcoinName           | string   | 资产名称                                 |
| balanceAmount       | string   | 可用余额                                 |
| balanceAmountChange | string   | 可用变动金额                             |
| frozenAmount        | string   | 冻结余额                                 |
| frozenAmountChange  | string   | 冻结变动金额                             |
| type                | string   | <a href="#account_position">变动类型</a> |
| time                | long     | 结算时间                                 |

## 现货账户成交

>**request:**

```
{
    "method": "SUBSCRIPTION",
    "params": [
        "spot@private.deals.v3.api.pb"
    ]
}
```

> **response:**

```
{
	channel: "spot@private.deals.v3.api.pb"
	symbol: "MXUSDT"
	sendTime: 1736417034332
	privateDeals {
  	price: "3.6962"
		quantity: "1"
 		amount: "3.6962"
	  tradeType: 2
	  tradeId: "505979017439002624X1"
	  orderId: "C02__505979017439002624115"
	  feeAmount: "0.0003998377369698171"
 		feeCurrency: "MX"
	  time: 1736417034280
	}
}
```

**请求参数：** `spot@private.deals.v3.api.pb`

**返回参数:**

| 参数名        | 数据类型 | 说明                            |
| :------------ | :------- | :------------------------------ |
| symbol        | string   | 交易对                          |
| sendTime      | long     | 事件时间                        |
| privateDeals  | json     | 账户成交信息                    |
| price         | string   | 交易价格                        |
| quantity      | string   | 交易数量                        |
| amount        | string   | 交易金额                        |
| tradeType     | int      | 交易类型 1:买 2:卖              |
| tradeId       | string   | 成交id: tradeId                 |
| orderId       | string   | 订单id: orderId                 |
| clientOrderId | string   | 用户自定义订单id: clientOrderId |
| feeAmount     | string   | 手续费数量                      |
| feeCurrency   | string   | 手续费币种                      |
| time          | long     | 成交时间                        |

## 现货账户订单

>**request:**

```
{
  "method": "SUBSCRIPTION",
  "params": [
      "spot@private.orders.v3.api.pb"
  ]
}
```

**请求参数：** `spot@private.orders.v3.api.pb`

> **response:**

```
{
	channel: "spot@private.orders.v3.api.pb"
	symbol: "MXUSDT"
	sendTime: 1736417034281
	privateOrders {
	  id: "C02__505979017439002624115"
	  price: "3.5121"
	  quantity: "1"
	  amount: "0"
	  avgPrice: "3.6962"
	  orderType: 5
	  tradeType: 2
	  remainAmount: "0"
	  remainQuantity: "0"
	  lastDealQuantity: "1"
	  cumulativeQuantity: "1"
	  cumulativeAmount: "3.6962"
	  status: 2
	  createTime: 1736417034259
	}
}
```

**返回参数:**

| 参数名             | 数据类型   | 说明                                                         |
| :----------------- | :--------- | :----------------------------------------------------------- |
| symbol             | string     | 交易对                                                       |
| sendTime           | long       | 事件时间                                                     |
| privateOrders      | json       | 账户订单信息                                                 |
| id                 | string     | 订单id                                                       |
| price              | bigDecimal | 下单价格                                                     |
| quantity           | bigDecimal | 下单数量                                                     |
| amount             | bigDecimal | 下单总金额                                                   |
| avgPrice           | bigDecimal | 平均成交价                                                   |
| orderType          | int        | 订单类型LIMIT_ORDER(1),POST_ONLY(2),IMMEDIATE_OR_CANCEL(3),<br />FILL_OR_KILL(4),MARKET_ORDER(5); 止盈止损（100） |
| tradeType          | int        | 交易类型 1:买 2:卖                                           |
| remainAmount       | bigDecimal | 实际剩余金额: remainAmount                                   |
| remainQuantity     | bigDecimal | 实际剩余数量: remainQuantity                                 |
| cumulativeQuantity | bigDecimal | 累计成交数量                                                 |
| cumulativeAmount   | bigDecimal | 累计成交金额                                                 |
| status             | int        | 订单状态 1:未成交 2:已成交 3:部分成交 4:已撤单 5:部分撤单    |
| createTime         | long       | 订单创建时间                                                 |

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

**接口权限要求:** 账户读 / SPOT_ACCOUNT_R

**权重(IP):** 1

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
             "type": "spot",       // 返佣类型：现货，合约
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
             "type": "spot", // 返佣类型：现货，合约
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

**接口权限要求:** 账户读 / SPOT_ACCOUNT_R

**权重(IP):** 1

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
|type|string|返佣类型：现货，合约|
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
            "type": "spot",        // 返佣类型：现货，合约
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
            "type": "spot", // 返佣类型：现货，合约
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

**接口权限要求:** 账户读 / SPOT_ACCOUNT_R

**权重(IP):** 1

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
|type|string|返佣类型：现货，合约|
|rate|string|返佣比例|
|amount|string|返佣金额|
|uid|string|受邀人UID|
|account|string|受邀人账号|
|tradeTime|long|用户交易时间|
|updateTime|long|获取返佣时间|

若startTime和endTime均未发送,返回最近一年的数据。

## 获取邀请人

> 请求示例

```
get /api/v3/rebate/referCode?timestamp=1597026383085&signature=abc
```
> 返回示例

```json
{
    "referCode": "in3jd"
}
```
**HTTP请求**

- **GET** ```/api/v3/rebate/referCode```  

**接口权限要求:** 账户读 / SPOT_ACCOUNT_R

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
| recvWindow | long | 否       |        |
| timestamp  | long | 是       |        |
| signature  | string | 是     |        |


**返回参数**

| 参数名  |类型 | 说明|
| :------------ | :-------- | :--------|
|referCode|string|邀请人的邀请码，非用户本身的|

## 获取代理邀请返佣记录 （代理账户）

> 请求示例

```
get /api/v3/rebate/affiliate/commission?timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
    "success": true,
    "code": 0,
    "message": null,
    "data": {
        "pageSize": 10,
        "totalCount": 2,
        "totalPage": 1,
        "currentPage": 1,
        "usdtAmount": null,
        "totalCommissionUsdtAmount": null,
        "totalTradeUsdtAmount": null,
        "finished": null,
        "resultList": [
            {
                "uid": "27121050",
                "account": "",
                "inviteCode": "mexc-12345",
                "inviteTime": 1637145911,
                "spot": "0.00000000",
                "etf": "0.21131086",
                "futures": "0.74546367",
                "total": "0.95677453",
                "deposit": null,
                "firstDepositTime": null
            },
            {
                "uid": "52813530",
                "account": "",
                "inviteCode": "mexc-12345",
                "inviteTime": 1637145478,
                "spot": "1.25023599",
                "etf": "0.00000000",
                "futures": "0.00000000",
                "total": "1.25023599",
                "deposit": "26000.00000000",
                "firstDepositTime": "2021-11-19"
            }
        ]
    }
}
​
```
**HTTP请求**

- **GET** ```/api/v3/rebate/affiliate/commission```  

**接口权限要求:** 账户读 / SPOT_ACCOUNT_R

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
| startTime  | long    | 否       | 开始时间（佣金、入金数据时间） |
| endTime    | long    | 否       | 截止时间（佣金、入金数据时间） |
| inviteCode | string  | 否       | 邀请码  |
| page       | int     | 否       | 页数  |
| pageSize   | int     | 否       | 页面内容,不传默认10  |
| timestamp  | long    | 是       | 时间戳    |
| signature  | string  | 是       |  签名  |


**返回参数**

| 参数名  |类型 | 说明|
| :------------ | :-------- | :--------|
| uid |string|用户uid|
| account |string|邮箱账号(如果是手机号账号，返回null)|
| inviteCode |string|邀请码|
| inviteTime |long|注册时间|
| spot |string|现货返佣(usdt)|
| etf |string|ETF返佣(usdt) |
| futures |string|合约返佣(usdt) |
| total |string|返佣总额(usdt) |
| deposit |string|已入金金额(usdt)|
| firstDepositTime |string|首次入金日期(若没有，返回null)|

若startTime和endTime均未发送,返回最近半年的数据。

## 获取代理提现记录 （代理账户）

> 请求示例

```
get /api/v3/rebate/affiliate/withdraw?timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
    "success": true,
    "code": 0,
    "message": null,
    "data": {
        "pageSize": 10,
        "totalCount": 15,
        "totalPage": 2,
        "currentPage": 1,
        "resultList": [
            {
                "withdrawTime": 1682321417000,
                "asset": "USDT",
                "amount": "0.00001000"
            },
            {
                "withdrawTime": 1682321405000,
                "asset": "USDC",
                "amount": "0.00001000"
            }
        ]
    }
}

​
```
**HTTP请求**

- **GET** ```/api/v3/rebate/affiliate/withdraw```  

**接口权限要求:** 账户读 / SPOT_ACCOUNT_R

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
| startTime  | long    | 否       | 开始时间（佣金、入金数据时间） |
| endTime    | long    | 否       | 截止时间（佣金、入金数据时间） |
| page       | int     | 否       | 页数  |
| pageSize   | int     | 否       | 页面内容,不传默认10  |
| timestamp  | long    | 是       | 时间戳    |
| signature  | string  | 是       |  签名  |


**返回参数**

| 参数名  |类型 | 说明|
| :------------ | :-------- | :--------|
| withdrawalTime |long|提现时间|
| asset |string|提现币种|
| amount |string|提现金额|

若startTime和endTime均未发送,返回最近半年的数据。

## 获取代理返佣明细 （代理账户）

> 请求示例

```
get /api/v3/rebate/affiliate/commission/detail?timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
    "success": true,
    "code": 0,
    "message": null,
    "data": {
        "pageSize": 10,
        "totalCount": 5,
        "totalPage": 1,
        "currentPage": 1,
        "totalCommissionUsdtAmount": "0.0011",
        "totalTradeUsdtAmount": "281.8096",
        "resultList": [
            {
                "type": 2,
                "sourceType": 2,
                "state": 2,
                "date": 1689264000000,
                "uid": "17875073",
                "rate": 0.1,
                "symbol": "USDT",
                "takerAmount": "170.49326",
                "makerAmount": "0",
                "amountCurrency": "USDT",
                "usdtAmount": "170.49326",
                "commission": "0.00085246",
                "currency": "USDT"
            }
        ]
    }
}

​
```
**HTTP请求**

- **GET** ```/api/v3/rebate/affiliate/commission/detail```  

**接口权限要求:** 账户读 / SPOT_ACCOUNT_R

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
| startTime  | long    | 否       | 开始时间（佣金、入金数据时间） |
| endTime    | long    | 否       | 截止时间（佣金、入金数据时间） |
| inviteCode | string  | 否       | 邀请码  |
| page       | int     | 否       | 页数  |
| pageSize   | int     | 否       | 页面内容,不传默认10  |
| type       | int     | 否       | 返佣类型,1：现货、2：合约、3：ETF  |
| timestamp  | long    | 是       | 时间戳    |
| signature  | string  | 是       |  签名  |


**返回参数**

| 参数名  |类型 | 说明|
| :------------ | :-------- | :--------|
| totalCommissionUsdtAmount| string|总佣金|
| totalTradeUsdtAmount|string|总交易量|
| type|int| 返佣类型,1：现货、2：合约、3：ETF|
| sourceType|int|1：直客、2：子代理|
| state|int|返佣状态|
| date|long|交易日期|
| uid |string|用户uid|
| rate|string|返佣比例|
| symbol|string|交易对|
| takerAmount|string|taker金额|
| makerAmount|string|maker金额|
| amountCurrency|string|金额币种|
| usdtAmount|string|usdt金额|
| commission|string|返佣金额|
| currency|string|返佣币种|




若startTime和endTime均未发送,返回T-7~T的日期(近8天內日期)的数据,type不填则返回全部种类数据。

## 获取代理活动页面数据 （代理账户）

> 请求示例

```
get /api/v3/rebate/affiliate/campaign?timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
    "success": true,
    "code": 0,
    "message": null,
    "data": {
        "pageSize": 10,
        "totalCount": 15,
        "totalPage": 2,
        "currentPage": 1,
        "resultList": [
            {
                "campaign": "11kd",
                "inviteCode": "mexc-11Kd",
                "clickTime": 0,
                "createTime": 1695125287000,
                "signup": 0,
                "traded": 0,
                "deposited": 0,
                "depositAmount": "0",
                "tradingAmount": "0",
                "commission": "0"
            },
            {
                "campaign": "New10",
                "inviteCode": "mexc-newcode",
                "clickTime": 7,
                "createTime": 1693152531000,
                "signup": 0,
                "traded": 0,
                "deposited": 0,
                "depositAmount": "0",
                "tradingAmount": "0",
                "commission": "0"
            }
        ]
    }
}

​
```
**HTTP请求**

- **GET** ```/api/v3/rebate/affiliate/campaign```  

**接口权限要求:** 账户读 / SPOT_ACCOUNT_R

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
| startTime  | long    | 否       | 开始时间（佣金、入金数据时间） |
| endTime    | long    | 否       | 截止时间（佣金、入金数据时间） |
| page       | int     | 否       | 页数  |
| pageSize   | int     | 否       | 页面内容,不传默认10  |
| timestamp  | long    | 是       | 时间戳    |
| signature  | string  | 是       |  签名  |

**返回参数**

| 参数名  |类型 | 说明|
| :------------ | :-------- | :--------|
| campaign|string|活动名称|
| inviteCode|string|活动邀请码|
| createTime|long|活动创建时间|
| clickTime|int|邀请码点击次数|
| signup|int|注册人数|
| deposited|int|已入金人数|
| depositAmount|string|入金量，以usdt计算|
| tradingAmount|string|交易量，以usdt计算|
| traded|int|交易人数|
| commission|string|佣金|


startTime、endTime若不填写，则预设查询T-7~T日內数据。

## 查询直客页面数据（代理账户）

> 请求示例

```
get /api/v3/rebate/affiliate/referral?timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
    "success": true,
    "code": 0,
    "message": null,
    "data": {
        "pageSize": 10,
        "totalCount": 15,
        "totalPage": 2,
        "currentPage": 1,
        "resultList": [
            {
                "uid": "42469975",
                "nickName": null,
                "email": "",
                "registerTime": 1640275818000,
                "inviteCode": "mexc-12201950",
                "depositAmount": "0.00000000",
                "tradingAmount": "0.00000000",
                "commission": "0.00000000",
                "firstDepositTime": null,
                "firstTradeTime": null,
                "lastDepositTime": null,
                "lastTradeTime": null,
                "withdrawAmount": "0.00000000",
                "asset": "0 USDT",
                "identification": 1
          }
        ]
    }
}

​
```
**HTTP请求**

- **GET** ```/api/v3/rebate/affiliate/referral```  

**接口权限要求:** 账户读 / SPOT_ACCOUNT_R

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
| startTime  | long    | 否       | 开始时间（佣金、入金数据时间） |
| endTime    | long    | 否       | 截止时间（佣金、入金数据时间） |
| uid        |  string | 否       | 直客uid|
| inviteCode |  string | 否       | 邀请码|
| page       | int     | 否       | 页数  |
| pageSize   | int     | 否       | 页面内容,不传默认10  |
| timestamp  | long    | 是       | 时间戳    |
| signature  | string  | 是       |  签名  |


**返回参数**

| 参数名 | 类型 | 说明 |
| :------------ | :-------- | :--------|
| uid | int | uid |
| account | string | 邮箱账号|
| inviteCode | string | 邀请码 |
| inviteTime | long | 注册时间 |
| nickName | string | 用户昵称，如果无数据返回空白 |
| firstDeposit | long | 首次入金时间 |
| firstTrade | long | 首次交易时间 |
| lastDeposit | long | 最近一次入金时间 |
| lastTrade | long | 最近一次交易时间|
| depositAmount | string | 入金量，仅显示数值并统一换算USDT |
| tradingAmount | string | 交易量，仅显示数值并统一换算USDT |
| amount | string | 佣金，仅显示数值并统一换算USDT |
| asset | string | 固定选项9种： 0 USDT、1-1,000 USDT、1,000 - 10,000 USDT、 10,000 - 50,000 USDT、50,000 - 100,000 USDT、 100,000 - 500,000 USDT、500,000 - 1,000,000 USDT、 1,000,000 - 5,000,000 USDT、>5,000,000 USDT |
| withdrawalAmount | string | 提现金额，仅显示数值并统一换算USDT |
| identification | int | 1：未认证、2：初级、3：高级、4：机构 |

startTime、endTime若不填写，则预设查询T-7~T日內数据。

## 查询子代理页面数据（代理账户）

> 请求示例

```
get /api/v3/rebate/affiliate/subaffiliates?timestamp={{timestamp}}&signature={{signature}}
```
> 返回示例

```json
{
    "success": true,
    "code": 0,
    "message": null,
    "data": {
        "pageSize": 10,
        "totalCount": 15,
        "totalPage": 2,
        "currentPage": 1,
        "resultList": [
            {
                "subaffiliateName": "ada176@mailtemp.top ada176",
                "subaffiliateMail": "ad*****6@mailtemp.top",
                "campaign": "new1",
                "inviteCode": "mexc-12181621",
                "activationTime": 1639834136000,
                "registered": 0,
                "deposited": 0,
                "depositAmount": "0",
                "commission": "0"
            },
            {
                "subaffiliateName": "ada165@mailtemp.top ada165",
                "subaffiliateMail": "ad*****5@mailtemp.top",
                "campaign": null,
                "inviteCode": "1KMyk",
                "activationTime": 1639831541000,
                "registered": 0,
                "deposited": 1,
                "depositAmount": "21.15318",
                "commission": "0.5161221"
            }
        ]
    }
}

​
```
**HTTP请求**

- **GET** ```/api/v3/rebate/affiliate/subaffiliates```  

**接口权限要求:** 账户读 / SPOT_ACCOUNT_R

**权重(IP):** 1

**请求参数**

| 参数名 | 数据类型| 是否必须  | 说明 | 
| :------ | :-------- | :-------- | :---------- |
| startTime  | long    | 否       | 开始时间（佣金、入金数据时间） |
| endTime    | long    | 否       | 截止时间（佣金、入金数据时间） |
| inviteCode | string  | 否       | 邀请码 |
| page       | int     | 否       | 页数  |
| pageSize   | int     | 否       | 页面内容,不传默认10  |
| timestamp  | long    | 是       | 时间戳    |
| signature  | string  | 是       |  签名  |


**返回参数**

| 参数名  |类型 | 说明|
| :------------ | :-------- | :--------|
| subaffiliateName|string|子代理名称|
| subaffiliateMail|string|子代理邮箱|
| campaign|string|子代理注册时的活动|
| inviteCode|string|子代理注册时的邀请码|
| activationTime|long|子代理开通时间|
| registered|int|注册人数|
| deposited|int|已入金人数|
| depositAmount|string|入金量|
| commission|string|佣金|

startTime、endTime若不填写，则预设查询T-7~T日內数据。


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
- 1W  1周
- 1M  1月

### <a id="account_position">变动类型</a>

- WITHDRAW  提现
- WITHDRAW_FEE 提现手续费
- DEPOSIT 充值
- DEPOSIT_FEE 充值手续费
- ENTRUST 委托成交
- ENTRUST_PLACE 下单
- ENTRUST_CANCEL 撤单
- TRADE_FEE 手续费
- ENTRUST_UNFROZEN 订单冻结资金返还
- SUGAR 空投
- ETF_INDEX ETF下单



