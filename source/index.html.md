---
title: API 文档

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

includes:

search: true

meta:
  - name: description
    content: Documentation for the mexc global API
---

# 简介

欢迎使用MEXC API！本文档为您提供了REST API的相关信息，帮助您获取市场行情，管理账户信息，并进行交易等。

## 什么是API？

API是应用程序接口（Application Programming Interface），缩写为API，是一种结算接口，它定义多个应用程序之间的交互，以及可以进行的调用（call）或请求（request）的种类，如何进行调用或发出请求，应使用的数据格式，应遵循的惯例等。API文档中描述了应用程序如何与我们的交易所进行交互。

## 使用流程

步骤：开发者如需使用API，请先 <a href="https://www.mexc.com/user/openapi" target="_blank">创建APIKey</a> ，然后根据此文档详情进行开发交易，使用过程中如有问题或者建议请及时反馈。 

- 请参考 <a href="https://support.mxc-exchange.com/hc/zh-cn/articles/360056373151" target="_blank">这个页面</a> 来设置API Key。
- 设置API Key的同时，为了安全，建议设置IP访问白名单。
- 永远不要把你的API key/secret告诉给任何人。

## 接口类型 REST API

REST，即Representational State Transfer的缩写，是目前较为流行的基于HTTP的一种通信机制。它结构清晰、符合标准、易于理解、扩展方便，正得到越来越多网站的采用。其优点如下：

- 在RESTful架构中，每一个URL代表一种资源；
- 客户端和服务器之间，传递这种资源的某种表现层；
- 建议开发者使用Rest API进行币币交易或者资产提现等操作；
- 客户端通过四个HTTP指令，对服务器端资源进行操作，实现“表现层状态转化”；

## API V1或API V2

<aside class="notice">
API V1将于2021年6月底停用，不再维护，请提前做好准备。
</aside>

我们建议所有用户在API的V2上构建其应用程序。使用V2具有以下优点：

- 相对API V1，API V2签名的安全性和合理性更好。
- 提高了特定端点/通道的性能。
- 我们的官方客户库提供了更广泛的支持。

# 更新日志

| 时间       | 接口                                                                                      | 更新类型 | 说明                                                                                                                                |
| ---------- | ----------------------------------------------------------------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| 2020-01-09 | *                                                                                         | 新增     | REST API V2发布                                                                                                                     |
| 2020-02-24 | /open/api/v2/order/place<br/>/open/api/v2/order/place_batch<br/>/open/api/v2/order/cancel | 更新     | 添加client order id支持                                                                                                             |
| 2020-07-20 | /open/api/v2/order/cancel_by_symbol                                                       | 新增     | 按交易对撤单                                                                                                                        |
| 2021-03-01 | /open/api/v2/order/list                                                                   | 修改     | 入参states由非必填改为必填，且只能单状态查询；入参start_time修改为默认查询最近7天，最多查询30天；修复入参start_time时间不准确的情况 |
| 2021-08-27 | /open/api/v2/market/api_default_symbols                                                   | 新增     | 新增获取平台支持API交易的交易对接口；取消展示签名方式二，保留同合约的签名方式                                                       |

# 接入说明

## 接入URL

请选用以下的baseurl进行API请求：

- ```https://www.mexc.com```

## 请求格式

相应API接受GET，POST或DELETE类型的请求

- 对于GET/DELETE请求，所有参数都放在路径（request param）中
- 对于POST请求，所有参数都放在请求体（request body）中

## 返回格式

所有接口的返回数据均为JSON形式

## 签名规则

我们提供了公共接口（市场信息，交易行情数据），以及私有接口（账户信息，订单操作，资产操作等）<br/><br/>对于公共接口，不需要进行签名<br/><br/>而对于私有接口，需要对接口信息及相应参数进行签名操作，收到请求后服务端验证签名通过后才能进行相应的操作<br/><br/>请参考详细的[签名方法](#8e3023a1c8)

## 时间安全

所有签名接口均需要请求头中传入参数```Request-Time```，服务端接收到请求后会验证请求发出的时间范围。

若接受请求时，收到的```Request-Time```小于或大于服务端时间10秒（默认值）以上（该时间窗口值可以通过发送可选header参数 ```Recv-Window```来自定义，其最大值为60，不推荐使用30秒以上的```Recv-Window```），则认为该请求无效。

## 签名操作的组成

各接口与签名验证相关的数据

| 组成部分           | 说明                                                                           |
| ------------------ | ------------------------------------------------------------------------------ |
| ```ApiKey```       | API key中的access key                                                          |
| ```Request-Time``` | 发出请求的时间戳，以秒表示的13位时间戳字符串，如```1572537600000```            |
| ```Signature```    | 生成的签名字符串（使用HMAC SHA256算法对 apikey + timestamp + params 进行签名） |
| 接口HTTP请求方法   | 各接口对应的HTTP方法，```GET```，```POST```或```DELETE```                      |
| 接口URI            | 接口对应的URI字符串                                                            |
| 业务参数           | 各接口要求的业务参数，仅```GET```及```DELETE```方法需要将业务参数纳入签名计算  |

## 创建API key

用户可以在MEXC站点个人中心，创建API key，其包括两个部分，```Access key```API的访问秘钥，```Secret key```对应的秘钥，用于签名计算及验证。开始使用前，请为生成的API key设置相应的权限。

<aside class="warning">
Secret key仅在申请时展示，请做好记录留存
</aside>

## 签名方法 

> java示例

```java
/**
 * 获取get请求参数字符串
 *
 * @param param get/delete请求参数map
 * @return
 */
public static String getRequestParamString(Map<String, String> param) {
    if (MapUtils.isEmpty(param)) {
        return "";
    }
    StringBuilder sb = new StringBuilder(1024);
    SortedMap<String, String> map = new TreeMap<>(param);
    for (Map.Entry<String, String> entry : map.entrySet()) {
        String key = entry.getKey();
        String value = StringUtils.isBlank(entry.getValue()) ? "" : entry.getValue();
        sb.append(key).append('=').append(urlEncode(value)).append('&');
    }
    sb.deleteCharAt(sb.length() - 1);
    return sb.toString();
}

public static String urlEncode(String s) {
    try {
        return URLEncoder.encode(s, "UTF-8").replaceAll("\\+", "%20");
    } catch (UnsupportedEncodingException e) {
        throw new IllegalArgumentException("UTF-8 encoding not supported!");
    }
}

/**
 * 签名
 */
public static String sign(SignVo signVo) {
    if (signVo.getRequestParam() == null) {
        signVo.setRequestParam("");
    }
    String str = signVo.getAccessKey() + signVo.getReqTime() + signVo.getRequestParam();
    return actualSignature(str, signVo.getSecretKey());
}

public static String actualSignature(String inputStr, String key) {
    Mac hmacSha256;
    try {
        hmacSha256 = Mac.getInstance("HmacSHA256");
        SecretKeySpec secKey =
                new SecretKeySpec(key.getBytes(StandardCharsets.UTF_8), "HmacSHA256");
        hmacSha256.init(secKey);
    } catch (NoSuchAlgorithmException e) {
        throw new RuntimeException("No such algorithm: " + e.getMessage());
    } catch (InvalidKeyException e) {
        throw new RuntimeException("Invalid key: " + e.getMessage());
    }
    byte[] hash = hmacSha256.doFinal(inputStr.getBytes(StandardCharsets.UTF_8));
    return Hex.encodeHexString(hash);
}

@Getter
@Setter
public static class SignVo {
    private String reqTime;
    private String accessKey;
    private String secretKey;
    private String requestParam; //get请求参数根据字典顺序排序,使用&拼接字符串,post为json字符串
}
```

1. 对于公共接口,不需要签名。

2. 对于私有接口,需要在header中传入ApiKey、Request-Time（以13位毫秒表示的时间戳字符串）、Signature、Content-Type 必须指定为application/json、Recv-Window(可选)参数,Signature为签名字符串

* 签名规则如下:
    1. 签名时需要先获得请求参数字符串，无参时为""：<br />对于GET/DELETE请求，按 **字典序** 拼接业务参数以&间隔，并最终获得签名目标串（在批量操作的API中，若参数值中有逗号等特殊符号，这些符号在签名时需要做URL encode）。<br />对于POST请求，签名参数为json字符串（无需进行字典排序）。
    2. 获得参数字符串后，再拼接签名目标串，规则为：accessKey+时间戳+获取到的参数字符串
    3. 使用HMAC SHA256算法对目标串用SecretKey进行签名，并最终将签名作为参数携带到header中

注意：

  1)参与签名的业务参数为null时，不参与签名；注意get请求将参数拼接至url上时，如果参数为null， 后台解析时，会解析成""，POST请求，参数为null时，不要传该参数，或者签名时，将该参数的值设置为""，否则会出现验签失败。

  2)请求时将签名时用到的Request-Time的值放入header的Request-Time参数中，获得的签名字符串放入header的Signature参数中，将APIKEY的Access Key放在header的ApiKey参数中，其余业务参数按正常传递即可。

  3)获得的签名字符串不需要进行base64进行编码。


## 错误码

以下为接口可能返回的错误码信息

| 错误码 | 说明                            |
| ------ | ------------------------------- |
| 400    | 请求参数无效                    |
| 401    | 签名验证失败                    |
| 429    | 请求过于频繁                    |
| 10072  | 无效的access key                |
| 10073  | 无效的请求时间                  |
| 30000  | 当前交易对已暂停交易            |
| 30001  | 当前交易方向不允许下单          |
| 30002  | 小于最小交易金额                |
| 30003  | 大于最大交易金额                |
| 30004  | 持仓不足                        |
| 30005  | 卖出超额                        |
| 30010  | 下单价格超过范围                |
| 30016  | 暂停交易                        |
| 30019  | 订单集合超出最大允许长度        |
| 30020  | 受限制的交易对，暂不支持API访问 |
| 30021  | 无效的交易对                    |

## 限频规则

对REST API的访问有频率限制，当超出限制时，返回状态429：请求过于频繁

需要携带access key进行访问的接口，以账号作为限速的基本单位；不需要携带access key进行访问的接口，以IP作为限速的基本单位

未说明限速规则的接口默认为20次/秒

## 枚举定义

### 订单状态

|                    |          |
| ------------------ | -------- |
| NEW                | 未成交   |
| FILLED             | 已成交   |
| PARTIALLY_FILLED   | 部分成交 |
| CANCELED           | 已撤单   |
| PARTIALLY_CANCELED | 部分撤单 |


### 订单类型

|                     |            |
| ------------------- | ---------- |
| LIMIT_ORDER         | 限价订单   |
| POST_ONLY           | 限价做市单 |
| IMMEDIATE_OR_CANCEL | 下单即撤销 |


### 交易类型

|     |      |
| --- | ---- |
| BID | 买单 |
| ASK | 卖单 |

### 充值状态

|         |        |
| ------- | ------ |
| PENDING | 入账中 |
| SUCCESS | 已完成 |

### 时间间隔

m -> 分钟; h -> 小时; d -> 天; M -> 月

- 1m
- 5m
- 15m
- 30m
- 60m
- 4h
- 1M

# 基本信息

## 所有交易对信息

> 响应示例

```json
{
  "code": 200,
  "data": [
    {
      "symbol": "QTUM_USDT",
      "state": "ENABLED",
      "price_scale": 4,
      "quantity_scale": 2,
      "min_amount": "5",
      "max_amount": "5000000",
      "maker_fee_rate": "0.002",
      "taker_fee_rate": "0.002",
      "limited": false,
      "etf_mark": 0,
      "symbol_partition": "MAIN"
    }
  ]
}
```

- **GET** ```/open/api/v2/market/symbols```

参数：None

响应：

| 字段名         | 数据类型 | 是否必须                         |
| -------------- | -------- | -------------------------------- |
| symbol         | string   | 交易对名称                       |
| state          | string   | 交易对状态，当前是否可以进行交易 |
| price_scale    | integer  | 价格精度                         |
| quantity_scale | integer  | 数量精度                         | ## 各接口限速信息 |

> 响应示例

```json
{
    "code": 200,
    "data": {
        "total_limit": "100",
        "request_limit": {
            "/api/v2/market/symbols": "5",
            "/api/v2/market/depth": "5"
        }
    }
}
```

- **GET** ```/open/api/v2/common/rate_limit```

参数：None

响应

| 字段名           | 数据类型 | 说明                                     |
| ---------------- | -------- | ---------------------------------------- |
| total_limit      | string   | 用户每秒最大请求阈值                     |
| request_limit    | map      | 用户每秒每个API最大请求阈值              |
| min_amount       | string   | 最小交易金额                             |
| max_amount       | string   | 最大交易金额                             |
| maker_fee_rate   | string   | Maker费率                                |
| taker_fee_rate   | string   | Taker费率                                |
| limited          | string   | API交易使能标记（有效值：true, false）   |
| etf_mark         | integer  | Etf标识，0代表不是ETF，正负整数代表是ETF |
| symbol-partition | string   | 交易区，如主板区                         |





## 当前系统时间

> 响应示例

```json
{
    "code": 200,
    "data": 1573542414480
}
```

- **GET** ```/open/api/v2/common/timestamp```

参数：None

响应

| 字段名 | 数据类型 | 说明                                   |
| ------ | -------- | -------------------------------------- |
| data   | long     | 系统当前时间戳，Unix epoch以来的毫秒数 |

## Ping

> 响应示例

```json
{
    "code": 200
}
```

- **GET** ```/open/api/v2/common/ping```

参数：None

响应

| 字段名 | 数据类型 | 说明                 |
| ------ | -------- | -------------------- |
| code   | int      | 有返回则服务器状态OK |

## 获取平台支持接口交易的交易对

> 响应示例

```json
{
  "code": 200,
  "data": [
    {
      "ALEPH_USDT",
      "XFI_USDT",
      "ETH3S_USDT",
      "OGN_USDT",
      "HC_USDT",
      "PAX_USDT",
      "BNU_USDT",
    }
  ]
}
```

获取平台支持API交易的交易对。

- **GET** ```/open/api/v2/market/api_default_symbols```

<aside>
限速规则: 20次/2秒
</aside>

**请求参数:**

None

**响应参数:**

| 参数名  | 类型    | 说明             |
| ------- | ------- | ---------------- |
| code    | integer | 状态码           |
| message | string  | 错误描述（如有） |
| <data>  | array   |                  |
| symbol  | string  | 交易对           |
| </data> |         |                  |

# 行情数据

## Ticker行情

> 响应示例

```json
{
    "code": 200,
    "data": [
        {
             "symbol": "ETH_USDT",
             "volume": "0",
             "high": "182.4117576",
             "low": "182.4117576",
             "bid": "182.0017985",
             "ask": "183.1983186",
             "open": "182.4117576",
             "last": "182.4117576",
             "time": 1574668200000,
             "change_rate": "0.00027307"
        }
    ]
}
```

- **GET** ```/open/api/v2/market/ticker```

参数：

| 参数名 | 数据类型 | 是否必须 | 说明       |
| ------ | -------- | -------- | ---------- |
| symbol | string   | 是       | 交易对名称 |

响应：

| 参数名      | 数据类型 | 说明                    |
| ----------- | -------- | ----------------------- |
| symbol      | string   | 交易对                  |
| volume      | string   | 本阶段交易量            |
| high        | string   | 本阶段最高价            |
| low         | string   | 本阶段最低价            |
| bid         | string   | 当前最高买价            |
| ask         | string   | 当前最低卖价            |
| open        | string   | 本阶段开盘价            |
| last        | string   | 本阶段最新成交价        |
| time        | string   | 最新报价时间            |
| change_rate | string   | 本阶段涨跌幅## 深度信息 |

> 响应示例

```json
{
    "code": 200,
    "data": {
        "asks": [
            {
                "price": "183.1683154",
                "quantity": "128.5"
            },
            {
                "price": "183.1983186",
                "quantity": "101.6"
            }
        ],
        "bids": [
            {
                "price": "182.4417544",
                "quantity": "115.5"
            },
            {
                "price": "182.4217568",
                "quantity": "135.7"
            }
        ]
    }
}
```

- **GET** ```/open/api/v2/market/depth ```

参数：

| 参数名 | 数据类型 | 是否必须 | 说明         | 取值范围 |
| ------ | -------- | -------- | ------------ | -------- |
| symbol | string   | 是       | 交易对名称   |          |
| depth  | string   | 是       | 返回的深度数 | 1~2000   |

响应：

| 参数名 | 数据类型 | 说明                                       |
| ------ | -------- | ------------------------------------------ |
| bids   | object   | 买单，包含字段[price, quantity] 价格及数量 |
| asks   | object   | 卖单，包含字段[price, quantity] 价格及数量 |  |

<aside class="notice">
阶段是以当前时间的滚动24小时计。
</aside>
## 深度信息

> 响应示例

```json
{
    "code": 200,
    "data": {
        "asks": [
            {
                "price": "183.1683154",
                "quantity": "128.5"
            },
            {
                "price": "183.1983186",
                "quantity": "101.6"
            }
        ],
        "bids": [
            {
                "price": "182.4417544",
                "quantity": "115.5"
            },
            {
                "price": "182.4217568",
                "quantity": "135.7"
            }
        ]
    }
}
```

- **GET** ```/open/api/v2/market/depth ```

参数：

| 参数名 | 数据类型 | 是否必须 | 说明 | 取值范围 |
|-----|-----|-----|-----|-----|
|symbol|string|是|交易对名称| |
|depth|string|是|返回的深度数| 1~2000|

响应：

| 参数名 | 数据类型 | 说明 |
|-----|-----|-----|
|bids|object|买单，包含字段[price, quantity] 价格及数量|
|asks|object|卖单，包含字段[price, quantity] 价格及数量|

## 成交记录

> 响应示例

```json
{
    "code": 200,
    "data": [
        {
            "trade_time": 1573267931530,
            "trade_price": "183.1683154",
            "trade_quantity": "5",
            "trade_type": "BID"
        },
        {
            "trade_time": 1573266717841,
            "trade_price": "183.1683154",
            "trade_quantity": "0.5",
            "trade_type": "ASK"
        },
        {
            "trade_time": 1573013871967,
            "trade_price": "183.1183105",
            "trade_quantity": "128.6",
            "trade_type": "BID"
        }
    ]
}
```

- **GET** ```/open/api/v2/market/deals```

参数：

| 参数名 | 数据类型 | 是否必须 | 说明       | 取值范围          |
| ------ | -------- | -------- | ---------- | ----------------- |
| symbol | string   | 是       | 交易对名称 |                   |
| limit  | integer  | 否       | 返回的条数 | 1~1000，默认值100 |

响应：

| 参数名         | 数据类型 | 说明               |
| -------------- | -------- | ------------------ |
| trade_time     | long     | 成交时间           |
| trade_price    | string   | 成交价格           |
| trade_quantity | string   | 成交数量           |
| trade_type     | string   | 交易方向，BID或ASK |

## K线数据

> 响应示例

```json
{
    "code": 200,
    "data": [
        [
            1557728040,    //timestamp in seconds
            "7054.7",      //open
            "7056.26",     //close
            "7056.29",     //high
            "7054.16",     //low
            "9.817734",    //vol
            "6926.521"     //amount
        ],
        [
            1557728100,
            "7056.26",
            "7042.17",
            "7056.98",
            "7042.16",
            "23.69423",
            "1677.931"
        ]
    ]
}
```

- **GET** ```/open/api/v2/market/kline```

参数：

| 参数名     | 数据类型 | 是否必须 | 说明                         | 取值范围                                                  |
| ---------- | -------- | -------- | ---------------------------- | --------------------------------------------------------- |
| symbol     | string   | 是       | 交易对名称                   |                                                           |
| interval   | string   | 是       | 时间间隔                     | 分钟制:1m，5m，15m，30m，60m。小时制:4h，天制:1d，月制:1M |
| start_time | long     | 否       | 起始时间。以秒记的10位时间戳 |                                                           |
| limit      | integer  | 否       | 返回条数                     | 1~1000，默认值100                                         |

响应：

| 参数名 | 说明                            |
| ------ | ------------------------------- |
| time   | 开始时间 (以秒表示的10位时间戳) |
| open   | 开盘价                          |
| close  | 收盘价                          |
| high   | 最高价                          |
| low    | 最低价                          |
| vol    | 成交量                          |
| amount | 计价货币成交量                  |

## 获取币种信息

> 响应示例

```json
{
    "code": 200,
    "data": [
        {
            "currency": "AGLD",
            "coins": [
                {
                    "chain": "ERC20",
                    "precision": 18,
                    "fee": 15.37,
                    "is_withdraw_enabled": true,
                    "is_deposit_enabled": true,
                    "deposit_min_confirm": 16,
                    "withdraw_limit_max": 500000.0,
                    "withdraw_limit_min": 14.0
                }
            ],
            "full_name": "Adventure Gold"
        }
    ]
}
```

此接口，返回币种详情列表。

- **GET** ```/open/api/v2/market/coin/list```

<aside>
限速规则: 20次/2秒
</aside>

**需要权限:** 提币读

**请求参数:**

| 参数名   | 类型   | 是否必填 | 说明 |
| -------- | ------ | -------- | ---- |
| currency | string | false    | 币种 |

**响应参数:**

| 参数名              | 类型   | 说明               |
| ------------------- | ------ | ------------------ |
| code                | int    | 状态码             |
| message             | string | 错误描述（如有）   |
| currency            | string | 币种               |
| full_name           | string | 币种全称           |
| chain               | string | 链名称             |
| precision           | string | 币种精度           |
| is_withdraw_enabled | string | 是否可提现         |
| is_deposit_enabled  | string | 是否可充值         |
| deposit_minconfirm  | number | 充值区块最小确认数 |
| withdraw_limit_max  | number | 单次最大提币数量   |
| withdraw_limit_min  | number | 单次最小提币数量   |
| fee                 | string | 提币手续费数量     |

注意：
隐藏币种及下架币种不显示；

# 账户信息

## 账户余额

> 响应示例

```json
{
    "code": 200,
    "data": {
        "BTC": {
            "frozen": "0",
            "available": "140"
        },
        "ETH": {
            "frozen": "8471.296525048",
            "available": "483280.9653659222035"
        },
        "USDT": {
            "frozen": "0",
            "available": "27.3629"
        },
        "MX": {
            "frozen": "30.9863",
            "available": "450.0137"
        }
    }
}
```

**GET** ```/open/api/v2/account/info```

参数：None

响应：

币种对应的冻结余额和可用余额

| 参数名    | 数据类型 | 说明     |
| --------- | -------- | -------- |
| frozen    | string   | 冻结余额 |
| available | string   | 可用余额 |



## 获取账户可接口交易的交易对

> 响应示例

```json
{
  "code": 200,
  "data": [
    {
      "ALEPH_USDT",
      "XFI_USDT",
      "ETH3S_USDT",
      "OGN_USDT",
      "HC_USDT",
      "PAX_USDT",
      "BNU_USDT",
    }
  ]
}
```

获取账户可API交易的交易对，私有接口。

- **GET** ```/open/api/v2/market/api_symbols```

<aside>
限速规则: 20次/2秒
</aside>

**请求参数:**

None

**响应参数:**

| 参数名  | 类型    | 说明             |
| ------- | ------- | ---------------- |
| code    | integer | 状态码           |
| message | string  | 错误描述（如有） |
| <data>  | array   |                  |
| symbol  | string  | 交易对           |
| </data> |         |                  |



# 现货交易

## 下单


> 请求示例

```json
{
    "order_type": "LIMIT_ORDER",
    "price": "0.00846945",
    "quantity": "1",
    "symbol": "RACA_USDT",
    "trade_type": "ASK"
}
```

> 响应示例

```json
{
    "code": 200,
    "data": "c8663a12a2fc457fbfdd55307b463495"
}
```

- **POST** ```/open/api/v2/order/place```

参数：

| 参数名          | 数据类型 | 是否必须 | 说明       | 取值范围                                    |
| --------------- | -------- | -------- | ---------- | ------------------------------------------- |
| symbol          | string   | 是       | 交易对名称 |                                             |
| price           | string   | 是       | 交易价格   |                                             |
| quantity        | string   | 是       | 交易量     |                                             |
| trade_type      | string   | 是       | 交易类型   | BID，ASK                                    |
| order_type      | string   | 是       | 订单类型   | LIMIT_ORDER，POST_ONLY，IMMEDIATE_OR_CANCEL |
| client_order_id | string   | 否       | 客户订单id | 最大长度32位字符                            |

<aside class="notice">
用户需要维护client order id的唯一性
</aside>

响应：

| 参数名 | 数据类型 | 说明   |
| ------ | -------- | ------ |
| data   | string   | 订单id |


## 撤销订单

> 响应示例

```json
{
    "code": 200,
    "data": {
        "504feca6ba6349e39c82262caf0be3f4": "success"
    }
}
```

- **DELETE** ```/open/api/v2/order/cancel```

参数：

| 参数名           | 数据类型 | 是否必须 | 说明                                                               |
| ---------------- | -------- | -------- | ------------------------------------------------------------------ |
| order_ids        | string   | 否       | 订单号，支持批量撤单，各订单号以逗号分隔。最大批量操作数目为20     |
| client_order_ids | string   | 否       | 客户订单id，支持批量撤单，各订单号以逗号分隔。最大批量操作数目为20 |


响应：

| 参数名 | 数据类型 | 说明                 |
| ------ | -------- | -------------------- |
| data   | map      | 订单号及对应操作结果 |

<aside class="notice">
请求参数为order_ids与client_order_ids二选一，两者都提供时，将忽略client_order_ids
</aside>

<aside class="notice">
请求返回表示服务端接收到了对应订单的撤单请求，并不表示已经撤单完成
</aside>

## 批量下单

> 请求示例

```json
[
    {
        "order_type": "LIMIT_ORDER",
        "price": "40000",
        "quantity": "0.0002",
        "symbol": "BTC_USDT",
        "trade_type": "BID",
        "client_order_id":  9588234
    },
    {
        "order_type": "LIMIT_ORDER",
        "price": "0.00846945",
        "quantity": "1",
        "symbol": "RACA_USDT",
        "trade_type": "ASK"
    }
]
```


> 响应示例

> 在有client_order_id输入的情况下响应为

```json
{
    "code": 200,
    "data": {
        "1572936": "c8663a12a2fc457fbfdd55307b463495",
        "1572937": "ec42569b4f4349f7aabe26f78b0f8bd2",
        "1572938": "70669675cac2414c90493be2dcfaf7e3"
    }
}
```

> 没有client_order_id输入则返回

```json
{
    "code": 200,
    "data": [
        "e3e1ee06916c462eb8cd0349ff9ab242",
        "4d1f8c13f4cc40bcbfbac4da2a26d3a5"
    ]
}

```

- **POST** ```/open/api/v2/order/place_batch```

参数：

| 参数名          | 数据类型 | 是否必须 | 说明       | 取值范围                                    |
| --------------- | -------- | -------- | ---------- | ------------------------------------------- |
| symbol          | string   | 是       | 交易对名称 |                                             |
| price           | string   | 是       | 交易价格   |                                             |
| quantity        | string   | 是       | 交易量     |                                             |
| trade_type      | string   | 是       | 交易类型   | BID，ASK                                    |
| order_type      | string   | 是       | 订单类型   | LIMIT_ORDER，POST_ONLY，IMMEDIATE_OR_CANCEL |
| client_order_id | string   | 否       | 客户订单id | 最大长度32位字符                            |

响应：

| 参数名 | 数据类型 | 说明                                              |
| ------ | -------- | ------------------------------------------------- |
| data   | map      | 客户订单id(client_order_id)及对应订单号(order_id) |

<aside class="notice">
用户需要维护client order id的唯一性
</aside>

<aside class="notice">
对于同一次批量下单的操作，参数中的订单元素需要统一客户订单id行为，不能有些元素带有客户订单id另一些元素不带
</aside>

## 当前挂单

> 响应示例

```json
{
    "code": 200,
    "data": [
        {
            "id": "e5bb6963250146edb2f8677fcfcc97aa",
            "symbol": "MX_ETH",
            "price": "0.000907",
            "quantity": "300000",
            "state": "NEW",
            "type": "BID",
            "remain_quantity": "300000",
            "remain_amount": "272.1",
            "create_time": 1574338341797
        }
    ]
}
```

- **GET** ```/open/api/v2/order/open_orders```

参数：

| 参数名     | 数据类型 | 是否必须 | 说明       | 取值范围         |
| ---------- | -------- | -------- | ---------- | ---------------- |
| symbol     | string   | 是       | 交易对名称 |                  |
| start_time | string   | 否       | 起始时间   |                  |
| limit      | string   | 否       | 返回条数   | 1~1000，默认值50 |
| trade_type | string   | 否       | 交易类型   | BID，ASK         |


响应：

| 参数名          | 数据类型 | 说明       |
| --------------- | -------- | ---------- |
| symbol          | string   | 交易对名称 |
| id              | string   | 订单id     |
| price           | string   | 挂单价格   |
| quantity        | string   | 挂单数量   |
| remain_quantity | string   | 剩余数量   |
| remain_amount   | string   | 剩余金额   |
| create_time     | string   | 下单时间   |
| state           | string   | 订单状态   |
| type            | string   | 订单类型   |
| client_order_id | string   | 客户订单id |


## 所有订单

> 响应示例

```json
{
    "code": 200,
    "data": [
        {
            "id": "70669675cac2414c90493be2dcfaf7e3",
            "symbol": "MX_ETH",
            "price": "0.000901",
            "quantity": "300000",
            "state": "NEW",
            "type": "BID",
            "deal_quantity": "0",
            "deal_amount": "0",
            "create_time": 1573217964000
        },
        {
            "id": "ec42569b4f4349f7aabe26f78b0f8bd2",
            "symbol": "MX_ETH",
            "price": "0.000907",
            "quantity": "300000",
            "state": "NEW",
            "type": "ASK",
            "deal_quantity": "0",
            "deal_amount": "0",
            "create_time": 1573217963000
        }
    ]
}
```

- **GET** ```/open/api/v2/order/list```

参数：

| 参数名     | 数据类型 | 是否必须 | 说明         | 取值范围                                                                                                |
| ---------- | -------- | -------- | ------------ | ------------------------------------------------------------------------------------------------------- |
| symbol     | string   | 是       | 交易对名称   |                                                                                                         |
| start_time | string   | 否       | 起始时间     | 默认查询最近7天，最多查询30天                                                                           |
| limit      | string   | 否       | 返回条数     | 1~1000，默认值50                                                                                        |
| trade_type | string   | 是       | 交易类型     | BID，ASK                                                                                                |
| states     | string   | 是       | 查询订单状态 | NEW：未成交；FILLED：已成交；PARTIALLY_FILLED：部分成交；CANCELED：已撤单；PARTIALLY_CANCELED：部分撤单 |


响应：

| 参数名          | 数据类型 | 说明       |
| --------------- | -------- | ---------- |
| symbol          | string   | 交易对名称 |
| id              | string   | 订单id     |
| price           | string   | 挂单价格   |
| quantity        | string   | 挂单数量   |
| deal_quantity   | string   | 成交数量   |
| deal_amount     | string   | 成交金额   |
| create_time     | string   | 下单时间   |
| state           | string   | 订单状态   |
| type            | string   | 订单类型   |
| client_order_id | string   | 客户订单id |

## 查询订单

> 响应示例

```json
{
    "code": 200,
    "data": [
        {
            "id": "504feca6ba6349e39c82262caf0be3f4",
            "symbol": "MX_ETH",
            "price": "0.000901",
            "quantity": "300000",
            "state": "NEW",
            "type": "BID",
            "deal_quantity": "0",
            "deal_amount": "0",
            "create_time": 1573117266000
        },
        {
            "id": "72872b6ae721480ca4fe0f265d29dfee",
            "symbol": "MX_ETH",
            "price": "0.000907",
            "quantity": "300000",
            "state": "NEW",
            "type": "ASK",
            "deal_quantity": "0",
            "deal_amount": "0",
            "create_time": 1573117267000
        }
    ]
}
```

- **GET** ```/open/api/v2/order/query```

参数：

| 参数名    | 数据类型 | 是否必须 | 说明                                       | 取值范围 |
| --------- | -------- | -------- | ------------------------------------------ | -------- |
| order_ids | string   | 是       | 订单号，支持批量操作。最大批量操作数目为20 |          |

响应：

| 参数名          | 数据类型 | 说明       |
| --------------- | -------- | ---------- |
| symbol          | string   | 交易对名称 |
| id              | string   | 订单id     |
| price           | string   | 挂单价格   |
| quantity        | string   | 挂单数量   |
| deal_quantity   | string   | 成交数量   |
| deal_amount     | string   | 成交金额   |
| create_time     | string   | 下单时间   |
| state           | string   | 订单状态   |
| type            | string   | 订单类型   |
| client_order_id | string   | 客户订单id |


## 个人成交记录

> 响应示例

```json
{
    "code": 200,
    "data": [
        {
            "symbol": "ETH_USDT",
            "order_id": "a39ea6b7afcf4f5cbba1e515210ff827",
            "quantity": "54.1",
            "price": "182.6317377",
            "amount": "9880.37700957",
            "fee": "9.88037700957",
            "trade_type": "BID",
            "fee_currency": "USDT",
            "is_taker": true,
            "create_time": 1572693911000
        }
    ]
}
```

- **GET** ```/open/api/v2/order/deals```

参数：

| 参数名     | 数据类型 | 是否必须 | 说明         | 取值范围         |
| ---------- | -------- | -------- | ------------ | ---------------- |
| symbol     | string   | 是       | 交易对名称   |                  |
| limit      | string   | 否       | 返回条数     | 1~1000，默认值50 |
| start_time | string   | 否       | 查询起始时间 |                  |


响应：

| 参数名       | 数据类型 | 说明                      |
| ------------ | -------- | ------------------------- |
| symbol       | string   | 交易对                    |
| order_id     | string   | 订单id                    |
| trade_type   | string   | 交易类型                  |
| quantity     | string   | 成交数量                  |
| price        | string   | 成交价格                  |
| amount       | string   | 成交金额                  |
| fee          | string   | 成交手续费                |
| fee_currency | string   | 手续费币种                |
| is_taker     | bool     | 订单在成交中是否为taker单 |
| create_time  | long     | 成交时间                  |


## 成交明细

> 响应示例

```json
{
    "code": 200,
    "data": [
        {
            "symbol": "ETH_USDT",
            "order_id": "a39ea6b7afcf4f5cbba1e515210ff827",
            "quantity": "54.1",
            "price": "182.6317377",
            "amount": "9880.37700957",
            "fee": "9.88037700957",
            "trade_type": "BID",
            "fee_currency": "USDT",
            "is_taker": true,
            "create_time": 1572693911000
        }
    ]
}
```

- **GET** ```/open/api/v2/order/deal_detail```

参数：

| 参数名   | 数据类型 | 是否必须 | 说明 |
| -------- | -------- | -------- | ---- |
| order_id | string   | 是       |      |

响应：

| 参数名       | 数据类型 | 说明                      |
| ------------ | -------- | ------------------------- |
| symbol       | string   | 交易对                    |
| order_id     | string   | 订单id                    |
| trade_type   | string   | 交易类型                  |
| quantity     | string   | 成交数量                  |
| price        | string   | 成交价格                  |
| amount       | string   | 成交金额                  |
| fee          | string   | 成交手续费                |
| fee_currency | string   | 手续费币种                |
| is_taker     | bool     | 订单在成交中是否为taker单 |
| create_time  | long     | 成交时间                  |
## 按交易对撤销订单

> 响应示例

```json
{
    "code": 200,
    "data": [
        {
            "msg": "success",
            "order_id": "75ecf99feef04538b78e4622beaba6eb",
            "client_order_id": "a9329e86f2094b0d8b58e92c25029554"
        },
        {
            "msg": "success",
            "order_id": "139413c48f8b4c018f452ce796586bcf"
        },
        {
            "msg": "success",
            "order_id": "b58ef34c570e4917981f276d44091484"
        }
    ]
}
```

- **DELETE** ```/open/api/v2/order/cancel_by_symbol```

参数：

| 参数名 | 数据类型 | 是否必须 | 说明       | 取值范围 |
| ------ | -------- | -------- | ---------- | -------- |
| symbol | string   | 是       | 交易对名称 |          |

响应：

| 参数名 | 数据类型 | 说明                 |
| ------ | -------- | -------------------- |
| data   | map      | 订单号及对应操作结果 |

<aside class="notice">
若订单存在对应的client_order_id，则响应参数会返回client_order_id
</aside>

<aside class="notice">
请求返回表示服务端接收到了对应订单的撤单请求，并不表示已经撤单完成
</aside>

# 资产

> 响应示例

```json
{
    "code": 200,
    "data": {
        "currency": "USDT",
        "chains": [
            {
                "chain": "SOL",
                "address": "xxxxxxxxx"
            }
        ]
    }
}
```

当前仅开放读取充提信息相关接口，后续会开放提现接口（仍需开通可联系在线客服）。

## 获取充币地址

此节点用于查询特定币种在其所在区块链中的充币地址，母子用户均可用。

- **GET** ```/open/api/v2/asset/deposit/address/list```

<aside>
限速规则: 20次/2秒
</aside>

**需要权限:** 提币读

**请求参数:**

| 参数名   | 类型   | 是否必填 | 说明 |
| -------- | ------ | -------- | ---- |
| currency | string | ture     | 币种 |

**响应参数:**

| 参数名   | 类型   | 说明             |
| -------- | ------ | ---------------- |
| code     | int    | 状态码           |
| message  | string | 错误描述（如有） |
| currency | string | 币种             |
| chain    | string | 链名称           |
| address  | string | 充币地址         |

注意：
1、私有接口，需要签名认证；
2、只返回已生成的地址；

## 充值记录查询

- **GET** ```/open/api/v2/asset/deposit/list```

<aside>
限速规则: 20次/2秒
</aside>

**需要权限:** 提币读

**请求参数:**
       
| 参数名     | 类型   | 是否必填 | 说明                                |
| ---------- | ------ | -------- | ----------------------------------- |
| currency   | string | false    | 币种                                |
| state      | string | false    | 状态                                |
| start_time | long   | false    | 开始时间，单位ms，默认只查询最近1天 |
| end_time   | long   | false    | 结束时间，单位ms                    |
| page_num   | number | false    | 页数，默认1                         |
| page_size  | number | false    | 条数，默认20，最大50                |

**响应参数:**

| 参数名                | 类型    | 说明             |
| --------------------- | ------- | ---------------- |
| code                  | integer | 状态码           |
| message               | string  | 错误描述（如有） |
| currency              | string  | 币种             |
| actual_amount         | number  | 到账数量         |
| address               | string  | 充值地址         |
| amount                | number  | 充值数量         |
| confirmations         | number  | 区块确认数       |
| require_confirmations | number  | 最小区块确认数   |
| create_time           | number  | 发起提现时间     |
| explorer_url          | string  | 区块浏览器地址   |
| fee                   | string  | 手续费           |
| member_id             | string  | 用户ID           |
| state                 | string  | 状态             |
| txid                  | string  | 交易hash         |
| update_time           | string  | 更新时间         |
| wallet_type           | string  | 钱包类型         |
| current_page          | number  | 当前页           |
| current_result        | number  | 当前页条数       |
| total_result          | int     | 总条数           |
| total_page            | int     | 总页数           |

注意：通过单次查询可检索的范围最大为10天，通过多次平移窗口查询，最多可检索到过往180天的记录。


## 提币地址列表查询

- **GET** ```/open/api/v2/asset/address/list```

<aside>
限速规则: 20次/2秒
</aside>

**需要权限:** 提币读

**请求参数:**
       
| 参数名    | 类型   | 是否必填 | 说明                 |
| --------- | ------ | -------- | -------------------- |
| currency  | string | false    | 币种                 |
| page_num  | number | false    | 页数，默认1          |
| page_size | number | false    | 条数，默认20，最大50 |

**响应参数:**

| 参数名         | 类型    | 说明             |
| -------------- | ------- | ---------------- |
| code           | integer | 状态码           |
| message        | string  | 错误描述（如有） |
| currency       | string  | 币种             |
| chain          | string  | 链名称           |
| address        | string  | 地址             |
| address_tab    | string  | 地址标签         |
| current_page   | number  | 当前页           |
| current_result | number  | 当前页条数       |
| total_result   | int     | 总条数           |
| total_page     | int     | 总页数           |


## 提现记录查询

- **GET** ```/open/api/v2/asset/withdraw/list```

<aside>
限速规则: 20次/2秒
</aside>

**需要权限:** 提币读

**请求参数:**
       
| 参数名      | 类型   | 是否必填 | 说明                                |
| ----------- | ------ | -------- | ----------------------------------- |
| currency    | string | false    | 币种                                |
| withdraw_id | string | false    | 提现ID                              |
| state       | string | false    | 状态                                |
| start_time  | long   | false    | 开始时间，单位ms，默认只查询最近1天 |
| end_time    | long   | false    | 结束时间，单位ms                    |
| page_num    | number | false    | 页数，默认1                         |
| page_size   | number | false    | 条数，默认20，最大50                |

**响应参数:**

| 参数名       | 类型    | 说明             |
| ------------ | ------- | ---------------- |
| code         | integer | 状态码           |
| msg          | string  | 错误描述（如有） |
| result_list  | object  |                  |
| currency     | string  | 币种             |
| amount       | number  | 提现数量         |
| create_time  | number  | 发起提现时间     |
| explorer_url | string  | 区块浏览器地址   |
| fee          | string  | 手续费           |
| id           | string  | 提现ID           |
| remark       | string  | 提现备注         |
| state        | string  | 状态             |
| tx_id        | string  | 交易hash         |
| update_time  | string  | 更新时间         |
| page_num     | number  | 当前页           |
| page_size    | number  | 当前页条数       |
| total_size   | int     | 总条数           |
| total_page   | int     | 总页数           |

注意：通过单次查询可检索的范围最大为10天，通过多次平移窗口查询，最多可检索到过往180天的记录。

## 提币

- **POST** ```/open/api/v2/asset/withdraw```

<aside>
限速规则: 20次/2秒
</aside>

**需要权限:** 提币写

**请求参数:**

| 参数名   | 类型   | 是否必填 | 说明                                                         |
| -------- | ------ | -------- | ------------------------------------------------------------ |
| currency | string | true     | 币种                                                         |
| chain    | string | false    | 链名称，取值参考GET /open/api/v2/market/coin/list(币种信息查询) ，多链时必填（例如提USDT至OMNI时须设置此参数为"OMNI"，提USDT至TRX时须设置此参数为"TRC-20"，提USDT至ERC20时须设置此参数为"ERC-20"），非多链时无须设置此参数，具体取值参考币种信息查询接口 |
| amount   | number | true     | 提现数量                                                     |
| address  | string | true     | 提现地址 memo请使用:进行拼接                                 |
| remark   | string | false    | 备注                                                         |

**响应参数:**

| 参数名     | 类型   | 说明             |
| ---------- | ------ | ---------------- |
| code       | number | 状态码           |
| msg        | string | 错误描述（如有） |
| data       | object |                  |
| withdrawId | string | 提现ID           |

## 取消提币

- **DELETE** ```/open/api/v2/asset/withdraw```

<aside>
限速规则: 20次/2秒
</aside>

**需要权限:** 提币写

**请求参数:**

| 参数名      | 类型   | 是否必填 | 说明   |
| ----------- | ------ | -------- | ------ |
| withdraw_id | string | true     | 提币ID |

**响应参数:**

| 参数名 | 类型   | 说明             |
| ------ | ------ | ---------------- |
| code   | number | 状态码           |
| msg    | string | 错误描述（如有） |

## 内部资金划转 

支持母账号币币账户与合约账户间划转。 

支持子账号币币账户与合约账户间划转。 

- **POST** ```/open/api/v2/asset/internal/transfer``` 

<aside> 
限速规则: 2 次/1 秒 
</aside> 

**需要权限:** 划转写 

**请求参数:** 

| 参数名   | 类型   | 是否必填 | 说明                                       |
| -------- | ------ | -------- | ------------------------------------------ |
| currency | string | true     | 币种，如 usdt                              |
| amount   | number | true     | 划转数量                                   |
| from     | string | true     | 出账账户，币币账户 MAIN，合约账户 CONTRACT |
| to       | string | true     | 入账账户，币币账户 MAIN，合约账户 CONTRACT |

**响应参数:** 

| 参数名         | 类型   | 说明             |
| -------------- | ------ | ---------------- |
| code           | number | 状态码           |
| msg            | string | 错误描述（如有） |
| result_list    | object |                  |
| transact_id    | string | 划转交易 id      |
| currency       | string | 币种             |
| amount         | string | 金额             |
| from           | string | 出账账户         |
| to             | string | 入账账户         |
| transact_state | string | 交易状态         |

备注： 

1. 当前暂未开放逐仓杠杆账户。 

2. 提交成功不代表划转成功，可通过划转订单查询接口查询是否划转成功。

## 内部资金划转记录 

支持查询内部资金划转记录，且通过单次查询可检索的范围最大为 10 天，通过多次平移窗口查询，最多可检索到过往 180 天的记录。 

- **GET** ```/open/api/v2/asset/internal/transfer/record``` 

<aside> 
限速规则: 2 次/1 秒 
</aside> 

**需要权限:** 划转读 

**请求参数:** 

| 参数名     | 类型   | 是否必填 | 说明                                                   |
| ---------- | ------ | -------- | ------------------------------------------------------ |
| currency   | string | false    | 币种 （缺省值所有币种）                                |
| from       | string | false    | 出账账户，币币账户、逐仓杠杆账户、合约账户，缺省时所有 |
| to         | string | false    | 入账账户，币币账户、逐仓杠杆账户、合约账户，缺省时所有 |
| start_time | long   | false    | 开始时间                                               |
| end_time   | long   | false    | 结束时间                                               |
| page_num   | number | false    | 页数，默认 1                                           |
| page_size  | number | false    | 条数，默认 20，最大 50                                 |

**响应参数:**

| 参数名         | 类型    | 说明                                            |
| -------------- | ------- | ----------------------------------------------- |
| code           | integer | 状态码                                          |
| msg            | string  | 错误描述（如有）                                |
| currency       | string  | 币种                                            |
| amount         | string  | 金额                                            |
| from           | string  | 出账账户，币币账户、逐仓杠杆账户、合约账户      |
| to             | string  | 入账账户，币币账户、逐仓杠杆账户、合约账户      |
| transact_state | string  | 划转状态 成功 SUCCESS、失败 FAILED、划转中 WAIT |
| transact_id    | string  | 划转交易 id                                     |
| total_size     | int     | 总条数                                          |
| total_page     | int     | 总页数                                          |

## 获取可划转资金 

此接口可获取指定账户和币种下的可划转的资金。 

- **GET** ```/open/api/v2/account/balance``` 

<aside> 
限速规则: 2 次/1 秒 
</aside> 

**需要权限:** 划转读 

**请求参数:** 

| 参数名       | 类型   | 是否必填 | 说明                                 |
| ------------ | ------ | -------- | ------------------------------------ |
| currency     | string | true     | 币种                                 |
| account_type | string | false    | 账户类型：所有、币币、合约，默认币币 |
| sub_uid      | long   | false    | 子账号 uid，传了则 type 无效         |

**响应参数:** 

| 参数名       | 类型   | 说明             |
| ------------ | ------ | ---------------- |
| code         | number | 状态码           |
| msg          | string | 错误描述（如有） |
| data         | object |                  |
| account_type | string | 账户类型         |
| currency     | string | 币种             |
| balance      | string | 资金总额         |
| available    | string | 可用资金         |
| frozen       | string | 冻结资金         |

## 内部资金划转订单查询 

通过划转交易 id 查询，内部资金划转订单详情。 

- **GET** ```/open/api/v2/asset/internal/transfer/info``` 

<aside> 
限速规则: 2 次/1 秒 
</aside> 

**需要权限:** 划转读 

**请求参数:** 

| 参数名      | 类型   | 是否必填 | 说明        |
| ----------- | ------ | -------- | ----------- |
| transact_id | String | ture     | 划转交易 id |

**响应参数:** 

| 参数名      | 类型    | 说明                                       |
| ----------- | ------- | ------------------------------------------ |
| code        | integer | 状态码                                     |
| msg         | string  | 错误描述（如有）                           |
| transact_id | string  | 划转交易 id                                |
| currency    | string  | 币种                                       |  | amount | String | 划转数量 |
| from        | string  | 出账账户，币币账户、逐仓杠杆账户、合约账户 |
