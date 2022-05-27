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

# 更新日志

| 生效时间（北京时间 UTC+8) | 接口 | 更新类型 | 说明 |
|-----|-----|-----|-----|
|2021-01-15|*|新增|合约API发布|
|2021-03-30|*|修改|调整如下接口访问路径及数据返回格式（原路径仍支持，但会逐步废弃）：获取用户所有历史订单、获取用户当前未结束订单、获取用户历史持仓信息、获取止盈止损订单列表、获取计划委托订单列表、获取用户所有订单成交明细|

# 接入说明

## 接入url

> 响应示例

```json
{
  "success": true,
  "code": 0,
  "data": {
    "symbol": "BTC_USD",
    "fairPrice": 8000,
    "timestamp": 1587442022003
  }
} 
```

> 或

```json
{
  "success": false,
  "code":500,
  "message": "系统内部错误!"
}
```

- https://contract.mexc.com

相应API接受GET、POST或DELETE类型的请求，post请求的Content-Type为: application/json。

参数以json格式发送（参数命名规则为驼峰命名），get请求以requestParam形式发送（参数命名规则为'_'隔开）。

## 鉴权方式

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

2. 对于私有接口,需要在header中传入ApiKey、Request-Time、Signature、Content-Type 必须指定为application/json、Recv-Window(可选)参数,Signature为签名字符串,签名规则如下:

  1)签名时需要先获得请求参数字符串，无参时为""：

    对于GET/DELETE请求，按字典序拼接业务参数以&间隔，并最终获得签名目标串（在批量操作的API中，若参数值中有逗号等特殊符号，这些符号在签名时需要做URL encode）。
    
    对于POST请求，签名参数为json字符串（无需进行字典排序）。

  2)获得参数字符串后，再拼接签名目标串，规则为：accessKey+时间戳+获取到的参数字符串

  3)使用HMAC SHA256算法对目标串进行签名，并最终将签名作为参数携带到header中

注意：

  1)参与签名的业务参数为null时，不参与签名，对于path参数，也不参与签名；注意get请求将参数拼接至url上时，如果参数为null， 后台解析时，会解析成""，固当POST请求，某参数为null时，不要传该参数，或者签名时，将该参数的值设置为""，否则会出现验签失败。

  2)请求时将签名时用到的Request-Time的值放入header的Request-Time参数中，获得的签名字符串放入header的Signature参数中，将APIKEY的Access Key放在header的ApiKey参数中，其余业务参数按正常传递即可。

  3）获得的签名字符串不需要进行base64进行编码。

## 时间安全

所有签名接口均需要传入header参数Request-Time，即以毫秒表示的时间戳字符串，服务端接收到请求后会验证请求发出的时间
范围。若接受请求时，收到的req_time小于或大于服务端时间10秒（默认值）以上（该时间窗口值可以通过发送可选header参数
Recv-Window来自定义，其最大值为60，不推荐使用30秒以上的recv_window），则认为该请求无效

## 创建API key

用户可以在MEXC站点个人中心，创建API key，其包括两个部分，Access keyAPI的访问秘钥，Secret key对应的秘钥，用于签名计算及验证。

您可以点击 <a href="https://www.mexc.la/ucenter/openapi" target="_blank">这里</a> 创建API Key。

创建 API Key 时可以选择绑定 IP 地址，未绑定 IP 地址的 API Key 有效期为90天。（强烈建议绑定 IP 地址）

这两个密钥与账号安全紧密相关，无论何时都请勿向其它人透露。 

# 行情接口

[行情接口]模块下的API接口不需要身份验证。

## 获取服务器时间

> 请求示例

```
curl "https://contract.mexc.com/api/v1/contract/ping"
```

> 响应示例

```json
{
  "success": true,
  "data":1587442022003 
}
```

- **GET** ```api/v1/contract/ping```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**

无

## 获取合约信息

> 请求示例

```
curl "https://contract.mexc.com/api/v1/contract/detail"
```

> 响应示例

```json
{
    "success":true,
    "code":0,
    "data":[
        {
            "symbol":"BTC_USDT",
            "displayName":"BTC_USDT永续",
            "displayNameEn":"BTC_USDT SWAP",
            "positionOpenType":3,
            "baseCoin":"BTC",
            "quoteCoin":"USDT",
            "settleCoin":"USDT",
            "contractSize":0.0001,
            "minLeverage":1,
            "maxLeverage":125,
            "priceScale":2,
            "volScale":0,
            "amountScale":4,
            "priceUnit":0.5,
            "volUnit":1,
            "minVol":1,
            "maxVol":5000000,
            "bidLimitPriceRate":0.03,
            "askLimitPriceRate":0.03,
            "takerFeeRate":0.0006,
            "makerFeeRate":0.0002,
            "maintenanceMarginRate":0.004,
            "initialMarginRate":0.008,
            "riskBaseVol":150000,
            "riskIncrVol":150000,
            "riskIncrMmr":0.004,
            "riskIncrImr":0.004,
            "riskLevelLimit":5,
            "priceCoefficientVariation":0.05,
            "indexOrigin":[
                "Binance",
                "GATEIO",
                "HUOBI",
                "MXC"
            ],
            "state":0,
            "isNew":false,
            "isHot":true,
            "isHidden":false
        },
    ]
}
```

- **GET** ```api/v1/contract/detail```

<aside class="notice">
限速规则: 20次/2秒 
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
|  symbol | string  | false  | 合约名  |

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| symbol  | string | 合约名 |
| displayName  | string | 展示名 |
| displayNameEn  | string | 英文展示名 |
| positionOpenType  | int  |  开仓类型,1：逐仓，2：全仓，3：全仓，逐仓都支持 |
| baseCoin  | string  | 标的货币 如 BTC |
| quoteCoin  | string  | 标价货币 如 USDT |
| settleCoin  | string  | 结算货币 如 USDT|
| contractSize  | decimal  | 合约面值 |
| minLeverage  | int  | 杠杆倍数下限 |
| maxLeverage  | int  | 杠杆倍数上限 |
| priceScale  | int  | 价格精度 |
| volScale  | int  | 数量精度 |
| amountScale  | int  | 金额精度 |
| priceUnit  | int  | 价格的最小步进单位 |
| volUnit  | int  | 数量的最小步进单位 |
| minVol  | decimal  | 订单张数下限|
| maxVol  | decimal  | 订单张数上限 |
| bidLimitPriceRate  | decimal  | 卖单价格限制比率 |
| askLimitPriceRate  | decimal  | 买单价格限制比率 |
| takerFeeRate  | decimal  | 买单费率 |
| makerFeeRate  | decimal  | 卖单费率 |
| maintenanceMarginRate  | decimal  | 维持保证金率 |
| initialMarginRate  | decimal  | 初始保证金率 |
| riskBaseVol  | decimal  | 基本张数 |
| riskIncrVol  | decimal  | 递增张数 |
| riskIncrMmr  | decimal  | 维持保证金率递增量 |
| riskIncrImr  | decimal  | 初始保证金率递增量 |
| riskLevelLimit  | int  | 风险限额档位数 |
| priceCoefficientVariation  | decimal  | 合理价格偏离指数价格系数 |
| indexOrigin  | List<String>  | 指数来源 |
| state  | int  | 状态,0:启用,1:交割,2:交割完成,3:下线,4: 暂停|
| conceptPlate  |  List<String> | 归属板块，与板块列表entryKey字段对应 |
| riskLimitType  |  string | 风险限额类型，BY_VOLUME: 按张数 ，BY_VALUE：按仓位价值 |


## 获取可划转币种

> 请求示例

```
curl "https://contract.mexc.com/api/v1/contract/support_currencies"
```

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": [
        "BTC",
        "ETH",
        "USDT"
    ]
}
```

- **GET** ```api/v1/contract/support_currencies```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**

无

**响应参数:**

返回的“data”对象是一个字符串数组，每一个字符串代表一个支持的币种。

## 获取合约深度信息

> 请求示例

```
curl "https://contract.mexc.com/api/v1/contract/depth/BTC_USDT"
```

> 响应示例

```json
{
    "asks":[
        [
            3968.5,
            121
        ],
        [
            3968.6,
            160,
            4
        ]
    ],
    "bids":[
        [
            3968.4,
            179,
            4
        ],
        [
            3968,
            914,
            3
        ]
    ],
    "version":1,
    "timestamp":1587442022003
}
```

- **GET** ```api/v1/contract/depth/{symbol}```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol | string  | true  | 合约名  |
| limit | int  | false  | 档位数  |

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| asks  | List<Numeric[]> |卖方深度 |
| bids  | List<Numeric[]> | 买方深度 |
| version  | long  | 版本号 |
| timestamp  | long  | 系统时间戳 |

备注: [411.8, 10, 1] 411.8为价格，10为此价格的合约张数,1为订单数量

## 获取合约最近N条深度信息快照

> 请求示例

```
curl "https://contract.mexc.com/api/v1/contract/depth_commits/BTC_USDT/20"
```

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": [
        {
            "asks": [
                [
                    31792,
                    59105,
                    1
                ]
            ],
            "bids": [],
            "version": 1481763378
        }
    ]
}
```

- **GET** ```api/v1/contract/depth_commits/{symbol}/{limit}```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol | string  | true  | 合约名  |
| limit | int  | true  | 条数  |

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| asks  | List<Numeric[]> |卖方深度 |
| bids  | List<Numeric[]> | 买方深度 |
| version  | long  | 版本号 |

## 获取合约指数价格

> 请求示例

```
curl "https://contract.mexc.com/api/v1/contract/index_price/BTC_USDT"
```

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": {
        "symbol": "BTC_USDT",
        "indexPrice": 31104.6,
        "timestamp": 1609829627708
    }
}
```

- **GET** ```api/v1/contract/index_price/{symbol}```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol | string  | true  | 合约名  |

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| symbol  | string | 交易对 |
| indexPrice  | decimal  | 指数价格 |
| timestamp  | long   | 系统时间戳 |

## 获取合约合理价格

> 请求示例

```
curl "https://contract.mexc.com/api/v1/contract/fair_price/BTC_USDT"
```

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": {
        "symbol": "BTC_USDT",
        "fairPrice": 31103.4,
        "timestamp": 1609829705178
    }
}
```

- **GET** ```api/v1/contract/fair_price/{symbol}```

<aside class="notice">
限速规则: 20次/2秒
</aside>>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | 合约名  |

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| symbol | string| 合约名 |
| fairPrice  | decimal  | 合理价格 |
| timestamp  | long   | 系统时间戳 |

## 获取合约资金费率

> 请求示例

```
curl "https://contract.mexc.com/api/v1/contract/funding_rate/BTC_USDT"
```

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": {
        "symbol": "BTC_USDT",
        "fundingRate": -0.000489,
        "maxFundingRate": 0.001,
        "minFundingRate": -0.001,
        "collectCycle": 8,
        "nextSettleTime": 1609833600000,
        "timestamp": 1609829807577
    }
}
```

- **GET** ```api/v1/contract/funding_rate/{symbol}```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | 合约名  |

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| symbol  | string | 合约名 |
| fundingRate  | decimal  | 资金费率 |
| maxFundingRate  | decimal  | 资金费率上限 |
| minFundingRate  | decimal  | 资金费率下限 |
| collectCycle  | int  | 收取周期 |
| nextSettleTime  | long  | 下次收取时间 |
| timestamp  | long   | 系统时间戳 |

## 获取蜡烛图数据

> 请求示例

```
curl "https://contract.mexc.com/api/v1/contract/kline/BTC_USDT?interval=Min15&start=1609992674000&end=1609992694000"
```

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": {
        "time": [
            1609740600
        ],
        "open": [
            33016.5
        ],
        "close": [
            33040.5
        ],
        "high": [
            33094.0
        ],
        "low": [
            32995.0
        ],
        "vol": [
            67332.0
        ],
        "amount": [
            222515.85925
        ]
    }
}
```

- **GET** ```api/v1/contract/kline/{symbol}```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | 合约名  |
| interval   | string  | false  | 间隔: Min1、Min5、Min15、Min30、Min60、Hour4、Hour8、Day1、Week1、Month1，不填时默认Min1  |
| start  | long  | false  | 开始时间戳，单位秒  |
| end  | long  | false  | 结束时间戳，单位秒  |

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| open  | double  | 开盘价 |
| close  | double   | 收盘价 |
| high  | double   | 最高价 |
| low  | double   | 最低价 |
| vol  | double   | 成交量 |
| time  | long   | 时间窗口 |

注意：

1、单次请求的最大数据量是2000。如果您选择的开始/结束时间和时间粒度导致超过单次请求的最大数据量，您的请求将只会返回2000个数据。如果您希望在更大的时间范围内获取足够精细的数据，则需要使用多个开始/结束范围进行多次请求。

2、如果只提供了开始时间，则查询开始时间到系统当前时间的数据。如果只提供了结束时间，则返回离结束时间最近的2000条数据。如果开始时间和结束时间均未提供，则查询离系统当前时间最近的2000条数据。

## 获取指数价格蜡烛图数据

> 请求示例

```
curl "https://contract.mexc.com/api/v1/contract/kline/index_price/BTC_USDT?interval=Min15&start=1609992674000&end=1609992694000"
```

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": {
        "time": [
            1609740900
        ],
        "open": [
            33039.0
        ],
        "close": [
            33233.1
        ],
        "high": [
            33352.3
        ],
        "low": [
            33007.9
        ],
        "vol": [
            0.0
        ],
        "amount": [
            0.0
        ]
    }
}
```

- **GET** ```api/v1/contract/kline/index_price/{symbol}```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | 合约名  |
| interval   | string  | false  | 间隔: Min1、Min5、Min15、Min30、Min60、Hour4、Hour8、Day1、Week1、Month1，不填时默认Min1  |
| start  | long  | false  | 开始时间戳，单位秒  |
| end  | long  | false  | 结束时间戳，单位秒  |

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| open  | double  | 开盘价 |
| close  | double   | 收盘价 |
| high  | double   | 最高价 |
| low  | double   | 最低价 |
| vol  | double   | 成交量 |
| time  | long   | 时间窗口 |

注意：
1、单次请求的最大数据量是2000。如果您选择的开始/结束时间和时间粒度导致超过单次请求的最大数据量，您的请求将只会返回2000个数据。如果您希望在更大的时间范围内获取足够精细的数据，则需要使用多个开始/结束范围进行多次请求。

2、如果只提供了开始时间，则查询开始时间到系统当前时间的数据。如果只提供了结束时间，则返回离结束时间最近的2000条数据。如果开始时间和结束时间均未提供，则查询离系统当前时间最近的2000条数据。

## 获取合理价格蜡烛图数据

> 请求示例

```
curl "https://contract.mexc.com/api/v1/contract/kline/fair_price/BTC_USDT?interval=Min15&start=1609992674000&end=1609992694000"
```

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": {
        "time": [
            1609740900
        ],
        "open": [
            33041.0
        ],
        "close": [
            33233.3
        ],
        "high": [
            33354.8
        ],
        "low": [
            33009.4
        ],
        "vol": [
            0.0
        ],
        "amount": [
            0.0
        ]
    }
}
```

- **GET** ```api/v1/contract/kline/fair_price/{symbol}```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | 合约名  |
| interval   | string  | false  | 间隔: Min1、Min5、Min15、Min30、Min60、Hour4、Hour8、Day1、Week1、Month1，不填时默认Min1  |
| start  | long  | false  | 开始时间戳，单位秒  |
| end  | long  | false  | 结束时间戳，单位秒  |

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| open  | double  | 开盘价 |
| close  | double   | 收盘价 |
| high  | double   | 最高价 |
| low  | double   | 最低价 |
| vol  | double   | 成交量 |
| time  | long   | 时间窗口 |

注意：
1、单次请求的最大数据量是2000。如果您选择的开始/结束时间和时间粒度导致超过单次请求的最大数据量，您的请求将只会返回2000个数据。如果您希望在更大的时间范围内获取足够精细的数据，则需要使用多个开始/结束范围进行多次请求。

2、如果只提供了开始时间，则查询开始时间到系统当前时间的数据。如果只提供了结束时间，则返回离结束时间最近的2000条数据。如果开始时间和结束时间均未提供，则查询离系统当前时间最近的2000条数据。

## 获取成交数据

> 请求示例

```
curl "https://contract.mexc.com/api/v1/contract/deals/BTC_USDT"
```

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": [
        {
            "p": 31199,
            "v": 18,
            "T": 1,
            "O": 3,
            "M": 2,
            "t": 1609831235985
        },
        {
            "p": 31199,
            "v": 15,
            "T": 2,
            "O": 3,
            "M": 1,
            "t": 1609831234759
        }
    ]
}
```

- **GET** ```api/v1/contract/deals/{symbol}```

<aside class="notice">
限速规则: 20次/2秒 
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | 合约名  |
| limit  | int  | false  | 结果集数量，最大为100，不填默认返回100条  |

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| p  | decimal  | 成交价 |
| v  | decimal  | 数量 |
| T  | int  | 成交方向,1:买,2:卖 |
| O  | int   | 是否是开仓，1:是,2:否,当O为1的时候, vol是新增的持仓量 |
| M  | int   | 是否为自成交,1:是,2:否 |
| t  | long   | 成交时间|

## 获取合约行情数据

> 请求示例

```
curl "https://contract.mexc.com/api/v1/contract/ticker"
```

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": {
        "symbol": "BTC_USDT",
        "lastPrice": 31199,
        "bid1": 31198.5,
        "ask1": 31199,
        "volume24": 40146908,
        "amount24": 124905007.4428,
        "holdVol": 55102960,
        "lower24Price": 27795,
        "high24Price": 33152.5,
        "riseFallRate": -0.0176,
        "riseFallValue": -562,
        "indexPrice": 31016.3,
        "fairPrice": 31199.5,
        "fundingRate": 0.001,
        "maxBidPrice": 31946.5,
        "minAskPrice": 30085.5,
        "timestamp": 1609831334016
    }
}
```

- **GET** ```api/v1/contract/ticker```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | false  | 合约名 |

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| symbol  | string | 合约名 |
| lastPrice  | decimal  | 最新价 |
| bid1  | decimal  | 买一价 |
| ask1  | decimal  | 卖一价 |
| volume24  | decimal  | 24小时成交量，按张数统计 |
| amount24  | decimal  | 24小时成交额|
| holdVol| decimal  | 总持仓量 |
| lower24Price  | decimal  | 24小时最低价 |
| high24Price  | decimal  | 24小时内最高价 |
| riseFallRate  | decimal  | 涨跌幅 |
| riseFallValue  | decimal  | 涨跌额 |
| indexPrice  | decimal  | 指数价格 |
| fairPrice  | decimal  | 合理价 |
| fundingRate  | decimal  | 资金费率 |
| timestamp  | long   | 成交时间 |

## 获取所有合约风险基金余额

> 请求示例

```
curl "https://contract.mexc.com/api/v1/contract/risk_reverse"
```

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": [
        {
            "symbol": "BTC_USDT",
            "currency": "USDT",
            "available": 425018.32968325152473812,
            "timestamp": 1609831395734
        },
        {
            "symbol": "BTC_USD",
            "currency": "BTC",
            "available": 5.00211366264782435,
            "timestamp": 1609831395734
        },
    ]
}
```

- **GET** ```api/v1/contract/risk_reverse```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**

无

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| symbol  | string | 合约名 |
| currency  | string  | 结算货币 |
| available  | decimal  | 余额 |
| timestamp  | long  | 系统时间戳 |

## 获取合约风险基金余额历史

> 请求示例

```
curl "https://contract.mexc.com/api/v1/contract/risk_reverse/history?symbol=BTC_USDT&page_num=1&page_size=20"
```

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": {
        "pageSize": 2,
        "totalCount": 42,
        "totalPage": 21,
        "currentPage": 1,
        "resultList": [
            {
                "symbol": "BTC_USDT",
                "currency": "USDT",
                "available": 424288.053161046680168662,
                "snapshotTime": 1609819200000
            },
            {
                "symbol": "BTC_USDT",
                "currency": "USDT",
                "available": 423989.817244106347071489,
                "snapshotTime": 1609804800000
            }
        ]
    }
}
```

- **GET** ```api/v1/contract/risk_reverse/history```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | 合约名 |
| page_num  | int  | true  | 当前页数,默认为1  |
| page_size  | int  | true  | 每页大小,默认20,最大100  |

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| pageSize  | int  | 页面大小 |
| totalCount  | int  | 总条数 |
| totalPage  | int  | 总页数 |
| currentPage  | int  | 当前页 |
| resultList  | list  | 数据结果集 |
| symbol  | string | 合约名 |
| currency  | string  | 结算货币 |
| available  | decimal  | 余额 |
| snapshotTime  | long  | 快照时间 |

## 获取合约资金费率历史

> 请求示例

```
curl "https://contract.mexc.com/api/v1/contract/funding_rate/history?symbol=BTC_USDT&page_num=1&page_size=20"
```

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": {
        "pageSize": 2,
        "totalCount": 21,
        "totalPage": 11,
        "currentPage": 1,
        "resultList": [
            {
                "symbol": "BTC_USDT",
                "fundingRate": 0.000266,
                "settleTime": 1609804800000
            },
            {
                "symbol": "BTC_USDT",
                "fundingRate": 0.00029,
                "settleTime": 1609776000000
            }
        ]
    }
}
```

- **GET** ```api/v1/contract/funding_rate/history```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | 合约名 |
| page_num  | int  | true  | 当前页数,默认为1  |
| page_size  | int  | true  | 每页大小,默认20,最大100  |

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| pageSize  | int  | 页面大小 |
| totalCount  | int  | 总条数 |
| totalPage  | int  | 总页数 |
| currentPage  | int  | 当前页 |
| resultList  | list  | 数据结果集 |
| symbol  | string | 合约名 |
| fundingRate  | decimal  | 资金费率 |
| settleTime  | long  | 结算时间 |

# 账户和交易接口

[账户和交易接口]模块下的API接口需要身份验证

## 获取用户所有资产信息

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": [
        {
            "currency": "BTC",
            "positionMargin": 0,
            "availableBalance": 0,
            "cashBalance": 0,
            "frozenBalance": 0,
            "equity": 0,
            "unrealized": 0,
            "bonus": 0
        },
        {
            "currency": "ETH",
            "positionMargin": 0,
            "availableBalance": 0,
            "cashBalance": 0,
            "frozenBalance": 0,
            "equity": 0,
            "unrealized": 0,
            "bonus": 0
        },
        {
            "currency": "USDT",
            "positionMargin": 0,
            "availableBalance": 0.03176562,
            "cashBalance": 0.03176562,
            "frozenBalance": 0,
            "equity": 0.03176562,
            "unrealized": 0,
            "bonus": 0
        }
    ]
}
```

- **GET** ```api/v1/private/account/assets```

**需要权限:** 合约交易读取权限

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**

无

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| currency  | string  | 币种 |
| positionMargin  | decimal   | 仓位保证金 |
| frozenBalance  | decimal   | 冻结余额 |
| availableBalance  | decimal   | 当前可用余额 |
| cashBalance  | decimal   | 可提现余额 |
| equity  | decimal   | 总权益 |
| unrealized  | decimal   | 未实现盈亏 |

## 获取用户单个币种资产信息

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": {
        "currency": "USDT",
        "positionMargin": 0,
        "availableBalance": 0.03176562,
        "cashBalance": 0.03176562,
        "frozenBalance": 0,
        "equity": 0.03176562,
        "unrealized": 0,
        "bonus": 0
    }
}
```

- **GET** ```api/v1/private/account/asset/{currency}```

**需要权限:** 合约账户读取权限

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| currency  | string  | true  | 币种  |

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| currency  | string  | 币种 |
| positionMargin  | decimal   | 仓位保证金 |
| frozenBalance  | decimal   | 冻结余额 |
| availableBalance  | decimal   | 当前可用余额 |
| cashBalance  | decimal   | 可提现余额 |
| equity  | decimal   | 总权益 |
| unrealized  | decimal   | 未实现盈亏 |

## 获取用户资产划转记录

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": {
        "pageSize": 2,
        "totalCount": 88,
        "totalPage": 44,
        "currentPage": 1,
        "resultList": [
            {
                "id": 165230,
                "txid": "db13d56ca887429a8f5fe1d1cbc4559c",
                "currency": "USDT",
                "amount": 0.03176562,
                "type": "IN",
                "state": "SUCCESS",
                "createTime": 1609833219000,
                "updateTime": 1609833219000
            },
            {
                "id": 139320,
                "txid": "a57ff46de96545839185aff7343f9b7c",
                "currency": "USDT",
                "amount": 60.53383524,
                "type": "OUT",
                "state": "SUCCESS",
                "createTime": 1608200935000,
                "updateTime": 1608200935000
            }
        ]
    }
}
```

- **GET** ```api/v1/private/account/transfer_record```

**需要权限:** 合约账户读取权限

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| currency  | string  | false  | 币种  |
| state  | string  | false  | 状态:WAIT 、SUCCESS 、FAILED  |
| type  | string  | false  | 类型:IN 、OUT  |
| page_num  | int  | true  | 当前页数,默认为1  |
| page_size  | int  | true  | 每页大小,默认20,最大100  |

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| pageSize  | int  | 页面大小 |
| totalCount  | int  | 总条数 |
| totalPage  | int  | 总页数 |
| currentPage  | int  | 当前页 |
| resultList  | list  | 数据结果集 |
| id  | long  | id |
| txid  | string  | 流水号 |
| currency  | string  | 币种 |
| amount  | decimal  | 转账金额 |
| type  | string   | 类型:IN 、OUT |
| state  | string   | 状态:WAIT 、SUCCESS 、FAILED  |
| createTime  | long   | 创建时间 |
| updateTime  | long   | 修改时间 |

## 获取用户历史持仓信息

> 响应示例

```json
{
    "success": false,
    "code": 0,
    "message": "",
    "data": [{
        "positionId": 0,
        "symbol": "",
        "positionType": 0,
        "openType": 0,
        "state": 0,
        "holdVol": 0.0,
        "frozenVol": 0.0,
        "closeVol": 0.0,
        "holdAvgPrice": 0.0,
        "openAvgPrice": 0.0,
        "closeAvgPrice": 0.0,
        "liquidatePrice": 0.0,
        "oim": 0.0,
        "im": 0.0,
        "holdFee": 0.0,
        "realised": 0.0,
        "adlLevel": 0,
        "leverage": 0,
        "createTime": "",
        "updateTime": "",
        "autoAddIm": false
    }]
}
```

- **GET** ```api/v1/private/position/list/history_positions```

**需要权限:** 合约交易读取权限

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | false  | 合约名|
| type  | int  | false  | 仓位类型， 1多 2空|
| page_num  | int  | true  | 当前页数,默认为1  |
| page_size  | int  | true  | 每页大小,默认20,最大100  |

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| code | integer | 状态码 | 
| message | string | 错误描述（如有） | 
| <data> | array |  | 
| positionId  | long  | 持仓id |
| symbol  | string  | 合约名 |
| positionType  | int  | 仓位类型， 1多 2空 |
| openType  | int   | 开仓类型， 1逐仓 2全仓 |
| state  | int   | 仓位状态,1持仓中2系统代持3已平仓  |
| holdVol  | decimal  | 持仓数量 |
| frozenVol  | decimal   | 冻结量 |
| closeAvgPrice  | decimal   | 平仓均价 |
| openAvgPrice  | decimal   | 开仓均价 |
| liquidatePrice  | decimal   | 逐仓时的爆仓价 |
| oim  | decimal   | 原始初始保证金 |
| im  | decimal   | 初始保证金， 逐仓时可以加减此项以调节爆仓价 |
| holdFee  | decimal   | 资金费, 正数表示得到，负数表示支出 |
| realised  | decimal   | 已实现盈亏 |
| adlLevel  | int  | adl等级 |
| leverage  | int  | 杠杆倍数 |
| createTime  | date   | 创建时间 |
| updateTime  | date   | 修改时间 |
| autoAddIm  | boolean   | 是否自动追加保证金 |
| </data> |  |  | 

## 获取用户当前持仓

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": [
        {
            "positionId": 1394650,
            "symbol": "ETH_USDT",
            "positionType": 1,
            "openType": 1,
            "state": 1,
            "holdVol": 1,
            "frozenVol": 0,
            "closeVol": 0,
            "holdAvgPrice": 1217.3,
            "openAvgPrice": 1217.3,
            "closeAvgPrice": 0,
            "liquidatePrice": 1211.2,
            "oim": 0.1290338,
            "im": 0.1290338,
            "holdFee": 0,
            "realised": -0.0073,
            "leverage": 100,
            "createTime": 1609991676000,
            "updateTime": 1609991676000,
            "autoAddIm": false
        }
    ]
}
```

- **GET** ```api/v1/private/position/open_positions```

**需要权限:** 合约交易读取权限

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | false  | 合约名|

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| positionId  | long  | 持仓id |
| symbol  | string  | 合约名 |
| holdVol  | decimal  | 持仓数量 |
| positionType  | int  | 仓位类型， 1多 2空 |
| openType  | int   | 开仓类型， 1逐仓 2全仓 |
| state  | int   | 仓位状态,1持仓中2系统代持3已平仓  |
| frozenVol  | decimal   | 冻结量 |
| closeVol  | decimal   | 平仓量 |
| holdAvgPrice  | decimal   | 持仓均价 |
| closeAvgPrice  | decimal   | 平仓均价 |
| openAvgPrice  | decimal   | 开仓均价 |
| liquidatePrice  | decimal   | 逐仓时的爆仓价 |
| oim  | decimal   | 原始初始保证金 |
| adlLevel  | int   | adl减仓等级,取值为 1-5，为空时需等待刷新 |
| im  | decimal   | 初始保证金， 逐仓时可以加减此项以调节爆仓价 |
| holdFee  | decimal   | 资金费, 正数表示得到，负数表示支出 |
| realised  | decimal   | 已实现盈亏 |
| createTime  | date   | 创建时间 |
| updateTime  | date   | 修改时间 |

## 获取用户资金费用明细

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": {
        "pageSize": 2,
        "totalCount": 73,
        "totalPage": 37,
        "currentPage": 1,
        "resultList": [
            {
                "id": 328033,
                "symbol": "SUSHI_USDT",
                "positionType": 1,
                "positionValue": 41.8899,
                "funding": 0.0837798,
                "rate": -0.002,
                "settleTime": 1606435200000
            },
            {
                "id": 327194,
                "symbol": "SUSHI_USDT",
                "positionType": 1,
                "positionValue": 34.2654,
                "funding": 0.0685308,
                "rate": -0.002,
                "settleTime": 1606406400000
            }
        ]
    }
}
```

- **GET** ```api/v1/private/position/funding_records```

**需要权限:** 合约交易读取权限

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol | string  | false  | 合约名|
| position_id  | int  | false  | 仓位id|
| page_num  | int  | true  | 当前页数,默认为1  |
| page_size  | int  | true  | 每页大小,默认20,最大100  |

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| pageSize  | int  | 页面大小 |
| totalCount  | int  | 总条数 |
| totalPage  | int  | 总页数 |
| currentPage  | int  | 当前页 |
| resultList  | list  | 数据结果集 |
| id  | long  | id |
| symbol  | string  | 合约名 |
| positionId  | long  | 持仓id |
| positionType  | int  | 1:多仓,2:空仓 |
| positionValue  | decimal  | 仓位价值 |
| funding  | decimal   | 费用 |
| rate  | decimal   | 资金费率  |
| settleTime  | date   | 清算时间 |

## 获取用户当前未结束订单

> 响应示例

```json
{
    "success": false,
    "code": 0,
    "message": "",
    "data": [{
            "orderId": 0,
            "symbol": "",
            "positionId": 0,
            "price": 0.0,
            "vol": 0.0,
            "leverage": 0,
            "side": 0,
            "category": 0,
            "orderType": 0,
            "dealAvgPrice": 0.0,
            "dealVol": 0.0,
            "orderMargin": 0.0,
            "takerFee": 0.0,
            "makerFee": 0.0,
            "profit": 0.0,
            "feeCurrency": "",
            "openType": 0,
            "state": 0,
            "externalOid": "",
            "errorCode": 0,
            "usedMargin": 0.0,
            "createTime": "",
            "updateTime": "",
            "stopLossPrice": 0.0,
            "takeProfitPrice": 0.0
        }

    ]
}
```

- **GET** ```api/v1/private/order/list/open_orders/{symbol}```

**需要权限:** 合约交易读取权限

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
	
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | false  | 合约名,不传返回所有|
| page_num  | int  | true  | 当前页数,默认为1  |
| page_size  | int  | true  | 每页大小,默认20,最大100  |

**响应参数:**

| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| code | integer | 状态码 | 
| message | string | 错误描述（如有） | 
| <data> | array |  | 
| orderId  | long  | 订单id |
| symbol  | string  | 合约名 |
| positionId  | long  | 持仓id |
| price  | decimal  | 委托价格 |
| vol  | decimal  | 委托数量 |
| leverage  | long  | 杠杆倍数 |
| side  | int  | 订单方向 1开多,2平空,3开空,4平多 |
| category  | int  | 订单类别:1限价委托,2强平代管委托,4ADL减仓 |
| orderType  | int  | 1:限价单,2:Post Only只做Maker,3:立即成交或立即取消,4:全部成交或者全部取消，5:市价单,6:市价转现价|| dealAvgPrice  | decimal  | 成交均价 |
| dealAvgPrice  | decimal   | 成交均价 |
| dealVol  | decimal   | 成交数量 |
| orderMargin  | decimal   | 委托保证金  |
| takerFee  | decimal   | 买单手续费 |
| makerFee  | decimal   | 卖单手续费 |
| profit  | decimal   | 平仓盈亏 |
| feeCurrency  | string   | 收费币种 |
| openType  | int   | 开仓类型,1逐仓,2全仓 |
| state  | int   | 订单状态,1:待报,2未完成,3已完成,4已撤销,5无效 |
| externalOid  | string   | 外部订单号 |
| errorCode  | int   | 错误code,0:正常，1：参数错误，2：账户余额不足，3：仓位不存在，4：仓位可用持仓不足，5：多仓时， 委托价小于了强平价，空仓时， 委托价大于了强平价，6：开多时， 强平价大于了合理价，开空时， 强平价小于了合理价 ,7:超过风险限额限制，8：系统撤销|
| usedMargin  | decimal   | 已经使用的保证金  |
| createTime  | date   | 创建时间 |
| updateTime  | date   | 修改时间 |
| stopLossPrice  | decimal   | 止损价 |
| takeProfitPrice  | decimal   | 止盈价 |
| </data> |  |  | 


## 获取用户所有历史订单

> 响应示例

```json
{
    "success": false,
    "code": 0,
    "message": "",
    "data": [{
            "orderId": 0,
            "symbol": "",
            "positionId": 0,
            "price": 0.0,
            "vol": 0.0,
            "leverage": 0,
            "side": 0,
            "category": 0,
            "orderType": 0,
            "dealAvgPrice": 0.0,
            "dealVol": 0.0,
            "orderMargin": 0.0,
            "takerFee": 0.0,
            "makerFee": 0.0,
            "profit": 0.0,
            "feeCurrency": "",
            "openType": 0,
            "state": 0,
            "externalOid": "",
            "errorCode": 0,
            "usedMargin": 0.0,
            "createTime": "",
            "updateTime": "",
            "stopLossPrice": 0.0,
            "takeProfitPrice": 0.0
        }

    ]
}
```

- **GET** ```api/v1/private/order/list/history_orders```

**需要权限:** 合约交易读取权限

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**

| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | false  | 合约名|
| states  | string  | false  | 订单状态,1:待报,2未完成,3已完成,4已撤销,5无效;多个用 ',' 隔开|
| category  | int  | false  | 订单类别,1:限价委托,2:强平代管委托,4:ADL减仓|
| start_time  | long  | false  | 开始时间，开始时间和结束时间的跨度一次最大只能查90天，不传时间默认返回最近7天的数据|
| end_time  | long  | false  | 结束时间，开始时间和结束时间的跨度一次最大只能查90天|
| side  | int  | false  | 订单方向 1开多,2平空,3开空,4平多  |
| page_num  | int  | true  | 当前页数,默认为1  |
| page_size  | int  | true  | 每页大小,默认20,最大100  |

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| code | integer | 状态码 | 
| message | string | 错误描述（如有） | 
| <data> | array |  | 
| orderId  | long  | 订单id |
| symbol  | string  | 合约名 |
| positionId  | long  | 持仓id |
| price  | decimal  | 委托价格 |
| vol  | decimal  | 委托数量 |
| leverage  | long  | 杠杆倍数 |
| side  | int  | 订单方向 1开多,2平空,3开空,4平多 |
| category  | int  | 订单类别:1限价委托,2强平代管委托,4ADL减仓 |
| orderType  | int  | 1:限价单,2:Post Only只做Maker,3:立即成交或立即取消,4:全部成交或者全部取消，5:市价单,6:市价转现价|
| dealAvgPrice  | decimal  | 成交均价 |
| dealVol  | decimal   | 成交数量 |
| orderMargin  | decimal   | 委托保证金  |
| takerFee  | decimal   | 买单手续费 |
| makerFee  | decimal   | 卖单手续费 |
| profit  | decimal   | 平仓盈亏 |
| feeCurrency  | string   | 收费币种 |
| openType  | int   | 开仓类型,1逐仓,2全仓 |
| state  | int   | 订单状态,1:待报,2未完成,3已完成,4已撤销,5无效 |
| errorCode  | int   | 错误code,0:正常，1：参数错误，2：账户余额不足，3：仓位不存在，4：仓位可用持仓不足，5：多仓时， 委托价小于了强平价，空仓时， 委托价大于了强平价，6：开多时， 强平价大于了合理价，开空时， 强平价小于了合理价 |
| externalOid  | string   | 外部订单号 |
| usedMargin  | decimal   | 已经使用的保证金  |
| createTime  | date   | 创建时间 |
| updateTime  | date   | 修改时间 |
| stopLossPrice  | decimal   | 止损价 |
| takeProfitPrice  | decimal   | 止盈价 |
| </data> |  |  | 

## 根据外部号查询订单

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": {
        "orderId": "102015012431820288",
        "symbol": "ETH_USDT",
        "positionId": 1394917,
        "price": 1209.05,
        "vol": 1,
        "leverage": 0,
        "side": 2,
        "category": 1,
        "orderType": 5,
        "dealAvgPrice": 1208.35,
        "dealVol": 1,
        "orderMargin": 0,
        "takerFee": 0.0072501,
        "makerFee": 0,
        "profit": 0,
        "feeCurrency": "USDT",
        "openType": 1,
        "state": 3,
        "externalOid": "_m_f95eb99b061d4eef8f64a04e9ac4dad3",
        "errorCode": 0,
        "usedMargin": 0,
        "createTime": 1609992674000,
        "updateTime": 1609992674000
    }
}
```

- **GET** ```api/v1/private/order/external/{symbol}/{external_oid}```

**需要权限:** 合约交易读取权限

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | 合约名|
| external_oid  | string  | true  | 外部订单号|

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| orderId  | long  | 订单id |
| symbol  | string  | 合约名 |
| positionId  | long  | 持仓id |
| price  | decimal  | 委托价格 |
| vol  | decimal  | 委托数量 |
| leverage  | long  | 杠杆倍数 |
| side  | int  | 订单方向 1开多,2平空,3开空,4平多 |
| category  | int  | 订单类别:1限价委托,2强平代管委托,3代管平仓委托,4ADL减仓 |
| orderType  | int  | 1:限价单,2:Post Only只做Maker,3:立即成交或立即取消,4:全部成交或者全部取消，5:市价单,6:市价转现价|
| dealAvgPrice  | decimal  | 成交均价 |
| dealVol  | decimal   | 成交数量 |
| orderMargin  | decimal   | 委托保证金  |
| takerFee  | decimal   | 买单手续费 |
| makerFee  | decimal   | 卖单手续费 |
| profit  | decimal   | 平仓盈亏 |
| feeCurrency  | string   | 收费币种 |
| openType  | int   | 开仓类型,1逐仓,2全仓 |
| state  | int   | 订单状态,1:待报,2未完成,3已完成,4已撤销,5无效 |
| externalOid  | string   | 外部订单号 |
| createTime  | date   | 创建时间 |
| updateTime  | date   | 修改时间 |

## 根据订单号查询订单

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": {
        "orderId": "102015012431820288",
        "symbol": "ETH_USDT",
        "positionId": 1394917,
        "price": 1209.05,
        "vol": 1,
        "leverage": 0,
        "side": 2,
        "category": 1,
        "orderType": 5,
        "dealAvgPrice": 1208.35,
        "dealVol": 1,
        "orderMargin": 0,
        "takerFee": 0.0072501,
        "makerFee": 0,
        "profit": 0,
        "feeCurrency": "USDT",
        "openType": 1,
        "state": 3,
        "externalOid": "_m_f95eb99b061d4eef8f64a04e9ac4dad3",
        "errorCode": 0,
        "usedMargin": 0,
        "createTime": 1609992674000,
        "updateTime": 1609992674000
    }
}
```

- **GET** ```api/v1/private/order/get/{order_id}```

**需要权限:** 合约交易读取权限

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| order_id  | long  | true  | 订单号|

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| orderId  | long  | 订单id |
| symbol  | string  | 合约名 |
| positionId  | long  | 持仓id |
| price  | decimal  | 委托价格 |
| vol  | decimal  | 委托数量 |
| leverage  | long  | 杠杆倍数 |
| side  | int  | 订单方向 1开多,2平空,3开空,4平多 |
| category  | int  | 订单类别:1限价委托,2强平代管委托,3代管平仓委托,4ADL减仓 |
| orderType  | int  | 1:限价单,2:Post Only只做Maker,3:立即成交或立即取消,4:全部成交或者全部取消，5:市价单,6:市价转现价|
| dealAvgPrice  | decimal  | 成交均价 |
| dealVol  | decimal   | 成交数量 |
| orderMargin  | decimal   | 委托保证金  |
| takerFee  | decimal   | 买单手续费 |
| makerFee  | decimal   | 卖单手续费 |
| profit  | decimal   | 平仓盈亏 |
| feeCurrency  | string   | 收费币种 |
| openType  | int   | 开仓类型,1逐仓,2全仓 |
| state  | int   | 订单状态,1:待报,2未完成,3已完成,4已撤销,5无效 |
| externalOid  | string   | 外部订单号 |
| createTime  | date   | 创建时间 |
| updateTime  | date   | 修改时间 |

## 根据订单号批量查询订单

- **GET** ```/api/v1/private/order/batch_query```

**需要权限:** 合约交易读取权限

<aside class="notice">
限速规则: 5次/2秒 
</aside>

**请求参数:**
	
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| order_ids  | long  | true  | 订单号数组，可使用逗号隔开例如:order_ids = 1,2,3(最大50个订单):|

**响应参数:**
	
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| orderId  | long  | 订单id |
| symbol  | string  | 合约名 |
| positionId  | long  | 持仓id |
| price  | decimal  | 委托价格 |
| vol  | decimal  | 委托数量 |
| leverage  | long  | 杠杆倍数 |
| side  | int  | 订单方向 1开多,2平空,3开空,4平多 |
| category  | int  | 订单类别:1限价委托,2强平代管委托,3代管平仓委托,4ADL减仓 |
| orderType  | int  | 1:限价单,2:Post Only只做Maker,3:立即成交或立即取消,4:全部成交或者全部取消，5:市价单,6:市价转现价|
| dealAvgPrice  | decimal  | 成交均价 |
| dealVol  | decimal   | 成交数量 |
| orderMargin  | decimal   | 委托保证金  |
| takerFee  | decimal   | 买单手续费 |
| makerFee  | decimal   | 卖单手续费 |
| profit  | decimal   | 平仓盈亏 |
| feeCurrency  | string   | 收费币种 |
| openType  | int   | 开仓类型,1逐仓,2全仓 |
| state  | int   | 订单状态,1:待报,2未完成,3已完成,4已撤销,5无效 |
| externalOid  | string   | 外部订单号 |
| createTime  | date   | 创建时间 |
| updateTime  | date   | 修改时间 |

## 根据订单号获取订单成交明细

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": [
        {
            "id": "159274416",
            "symbol": "ETH_USDT",
            "side": 2,
            "vol": 1,
            "price": 1208.35,
            "feeCurrency": "USDT",
            "fee": 0.0072501,
            "timestamp": 1609992674000,
            "profit": 0,
            "category": 1,
            "orderId": "102015012431820288",
            "taker": true
        }
    ]
}
```

- **GET** ```api/v1/private/order/deal_details/{order_id}```

**需要权限:** 合约交易读取权限

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| order_id  | long  | true  | 订单id|

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| id  | long  | 成交id |
| symbol  | string  | 合约名 |
| side  | int  | 订单方向 1开多,2平空,3开空,4平多 |
| vol  | decimal  | 成交数量|
| price  | decimal   | 成交价格 |
| fee  | decimal   | 手续费 |
| feeCurrency  | string   | 收费币种 |
| profit  | decimal   | 盈利 |
| isTaker  | boolean   | 是否为taker单|
| category  | int   | 订单类别:1限价委托,2强平代管委托,4ADL减仓 |
| orderId  | long   | 订单id |
| timestamp  | long   | 成交时间时间 |

## 获取用户所有订单成交明细

> 响应示例

```json
{
    "success": false,
    "code": 0,
    "message": "",
    "data": [{
        "id": 0,
        "symbol": "",
        "side": 0,
        "vol": 0.0,
        "price": 0.0,
        "feeCurrency": "",
        "fee": 0.0,
        "timestamp": "",
        "profit": 0.0,
        "isTaker": false,
        "category": 0,
        "orderId": 0,
        "opponentOrderId": 0,
    }]
}
```

- **GET** ```api/v1/private/order/list/order_deals```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**

| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | 合约名|
| start_time  | long  | false  | 开始时间，不传默认为向前推7天的时间，传了时间，最大跨度为90天|
| end_time  | long  | false  | 结束时间，开始和结束时间的跨度为90天|
| page_num  | int  | true  | 当前页数,默认为1  |
| page_size  | int  | true  | 每页大小,默认20,最大100  |

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| code | integer | 状态码 | 
| message | string | 错误描述（如有） | 
| <data> | array |  | 
| id  | long  | 成交订单id |
| symbol  | string  | 合约名 |
| side  | int  | 订单方向 1开多,2平空,3开空,4平多 |
| vol  | decimal  | 成交数量|
| price  | decimal   | 成交价格 |
| fee  | decimal   | 手续费 |
| feeCurrency  | string   | 收费币种 |
| profit  | decimal   | 盈利 |
| isTaker  | boolean   | 是否为taker单|
| category  | int   | 订单类别:1限价委托,2强平代管委托,4ADL减仓 |
| orderId  | long   | 订单id |
| timestamp  | long   | 成交时间时间 |
| </data> |  |  | 

## 获取计划委托订单列表

> 响应示例

```json
{
    "success": false,
    "code": 0,
    "message": "",
    "data": [{
            "id": 0,
            "symbol": "",
            "leverage": 0,
            "side": 0,
            "triggerPrice": 0.0,
            "price": 0.0,
            "vol": 0.0,
            "openType": 0,
            "triggerType": 0,
            "state": 0,
            "executeCycle": 0,
            "trend": 0,
            "orderType": 0,
            "orderId": 0,
            "errorCode": 0,
            "createTime": "",
            "updateTime": ""
        }

    ]
}
```

- **GET** ```api/v1/private/planorder/list/orders```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**

| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | false  | 合约名|
| states  | string  | false  | 状态,1:未触发,2:已取消,3:已执行,4:已失效,5:执行失败;多个用 ',' 隔开|
| start_time  | long  | false  | 开始时间，开始时间和结束时间的跨度一次最大只能查90天，不传时间默认返回最近7天的数据|
| end_time  | long  | false  | 结束时间，开始时间和结束时间的跨度一次最大只能查90天|
| page_num  | int  | true  | 当前页数,默认为1  |
| page_size  | int  | true  | 每页大小,默认20,最大100  |

**响应参数:**

| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| code | integer | 状态码 | 
| message | string | 错误描述（如有） | 
| <data> | array |  | 
| id  | int  | 计划委托订单id |
| symbol  | string  | 合约名|
| leverage  | decimal   | 杠杆倍数 |
| side  | string   | 订单方向, 1开多,3开空 |
| triggerPrice  | decimal   | 触发价 |
| price  | decimal   | 执行价格 |
| vol  | decimal   | 下单数量 |
| openType  | int   | 开仓类型,1:逐仓,2:全仓 |
| triggerType  | int   | 触发类型,1:大于等于，2:小于等于 |
| state  | int   | 状态,1:未触发,2:已取消,3:已执行,4:已失效,5:执行失败 |
| executeCycle  | int   | 执行周期,单位:小时 |
| trend  | int   | 触发价格类型,1:最新价，2:合理价，3:指数价 |
| errorCode  | int   | 执行失败时错误码，0：正常|
| orderId  | long   | 订单id,执行成功时返回 |
| orderType  | int   | 订单类型,1:限价单,2:Post Only只做Maker,3:立即成交或立即取消,4:全部成交或者全部取消,5:市价单 |
| createTime  | long   | 创建时间 |
| updateTime  | long   | 修改时间 |
| </data> |  |  | 

## 获取止盈止损订单列表

> 响应示例

```json
{
    "success": false,
    "code": 0,
    "message": "",
    "data": [{
        "id": 0,
        "orderId": 0,
        "symbol": "",
        "positionId": 0,
        "stopLossPrice": 0.0,
        "takeProfitPrice": 0.0,
        "state": 0,
        "triggerSide": 0,
        "positionType": 0,
        "vol": 0.0,
        "realityVol": 0.0,
        "placeOrderId": 0,
        "errorCode": 0,
        "version": 0,
        "isFinished": 0,
        "createTime": "",
        "updateTime": ""
    }]
}
```

- **GET** ```api/v1/private/stoporder/list/orders```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | false  | 合约名|
| is_finished  | int  | false  | 终态标识:0:未完成，1:已完成|
| start_time  | long  | false  | 开始时间，开始时间和结束时间的跨度一次最大只能查90天，不传时间默认返回最近7天的数据|
| end_time  | long  | false  | 结束时间，开始时间和结束时间的跨度一次最大只能查90天|
| page_num  | int  | true  | 当前页数,默认为1  |
| page_size  | int  | true  | 每页大小,默认20,最大100  |

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| code | integer | 状态码 | 
| message | string | 错误描述（如有） | 
| <data> | array |  | 
| id  | long  | 止盈止损委托单id |
| symbol  | string  | 合约名|
| orderId  | long   | 限价订单id，如果是根据仓位下的，该值为0 |
| positionId  | long   | 仓位id |
| stopLossPrice  | decimal   | 止损价 |
| takeProfitPrice  | decimal   | 止盈价 |
| state  | int   | 状态,1:未触发,2:已取消,3:已执行,4:已失效,5:执行失败 |
| triggerSide  | int   | 触发方向，0:未触发,1:止盈，2:止损 |
| positionType  | int   | 仓位类型,1:多仓，2:空仓 |
| vol  | decimal   | 委托数量 |
| realityVol  | decimal   | 实际下单数量 |
| placeOrderId  | long   | 委托成功后订单id |
| errorCode  | int   | 错误码,0:正常，其他见错误码详情 |
| isFinished  | int   | 订单状态是否为终态标识（用于查询）,0.非终态，1.终态 |
| version  | int   | 版本号|
| createTime  | long   | 创建时间 |
| updateTime  | long   | 修改时间 |
| </data> |  |  | 

## 获取止盈止损订单执行明细

- **GET** ```api/v1/private/stoporder/order_details/{stop_order_id}```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**

| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| stop_order_id  | long  | true  | 止盈止损订单id|

**响应参数:**

| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| id  | long  | 明细id |
| stopOrderId  | long  | 止盈止损订单id|
| positionId  | long  | 仓位id|
| orderId  | long   | 限价订单id |
| symbol  | string  | 合约名|
| stopLossPrice  | decimal   | 止损价 |
| takeProfitPrice  | decimal   | 止盈价 |
| state  | int   | 状态,0:未触发,3:已执行，5：已撤销，6：执行失败|
| vol  | decimal   | 委托量 |
| realityVol  | decimal   | 实际下单数量 |
| triggerPrice  | decimal   | 触发价(等于止盈为止盈，等于止损为止损,为空未触发) |
| placeOrderId  | long   | 下单id|
| errorCode  | int   | 0:正常，其他参考错误码 |
| positionType  | int   | 仓位类型,1:多仓，2:空仓 |
| createTime  | long   | 创建时间 |
| updateTime  | long   | 修改时间 |

## 获取风险限额

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": {
        "BTC_USDT": [
            {
                "level": 1,
                "maxVol": 150000,
                "maxLeverage": 125,
                "mmr": 0.004,
                "imr": 0.008,
                "symbol": "BTC_USDT",
                "positionType": 2
            },
            {
                "level": 1,
                "maxVol": 150000,
                "maxLeverage": 125,
                "mmr": 0.004,
                "imr": 0.008,
                "symbol": "BTC_USDT",
                "positionType": 1
            }
        ]
    }
}
```

- **GET** ```api/v1/private/account/risk_limit```

**需要权限:** 合约交易读取权限

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | false  | 合约名,不传返回所有|

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| symbol  | string  | 合约名 |
| positionType  | int  | 持仓类型 1:多仓，2:空仓|
| level  | int   | 当前风险等级 |
| maxVol  | decimal   | 最大可持仓数量 |
| maxLeverage  | int   | 最大杠杆倍数 |
| mmr  | decimal   | 维持保证金率 |
| imr  | decimal   | 初始保证金率 |

## 获取用户当前手续费率

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": {
        "level": 0,
        "dealAmount": 1786.2594,
        "walletBalance": 0.03176562,
        "makerFee": 0.0002,
        "takerFee": 0.0006,
        "makerFeeDiscount": 1,
        "takerFeeDiscount": 1
    }
}
```

- **GET** ```api/v1/private/account/tiered_fee_rate```

**需要权限:** 合约交易读取权限

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | 合约名|

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| level  | int  | 阶梯费率等级 |
| dealAmount  | int  | 近30天成交额|
| walletBalance  | int   | 昨日钱包余额 |
| makerFee  | decimal   | makerFee |
| takerFee  | int   | takerFee |
| makerFeeDiscount  | decimal   | makerFee折扣 |
| takerFeeDiscount  | decimal   | takerFee折扣 |

## 增加或减少仓位保证金

> 响应示例

```json
{
    "success": true,
    "code": 0
}
```

- **POST** ```api/v1/private/position/change_margin```

**需要权限:** 合约交易权限

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| positionId  | long  | true  | 仓位id|
| amount  | decimal  | true  | 金额|
| type  | string  | true  | 类型,ADD:增加,SUB:减少|

**响应参数:**

公共参数,success: true成功,false失败

## 获取持仓杠杆倍数

- **GET** ```api/v1/private/position/leverage```

**需要权限:** 合约交易权限

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**

| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | 合约名称|


**响应参数:**

| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| positionType  | int  |  仓位类型， 1多 2空 |
| level  | int  | 杠杆风险限额等级 |
| imr  | decimal  | 杠杆风险限额等级对应初始保证金率|
| mmr  | decimal   | 杠杆风险限额等级对应维持保证金率 |
| leverage  | int  | 杠杆倍数|

## 修改杠杆倍数

- **POST** ```api/v1/private/position/change_leverage```

**需要权限:** 合约交易权限

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| positionId  | long  | false  | 仓位id，当存在仓位时，传入|
| leverage  | int  | true  | 杠杆倍数|
| openType  | int  | false  | 当不存在仓位时必需，开仓类型,1:逐仓,2:全仓|
| symbol  | string  | false  | 当不存在仓位时必需，合约名称 |
| positionType  | int  | false  |当不存在仓位时必需，  仓位类型， 1多 2空|

**响应参数:**

公共参数,success: true成功,false失败

**请求参数示例:**
   - 有仓位时：
    ```
    {
      "positionId": 1,
      "leverage": 20
    }
    ```
   - 无仓位时：
    ```
    {
      "openType": 1,
      "leverage": 20,
      "symbol": "BTC_USDT",
      "positionType": 1 
    }
    ```

## 获取用户仓位模式

- **GET** ```api/v1/private/position/position_mode```

**需要权限:** 合约交易权限

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
无


**响应参数:**

公共参数,success: true成功,false失败
1:双向持仓模式,2:单向持仓模式

**请求参数示例:**

    ```
    {"success":true,"code":0,"data":1}
    {"success":true,"code":0,"data":2}
    ```


## 修改用户仓位模式

- **POST** ```api/v1/private/position/change_position_mode```

**需要权限:** 合约交易权限

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| positionMode  | int  | true  | 1:双向，2：单向，修改仓位模式必须保证没有活跃订单、计划委托单、未完成仓位，否则无法修改。双向切换单向模式时，风险限额等级会重置为等级1，如需更改调用接口修改|


**响应参数:**

公共参数,success: true成功,false失败

**请求参数示例:**
    ```
    {"success":true,"code":0}
    ```

## 下单

> 响应示例

```json
{
    "success": true,
    "code": 0,
    "data": 102057569836905984
}
```

USDT永续合约交易提供了限价单和市价单下单模式。只有当您的账户有足够的资金才能下单。一旦下单，您的账户资金将在订单生命周期内被冻结。被冻结的资金以及数量取决于订单指定的类型和参数。

- **POST** ```api/v1/private/order/submit```

**需要权限:** 合约交易权限

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | 合约名|
| price  | decimal  | true  | 价格|
| vol  | decimal  | true  | 数量|
| leverage  | int  | false  | 杠杆倍数，逐仓时杠杆倍数必须传入 |
| side  | int  | true  | 订单方向 1开多，2平空，3开空，4平多|
| type  | int  | true  | 订单类型，1：限价单，2：Post Only只做Maker，3：立即成交或立即取消，4：全部成交或者全部取消，5：市价单，6：市价转现价|
| openType  | int  | true  | 开仓类型，1：逐仓，2：全仓|
| positionId  | long  | false  | 仓位id，平仓时建议传入该参数|
| externalOid  | string  | false  | 外部订单号|
| stopLossPrice  | decimal  | false  | 止损价|
| takeProfitPrice  | decimal  | false  | 止盈价 |
| positionMode  | int  | false  | 1:双向持仓，2:单向持仓，默认为1|
| reduceOnly  | boolean  | false  | 默认为false,单向持仓如果需要只减仓时传入true，双向持仓不受理此参数|

**响应参数:**

成功时,success =true,data值为订单id,success =false,失败data=null

## 批量下单

> 示例

```json
[
  {
    "symbol": "BTC_USD",
    "price": 8800,
    "vol": 100,
    "leverage": 20,
    "side": 1,
    "type": 1,
    "openType": 1,
    "externalOid": "order1"
  },
  {
    "symbol": "BTC_USD",
    "price": 500,
    "vol": 100,
    "leverage": 50,
    "side": 3,
    "type": 1,
    "openType": 1,
    "externalOid": "order2"
  }
]
```

批量进行合约下单操作。每个合约可批量下50个单。该接口暂未开放给所有用户，需要联系客服开通权限。

- **POST** ```api/v1/private/order/submit_batch```

**需要权限:** 合约交易权限

<aside class="notice">
限速规则: 1次/2秒
</aside>

**请求参数:**(最大50条)
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | 合约名|
| price  | decimal  | true  | 价格|
| vol  | decimal  | true  | 数量|
| leverage  | int  | false  | 杠杆倍数，逐仓时杠杆倍数必须传入|
| side  | int  | true  | 订单方向 1开多，2平空，3开空，4平多|
| type  | int  | true  | 订单类型，1：限价单，2：Post Only只做Maker，3：立即成交或立即取消，4：全部成交或者全部取消，5：市价单，6：市价转现价|
| openType  | int  | true  | 开仓类型，1：逐仓，2：全仓|
| positionId  | long  | false  | 仓位id，平仓时建议传入该参数|
| externalOid  | string  | false  | 外部订单号，如果已存在，返回已存在的订单id|
| stopLossPrice  | decimal  | false  | 止损价|
| takeProfitPrice  | decimal  | false  | 止盈价|

**响应参数:**
    
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| externalOid  | string  | 外部订单号 |
| orderId  | long  | 订单id,失败时为null  |
| errorMsg  | string  | 错误信息，失败时不为空|
| errorCode  | int  | 错误code，默认为0|

## 取消订单

> 响应示例

```json
{
 "success":true,
 "code":0,
 "data":[
 {
 "orderId":101716841474621953,
 "errorCode":2040,
 "errorMsg":"order not exist"
 },
 {
 "orderId":108885377779302912,
 "errorCode":2041,
 "errorMsg":"order state cannot be cancelled"
 },
 {
 "orderId":108886241042563584,
 "errorCode":0,
 "errorMsg":"success"
 }
 ]
}
```

撤销之前下的未完成订单，每次最多可撤50个单。

- **POST** ```api/v1/private/order/cancel```

**需要权限:** 合约交易权限

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| 无  | List<Long>  | true  | 订单id列表,最大50条| 

**响应参数:**

| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| orderId  | long  | 订单id  |
| errorMsg  | string  | 错误原因|
| errorCode  | int  | 错误码，非0即是撤单失败|

## 根据外部订单号取消订单

> 参数示例

```json
{
    "symbol":"BTC_USDT",
    "externalOid":"mexc-a-001"
}
```

根据指定的externalOid撤销某个合约的未完成订单，每次最多可撤1个单。

- **POST** ```api/v1/private/order/cancel_with_external```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**

| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | 合约名|
| externalOid  | string  | true  | 外部订单号|

## 取消某合约下所有订单

撤销某个合约下的所有未完成订单。

- **POST** ```api/v1/private/order/cancel_all```

**需要权限:** 合约交易权限

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | false| 合约名,传入symbol只取消该合约下的订单，不传取消所有合约下的订单|

**响应参数:**

公共参数,success: true成功,false失败

## 修改风险等级

\- **POST** ```api/v1/private/account/change_risk_level```

\- 已禁用 调用是返回错误码 8817 提示信息：风险限制功能已升级，详情请前往web端查看

## 计划委托下单

- **POST** ```api/v1/private/planorder/place```

<aside>
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | 合约名|
| price  | decimal  | false  | 执行价，市价时可不传|
| vol  | decimal  | true  | 数量|
| leverage  | int  | false  | 杠杆倍数，逐仓时杠杆倍数必须传入|
| side  | int  | true  | 订单类型 1开多，2平空，3开空，4平多|
| openType  | int  | true  | 开仓类型 1逐仓，2全仓|
| triggerPrice  | decimal  | true  | 触发价|
| triggerType  | int  | true  | 触发类型，1：大于等于，2：小于等于|
| executeCycle  | int  | true  | 执行周期，1：24小时，2：7天|
| orderType  | int  | true  | 订单类型，1：限价单，2：Post Only只做Maker，3：立即成交或立即取消，4：全部成交或者全部取消，5：市价单|
| trend  | int  | true  | 触发价格类型，1：最新价，2：合理价，3：指数价|

**响应参数:**

成功时,success =true,data值为订单id,success =false,失败data=null

## 取消计划委托订单

> 响应示例:

```json
[
  {
    "symbol": "BTC_USDT",
    "orderId": 1
  },
  {
    "symbol": "ETH_USDT",
    "orderId": 2
  }
]
```

- **POST** ```api/v1/private/planorder/cancel```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| 无  | List<CancelOrderRequest>  | true  | 取消订单列表,最大50条|

**CancelOrderRequest:**

| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  |string  | true  | 合约名|
| orderId  |string  | true  | 订单id|

**响应参数:**

公共参数,success: true成功,false失败

## 取消所有计划委托订单

- **POST** ```api/v1/private/planorder/cancel_all```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**
    
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | false  | 合约名，传入symbol只取消该合约下的订单，不传取消所有合约下的订单|

**响应参数:**

公共参数,success: true成功,false失败

## 取消止盈止损委托单

> 示例:

```json
[
  {
    "stopPlanOrderId": 1
  },
  {
    "stopPlanOrderId": 2
  }
]
```

- **POST** ```api/v1/private/stoporder/cancel```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**

| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| 无  | List<CancelOrderRequest>  | true  | 取消订单列表,最大50条|

**CancelOrderRequest:**

| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| stopPlanOrderId  |long  | true  | 止盈止损委托单id|

**响应参数:**

公共参数,success: true成功,false失败

## 取消所有止盈止损委托单

- **POST** ```api/v1/private/stoporder/cancel_all```

<aside>
限速规则: 20次/2秒
</aside>

**请求参数:**
      
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| positionId  | long  | false  | 仓位id,传入positionId，只取消对应仓位的委托单，不传则判断symbol|
| symbol  | string  | false  | 合约名,传入symbol只取消该合约下的委托单，不传取消所有合约下的委托单|

**响应参数:**

公共参数,success: true成功,false失败

## 修改限价单止盈止损价格

- **POST** ```api/v1/private/stoporder/change_price```

<aside class="notice">
限速规则: 20次/2秒
</aside>

**请求参数:**

| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| orderId  | long  | true  | 限价单订单id|
| stopLossPrice  | decimal  | false  | 止损价，止盈价和止损价同时为空或者同时为0时，则表示取消订单的止盈止损|
| takeProfitPrice  | decimal  | false  | 止盈价，止盈价和止损价同时为空或者同时为0时，则表示取消订单的止盈止损|

**响应参数:**

公共参数,success: true成功,false失败

## 修改止盈止损委托单止盈止损价格

- **POST** ```api/v1/private/stoporder/change_plan_price```

<aside>
限速规则: 20次/2秒
</aside>

**请求参数:**
       
| 参数名  | 类型  | 是否必填  |  说明 |
| ------------ | ------------ | ------------ | ------------ |
| stopPlanOrderId  | long  | true  | 止盈止损委托单订单id|
| stopLossPrice  | decimal  | false  | 止损价,和止盈价至少有一个不为空，且必须大于0|
| takeProfitPrice  | decimal  | false  | 止盈价,和止损价至少有一个不为空，且必须大于0|

**响应参数:**

公共参数,success: true成功,false失败

# WebSocket API

WebSocket是HTML5一种新的协议（Protocol）。它实现了客户端与服务器全双工通信，使得数据可以快速地双向传播。通过一次简单的握手就可以建立客户端和服务器连接，服务器根据业务规则可以主动推送信息给客户端。其优点如下：

1. 客户端和服务器进行数据传输时，请求头信息比较小，大概2个字节。
2. 客户端和服务器皆可以主动地发送数据给对方。
3. 不需要多次创建TCP请求和销毁，节约宽带和服务器的资源。

<aside class="notice">
强烈建议开发者使用WebSocket API获取市场行情和买卖深度等信息。
</aside>

## 原生ws连接地址

- wss://contract.mexc.com/ws

## 数据交互命令详解

> 发送ping消息

```json
{
  "method": "ping"
}
```

> 服务端返回

```json
{
  "channel": "pong",
  "data": 1587453241453
}
```

订阅/取消订阅数据命令列表（除个人相关命令列表之外，其余都不需要做ws认证）

1分钟以内未收到客户端ping，将断开该客户端连接，建议10~20秒发送一次ping

发送ping消息及服务端返回见右侧

## 订阅过滤

> 取消默认推送示例

```json
{
	"subscribe": false,
	"method": "login",
	"param": {
		"apiKey": "mxU1TzSmRDW1o5AsE",
		"signature": "8c957a757ea31672eca05cb652d26bab7f46a41364adb714dda5475264aff120",
		"reqTime": "1611038237237"
	}
}
```

> 只要资产

```json
{
    "method":"personal.filter",
    "param":{
        "filters":[
            {
                "filter":"asset"
            }
        ]
    }
}
```

> 只要ADL等级

```json
{
    "method":"personal.filter",
    "param":{
        "filters":[
            {
                "filter":"adl.level"
            }
        ]
    }
}
```

> 只要所有的成交单

```json
{
    "method":"personal.filter",
    "param":{
        "filters":[
            {
                "filter":"order.deal",
                "rules":[]
            }
        ]
    }
}
```

> 或者

```json
{
    "method":"personal.filter",
    "param":{
        "filters":[
            {
                "filter":"order.deal"
            }
        ]
    }
}
```

> 只要单个合约的成交单

```json
{
    "method":"personal.filter",
    "param":{
        "filters":[
            {
                "filter":"order.deal",
                "rules":[
                    "BTC_USDT"
                ]
            }
        ]
    }
}
```

> 混合使用

```json
{
    "method":"personal.filter",
    "param":{
        "filters":[
            {
                "filter":"order",
                "rules":[
                    "BTC_USDT"
                ]
            },
            {
                "filter":"order.deal",
                "rules":[
                    "EOS_USDT",
                    "ETH_USDT",
                    "BTC_USDT"
                ]
            },
            {
                "filter":"position",
                "rules":[
                    "EOS_USDT",
                    "BTC_USDT"
                ]
            },
            {
                "filter":"asset"
            }
        ]
    }
}
```

登录之后会推送所有私有数据：order订单、order.deal成交单、position持仓、plan.order计划委托单、stop.order止盈止损单、stop.planorder止盈止损计划委托单、risk.limit风险限额、adl.level ADL等级、asset资产

1、如果要取消默认推送，登录时新加参数： ```"subscribe":false，默认为true```;

2、登录之后通过发送 ```personal.filter``` 事件来过滤自己需要的数据，如果想要恢复推送所有数据，可发送： ```{"method":"personal.filter"}``` 或者 ```{"method":"personal.filter","param":{"filters":[]}}```

3、filter可用key：order、order.deal、position、plan.order、stop.order、stop.planorder、risk.limit、adl.level、asset 固定值，不可更改，若有错误会提示

其中asset和adl.level不支持过滤单个币种或者单个合约，其他均可以过滤单个合约

后面发送的filter事件会覆盖前面的

## 公共频道

### Tickers

> 订阅

```json
{
  "method": "sub.tickers",
  "param": {}
} 
```

> 如需返回明文(后面订阅一样):

```json
{
  "method": "sub.tickers",
  "param": {},
  "gzip": false
} 
```

> 取消订阅

```json
{
  "method": "unsub.tickers",
  "param": {}
} 
```

> 数据示例

```json
{
  "channel": "push.tickers",
  "data": [
    {
      "fairPrice": 183.01,
      "lastPrice": 183,
      "riseFallRate": -0.0708,
      "symbol": "BSV_USDT",
      "volume24": 200
    },
    {
      "fairPrice": 220.22,
      "lastPrice": 220.4,
      "riseFallRate": -0.0686,
      "symbol": "BCH_USDT",
      "volume24": 200
    }
  ],
  "ts": 1587442022003
} 
```

获取平台全部永续合约的最新成交价、买一价、卖一价和24交易量，无需用户登录，订阅后1秒发送一次。

订阅、取消订阅、数据示例见右侧。

**响应参数:**
	
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| symbol  | string | 合约名 |
| lastPrice  | decimal  | 最新价 |
| volume24  | decimal  | 24小时成交量，按张数统计 |
| riseFallRate  | decimal  | 涨跌幅 |
| fairPrice  | decimal  | 合理价 |

### 获取单个ticker

> 订阅

```json
{
    "method":"sub.ticker",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> 取消订阅

```json
{
    "method":"unsub.ticker",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> 数据示例

```json
{
    "channel":"push.ticker",
    "data":{
        "ask1":6866.5,
        "bid1":6865,
        "contractId":1,
        "fairPrice":6867.4,
        "fundingRate":0.0008,
        "high24Price":7223.5,
        "indexPrice":6861.6,
        "lastPrice":6865.5,
        "lower24Price":6756,
        "maxBidPrice":7073.42,
        "minAskPrice":6661.37,
        "riseFallRate":-0.0424,
        "riseFallValue":-304.5,
        "symbol":"BTC_USDT",
        "timestamp":1587442022003,
        "holdVol":2284742,
        "volume24":164586129
    },
    "symbol":"BTC_USDT",
    "ts":1587442022003
}
```

获取某个合约的最新成交价、买一价、卖一价和24交易量，无需用户登录，有成交数据就推送，订阅后1秒发送一次。

订阅、取消订阅、数据示例见右侧。

**响应参数:**
	
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| symbol  | string | 合约名 |
| lastPrice  | decimal  | 最新价 |
| bid1  | decimal  | 买一价 |
| ask1  | decimal  | 卖一价 |
| volume24  | decimal  | 24小时成交量，按张数统计 |
| holdVol| decimal  | 总持仓量 |
| lower24Price  | decimal  | 24小时最低价 |
| high24Price  | decimal  | 24小时内最高价 |
| riseFallRate  | decimal  | 涨跌幅 |
| riseFallValue  | decimal  | 涨跌额 |
| indexPrice  | decimal  | 指数价格 |
| fairPrice  | decimal  | 合理价 |
| fundingRate  | decimal  | 资金费率 |
| timestamp  | long   | 系统时间戳 |

### 成交

> 订阅

```json
{
    "method":"sub.deal",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> 取消订阅

```json
{
    "method":"unsub.deal",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> 数据示例

```json
{
    "channel":"push.deal",
    "data":{
        "M":1,
        "O":1,
        "T":1,
        "p":6866.5,
        "t":1587442049632,
        "v":2096
    },
    "symbol":"BTC_USDT",
    "ts":1587442022003
}
```

获取最近的成交数据，无需用户登录，有成交数据就推送。

订阅、取消订阅、数据示例见右侧。

**响应参数:**
	
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| p  | decimal  | 成交价 |
| v  | decimal  | 数量 |
| T  | int  | 成交方向,1:买,2:卖 |
| O  | int   | 是否是开仓，1:是,2:否,当O为1的时候, vol是新增的持仓量 |
| M  | int   | 是否为自成交,1:是,2:否 |
| t  | long   | 成交时间|

### 深度

> 订阅增量（全部）

```json
{
    "method":"sub.depth",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> 订阅增量（压缩后推送）

```json
{
    "method":"sub.depth",
    "param":{
        "symbol":"BTC_USDT",
        "compress":true
    }
}
```

> 订阅全量（limit可取值:5、10、20，不传默认为20档，只能订阅一个档位的全量）

```json
{
    "method":"sub.depth.full",
    "param":{
        "symbol":"BTC_USDT",
        "limit":5
    }
}
```

> 取消订阅（增量的都以该事件取消订阅）

```json
{
    "method":"unsub.depth",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> 取消订阅（取消订阅全量，limit可传可不传）

```json
{
    "method":"usub.depth.full",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> 数据示例

```json
{
    "channel":"push.depth",
    "data":{
        "asks":[
            [
                6859.5,
                3251,
                1
            ]
        ],
        "bids":[
        ],
        "version":96801927
    },
    "symbol":"BTC_USDT",
    "ts":1587442022003
}
```


订阅、取消订阅、数据示例见右侧。

**响应参数:**
	
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| asks  | List<Numeric[]> |卖方深度 |
| bids  | List<Numeric[]> | 买方深度 |
| version  | long  | 版本号 |

备注: [411.8, 10, 1] 411.8为价格，10为此价格的合约张数,1为订单数量

### K线数据

> 订阅

```json
{
    "method":"sub.kline",
    "param":{
        "symbol":"BTC_USDT",
        "interval":"Min60"
    }
}
```

> 取消订阅

```json
{
    "method":"unsub.kline",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> 数据示例

```json
{
    "channel":"push.kline",
    "data":{
        "a":233.740269343644737245,
        "c":6885,
        "h":6910.5,
        "interval":"Min60",
        "l":6885,
        "o":6894.5,
        "q":1611754,
        "symbol":"BTC_USDT",
        "t":1587448800
    },
    "symbol":"BTC_USDT",
    "ts":1587442022003
}
```

获取合约的K线数据，有更新就推送。

订阅、取消订阅、数据示例见右侧。

interval可选参数:  Min1、Min5、Min15、Min30、Min60、Hour4、Hour8、Day1、Week1、Month1 

**响应参数:**
	
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| symbol  | string | 合约名 |
| a  | decimal  | 总成交金额 |
| c  | decimal  | 收盘价 |
| interval  | string  | 间隔: Min1、Min5、Min15、Min30、Min60、Hour4、Hour8、Day1、Week1、Month1 |
| l  | decimal  | 最低价 |
| o  | decimal  | 开盘价 |
| q  | decimal  | 总成交量 |
| h  | decimal  | 最高价 |
| t  | long  | 交易时间，单位：秒（s），为窗口的开始时间（windowStart） |

### 资金费率

> 订阅

```json
{
    "method":"sub.funding.rate",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> 取消订阅

```json
{
    "method":"unsub.funding.rate",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> 数据示例

```json
{
    "channel":"push.funding.rate",
    "data":{
        "rate":0.001,
        "symbol":"BTC_USDT"
    },
    "symbol":"BTC_USDT",
    "ts":1587442022003
}
```

获取合约资金费率，有更新就推送。

订阅、取消订阅、数据示例见右侧。

**响应参数:**
	
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| symbol  | string | 合约名 |
| fundingRate  | decimal  | 资金费率 |
| nextSettleTime  | long  | 下一次结算时间 |

### 指数价格

> 订阅

```json
{
    "method":"sub.index.price",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> 取消订阅

```json
{
    "method":"unsub.index.price",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> 数据示例

```json
{
    "channel":"push.index.price",
    "data":{
        "price":0.001,
        "symbol":"BTC_USDT"
    },
    "symbol":"BTC_USDT",
    "ts":1587442022003
}
```

获取指数价格，指数价格有变化时就会推送一次数据。

订阅、取消订阅、数据示例见右侧。

**响应参数:**
	
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| symbol  | string | 合约名 |
| price  | decimal  | 价格 |

### 合理价格

> 订阅

```json
{
    "method":"sub.fair.price",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> 取消订阅

```json
{
    "method":"unsub.fair.price",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> 数据示例

```json
{
    "channel":"push.fair.price",
    "data":{
        "price":0.001,
        "symbol":"BTC_USDT"
    },
    "symbol":"BTC_USDT",
    "ts":1587442022003
}
```

订阅、取消订阅、数据示例见右侧。

**响应参数**
	
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| symbol  | string | 合约名 |
| price  | decimal  | 价格 |

## 私有频道

### 登录认证

> 示例

```json
{"channel":"rs.login",
"data":"success",
"ts":"1587442022003"
}
```

```json
{
	"method":"login",
	"param":{
		"apiKey":"apiKey", // openapi需要传此参数，参数构造方式参照openapi文档
		"reqTime":"reqTime", // openapi需要传此参数，参数构造方式参照openapi文档
		"signature":"signature" // openapi需要传此参数，参数构造方式参照openapi文档
	}
}
```

**响应参数:**

成功: 无，失败:返回对应错误信息,channel = rs.error

登录成功(channel = rs.login)

### 订单

> 数据示例

```json
{
    "channel":"push.personal.order",
    "data":{
        "category":1,
        "createTime":1610005069976,
        "dealAvgPrice":0.731,
        "dealVol":1,
        "errorCode":0,
        "externalOid":"_m_95bc2b72d3784bce8f9efecbdef9fe35",
        "feeCurrency":"USDT",
        "leverage":0,
        "makerFee":0,
        "openType":1,
        "orderId":"102067003631907840",
        "orderMargin":0,
        "orderType":5,
        "positionId":1397818,
        "price":0.707,
        "profit":-0.0005,
        "remainVol":0,
        "side":4,
        "state":3,
        "symbol":"CRV_USDT",
        "takerFee":0.00004386,
        "updateTime":1610005069983,
        "usedMargin":0,
        "version":2,
        "vol":1
    },
    "ts":1610005069989
}
```

```channel = push.personal.order```

| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| orderId  | long  | 订单id |
| symbol  | string  | 合约名 |
| positionId  | long  | 持仓id |
| price  | decimal  | 委托价格 |
| vol  | decimal  | 委托数量 |
| leverage  | long  | 杠杆倍数 |
| side  | int  | 订单方向 1开多,2平空,3开空,4平多 |
| category  | int  | 订单类别:1限价委托,2强平代管委托,4ADL减仓 |
| orderType  | int  | 1:限价单,2:Post Only只做Maker,3:立即成交或立即取消,4:全部成交或者全部取消| |
| dealAvgPrice  | decimal  | 成交均价 |
| dealVol  | decimal   | 成交数量 |
| orderMargin  | decimal   | 委托保证金  |
| usedMargin  | decimal   | 已经使用的保证金  |
| takerFee  | decimal   | 买单手续费 |
| makerFee  | decimal   | 卖单手续费 |
| profit  | decimal   | 平仓盈亏 |
| feeCurrency  | string   | 收费币种 |
| openType  | int   | 开仓类型,1逐仓,2全仓 |
| state  | int   | 订单状态,1:待报,2未完成,3已完成,4已撤销,5无效 |
| errorCode  | int   | 错误code,0:正常，1：参数错误，2：账户余额不足，3：仓位不存在，4：仓位可用持仓不足，5：多仓时， 委托价小于了强平价，空仓时， 委托价大于了强平价，6：开多时， 强平价大于了合理价，开空时， 强平价小于了合理价 ,7:超过风险限额限制，8:系统撤销|
| externalOid  | string   | 外部订单号 |
| createTime  | date   | 创建时间 |
| updateTime  | date   | 修改时间 |

### 资产

> 数据示例

```json
{
    "channel":"push.personal.asset",
    "data":{
        "availableBalance":0.7514236,
        "bonus":0,
        "currency":"USDT",
        "frozenBalance":0,
        "positionMargin":0
    },
    "ts":1610005070083
}
```

```channel = push.personal.asset```

| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| currency  | string  | 币种 |
| positionMargin  | decimal   | 仓位保证金 |
| frozenBalance  | decimal   | 冻结余额 |
| availableBalance  | decimal   | 当前可用余额 |
| cashBalance  | decimal   | 可提现余 额 |

### 仓位

> 数据示例

```json
{
    "channel":"push.personal.position",
    "data":{
        "autoAddIm":false,
        "closeAvgPrice":0.731,
        "closeVol":1,
        "frozenVol":0,
        "holdAvgPrice":0.736,
        "holdFee":0,
        "holdVol":0,
        "im":0,
        "leverage":15,
        "liquidatePrice":0,
        "oim":0,
        "openAvgPrice":0.736,
        "openType":1,
        "positionId":1397818,
        "positionType":1,
        "realised":-0.0005,
        "state":3,
        "symbol":"CRV_USDT"
    },
    "ts":1610005070157
}
```

```channel = push.personal.position```
 	
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| positionId  | long  | 持仓id |
| symbol  | string  | 合约名 |
| holdVol  | decimal  | 持仓数量 |
| positionType  | int  | 仓位类型， 1多 2空 |
| openType  | int   | 开仓类型， 1逐仓 2全仓 |
| state  | int   | 仓位状态,1持仓中2系统代持3已平仓  |
| frozenVol  | decimal   | 冻结量 |
| closeVol  | decimal   | 平仓量 |
| holdAvgPrice  | decimal   | 持仓均价 |
| closeAvgPrice  | decimal   | 平仓均价 |
| openAvgPrice  | decimal   | 开仓均价 |
| liquidatePrice  | decimal   | 逐仓时的爆仓价 |
| oim  | decimal   | 原始初始保证金 |
| adlLevel  | int   | adl减仓等级,取值为 1-5，为空时需等待刷新 |
| im  | decimal   | 初始保证金， 逐仓时可以加减此项以调节爆仓价 |
| holdFee  | decimal   | 资金费, 正数表示得到，负数表示支出 |
| realised  | decimal   | 已实现盈亏 |
| createTime  | date   | 创建时间 |
| updateTime  | date   | 修改时间 |

### 风险限额

```channel = push.personal.risk.limit```
 	
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| symbol  | string  | 合约名 |
| positionType  | int  | 持仓类型 1:多仓，2:空仓|
| riskSource| int | 风险限制来源 0:其它 1:爆仓服务| 
| level  | int   | 当前风险等级 |
| maxVol  | decimal   | 最大可持仓数量 |
| maxLeverage  | int   | 最大杠杆倍数 |
| mmr  | decimal   | 维持保证金率 |
| imr  | decimal   | 初始保证金率 |

### adl自动减仓等级

> 数据示例

```json
{
    "channel":"push.personal.adl.level",
    "data":{
        "adlLevel":0,
        "positionId":1397818
    },
    "ts":1610005032231
}
```

```channel = push.personal.adl.level```
 	
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
| adlLevel| int   | 当前adl等级 ：1-5|
| positionId  | long   | 仓位id |

## 如何维护深度信息

> 例如订阅成交信息

```json
{"method":"sub.deal",
"param":{
    "symbol":"BTC_USDT"
}
}
```

> 订阅成功响应

```json
{"channel":"rs.sub.deal",
"data":"success",
"ts":"1587442022003"
}
```

> 订阅失败响应

```json
{"channel":"rs.error",
"data":"合约不存在!",
"ts":"1587442022003"
}
```
### 仓位模式

> 数据示例

```json
{
    "channel":"push.personal.position.mode",
    "data":{
        positionMode: 1
    },
    "ts":1610005070157
}
```

```channel = push.personal.position.mode```
 	
| 参数名  | 类型  | 说明  |
| ------------ | ------------ | ------------ |
|positionMode|int|仓位模式,1:双向，2:单向|


**如何维护增量深度信息:**

1. 通过接口 https://contract.mexc.com/api/v1/contract/depth/BTC_USDT获取全量深度信息，保存当前version
2. 订阅ws深度信息，收到更新后，如果收到的数据version>当前version,同一个价位，后收到的更新覆盖前面的。
3. 通过接口 https://contract.mexc.com/api/v1/contract/depth_commits/BTC_USDT/1000获取最新1000条深度快照
4. 将目前缓存的深度信息中同一价格，version<步骤3获取到的快照中的version的数据丢弃
5. 将深度快照中的内容更新至本地缓存，并从ws接收到的event开始继续更新
5. 每一个新event的version应该恰好等于上一个event的version+1，否则可能出现了丢包，如出现丢包或者获取到的event的version不连续,请从步骤3重新进行初始化。
6. 每一个event中的挂单量代表这个价格目前的挂单量绝对值，而不是相对变化。
7. 如果某个价格对应的挂单量为0，表示该价位的挂单已经撤单或者被吃，应该移除这个价位。

**订阅类事件，订阅成功响应:**  

channel 为 rs. + 订阅的method，
data为 "success"


# 错误码

## 错误码示例

每个接口都有可能抛出异常

以下为接口可能返回的错误码信息

|  错误码  |  说明  |
| ------------ | -------------------------- |
| 0     | 操作成功  |
| 9999  | 公共异常  |
| 500   | 内部错误  |
| 501   | 系统繁忙  |
| 401   | 未授权  | 
| 402   | api_key过期  |
| 406   | 访问ip不在白名单  |
| 506   | 未知的请求来源  |
| 510   | 请求过于频繁  |
| 511   | 接口禁止访问  |
| 513   | 请求无效(针对open api 请求时间>服务器时间2秒或者<服务器时间10秒以上)  |
| 600   | 参数错误  |
| 601   | 数据解析错误  |
| 602   | 验签失败  |
| 603   | 重复请求  |
| 701   | 需要账户读权限  |
| 702   | 需要账户写权限  |
| 703   | 需要交易读权限  |
| 704   | 需要交易写权限  |
| 1000  | 账户不存在  |
| 1001  | 合约不存在  |
| 1002  | 合约未启用  |
| 1003  | 风险限额等级错误  |
| 1004  | 金额错误  |
| 2001  | 订单方向错误  |
| 2002  | 开仓类型错误  |
| 2003  | 买单价格过高  |
| 2004  | 卖单价格过低  |
| 2005  | 余额不足  |
| 2006  | 杠杆倍数错误  |
| 2007  | 订单价格错误  |
| 2008  | 可平数量不足  |
| 2009  | 仓位不存在或已平仓  |
| 2011  | 订单数量错误  |
| 2013  | 取消订单数量超过最大限制  |
| 2014  | 批量下单数量超限  |
| 2015  | 价格或者数量精度错误  |
| 2016  | 计划委托超过最大委托数量  |
| 2018  | 超过最大可减保证金  |
| 2019  | 存在开仓活跃委托  |
| 2021  | 下单杠杆倍数和已有仓位杠杆倍数不一致  |
| 2022  | 持仓类型错误  |
| 2023  | 存在大于新档位最大杠杆倍数的持仓  |
| 2024  | 存在大于新档位最大杠杆倍数的订单  |
| 2025  | 当前持仓数量大于新档位最大允许数量  |
| 2026  | 全仓不支持修改杠杆  |
| 2027  | 同一方向全仓和逐仓只能存在一个  |
| 2028  | 超过最大下单数量   |
| 2029  | 订单类型错误   |
| 2030  | 外部订单id过长(最大32位长度)  |
| 2031  | 超过当前风险限额最大允许持仓数量  |
| 2032  | 下单价格小于多仓强平价  |
| 2033  | 下单价格大于空仓强平价  |
| 2034  | 批量查询数量超限  |
| 2035  | 不支持的市价单档位  |
| 3001  | 计划委托价格类型错误  |
| 3002  | 计划委托触发类型错误  |
| 3003  | 执行周期错误  |
| 3004  | 触发价格错误  |
| 4001  | 不支持的币种  |
| 2036  |  下单次数超过上限，请联系客服 |
| 2037  |  交易频繁,请稍后再试   |
| 2038  |  超过最大允许持仓数量，请联系客服!  |
| 5001  |  止盈价和止损价不能同时为空  |
| 5002  |  止盈止损单不存在或已关闭  |
| 5003  |  止盈止损价设置有误   |
| 5004  |  止盈止损单总挂单量大于仓位可平数量  |
| 6001  |  禁止交易  |
| 6002  |  禁止开仓  |
| 6003  |  时间范围错误  |
| 6004  |  必须传交易对和状态  |
| 6005  |  交易对未开放  |



