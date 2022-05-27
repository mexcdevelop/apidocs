---
title: MXC CONTRACT API

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

# Update log

| Effective Time（UTC+8) | Endpoint | Update Type | Description |
|-----|-----|-----|-----|
|2021-01-15|*|Add|Release of contract API|
| change | | 2021-03-30 | * adjust ｜ the following endpoints to access the paths and the data return format (the original paths still supported, but will gradually abandoned) : get the user’s all history orders, get the user’s ongoing orders, get the user’s history position information, get the stop-limit orders list, get the trigger orders list, get the user’s all transaction details |

# Integration guide

## Access to url

> general  data structures

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

> or

```json
{
  "success": false,
  "code":500,
  "message": "System internal error!"
}
```

- https://contract.mexc.com

The corresponding API accepts a request of Type GET, POST, or DELETE. The content-type of POST request is: application/JSON.

Parameters are sent in JSON format (parameter naming rules are camel named), and get requests are sent in requestParam (parameter naming rules are '_' delimited)

## Authentication method

> java example

```java
/**
 * Gets the get request parameter string
 *
 * @param param get/delete Request parameters map
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
 * signature
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
    private String requestParam; //get the request parameters are sorted in dictionary order, with & concatenated strings, POST should be a JSON string
}
```

1. Signature is not required for public endpoint.

2. For private endpoint, ApiKey, Request-Time, Signature and Content-Type need to be passed into the header, must be specified as application / JSON, Recv-Window (optional) parameters, Signature is a signature string. The signature rules are as follows:

  1) When signing, you need to get the request parameter string first. It is "" if there is no parameter:

    For GET/DELETE requests, the service parameters are spliced in dictionary order with & interval, and finally the signature target string is obtained (in the API of batch operation, if there are special symbols such as comma in the parameter value, these symbols need to be URL encoded when signing).
    
    For POST requests, the signature parameter is a JSON string (dictionary sorting is not required).

  2) After obtaining the parameter string, the signature target string is spliced. The rule is: accessKey + timestamp + obtained parameter string.

  3) The HMAC SHA256 algorithm is used to sign the target string, and finally the signature is passed into the header as a parameter.

Note：

  1) When the service parameter participating in the signature is null, it does not participate in the signature. For the path parameter, it does not participate in the signature; note that when get request stitches the parameter and pass it in the URL, if the parameter is null, it will be parsed into "" in the background parsing, fixed post request, when the parameter is null, do not pass the parameter, or set the value of the parameter to "" when signing, otherwise signature verification will fail.

  2) When requesting, put the value of Request-Time used in signing into the Request-Time parameter of the header, put the obtained signature string into the signature parameter of the header, put the Access Key of APIKEY into the ApiKey parameter of the header, and pass the other service parameters.

  3) The obtained signature string does not need to be base64 encoded.

## Time security

All APIs that require signature process need to fill in header parameter of Request-time, which is timestamp in milliseconds, when receives the request, the system verifies the time range from which the request was issued. The request is considered invalid if the received req_time is less or more than 10 seconds (the default value) (the time window can be adjusted by sending an optional header parameter ```recv-window``` with a maximum value of 60, ```recv_window``` of 30 seconds or more is not recommended)

## Create API key

Users can <a href="https://www.mexc.com/ucenter/openapi" target="_blank">create API key</a> in the personal center of MEXC, which is used for signature calculation and authentication, an API key is consist of two parts, secret key of Access keyAPI and secret key corresponding to Secret key.

# Error code

## Error code Example

Every endpoint has the potential for abnormalities.

The following is the error code information that the endpoint might return

| code  | description  |
| ------------ | ------------ |
| 0  | Operate succeed  |
| 9999  | Public abnormal  |
| 500  | Internal error  |
| 501  | System busy  |
| 401  | Unauthorized | 
| 402  | Api_key expired  |
| 406  | Accessed IP is not in the  whitelist  |
| 506  | Unknown source of request  |
| 510  |Excessive frequency of requests  |
| 511  | Endpoint inaccessible  |
| 513  | Invalid request(for open api serves  time more or less than 10s)  |
| 600  | Parameter error  |
| 601  | Data decoding error  |
| 602  | Verify failed  |
| 603  | Repeated requests  |
| 701 | Account read permission is required |
| 702 | Account modify permission is required |
| 703 | Trade information read permission is required |
| 704 | Transaction information modify permission is required|
| 1000  | Account does not exist  |
| 1001  | Contract does not exist  |
| 1002  |Contract not activated  |
| 1003  | Error in risk limit level  |
| 1004  | Amount error  |
| 2001  | Wrong order direction  |
| 2002  | Wrong opening type  |
| 2003  | Overpriced to pay  |
| 2004  | Low-price for selling  |
| 2005  | Balance insufficient  |
| 2006  | Leverage ratio error  |
| 2007  | Order price error  |
| 2008  | The quantity  is insufficient  |
| 2009  | Positions do not exist or have been closed  |
| 2011  | Order quantity error  |
| 2013  | Cancel orders over maximum limit  |
| 2014  | The quantity of batch order exceeds the limit  |
| 2015  | Price or quantity accuracy error  |
| 2016  | Trigger volume over the maximum  |
| 2018  | Exceeding the maximum available margin  |
| 2019  | There is an active open position  |
| 2021  | The single leverage is not consistent with the existing position leverage   |
| 2022  | Wrong position type  |
| 2023  | There are  positions  over the maximum leverage  |
| 2024  | There are orders with leverage over the maximum  |
| 2025  | The holding positions is over the maximum allowable positions  |
| 2026  | Modification of leverage is not supported for cross  |
| 2027  | There is only one cross or isolated  in the same direction  |
| 2028 | The maximum order quantity is exceeded |
| 2029 | Error order type |
| 2030 |External order ID is too long (Max. 32 bits ) |
| 2031 | The allowable holding position exceed the current risk limit |
| 2032 | Order price is less than long position force liquidate price |
| 2033 | Order price is more than short position force liquidate price |
| 2034 | The batch query quantity limit is exceeded |
| 2035 | Unsupported market price tier |
| 3001  | Trigger price type error |
| 3002  | Trigger type error |
| 3003  | Executive cycle error |
| 3004  | Trigger price error  |
| 4001  |Unsupported currency  |
| 2036 | The orders more than the limit, please contact customer service|
| 2037 | Frequent transactions, please try it later |
| 2038 | The maximum allowable position quantity is exceeded, please contact customer service! |
| 5001 | The take-price and the stop-loss price cannot be none at the same time |
| 5002 | The Stop-Limit order does not exist or has closed |
| 5003 | Take-profit and stop-loss price setting is wrong |
| 5004 | The take-profit and stop-loss order volume is more than the holding positions can be liquidated |
| 6001 | Trading forbidden |
| 6002 | Open forbidden |
| 6003 | Time range error |
| 6004 | The trading pair and status should be fill in |
| 6005 | The trading pair is not available |


# Market endpoints

The API endpoint under the [Market endpoints] module doesn't require authentication.

## Get the server time

> Request

```
curl "https://contract.mexc.com/api/v1/contract/ping"
```

> Response

```json
{
  "success": true,
  "data":1587442022003 
}
```

- **GET** ```api/v1/contract/ping```

<aside class="notice">
rate limit: 20 times / 2 seconds
</aside>

**Request parameters:** 

None

## Get the contract information

> Request

```
curl "https://contract.mexc.com/api/v1/contract/detail"
```

> Response

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
Rate limit: 1 times / 5 seconds
</aside>

**Request parameters:**
    
| Parameter  | Date Type  | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
|  symbol | string  | false  | the name of the contract  |

**Response parameters:**
    
| Parameter  | Date Type  | Description  |
| ------------ | ------------ | ------------ |
| symbol  | string | the name of the contract|
| displayName  | string | display name |
| displayNameEn  | string | english display name |
| positionOpenType  | int  |  position open type,1：isolated，2：cross，3：both |
| baseCoin  | string  | base currency such as BTC |
| quoteCoin  | string  | quote currency such as USDT  |
| settleCoin  | string  | liquidation currency such as USDT|
| contractSize  | decimal  | contract value |
| minLeverage  | int  | minimum leverage|
| maxLeverage  | int  | maximum leverage |
| priceScale  | int  | price scale |
| volScale  | int  | quantity scale |
| amountScale  | int  | amount scale  |
| priceUnit  | int  | price unit |
| volUnit  | int  | volume unit |
| minVol  | decimal  | minimum volume|
| maxVol  | decimal  | maximum volume|
| bidLimitPriceRate  | decimal  | bid limit price rate |
| askLimitPriceRate  | decimal  | ask limit price rate |
| takerFeeRate  | decimal  | taker rate |
| makerFeeRate  | decimal  | maker rate |
| maintenanceMarginRate  | decimal  |maintenance margin rate|
| initialMarginRate  | decimal  | initial margin rate |
| riskBaseVol  | decimal  |  initial volume |
| riskIncrVol  | decimal  | risk increasing volume |
| riskIncrMmr  | decimal  | maintain increasing margin rate |
| riskIncrImr  | decimal  | initial increasing margin rate|
| riskLevelLimit  | int  | risk level limit |
| priceCoefficientVariation  | decimal  |fair price coefficient variation  |
| indexOrigin  | List  | index origin |
| state  | int  | status, 0:enabled,1:delivery, 2:completed, 3: offline, 4: pause|
| conceptPlate  | List  | The zone, corresponding to the entryKey field of the section list |
| riskLimitType  | List  | Risk limit type, BY_VOLUME: by the volume, BY_VALUE: by the position |

## Get the transferable currencies

> Request

```
curl "https://contract.mexc.com/api/v1/contract/support_currencies"
```

> Response

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
Rate limit: 20 times /2 seconds
</aside>

**Request parameters:** 

None

**Response parameters:**

The returned "data" field contains a list of string with each string represents a suppported currency.

## Get the contract‘s  depth information

> Request

```
curl "https://contract.mexc.com/api/v1/contract/depth/BTC_USDT"
```

> Response

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
Rate limit: 20 times /2 seconds
</aside>

**Request parameters:**
    
| Parameter  | Date Type  | Mandatory   |  Description  |
| ------------ | ------------ | ------------ | ------------ |
| symbol | string  | true  | the name of the contract |
| limit | int  | false  | tier  |

**Response parameters:**
    
| Parameter | Data Type  | Description  |
| ------------ | ------------ | ------------ |
| asks  | List |the seller depth |
| bids  | List | the buyer depth  |
| version  | long  | the version number |
| timestamp  | long  | system timestamp |

note: [411.8, 10, 1] 411.8 is the price，10 is the volume of contracts for this price,1 is the order quantity

## Get a snapshot of the latest N depth information of the contract

> Request

```
curl "https://contract.mexc.com/api/v1/contract/depth_commits/BTC_USDT/20"
```

> Response

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
Rate limit: 20 times /2 seconds
</aside>

**Request parameter:**
    
| Parameter  | Data Type  | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol | string  | true  | the name of the contract  |
| limit | int  | true  | count  |

**Response parameters:**
    
| Parameter  | Data Type  | Description  |
| ------------ | ------------ | ------------ |
| asks  | List | the seller depth |
| bids  | List | the buyer depth |
| version  | long  | the version number |

## Get contract  index price

> Request

```
curl "https://contract.mexc.com/api/v1/contract/index_price/BTC_USDT"
```

> Response

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
Rate limit: 20 times /2 seconds
</aside>

**Request parameters:**
    
| Parameter  | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol | string  | true  | the name of the contract  |

**Response parameters:**
    
| Parameter  | Data Type  | Description  |
| ------------ | ------------ | ------------ |
| symbol  | string | trading pair |
| indexPrice  | decimal  | index price |
| timestamp  | long   | system timestamp |

## Get contract fair price

> Request

```
curl "https://contract.mexc.com/api/v1/contract/fair_price/BTC_USDT"
```

> Response

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
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter  | Data Type  | Mandatory |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | the name of the contract  |


**Response parameters:**
    
| Parameter | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| symbol | string | the name of the contract |
| fairPrice  | decimal  | fair price|
| timestamp  | long   | system timestamp|


## Get contract funding rate


> Request

```
curl "https://contract.mexc.com/api/v1/contract/funding_rate/BTC_USDT"
```

> Response

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
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter  | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | the name of the contract |

**Response parameters:**
    
| Parameter  | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| symbol  | string | the name of the contract |
| fundingRate  | decimal  | funding rate |
| maxFundingRate  | decimal  | max funding rate |
| minFundingRate  | decimal  | min funding rate |
| collectCycle  | int  | charge cycle |
| nextSettleTime  | long  | next charge time |
| timestamp  | long   | system timestamp |

## K-line data

> Request

```
curl "https://contract.mexc.com/api/v1/contract/kline/BTC_USDT?interval=Min15&start=1609992674000&end=1609992694000"
```

> Response

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
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter  | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | the name of the contract  |
| interval   | string  | false  | interval: Min1、Min5、Min15、Min30、Min60、Hour4、Hour8、Day1、Week1、Month1,default: Min1  |
| start  | long  | false  | start timestamp,seconds  |
| end  | long  | false  | end timestamp,seconds |

**Response parameters:**
    
| Parameter  | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| open  | double  | the opening price |
| close  | double   | the closing price|
| high  | double   | the highest price |
| low  | double   | the lowest price |
| vol  | double   | volume |
| time  | long   | time window |

Attention:

1、The maximum data in a single request is 2000 pieces. If your choice of start/end time and granularity of time results in more than the maximum volume of data in a single request, your request will only return 2000 pieces. If you want to get sufficiently fine-grained data over a larger time range, you need to make several times requests.

2、If only the start time is provided, then query the data from the start time to the current system time. If only the end time is provided, the 2000 pieces of data closest to the end time are returned. If neither start time nor end time is provided, the 2000 pieces of data closest to the current time in the system are queried.

## Get K-line data of the index price

> Request

```
curl "https://contract.mexc.com/api/v1/contract/kline/index_price/BTC_USDT?interval=Min15&start=1609992674000&end=1609992694000"
```

> Response

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
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | the name of the contract  |
| interval   | string  | false  | interval: Min1、Min5、Min15、Min30、Min60、Hour4、Hour8、Day1、Week1、Month1,default: Min1  |
| start  | long  | false  | start timestamp,seconds  |
| end  | long  | false  | end timestamp,seconds |

**Response parameters:**
    
| Parameter | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| open  | double  | the opening price |
| close  | double   | the closing price |
| high  | double   | the highest price |
| low  | double   | the lowest price|
| vol  | double   | volume |
| time  | long   | time window |

Attention:

1、The maximum data in a single request is 2000 pieces. If your choice of start/end time and granularity of time results in more than the maximum volume of data in a single request, your request will only return 2000 pieces. If you want to get sufficiently fine-grained data over a larger time range, you need to make several times requests.

2、If only the start time is provided, then query the data from the start time to the current system time. If only the end time is provided, the 2000 pieces of data closest to the end time are returned. If neither start time nor end time is provided, the 2000 pieces of data closest to the current time in the system are queried.

## Get K-line data of the fair price

> Request

```
curl "https://contract.mexc.com/api/v1/contract/kline/fair_price/BTC_USDT?interval=Min15&start=1609992674000&end=1609992694000"
```

> Response

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
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter  | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | the name of the contract  |
| interval   | string  | false  | interval: Min1、Min5、Min15、Min30、Min60、Hour4、Hour8、Day1、Week1、Month1,default: Min1  |
| start  | long  | false  | start timestamp,seconds  |
| end  | long  | false  | end timestamp,seconds  |

**Response parameters:**
    
| Parameter  | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| open  | double  | the opening price |
| close  | double   | the closing price |
| high  | double   | the highest price |
| low  | double   | the lowest price |
| vol  | double   | volume |
| time  | long   | time window 

Attention:

1、The maximum data in a single request is 2000 pieces. If your choice of start/end time and granularity of time results in more than the maximum volume of data in a single request, your request will only return 2000 pieces. If you want to get sufficiently fine-grained data over a larger time range, you need to make several times requests.

2、If only the start time is provided, then query the data from the start time to the current system time. If only the end time is provided, the 2000 pieces of data closest to the end time are returned. If neither start time nor end time is provided, the 2000 pieces of data closest to the current time in the system are queried.

## Get contract transaction data

> Request

```
curl "https://contract.mexc.com/api/v1/contract/deals/BTC_USDT"
```

> Response

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
Rate limit:20 times/2 seconds 
</aside>

**Request parameters:**
    
| Parameter  | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | the name of the contract  |
| limit  | int  | false  | consequence set quantity ，maximum is 100,  default 100 without setting  |

**Response parameters:**
    
| Parameter  | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| p  | decimal  | transaction price |
| v  | decimal  | quantity |
| T  | int  | deal type,1:purchase,2:sell |
| O  | int   | open position, 1: Yes,2: No, when O is 1, vol is additional position |
| M  | int   |self-transact,1:yes,2:no |
| t  | long   | transaction time |

## Get contract trend data

> Request

```
curl "https://contract.mexc.com/api/v1/contract/ticker"
```

> Response

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
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter  | Data Type   | Mandatory |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | false  | the name of the contract |

**Response parameters:**
    
| Parameter  | Data Type  | Description |
| ------------ | ------------ | ------------ |
| symbol  | string | the name of the contract |
| lastPrice  | decimal  | the latest price |
| bid1  | decimal  | purchase price |
| ask1  | decimal  | sell price |
| volume24  | decimal  | 24 hours trading volume, according to the volume of statistical count |
| amount24  | decimal  | 24 hours  transaction volume  |
| holdVol| decimal  | total holdings |
| lower24Price  | decimal  | lowest price within 24 hours |
| high24Price  | decimal  | highest price within 24 hours |
| riseFallRate  | decimal  | rise/fall rate |
| riseFallValue  | decimal  | rise/fall value |
| indexPrice  | decimal  | index price |
| fairPrice  | decimal  | fair price |
| fundingRate  | decimal  | funding rate |
| timestamp  | long   | transaction timestamp |

## Get all contract risk fund balance

> Request

```
curl "https://contract.mexc.com/api/v1/contract/risk_reverse"
```

> Response

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
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**

None

**Response parameters:**
    
| parameter name | type | description|
| ------------ | ------------ | ------------ |
| symbol | string | the name of the cntract |
| currency | string | currency |
| available | decimal | available balance |
| timestamp | long | system timestamp |

## Get contract risk fund balance history

> Request

```
curl "https://contract.mexc.com/api/v1/contract/risk_reverse/history?symbol=BTC_USDT&page_num=1&page_size=20"
```

> Response

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
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter  | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | the name of the contract |
| page_num  | int  | true  | current page number, default is 1 |
| page_size  | int  | true  | the page size, default 20, maximum 100  |

**Response parameters:**
    
| Parameter  | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| pageSize  | int  |  page size |
| totalCount  | int  |  total count  |
| totalPage  | int  | total pages  |
| currentPage  | int  |  current page |
| resultList  | list  | data consequence set |
| symbol  | string | the name of the contract |
| currency  | string  | liquidation currency |
| available  | decimal  | balance |
| snapshotTime  | long  |  snapshot  time |

## Get contract funding rate history

> Request

```
curl "https://contract.mexc.com/api/v1/contract/funding_rate/history?symbol=BTC_USDT&page_num=1&page_size=20"
```

> Response

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
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter  | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | the name of the contract |
| page_num  | int  | true  | current page number, default is 1  |
| page_size  | int  | true  | the page size, default 20, maximum 100  |

**Response parameters:**
    
| Parameter  | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| pageSize  | int  | page size |
| totalCount  | int  |  the total count |
| totalPage  | int  | the total pages |
| currentPage  | int  | the current page |
| resultList  | list  | data consequence set |
| symbol  | string | the name of the contract |
| fundingRate  | decimal  | funding rate |
| settleTime  | long  | liquidation time |

# Account and trading endpoints

The API endpoint under the [Account and trading endpoints] module requires authentication.

> Response

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

## Get all informations of user's asset

- **GET** ```api/v1/private/account/assets```

**Required permissions:** Trade reading permission

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**

None

**Response parameters:**
    
| Parameter | Data Type   | Description |
| ------------ | ------------ | ------------ |
| currency  | string  | currency |
| positionMargin  | decimal   | position margin |
| frozenBalance  | decimal   | frozen balance |
| availableBalance  | decimal   | available balance |
| cashBalance  | decimal   | drawable balance |
| equity  | decimal   | total equity |
| unrealized  | decimal   | unrealized profit and loss |

## Get the user's single currency asset information

> Response

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

**Required permissions:** Account reading permission

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter | Data Type   | Mandatory |  Description |
| ------------ | ------------ | ------------ | ------------ |
| currency  | string  | true  | currency|

**Response parameters:**
    
| Parameter | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| currency  | string  | currency |
| positionMargin  | decimal   | position margin |
| frozenBalance  | decimal   | frozen balance |
| availableBalance  | decimal   | available balance |
| cashBalance  | decimal   | drawable balance |
| equity  | decimal   | total equity |
| unrealized  | decimal   | unrealized profit and loss |

## Get the user's asset transfer records

> Response

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

**Required permissions:** Account reading permission

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| currency  | string  | false  | currency  |
| state  | string  | false  | state:WAIT 、SUCCESS 、FAILED  |
| type  | string  | false  | type:IN 、OUT  |
| page_num  | int  | true  | current page number, default is 1 |
| page_size  | int  | true  |  page size, default 20, maximum 100  |

**Response parameters:**
    
| Parameter | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| pageSize  | int  | page size |
| totalCount  | int  | the total count |
| totalPage  | int  | the total page |
| currentPage  | int  | the current page |
| resultList  | list  | data consequence set |
| id  | long  | id |
| txid  | string  | flow number |
| currency  | string  | currency|
| amount  | decimal  | transfer amount |
| type  | string   | type:IN 、OUT |
| state  | string   | state:WAIT 、SUCCESS 、FAILED  |
| createTime  | long   | create time |
| updateTime  | long   | update time |

## Get the user’s history position information

> Response

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

**Required permissions:** Trade reading permissions

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter | Data Type  | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | false  | the name of the contract |
| type  | int  | false  | position type， 1long 2short|
| page_num  | int  | true  | current page number , default is 1  |
| page_size  | int  | true  | page size , default 20, maximum 100  |

**Response parameters:**
    
| Parameter  | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| code  | number  | Status code  |
| message  | string  | Misdescription (If there has ) |
| <data> | array |  | 
| positionId  | long  | position id |
| symbol  | string  | the name of the contract |
| positionType  | int  | position type， 1 long  2 short |
| openType  | int   | open type， 1isolated 2cross |
| state  | int   | position state,1holding 2 system auto-holding 3closed  |
| holdVol  | decimal  | holding volume |
| frozenVol  | decimal   | frozen volume |
| closeAvgPrice  | decimal   | close average price |
| openAvgPrice  | decimal   | open average price |
| liquidatePrice  | decimal   | liquidation  price |
| oim  | decimal   | original initial margin |
| im  | decimal   | initial margin， add or subtract  items can be used to adjust the liquidate price |
| holdFee  | decimal   | holding  fee,  positive  means  get it,  negative  means lost it |
| realised  | decimal   | realized profit and loss|
| adlLevel | int | adl level
| leverage | int | leverage multiple｜
| createTime  | date   | create time |
| updateTime  | date   | update time |
| autoAddIm | boolean | automatic margin |
| </data> |  |  | 

## Get the user's current holding position

> Response

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

**Required permissions:** Trade reading permission

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter  | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | false  | the name of the contract|

**Response parameters:**
    
| Parameter  | Data Type  | Description  |
| ------------ | ------------ | ------------ |
| positionId  | long  | position id |
| symbol  | string  | the name of the contract |
| holdVol  | decimal  | holding volume |
| positionType  | int  | position type， 1 long  2 short  |
| openType  | int   | open type， 1 isolated 2 cross |
| state  | int   | position state,1holding. 2 system auto-holding 3 closed  |
| frozenVol  | decimal   | frozen volume |
| closeVol  | decimal   | close volume |
| holdAvgPrice  | decimal   | holdings average price |
| closeAvgPrice  | decimal   | close average price |
| openAvgPrice  | decimal   | open average price |
| liquidatePrice  | decimal   | liquidate price |
| oim  | decimal   | original initial margin |
| adlLevel  | int   | the value of ADL is 1-5. If it is empty, wait for the refresh |
| im  | decimal   | initial margin， add or subtract  items can be used to adjust the liquidate price |
| holdFee  | decimal   | holding fee,  positive  means  get it,  negative  means lost it |
| realised  | decimal   | realized profit and loss |
| createTime  | date   | create time |
| updateTime  | date   | update time |

## Get details of user‘s funding rate

> Response

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

**Required permissions:** Trade reading permission

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter  | Data Type  | Mandatory |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol | string  | false  | the name of the contract|
| position_id  | int  | false  | position id|
| page_num  | int  | true  | current page number, default is 1  |
| page_size  | int  | true  | page size, default 20, maximum 100  |

**Response parameters:**
    
| Parameter | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| pageSize  | int  | page size |
| totalCount  | int  | the total count |
| totalPage  | int  | the total page|
| currentPage  | int  | the current page |
| resultList  | list  | data consequence list |
| id  | long  | id |
| symbol  | string  | the name of the contract |
| positionId  | long  | position id |
| positionType  | int  |  1 long  2 short |
| positionValue  | decimal  | position value |
| funding  | decimal   | funding |
| rate  | decimal   | funding rate  |
| settleTime  | date   | liquidation time |

## Get the user's current pending order

> Response

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

**Required permissions:** Trade reading permission

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
	
| Parameter  | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | false  | the name of the contract,  return all the contract parameters  if there no fill in |
| page_num  | int  | true  | current page number, default is 1 |
| page_size  | int  | true  |  page size default 20, maximum 100 |

**Response parameters:**
	
| Parameter  |  Data Type   | Description  |
| ------------ | ------------ | ------------ |
| code  | number  | Status code  |
| message  | string  | Misdescription (If there has ) |
| <data> | array |  | 
| orderId  | long  | orderid |
| symbol  | string  | the name of the contract |
| positionId  | long  | position id |
| price  | decimal  | trigger price|
| vol  | decimal  | trigger volume |
| leverage  | long  | leverage |
| side  | int  | order direction 1open long,2close short,3open short, 4 close long |
| category  | int  | order category:1limit order, 2 system take-over delegate, 3 close delegate 4 ADL reduction |
| orderType  | int  | 1:price limited order,2:post only Maker,3:transact  or cancel instantly ,4 : transact completely or cancel completely，5:market orders,6 convert market price to current price |
| dealAvgPrice  | decimal   | deal average price |
| dealVol  | decimal   | transaction volume |
| orderMargin  | decimal   | order margin  |
| usedMargin  | decimal   | used margin  |
| takerFee  | decimal   | taker fee |
| makerFee  | decimal   | maker fee |
| profit  | decimal   | close profit|
| feeCurrency  | string   | fee currency|
| openType  | int   | open type,1 isolated,2 cross |
| state  | int   | order state,1 uninformed, 2uncompleted, 3completed, 4cancelled, 5invalid |
| errorCode  | int   | error code,0:normal，1：parameter errors，2：account balance is insufficient，3：the position does not exist，4：  position insufficient，5：For long positions, the order price is less than the close price, while for short positions, the order price is more than the close rice，6：When opening long, the close price is more than the fair price, while when opening short, the close price is less than the fair price  ,7:exceed risk quota restrictions, 8: system canceled |
| externalOid  | string   | external order ID |
| createTime  | date   | create time  |
| updateTime  | date   | update time |
| stopLossPrice | decimal | stop-loss price ｜
| takeProfitPrice | decimal | take-profit price ｜
| </data> |  |  | 

## Get all of the user's historical orders

> Response

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

**Required permissions:** Trade reading permission

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**

| Parameter | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | false  | the name of the contract |
| states  | string  | false  | order state,1 1 uninformed, 2uncompleted, 3completed, 4cancelled, 5invalid; multiple  separate by ','|
| category  | int  | false  | order category:1limit order, 2 system take-over delegate, 3 close delegate 4 ADL reduction |
| start_time  | long  | false  | start time, start time and end time span can only check 90 days at a time, default return the last 7 days of data without fill in  |
| end_time  | long  | false  | end time, start time, and end time spans can only be checked for 90 days at a time|
| side  | int  | false  |  order direction long,2close short,3open short 4 close long |
| page_num  | int  | true  | current page number, default is 1  |
| page_size  | int  | true  | page size, default 20, maximum 100 |

**Response parameters:**
    
| Parameter  | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| code  | number  | Status code  |
| message  | string  | Misdescription (If there has ) |
| <data> | array |  | 
| orderId  | long  | orderid |
| symbol  | string  | the name of the contract |
| positionId  | long  | position id |
| price  | decimal  | trigger price|
| vol  | decimal  | trigger volume |
| leverage  | long  | leverage |
| side  | int  | order direction 1open long,2close short,3open short 4 close long |
| category  | int  | order category:1limit order, 2 system take-over delegate, 3 close delegate 4 ADL reduction |
| orderType  | int  | 1:price limited order,2:Post Only Maker,3:transact  or cancel instantly ,4 : transact completely or cancel completely，5:market orders,6 convert market price to current price |
| dealAvgPrice  | decimal  | transaction average price |
| dealVol  | decimal   | transaction volume |
| orderMargin  | decimal   | order margin  |
| takerFee  | decimal   | taker fee |
| makerFee  | decimal   | maker fee
| profit  | decimal   | close profit |
| feeCurrency  | string   | fee currency |
| openType  | int   | open type,1 isolated,2 cross |
| state  | int   | order state,1 uninformed, 2 uncompleted, 3 completed, 4 cancelled, 5 invalid |
| errorCode  | int   | error code,0:normal，1：parameter errors，2：account balance is insufficient，3：the position does not exist，4： position insufficient，5：For long positions, the order price is less than the close price, while for short positions, the order price is more than the close rice.，6：When opening long, the close price is more than the fair price, while when opening short, the close price is less than the fair price. |
| externalOid  | string   | external order ID |
| usedMargin  | decimal   | used margin  |
| createTime  | date   | create time |
| updateTime  | date   | update tine |
| stopLossPrice | decimal | stop-loss price ｜
| takeProfitPrice | decimal | take-profit price ｜
| </data> |  |  | 

## Query the order based on the external number

> Response

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

**Required permissions:** Trade reading permission

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter  | Data Type  | Mandatory |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | the name of the contract|
| external_oid  | string  | true  | external order ID|

**Response parameters:**
    
| Parameter  | Data Type  | Description  |
| ------------ | ------------ | ------------ |
| orderId  | long  | orderid |
| symbol  | string  | the name of the contract |
| positionId  | long  | position id |
| price  | decimal  | trigger price|
| vol  | decimal  | trigger volume |
| leverage  | long  | leverage |
| side  | int  | order direction 1open long,2close short,3open short 4 close long |
| category  | int  | order category:1limit order, 2 system take-over delegate, 3 close delegate 4 ADL reduction |
| orderType  | int  | 1:price limited order,2:Post Only Maker,3:transact  or cancel instantly ,4 : transact completely or cancel completely，5:market orders,6 convert market price to current price |
| dealAvgPrice  | decimal  | transaction average price |
| dealVol  | decimal   | transaction volume |
| orderMargin  | decimal   | order margin |
| takerFee  | decimal   | taker fee |
| makerFee  | decimal   | maker fee |
| profit  | decimal   | close profit |
| feeCurrency  | string   | fee currency |
| openType  | int   | open type,1isolated,2cross |
| state  | int   | order state,1: uninformed,2uncompleted,3completed,4canceled,5invalid|
| externalOid  | string   | external order ID |
| createTime  | date   | create time|
| updateTime  | date   | update time |

## Query the order based on the order number

> Response

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

**Required permissions:** Trade reading permission

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter  | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| order_id  | long  | true  | order ID|

**Response parameters:**
    
 Parameter  | Data Type   | Description |
| ------------ | ------------ | ------------ |
| orderId  | long  | orderid |
| symbol  | string  | the name of the contract |
| positionId  | long  | position id |
| price  | decimal  | trigger price|
| vol  | decimal  | trigger volume |
| leverage  | long  | leverage |
| side  | int  | order direction :1 open long,2close short,3open short, 4 close long |
| category  | int  | order category:1limit order, 2 system take-over delegate, 3 close delegate 4 ADL reduction |
| orderType  | int  | 1:price limited order,2:Post Only Maker,3:transact  or cancel instantly ,4 : transact completely or cancel completely，5:market orders,6 convert market price to current price |
| dealAvgPrice  | decimal  | transaction average price |
| dealVol  | decimal   | transaction volume |
| orderMargin  | decimal   | order margin  |
| takerFee  | decimal   | taker fee |
| makerFee  | decimal   | maker fee |
| profit  | decimal   | close profit |
| feeCurrency  | string   | fee currency |
| openType  | int   | open type,1isolated,2cross |
| state  | int   | order state,1 uninformed,  2 uncompleted,  3completed,  4cancelled, 5 invalid |
| externalOid  | string   |External order ID|
| createTime  | date   | create time  |
| updateTime  | date   | update time |

## Query the order in bulk based on the order number

- **GET** ```/api/v1/private/order/batch_query```

**Required permissions:** Trade reading permission

<aside class="notice">
Rate limit:5 times/2 seconds
</aside>

**Request parameters:**
	
| Parameter  | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| order_ids  | long  | true  | order number array，can be separated by "," for example :order_ids = 1,2,3(maximum 50 orders):|

**Response parameters:**
	
 Parameter  | Data Type   | Description |
| ------------ | ------------ | ------------ |
| orderId  | long  | orderid |
| symbol  | string  | the name of the contract |
| positionId  | long  | position id |
| price  | decimal  | trigger price|
| vol  | decimal  | trigger volume |
| leverage  | long  | leverage |
| side  | int  | order direction 1open long,2close short,3open short, 4 close long |
| category  | int  | order category:1limit order, 2 system take-over delegate, 3 close delegate 4 ADL reduction |
| orderType  | int  | 1:price limited order,2:Post Only Maker,3:transact  or cancel instantly ,4 : transact completely or cancel completely，5:market orders,6 convert market price to current price |
| dealAvgPrice  | decimal  | transaction average price |
| dealVol  | decimal   | transaction volume |
| orderMargin  | decimal   | order margin  |
| takerFee  | decimal   | taker fee |
| makerFee  | decimal   | maker fee |
| profit  | decimal   | close profit |
| feeCurrency  | string   | fee currency |
| openType  | int   | open type,1isolated,2cross |
| state  | int   | order state,1: uninformed, 2uncompleted 3 completed, 4cancelled, 5invalid |
| externalOid  | string   |external order ID|
| createTime  | date   | create time  |
| updateTime  | date   | update time |

## Get order transaction details based on the order ID

> Response

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

**Required permissions:** Trade reading permission

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| order_id  | long  | true  | order id|

**Response parameters:**
    
| Parameter  | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| id  | long  | transactionid |
| symbol  | string  | the name of the contract |
| side  | int  |order direction 1open long,2close short,3open short 4 close long |
| vol  | decimal  | transaction volume |
| price  | decimal   | transaction price |
| fee  | decimal   | fee |
| feeCurrency  | string   | fee currency |
| profit  | decimal   | profit |
| isTaker  | boolean   | Is it taker order|
| category  | int  | order category:1limit order, 2 system take-over delegate, 3 close delegate 4 ADL reduction |
| orderId  | long   | order id |
| timestamp  | long   | transaction timestamp |

## Get all transaction details of the user’s order

> Response

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
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**

| Parameter | Data Type  | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | the name of the contact |
| start_time  | long  | false  | the starting time, the default is to push forward 7 days, and the maximum span is 90 days|
| end_time  | long  | false  |the end time, start and end time span is 90 days|
| page_num  | int  | true  | current page number, default is 1 |
| page_size  | int  | true  | page size , default 20, maximum 100 |

**Response parameters:**

| Parameter  |  Data Type   | Description  |
| ------------ | ------------ | ------------ |
| code  | number  | Status code  |
| message  | string  | Misdescription (If there has ) |
| <data> | array |  | 
| id  | long  | order id |
| symbol  | string  | the name of the contact |
| side  | int  | order direction 1open long,2close short,3open short 4 close long |
| vol  | decimal  | transaction volume |
| price  | decimal   | transaction price|
| fee  | decimal   | fee |
| feeCurrency  | string   | currency  |
| profit  | decimal   | profit |
| isTaker  | boolean   | is it taker order|
| category | int | order category:1limit order, 2 system take-over delegate, 3 close delegate 4 ADL reduction |
| orderId  | long   | order id |
| timestamp  | long   | transaction timestamp |
| </data> |  |  | 

## Gets the trigger order list

> Response

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
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | false  | the name of the contract |
| states  | string  | false  | order state,1 uninformed, 2uncompleted,3completed,4cancelled, 5invalid; Multiple  separate by ','|
| start_time  | long  | false  | start time, start time and end time span can only check 90 days at a time, default return the last 7 days of data without fill in  |
| end_time  | long  | false  | end time, start time, and end time spans can only be checked for 90 days at a time|
| page_num  | int  | true  | current page number, default is 1  |
| page_size  | int  | true  | page size, default 20, maximum 100 |

**Response parameters:**
    
| Parameter  | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| code  | number  | Status code  |
| message  | string  | Misdescription (If there has ) |
| <data> | array |  | 
| id  | int  | trigger order id |
| symbol  | string  | the name of the contract |
| leverage  | long  | leverage |
| side  | int  | order direction  1open long, 3open short |
| triggerPrice  | decimal   | trigger price |
| price  | decimal   | execute price |
| vol  | decimal   | order volume  |
| openType  | int   | open type， 1isolated 2cross |
| triggerType  | int   | trigger type,1: more than or equal, 2: less than or equal |
| state  | int   | status,1: untriggered, 2: cancelled, 3: executed,4: invalid,5: execution failed |
| executeCycle  | int   | execution cycle, unit: hours |
| trend  | int   | trigger price type,1: latest price, 2: fair price, 3: index price |
| errorCode  | int   | error code on failed execution, 0: normal|
| orderId  | long   | order ID, Return on successful execution |
| orderType  | int   |order type,1: limit order,2:Post Only Maker,3: close or cancel instantly 4: close or cancel completely,5: Market order |
| createTime  | long   | create time  |
| updateTime  | long   | update time |
| </data> |  |  | 

## Get the Stop-Limit order list

> Response

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
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter  | Data Type  | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | false  | the name of the contact |
| is_finished  | int  | false  | final state indicator :0: uncompleted, 1: completed|
| start_time  | long  | false  | start time, start time and end time span can only check 90 days at a time, default return the last 7 days of data without fill in  |
| end_time  | long  | false  | end time, start time, and end time spans can only be checked for 90 days at a time|
| page_num  | int  | true  | current page number, default is 1  |
| page_size  | int  | true  | page size, default 20, maximum 100  |

**Response parameters:**

| Parameter | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| code  | number  | Status code  |
| message  | string  | Misdescription (If there has ) |
| <data> | array |  | 
| id  | long  | Stop-Limit order ID |
| symbol  | string  | the name of the contract |
| orderId  | long   | limit order ID, which is 0 if it is based on a position|
| positionId  | long   | position id |
| stopLossPrice  | decimal   | stop-loss price |
| takeProfitPrice  | decimal   | take-profit price |
| state  | int   | status,1: untriggered, 2: cancelled, 3: executed,4: invalid,5: execution failed |
| triggerSide  | int   | trigger direction, 0: untriggered , 1: taker-profit , 2: stop-loss |
| positionType  | int   | position type,1: long, 2: short |
| vol  | decimal   | trigger volume  |
| realityVol | decimal | actual number of orders |
| placeOrderId | long | order id after successful delegation ｜
| errorCode | int | errorCode,0: normal,  other errorCode details |
| isFinished | int | whether the order status is the end-state identifier (for query),0. Non-terminal, 1. Terminal |
| version | int | version |
| createTime | long | createTime |
| updateTime | long |update  time |
| </data> |  |  | 

## Get risk limits

> Response

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

**Required permissions:** Trade reading permission

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter | Data Type  | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | false  | the name of the contract , not uploaded will return all|

**Response parameters:**
    
| Parameter | Data Type   | Description |
| ------------ | ------------ | ------------ |
| symbol  | string  | the name of the contract |
| positionType  | int  | position type 1:long，2:short |
| level  | int   | current risk level |
| maxVol  | decimal   | maximum position volume |
| maxLeverage  | int   | maximum leverage rate|
| mmr  | decimal   | maintenance margin rate |
| imr  | decimal   | initial margin rate |

## Gets the user's current trading fee  rate

> Response

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

**Required permissions:** Trade reading permission

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter | Data Type  | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | the name of the  contract |

**Response parameters:**
    
| Parameter | Data Type   | Description |
| ------------ | ------------ | ------------ |
| level  | int  | tiered trading fee rate  |
| dealAmount  | int  | the last 30 days' turnover|
| walletBalance  | int   | wallet balance of yesterday |
| makerFee  | decimal   | makerFee |
| takerFee  | int   | takerFee |
| makerFeeDiscount  | decimal   | makerFee discount |
| takerFeeDiscount  | decimal   | takerFee discount |

## Increase or decrease margin

> Response

```json
{
    "success": true,
    "code": 0
}
```

- **POST** ```api/v1/private/position/change_margin```

**Required permissions:** Trading permission

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter  | Data Type   | Mandatory |  Description |
| ------------ | ------------ | ------------ | ------------ |
| positionId  | long  | true  | position id|
| amount  | decimal  | true  | amount |
| type  | string  | true  | type ,ADD: increase,SUB: decrease|

**Response parameters:**

public parameters, success: true, success, false ,failure



## Get leverage

- **GET** ```api/v1/private/position/leverage```

**Required permissions:** Trading permission

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter  | Data Type   | Mandatory|  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | symbol|


**Response parameters:**

| Parameter | Type  | Description  |
| ------------ | ------------ | ------------ |
| positionType  | int  |  positon type， 1:long 2:short |
| level  | int  | risk level |
| imr  | decimal  | The leverage risk limit level corresponds to initial margin rate|
| mmr  | decimal   | Leverage risk limit level corresponds to maintenance margin rate |
| leverage  | int  | leverage|



## Switch leverage

- **POST** ```api/v1/private/position/change_leverage```

**Required permissions:** Trading permission

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter  | Data Type   | Mandatory|  Description |
| ------------ | ------------ | ------------ | ------------ |
| positionId  | long  | true  | position id|
| leverage  | int  | true  | leverage|
| openType  | int  | false  | Required when there is no position, openType, 1: isolated position, 2: full position|
| symbol  | string  | false  | equired when there is no position，symbol |
| positionType  | int  | false  |equired when there is no position,  positionType: 1 Long 2:short|

**Response parameters:**

public parameters, success: true, success, false ,failure

**request parameters example:**
   - Has positon:

    ```
    {
      "positionId": 1,
      "leverage": 20
    }
    ```
   - no positon:

    ```
    {
      "openType": 1,
      "leverage": 20,
      "symbol": "BTC_USDT",
      "positionType": 1 
    }
    ```



## Get position mode

- **GET** ```api/v1/private/position/position_mode```

**Required permissions:** Trading permission

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
None


**Response parameters:**

public parameters, success: true, success, false ,failure

position mode,1:hedge，2:one-way

**request parameters example:**
    ```
    {"success":true,"code":0,"data":2}
    ```



## Change position mode

- **POST** ```api/v1/private/position/change_position_mode```

**Required permissions:** Trading permission

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter  | Data Type   | Mandatory|  Description |
| ------------ | ------------ | ------------ | ------------ |
| positionMode  | int  | true  | 1: Hedge，2, 2: One-way, the modification of the position mode must ensure that there are no active orders, planned orders, or unfinished positions, otherwise it cannot be modified. When switching the one-way mode in both directions, the risk limit level will be reset to level 1. If you need to change the call interface, modify|


**Response parameters:**

public parameters, success: true, success, false ,failure

**request parameters example:**
    ```
    {"success":true,"code":0}
    ```



## Order

> Response

```json
{
    "success": true,
    "code": 0,
    "data": 102057569836905984
}
```

USDT perpetual contract trading offers limit and market orders.  You can place an order only you have enough money in your account. Once you place an order, your account funds will be frozen . The amount of funds frozen depends on the type and parameters specified in the order.

- **POST** ```api/v1/private/order/submit```

**Required permissions:** Trading permission

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter  | Data Type   | Mandatory  |  Description|
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | the name of the contract|
| price  | decimal  | true  | price |
| vol  | decimal  | true  | volume|
| leverage  | int  | false  | leverage ,Leverage is necessary on Isolated Margin|
| side  | int  | true  | order direction 1 open long ,2close short,3open short ,4 close l|
| type  | int  | true | orderType,1:price limited order,2:Post Only Maker,3:transact  or cancel instantly ,4 : transact completely or cancel completely，5:market orders,6 convert market price to current price |
| openType  | int  | true  | open type,1:isolated,2:cross|
| positionId  | long  | false  | position Id，It is recommended to fill in this parameter when closing a position|
| externalOid  | string  | false  | external order ID|
| stopLossPrice  | decimal  | false  | stop-loss price|
| takeProfitPrice  | decimal  | false  | take-profit price|
| positionMode  | int  | false  |  position mode,1:hedge，2:one-way|
| reduceOnly  | boolean  | false  | Default false,For one-way positions, if you need to only reduce positions, pass in true, and two-way positions will not accept this parameter.|

**Response parameters:**

success, success =true, data represent the order id success =false, failure data=null

## Bulk order

> Response

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

Order the contract in batch. Each contract can place 50 orders in the batch. This endpoint is not available for all users , please contact customer service to get this  permission.

- **POST** ```api/v1/private/order/submit_batch```

**Required permissions:** Trading permission

<aside class="notice">
Rate limit:1/2 seconds
</aside>

**Request parameters:**(maximum 50 )
    
| Parameter  | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | the name of the contract |
| price  | decimal  | true  | price|
| vol  | decimal  | true  | volume|
| leverage  | int  | false  | leverage ,Leverage is necessary on Isolated Margin|
| side  | int  | true  | order side 1open long,2close short,3open short, 4 close long|
| type  | int  |true |  order type :1 price limited order,2:Post Only Maker,3:transact  or cancel instantly ,4 : transact completely or cancel completely，5:market orders,6 convert market price to current price
| openType  | int  | true  | open type,1:isolated,2:cross||
| positionId  | long  | false  | position Id，It is recommended to fill in this parameter when closing a position|
| externalOid  | string  | false  | external order ID, return  the existing order ID if it already exists|
| stopLossPrice  | decimal  | false  | stop-loss price|
| takeProfitPrice  | decimal  | false  | take-profit price|

**Response parameters:**
    
| Parameter   | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| externalOid  | string  | external order ID |
| orderId  | long  | order ID, null on failure  |
| errorMsg  | string  | error message, not null when failed|
| errorCode  | int  | error code, default is 0|


## Cancel  the order

> Response

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

Cancel the pending order placed before, each time can cancel up to 50 orders.

- **POST** ```api/v1/private/order/cancel```

**Required permissions:** Trading permission

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| None  | List<Long>  | true  | order id list, maximum 50|

**Response parameters:**

| Parameter  | Data Type  | Description  |
| ------------ | ------------ | ------------ |
| orderId  | long  | order ID  |
| errorMsg  | string  | error message  |
| errorCode  | int  | error code，Not 0 means the revoke failed  |

## Cancel the order according to the external order ID

> Response

```json
{
    "symbol":"BTC_USDT",
    "externalOid":"mexc-a-001"
}
```

Cancel  the uncompleted order under a contract according to the specified externalOid, only 1 order for each cancellation.

- **POST** ```api/v1/private/order/cancel_with_external```

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**

| Parameter | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | the name of the contract|
| externalOid  | string  | true  | external orderid|

## Cancel all orders under a contract

Cancel all uncompleted orders under a contract.

- **POST** ```api/v1/private/order/cancel_all```

**Required permissions:** Trading permission

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter   | Data Type   | Mandatory |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | false| the name of the contract, cancel specific orders placed under this contract when fill the symbol , otherwise , cancel all orders without filling |

**Response parameters:**

public parameters , success: true success, false failure



## Switch the risk level

\- **POST** ```api/v1/private/account/change_risk_level```

\- Disabled The call returns the error code 8817 Prompt information: The risk restriction function has been upgraded. For details, please go to the web to view



## Trigger order

- **POST** ```api/v1/private/planorder/place```

<aside>
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter   | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | true  | the name of the contract |
| price  | decimal  | false  | execut price, market price may not fill in |
| vol  | decimal  | true  | volume |
| leverage  | int  | false  | leverage , Leverage is necessary on Isolated Margin  |
| side  | int  | true  | 1open long,2close short,3open short 4 close long|
| openType  | int  | true  | open type,1:isolated,2:cross|
| triggerPrice  | decimal  | true  | trigger price|
| triggerType  | int  | true  | trigger type,1: more than or equal, 2: less than or equal|
| executeCycle  | int  | true  | execution cycle,1: 24 hours,2: 7 days|
| orderType  | int  | true  | order type,1: limit order,2:Post Only Maker,3: close or cancel instantly ,4: close or cancel completely,5: Market order|
| trend  | int  | true  | trigger price type,1: latest price, 2: fair price, 3: index price|

**Response parameters:**

success, success =true, data value is the order ID, success =false, failure data=null

## Cancel the trigger order

> Response

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
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter  | Data Type  | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| None  | List<CancelOrderRequest>  | true  | cancel the order list, maximum 50|

**CancelOrderRequest:**

| Parameter  | Data Type  | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  |string  | true  | the name of the contract|
| orderId  |string  | true  | orderId|

**Response parameters:**

public parameters, Success: true success, false failure

## Cancel all trigger orders

- **POST** ```api/v1/private/planorder/cancel_all```

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
    
| Parameter   | Data Type   | Mandatory |  Description |
| ------------ | ------------ | ------------ | ------------ |
| symbol  | string  | false| the name of the contract, cancel specific orders placed under this contract when fill the symbol , otherwise , cancel all orders without filling |

**Response parameters:**

public parameters, Success: true success, false failure

## Cancel the Stop-Limit trigger order

> Response

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
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**

| Parameter | Data Type | Mandatory | Description |
| ------------ | ------------ | ------------ | ------------ |
| none | List<CancelOrderRequest> | true | cancel order list, maximum 50|

**CancelOrderRequest:**

| Parameter | Data Type |Mandatory | Description |
| ------------ | ------------ | ------------ | ------------ |
| stopPlanOrderId |long | true |the Stop-Limit trigger order ID|

## Cancel all Stop-Limit price trigger orders

- **POST** ```api/v1/private/stoporder/cancel_all```

<aside>
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
      
| Parameter | Data Type  | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| positionId  | long  | false  | position id, fill in positionId，only cancel the trigger order of the corresponding position, and check the symbol without filling |
| symbol  | string  | false  |the name of the contact ,only cancels the delegate  order under this contract based on the symbol,  cancel all orders without filling the symbol|

**Response parameters:**

public parameters, success: true success ,false failure

## Switch  Stop-Limit  limited order  price

- **POST** ```api/v1/private/stoporder/change_price```

<aside class="notice">
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**

| Parameter   | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| orderId  | long  | true  | limit order id|
| stopLossPrice  | decimal  | false  | stop-loss price, take-profit and stop-loss price are empty or 0 at the same time, indicating to cancel and take profit |
| takeProfitPrice  | decimal  | false  | take-profit price，take-profit and stop-loss price are empty or 0 at the same time, indicating to cancel stop-loss and take profit |

**Response parameters:**

public parameters, success: true success ,false failure

## Switch  the Stop-Limit price of trigger orders

- **POST** ```api/v1/private/stoporder/change_plan_price```

<aside>
Rate limit:20 times/2 seconds
</aside>

**Request parameters:**
       
| Parameter   | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| stopPlanOrderId  | long  | true  | the Stop-Limit price of trigger order id|
| stopLossPrice  | decimal  | false  | at least one stop-loss price and one take-profit  price is not empty and must be more than 0|
| takeProfitPrice  | decimal  | false  | at least one take-profit price and  stop-loss price is not empty and must be more than 0|

**Response parameters:**

public parameters, success: true success ,false failure

# WebSocket API

WebSocket is a new Protocol in HTML5. It realizes full-duplex communication between client and server. A single handshake  can establish the connection between the client and the server, and the server can actively send information to the client according to the rules. The advantages are as follows:

1. The request header information is relatively small about 2 bytes when the client and server transfer the data.
2. Both the client and the server can actively send data to each other.
3. No need to create or destroy TCP requests many times, saving bandwidth and server resources.

Developers are strongly advised to use the WebSocket API for market trends and buying/ selling depth information.

## Native WS connection address

- wss://contract.mexc.com/ws

## Detailed data interaction commands

> Send ping message

```json
{
  "method": "ping"
}
```

> Server return

```json
{
  "channel": "pong",
  "data": 1587453241453
}
```

List of subscribe/unsubscribe data commands ( ws identification is not required except the list of personal related commands)

If no ping is received within 1 minute, the connection will be disconnected. It is recommended to send a ping for 10-20 seconds

The ping message and server return are shown on the right

## Public Channels

### Tickers

> Subscribe

```json
{
  "method": "sub.tickers",
  "param": {}
} 
```

> If you want to return content (the same with following subscription):

```json
{
  "method": "sub.tickers",
  "param": {},
  "gzip": false
} 
```

> Unsubscribe

```json
{
  "method": "unsub.tickers",
  "param": {}
} 
```

> Example

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

Get the latest transaction price, buy-price, sell-price and 24 transaction volume of all the perpetual contracts on the platform without login. Send once a second after subscribing.

subscribe , unsubscribe, example is shown on the right.

**Response parameters:**
	
| Parameter   | Data Type  | Description  |
| ------------ | ------------ | ------------ |
| symbol  | string | the name of the contract |
| lastPrice  | decimal  |  the last price |
| volume24  | decimal  | 24 hours trading volume, according to the  statistics count |
| riseFallRate  | decimal  | rise/fall rate |
| fairPrice  | decimal  | fair price |

### Ticker

> Subscribe

```json
{
    "method":"sub.ticker",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> Unsubscribe

```json
{
    "method":"unsub.ticker",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> Example

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

Get the latest transaction price, buy price, sell price and 24 transaction volume of a contract, send the transaction data without users' login, and send once a second after subscription.

subscribe , unsubscribe, example is shown on the right.

**Response parameters:**
	
| Parameter  | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| symbol  | string | the name of the contract |
| lastPrice  | decimal  | last price |
| bid1  | decimal  | bid/price |
| ask1  | decimal  | ask/price|
| volume24  | decimal  |  24 hours transaction volume, according to the statistical count |
| holdVol| decimal  |  hold volume |
| lower24Price  | decimal  | lowest price within 24 hours |
| high24Price  | decimal  | highest price in 24 hours |
| riseFallRate  | decimal  | rise fall rate |
| riseFallValue  | decimal  | rise fall value|
| indexPrice  | decimal  | index price |
| fairPrice  | decimal  | fair price |
| fundingRate  | decimal  | funding fee |
| timestamp  | long   | system timestamp|

### Transaction

> subscribe

```json
{
    "method":"sub.deal",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> Unsubscribe

```json
{
    "method":"unsub.deal",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> Example

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

Access to the latest data without login, and keep updating.

subscribe , unsubscribe, example is shown on the right.

**Response parameters:**
	
| Parameter   | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| p  | decimal  | transaction  price |
| v  | decimal  | volume |
| T  | int  | transaction direction,1:purchase,2:sell |
| O  | int   | open position?, 1: Yes,2: No, vol is the additional position when O is 1 |
| M  | int   | Is it auto-transact ? 1: Yes,2: No |
| t  | long   | transaction time |

### Depth

> Subscription increments (all)

```json
{
    "method":"sub.depth",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> Subscription increments (zipped push)

```json
{
    "method":"sub.depth",
    "param":{
        "symbol":"BTC_USDT",
        "compress":true
    }
}
```

> Full subscription(Limit could be 5, 10 or 20, default 20 without define., only subscribe to the full amount of one gear)

```json
{
    "method":"sub.depth.full",
    "param":{
        "symbol":"BTC_USDT",
        "limit":5
    }
}
```

> unsubscribe (cancel the incremental subscription)

```json
{
    "method":"unsub.depth",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> Unsubscribe (cancel the full subscription, limit is not mandatory)

```json
{
    "method":"usub.depth.full",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> Example

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

subscribe , unsubscribe, example is shown on the right.

**Response Parameter:**
	
| Parameter  | Data Type  | Description |
| ------------ | ------------ | ------------ |
| asks  | List<Numeric[]> |seller depth |
| bids  | List<Numeric[]> | buyer depth |
| version  | long  | the version number |

Tip: [411.8, 10, 1] 411.8 is price，10 is the order numbers of the contract ,1 is the order quantity

### K-line

> Subscribe

```json
{
    "method":"sub.kline",
    "param":{
        "symbol":"BTC_USDT",
        "interval":"Min60"
    }
}
```

> Unsubscribe

```json
{
    "method":"unsub.kline",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> Example

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

Get the k-line data of the contract and keep updating.

subscribe , unsubscribe, example is shown on the right.

interval optional parameters:  Min1、Min5、Min15、Min30、Min60、Hour4、Hour8、Day1、Week1、Month1

**Response parameters:**
	
| Parameter   | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| symbol  | string | the name of the contract |
| a  | decimal  | total transaction amount |
| c  | decimal  | the closing price |
| interval  | string  | interval: Min1、Min5、Min15、Min30、Min60、Hour4、Hour8、Day1、Week1、Month1 |
| l  | decimal  | the lowest price |
| o  | decimal  | the opening price |
| q  | decimal  | total transaction volume |
| h  | decimal  | the highest price |
| t  | long  | trading time，unit：second（s）， the start time of the window（windowStart）|

### Funding rate

> Subscribe

```json
{
    "method":"sub.funding.rate",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> unsubscribe

```json
{
    "method":"unsub.funding.rate",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> Example

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

Get the contract funding rate, and keep updating.

subscribe , unsubscribe, example is shown on the right.

**Response parameters:**
	
| Parameter   | Data Type  | Description |
| ------------ | ------------ | ------------ |
| symbol  | string | the name of the contract |
| fundingRate  | decimal  | funding rate |
| nextSettleTime  | long  | next liquidate time |

### Index price

> subscribe

```json
{
    "method":"sub.index.price",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> unsubscribe

```json
{
    "method":"unsub.index.price",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> Example

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

Get the index price, and will keep updating  if there is  any changes.

subscribe , unsubscribe, example is shown on the right.

**Response parameters:**
	
| Parameter   | Data Type  | Description |
| ------------ | ------------ | ------------ |
| symbol  | string | the name of the contract  |
| price  | decimal  | price |

### Fair price

> Subscribe

```json
{
    "method":"sub.fair.price",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> Unsubscribe

```json
{
    "method":"unsub.fair.price",
    "param":{
        "symbol":"BTC_USDT"
    }
}
```

> Example

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

subscribe , unsubscribe, example is shown on the right.

**Response parameters**
	
| Parameter   | Data Type  | Description |
| ------------ | ------------ | ------------ |
| symbol  | string | the name of the contract  |
| price  | decimal  | price |

## Private Channels

### Login authentication

> Payload

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
		"apiKey":"apiKey", // openapi need to fill in this parameter，Parameters are constructed in accordance with the OpenAPI documentation
		"reqTime":"reqTime", // openapi need to fill in this parameters，Parameters are constructed in accordance with the OpenAPI documentation
		"signature":"signature" // openapi need to fill in this parameters，Parameters are constructed in accordance with the OpenAPI documentation
	}
}
```

**Response parameters:**

Success: none, failure: return the corresponding error message, channel = rs.error

Login successful (channel = rs.login)

### Order

> Payload

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

| Parameter   | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| orderId  | long  | orderid |
| symbol  | string  | the name of the contract |
| positionId  | long  | position id |
| price  | decimal  | trigger  price |
| vol  | decimal  | trigger  volume |
| leverage  | long  | leverage |
| side  | int  | order side 1open long,2close short,3open short 4 close long |
| category  | int  | order category:1limit order, 2 system take-over delegate, 3 close delegate 4 ADL reduction |
| orderType  | int  | true  | Order type,1: limit order,2:Post Only Maker,3: close or cancel instantly ,4: close or cancel completely |
| dealAvgPrice  | decimal  | transaction average price |
| dealVol  | decimal   | transaction volume |
| orderMargin  | decimal   | order margin  |
| usedMargin  | decimal   | used margin  |
| takerFee  | decimal   | taker fee |
| makerFee  | decimal   | maker fee |
| profit  | decimal   | close profit |
| feeCurrency  | string   | fee currency |
| openType  | int   | open type,1:isolated,2:cross| 
| state  | int   | order state,1 uninformed,2 uncompleted,3 completed,4 cancelled,5 invalid |
| errorCode  | int   |error code,0:normal，1：parameter errors，2：account balance is insufficient，3：the position does not exist，4： position insufficient，5：For long positions, the order price is less than the close price, while for short positions, the order price is more than the close rice.，6：When opening long, the close price is more than the fair price, while when opening short, the close price is less than the fair price ,7:exceed the risk limit，8:system  cancelled |
| externalOid  | string   |external order id |
| createTime  | date   | create time |
| updateTime  | date   | update time |

### Asset

> Payload

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

| Parameter   | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| currency  | string  | currency |
| positionMargin  | decimal   | position margin |
| frozenBalance  | decimal   | frozen balance |
| availableBalance  | decimal   | available balance |
| cashBalance  | decimal   | drawable balance |

### Position

> Payload

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
 	
| Parameter  | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| positionId  | long  | position id |
| symbol  | string  | the name of the contract |
| holdVol  | decimal  | hold volume |
| positionType  | int  | position type， 1long 2short |
| openType  | int   | open type， 1isolated 2cross |
| state  | int   | position state,1holding2system holding 3closed  |
| frozenVol  | decimal   | frozen volume |
| closeVol  | decimal   | close volume|
| holdAvgPrice  | decimal   | hold average price |
| closeAvgPrice  | decimal   | close average price |
| openAvgPrice  | decimal   | open average price |
| liquidatePrice  | decimal   | liquidate price |
| oim  | decimal   | original initial margin |
| adlLevel  | int   | the value of ADL is 1-5. If it is empty,  wait for the refresh |
| im  | decimal   | initial margin， add or subtract this item can be used to adjust the liquidate price |
| holdFee  | decimal   | hold fee,  positive  means u get it,  negative means lose it |
| realised  | decimal   | realized profit and loss  |
| createTime  | date   | create time|
| updateTime  | date   | update time |

### Risk limitation

```channel = push.personal.risk.limit```

| Parameter   | Data Type   | Description  |
| ------------ | ------------ | ------------ |
| symbol  | string  | the name of the contract |
| positionType  | int  | position type 1:long，2:short|
| riskSource| int | Source of risk 0:other 1:Liquidation Service|
| level  | int   | current risk level |
| maxVol  | decimal   | maximum position volume |
| maxLeverage  | int   | maximum leverage ratio |
| mmr  | decimal   | maintenance margin rate |
| imr  | decimal   | initial margin rate|

### Adl automatic reduction of position level

> Payload

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
 	

| Parameter   | Data Type  | Description |
| ------------ | ------------ | ------------ |
| adlLevel| int   | the current adl level ：1-5|
| positionId  | long   | position id |

### Position Mode


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

| Parameter   | Data Type   | Description  |
| ------------ | ------------ | ------------ |
|positionMode|int|position mode,1:hedge，2:one-way|

## How is depth information maintained

> Example: Submit subscription information

```json
{"method":"sub.deal",
"param":{
    "symbol":"BTC_USDT"
}
}
```

> subscribe succeed response

```json
{"channel":"rs.sub.deal",
"data":"success",
"ts":"1587442022003"
}
```

> subscribe failed response

```json
{"channel":"rs.error",
"data":"Contract doesn't exist!",
"ts":"1587442022003"
}
```

**How is incremental depth information maintained:**

1. Though /api/v1/contract/depth/BTC_USDT to get full amount of depth information, save the current version.
2. Subscribe to ws depth information, if the received data version more than the current version after update,  the later received update cover the previous one at the same price.
3. Through /api/v1/contract/depth_commits/BTC_USDT/1000 get  the latest 1000 depth snapshots.
4. Discard version data from the snapshot obtained by Version (less than step 3 )for the same price in the current cached depth information
5. Update the contents of the deep snapshots to the local cache and keep updating from the event received by the WS
6. The version of each new event should be exactly equal to version+1 of the previous event, otherwise packet loss may occur. In case of packet loss or discontinuous version of the event retrieved, please re-initialize from Step 3.
7. The amount of hanging orders in each event represents the absolute value of the current hanging orders of the price, rather than the relative change.
8. If the amount of a hanging order corresponding to a certain price is 0, it means that the hanging order at that price has been cancelled, the price should be removed.

**Subscriptions，subscribe succeed response:**  

channel : rs. +  subscription method，
data is "success"
