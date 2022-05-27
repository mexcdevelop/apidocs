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

# Introduction

Welcome to use MEXC API! This document provides you with REST API related information to help you obtain market information, manage account information, and conduct trading.

## What is API？

API is an Application Programming Interface, abbreviated as API, which is a settlement interface. It defines the interaction between multiple applications, the types of calls or requests that can be made, how to make calls or requests, the data format that should be used, the conventions that should be followed, etc. The API document describes how the application interacts with our exchange.

## Instructions

Step: if the developer needs to use the API, please first <a href="https://www.mexc.io/user/openapi" target="_blank">create APIKey</a> and then carry out the development of trading according to the details of this document. If you have any problems or suggestions in the process of using it, please let us know in time.

- Please refer to <a href="https://support.mxc-exchange.com/hc/en-001/articles/360055933652" target="_blank">this page</a> to set the API Key.
- When setting API key, it is recommended to set IP access whitelist for security.
- Never tell anyone your API key/secret.

##Interface type REST API

REST, the abbreviation of Representational State Transfer, is a popular communication mechanism based on HTTP. Its structure is clear, standard, easy to understand, easy to expand, and is being adopted by more and more websites. Its advantages are as follows:

- Each URL represents a resource in RESTful structure;
- Some presentation layer of the resource is passed between the client and the server;
- It is suggested that developers use Rest API for currency trading or asset withdrawal;
- The client uses four HTTP instructions to operate the server-side resources to achieve "Representational State Transfer";

## API V1 or API V2

<aside class="notice">
API V1 will no longer be maintained starting from the end of June 2021. Please prepare in advance.
</aside>

We recommend that all users build their applications on V2 of the API. Using V2 has the following advantages:

- Compared with API V1, the security and rationality of API V2 signature are better.
- Improved performance for particular endpoints / channels.
- Our official customer base provides a wider range of support.

# Change log

| Effective Time（UTC+8) | Interface | Update Type | Description |
|-----|-----|-----|-----|
|2020-01-09|*|Add|REST API V2 released|
|2020-02-24|/open/api/v2/order/place<br/>/open/api/v2/order/place_batch<br/>/open/api/v2/order/cancel|Update|Add support for client order id|
|2020-07-20|/open/api/v2/order/cancel_by_symbol|Add|New API for canceling orders|
|2021-03-01|/open/api/v2/order/list| change | Parameter states change to the mandatory than optional, and only single statu query supported; Parameter start_time default queries in last 7 days, maximum is 30 days; Fixed the situation of incorrect time about parameter start_time|
|2021-08-27|/open/api/v2/market/api_default_symbols|Add|The newly acquired platform supports the trading pair endpoint of API transactions; Cancel the display of signature method 2 and retain the signature method of the same futures.|

# Integration guide

## Access URLs

Please make API requests with the following base urls:

- ```https://www.mexc.com```

## Request Format

The APIs accept GET, POST or DELETE request, as will be described in later sections

- For a GET or DELETE reqeust, all parameters are path paremeters (query string)
- For a POST reqeust, business parameters are to be put in request body and of JSON format(with```content-type```set to```application/json```), they will not be used for signing of the request. To calculate signature, params ```api_key```、```req_time```、```recv_window```(optional)、```sign``` need to be sent as path parameter

## Response Format

Response is of JSON format for all APIs

## Signature

Public APIs (for market data) and private APIs (for account and order operations) are provided.<br/><br/>Signature is not required for public APIs.<br/><br/>And for private APIs, signature is required and will be used for checking the validity of each request.<br/><br/>Please refer to [Signature Method](#signature-method) for detail

## Time Security

```
 if (req_time > (server_time + 2 ) || req_time < (server_time - recv_window)) {
   // reject request     
 }else{
  // process request
 }

```

Parameter ```req_time``` is required for each private API, After API server receives a request, timestamp validation will be conducted to make sure the requesting time from client is valid.

The request is considered invalid if the received req_time is less or more than 10 seconds (the default value) (the time window can be adjusted by sending an optional header parameter ```recv-window``` with a maximum value of 60, ```recv_window``` of 30 seconds or more is not recommended)

## Signature Parameters

Parameters related to request signature

|   Components   |   Description  |
| ------------ | -------------------------- |
|   param ```api_key```  |  access key from API key    |
|   param ```req_time```  |  the timestamp when sending the request, string of 10 digits stands for the seconds since Unix epoch, for instance ```1572537600```    |
|   param ```sign```  |  calculated signature    |
|   HTTP request method  |  GET, POST or DELETE as described in later sections for each API    |
|   URI  |  URI of the API    |
|   business parameters  |  business parameters required by each API, only the business parameters of ```GET``` and ```DELETE``` requests will be included in the signature calulation |

## Creating API key

API key can be created in the ```User Center``` of MEXC site. There are two parts of API key, ```Access key``` and ```Secret key```，both of them will be used for calculating and validating a signature. Please grant appropriate permissions for the created API key, before using it. 

<aside class="warning">
Secret key will ONLY be displayed in the page when API key is generated, please make records accordingly
</aside>

## Signature Method 

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

2. For private endpoint, ApiKey, Request-Time(Timestamp string displayed in milliseconds
	), Signature and Content-Type need to be passed into the header, must be specified as application / JSON, Recv-Window (optional) parameters, Signature is a signature string. The signature rules are as follows:

	1) When signing, you need to get the request parameter string first. It is "" if there is no parameter:

		For GET/DELETE requests, the service parameters are spliced in dictionary order with & interval, and finally the signature target string is obtained (in the API of batch operation, if there are special symbols such as comma in the parameter value, these symbols need to be URL encoded when signing).

		For POST requests, the signature parameter is a JSON string (dictionary sorting is not required).

	2) After obtaining the parameter string, the signature target string is spliced. The rule is: accessKey + timestamp + obtained parameter string.

	3) The HMAC SHA256 algorithm is used to sign the target string, and finally the signature is passed into the header as a parameter.

Note：

	1) When the service parameter participating in the signature is null, it does not participate in the signature. For the path parameter, it does not participate in the signature; note that when get request stitches the parameter and pass it in the URL, if the parameter is null, it will be parsed into "" in the background parsing, fixed post request, when the parameter is null, do not pass the parameter, or set the value of the parameter to "" when signing, otherwise signature verification will fail.
	
	2) When requesting, put the value of Request-Time used in signing into the Request-Time parameter of the header, put the obtained signature string into the signature parameter of the header, put the Access Key of APIKEY into the ApiKey parameter of the header, and pass the other service parameters.
	
	3) The obtained signature string does not need to be base64 encoded.

## Error Code

The following error information can be returend

|   Code     |   Description    |
| ------------ | -------------------------- |
| 400     | Invalid parameter |
| 401     | Invalid signature, fail to pass the validation |
| 429     | Too many requests, rate limit rule is violated |
| 10072     | Invalid access key |
| 10073     | Invalid request time |
| 30000     | Trading is suspended for the requested symbol |
| 30001     | Current trading type (bid or ask) is not allowed |
| 30002     | Invalid trading amount, smaller than the symbol minimum trading amount |
| 30003     | Invalid trading amount, greater than the symbol maximum trading amount |
| 30004    | Insufficient balance |
| 30005    | Oversell error |
| 30010    | Price out of allowed range |
| 30016    | Market is closed |
| 30019    | Orders count over limit for batch processing |
| 30020    | Restricted symbol, API access is not allowed for the time being |
| 30021    | Invalid symbol |

## Rate Limit

There is rate limit for API access frequency, upon exceed client will get code 429: Too many requests.

The account is used as the basic unit of speed limit for the endpoints that need to carry access keys. For endpoints that do not need to carry access keys, IP addresses are used as the basic unit of rate limiting.

The default rate limiting rule for an endpoint is 20 times per second.

## ENUM Definition

### Order State

|  |   |
|----------|------------|
|NEW|New order, waiting to be filled|
|FILLED|Order fully filled|
|PARTIALLY_FILLED|Order partially filled|
|CANCELED|Order canceled|
|PARTIALLY_CANCELED|Order filled partially, and then the rest of the order is canceled|


### Order Type

|  |   |
|----------|------------|
|LIMIT_ORDER|Limit price order|
|POST_ONLY|Post only maker order|
|IMMEDIATE_OR_CANCEL|Immediate or cancel|


### Trade Type

|  |   |
|----------|------------|
|BID|Buy|
|ASK|Sell|

### Time Interval

m -> minute; h -> hour; d -> day; M -> month

- 1m
- 5m
- 15m
- 30m
- 60m
- 4h
- 1M

# General data

## All symbols

> Response example

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

Request parameters：None

Response

| Feild | Data type | Description |
|----------|------------|------------|
|symbol|string|symbol name|
|state|string|symbol status, whether available for trading|
|price_scale|integer|price precision|
|quantity_scale|integer|quantity precision|
|min_amount|string|minimum amount|
|max_amount|string|maximum amount|
|maker_fee_rate|string|maker fee|
|taker_fee_rate|string|taker fee|
|limited|string|API trading enables marking (Valid values: true, false)|
|etf_mark|integer|Etf identification, 0 represents not ETF, and positive and negative integers represent ETF|
|symbol-partition|string|Trading areas, such as the Main|

## Current System Time

> Response example

```json
{
    "code": 200,
    "data": 1573542414480
}
```

- **GET** ```/open/api/v2/common/timestamp```

Request parameters：None

Response

| Field | Data type | Description |
|----------|------------|------------|
|data|long|System timestamp, milliseconds since Unix epoch|

## Ping

> Response example

```json
{
    "code": 200
}
```

- **GET** ```/open/api/v2/common/ping```

Request parameters：None

Response

| Field | Data type | Description |
|----------|------------|------------|
|code|int|With response indicates server OK|

## Obtain the transaction pairs that supports API transactions on the platform.

> Response example

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

Obtain the transaction pairs that supports API transactions on the platform.

- **GET** ```/open/api/v2/market/api_default_symbols```

<aside>
Rate Limit : 20times/2s
</aside>

**Request Parameters:**

None

**Response Parameters:**

| Parameter  | Data Type | Description  |
| ------------ | ------------ | ------------ |
| code | integer | Status code | 
| message | string | Misdescription (If there has )） | 
| <data> | array |  | 
| symbol  | string  | symbol name |
| </data> |  |  | 

# Market Data

## Ticker Information

> Response example

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

Request parameters：

| Parameter | Data type | Mandatory | Description |
|-----|-----|-----|-----|
|symbol|string|Y|symbol name|

Response：

| Field | Data type | Description |
|-----|-----|-----|
|symbol|string|symbol name|
|volume|string|deal total amount of this period|
|high|string|the highest price of this period|
|low|string|the lowest price of this period|
|bid|string|current highest bid price|
|ask|string|current lowest ask price|
|open|string|open price of this period|
|last|string|the latest deal price|
|time|string|timestamp of the latest quote|
|change_rate|string|price change rate of this period|

<aside class="notice">
The module is refreshed according to a 24-hour cycle.
</aside>


## Market depth

> Response example

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

Request parameters：

| Parameter | Data type | Mandatory | Description | Allowed range |
|-----|-----|-----|-----|-----|
|symbol|string|Y|symbol name| |
|depth|string|Y|number of depth to be returned| 1~2000|

Response：

| Field | Data type | Description |
|-----|-----|-----|
|bids|object|bids data, including the fields of price and quantity|
|asks|object|asks data, including the fields of price and quantity|

## Latest Deals

> Response example

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

Request paramters：

| Parameter | Data type | Mandatory | Description | Allowed range |
|-----|-----|-----|-----|-----|
|symbol|string|Y|symbol name| |
|limit|integer|N|Number of records to be returned| 1~1000，default to 100|

Response：

| Field | Data type | Description |
|-----|-----|-----|
|trade_time|long|deal time|
|trade_price|string|deal price|
|trade_quantity|string|volume|
|trade_type|string|trade type, BID or ASK|

## Candlestick Data

> Response example

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

Request parameters：

| Parameter | Data type | Mandatory | Description | Allowed range |
|-----|-----|-----|-----|-----|
|symbol|string|Y|symbol name| |
|interval|string|Y|inteval|of minutes: 1m, 5m, 15m, 30m, 60m. of hour: 4h, of day: 1d, of month: 1M|
|start_time|long|N|start time, string of 10 digits stands for the seconds since Unix epoch| |
|limit|integer|N|number of records to be returned| 1~1000，default to 100|

Response：

| Field | Data type |
|-----|-----|
|time|start time, string of 10 digits stands for seconds since Unit epoch|
|open|opening price|
|close|closing price|
|high|highest price|
|low|lowest price|
|vol|volume|
|amount|trading volume in the pricing currency|


## Get currency information

This endpoint returns a list of currency details.

- **GET** ```/open/api/v2/market/coin/list```

<aside>
Rate Limit : 20times/2s
</aside>

**API Permission:** Read(for public )

**Request Parameters:**

| Parameter  | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| currency  | string  |  false  | Crypto currency |

**Response Parameters:**

| Parameter  | Data Type | Description  |
| ------------ | ------------ | ------------ |
| code  | int  | Status code |
| message  | string  |  Misdescription (If there has ) |
| currency  | string  | Crypto currency |
| full_name  | string  | Crypto currency name |
| chain  | string  | Block chain name |
| precision  | string  | Currency precision |
| is_withdraw_enabled  | string  | Withdrawable  or not |
| is_deposit_enabled  | string  | Deposit or not  |
| deposit_minConfirm   | number   | Minimum confirmation of blocks |
| withdraw_limit_max   | number   | Maximum withdraw amount in each request |
| withdraw_limit_min  | number   | Minimum withdraw amount in each request  |
| fee  | string   | Withdraw fee |

Note: 
the hidden currencies and off shelve currencies does not display; 


# Account Information

## Balance

> Resposne example

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

- **GET** ```/open/api/v2/account/info```

Request parameters：None

Response：

Balance information of each currency

| Field | Data type | Description |
|-----|-----|-----|
|frozen|string|frozen balance|
|available|string|available balance|

## Obtain the trading pairs of the accounts that can trade through the API

> Response example

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

Obtain the transaction pairs where the API transactions and private endpoint are enabled by the account. 

- **POST** ```/open/api/v2/market/api_symbols```

<aside>
Rate Limit : 20times/2s
</aside>

**Request Parameters:**

None

**Response Parameters:**

| Parameter  | Data Type | Description  |
| ------------ | ------------ | ------------ |
| code | integer | Status code | 
| message | string | Misdescription (If there has )） | 
| <data> | array |  | 
| symbol  | string  | symbol name |
| </data> |  |  | 

# Spot Trading

## Place Order

> Response example

```json
{
    "code": 200,
    "data": "c8663a12a2fc457fbfdd55307b463495"
}
```

- **POST** ```/open/api/v2/order/place```

Request parameters：

| Parameter | Data type | Mandatory | Description | Allowed range |
|-----|-----|-----|-----|-----|
|symbol|string|Y|symbol name| |
|price|string|Y|price| |
|quantity|string|Y|quantity| |
|trade_type|string|Y|trade type|BID，ASK|
|order_type|string|Y|order type|LIMIT_ORDER，POST_ONLY，IMMEDIATE_OR_CANCEL|
|client_order_id|string|N|client order id|With maximum length of 32 characters|

<aside class="notice">
It's the user's responsibility to maintain the uniqueness of the client order id
</aside>

Response：

| Field | Data type | Description |
|-----|-----|-----|
|data|string|new order id|

## Cancel Order

> Response example

```json
{
    "code": 200,
    "data": {
        "504feca6ba6349e39c82262caf0be3f4": "success"
    }
}
```

- **DELETE** ```/open/api/v2/order/cancel```

Request parameters：

| Parameter | Data type | Mandatory | Description |
|-----|-----|-----|-----|
|order_ids|string|N|order id. Cancel in batch is supported, the ids should be separated by comma. The maximum order count in a batch is 20|
|client_order_ids|string|N|Client order id of orders to be canceled. Cancel in batch is supported, the ids should be separated by comma. The maximum order count in a batch is 20|


Response：

| Field | Data type | Description |
|-----|-----|-----|
|data|map|order id and the relevant processing result|

<aside class="notice">
Either order_ids or client_order_ids have to be picked as parameter. When both of them exist, the client_order_ids will be ignored
</aside>

<aside class="notice">
When client recieves response from server, it only means the cancelling request has been accepted, doesn't mean the cancellation is finished
</aside>

## Place Order In Batch

> Response example

> response when requesting with client_order_id

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

> response when requesting without client_order_id

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

Request parameters：

| Parameter | Data type | Mandatory | Description | Allowed range |
|-----|-----|-----|-----|-----|
|symbol|string|Y|symbol name| |
|price|string|Y|price| |
|quantity|string|Y|quantity of the order| |
|trade_type|string|Y|trade type|BID，ASK|
|order_type|string|Y|order type|LIMIT_ORDER，POST_ONLY，IMMEDIATE_OR_CANCEL|
|client_order_id|string|N|client order id|With maximum length of 32 characters|

Response：

| Field | Data type | Description |
|-----|-----|-----|
|data|map|client order id and the corresponding new order id|

<aside class="notice">
It's the user's responsibility to maintain the uniqueness of the client order id
</aside>

<aside class="notice">
For each batch request, the parameter client_order_id should be consistent, meaning if any of the order contains client_order_id, then all orders should contain client_order_id as well
</aside>

## Open Orders

> Response example

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

Request parameters：

| Parameter | Data type | Mandatory | Description | Allowed range |
|-----|-----|-----|-----|-----|
|symbol|string|Y|symbol name| |
|start_time|string|N|start time| |
|limit|string|N|number of records to be returned| 1~1000，default to 50 |
|trade_type|string|N|order type| BID，ASK |


Response：

| Field | Data type | Description |
|-----|-----|-----|
|symbol|string|symbol name|
|id|string|order id|
|price|string|order price|
|quantity|string|order quantity|
|remain_quantity|string|remaining quantity|
|remain_amount|string|remaining volume|
|create_time|string|order create time|
|state|string|order state|
|type|string|order type|
|client_order_id|string|client order id|


## All Orders

> Response example

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

Request parameters：

| Parameter | Data type | Mandatory | Description | Allowed range |
|-----|-----|-----|-----|-----|
|symbol|string|Y|symbol name| |
|start_time|string|N|start time| the default is the last 7 days, and the maximum query is 30 days. |
|limit|string|N|number of records to be returned| 1~1000，default to 50|
|trade_type|string|Y|order type| BID，ASK |
|states|string|Y|state to be quired| NEW：Unfilled ；FILLED：Filled；PARTIALLY_FILLED：Partially filled；CANCELED：Canceled；PARTIALLY_CANCELED：Partially canceled |


Response：

| Field | Data type | Description |
|-----|-----|-----|
|symbol|string|symbol name|
|id|string|order id|
|price|string|order price|
|quantity|string|order quantity|
|deal_quantity|string|deal quantity|
|deal_amount|string|volume|
|create_time|string|order create time|
|state|string|order state|
|type|string|order type|
|client_order_id|string|client order id|


## Query Orders

> Response example

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

Request parameters：

| Parameter | Data type | Mandatory | Description | Allowed range |
|-----|-----|-----|-----|-----|
|order_ids|string|Y|order id, batch process is supported. There can be 20 ids in one batch at most| |

Response：

| Field | Data type | Description |
|-----|-----|-----|
|symbol|string|symbol name|
|id|string|order id|
|price|string|order price|
|quantity|string|order quantity|
|deal_quantity|string|deal quantity|
|deal_amount|string|volume|
|create_time|string|order create time|
|state|string|order state|
|type|string|order type|
|client_order_id|string|client order id|


## Deals History

> Response example

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

Request parameters：

| Parameter | Data type | Mandatory | Description | Allowed range |
|-----|-----|-----|-----|-----|
|symbol|string|Y|symbol name| |
|limit|string|N|number of records to be returned| 1~1000，default to 50|
|start_time|string|N|start time| |


Response：

| Field | Data type | Description |
|-----|-----|-----|
|symbol|string|symbol name|
|order_id|string|order id|
|trade_type|string|trade type|
|quantity|string|deal quantity|
|price|string|deal price|
|amount|string|volume|
|fee|string|deal fee|
|fee_currency|string|fee currency|
|is_taker|bool|taker order or not|
|create_time|long|deal time|


## Deals Detail

> Response example

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

Request parameters：

| Parameter | Data type | Mandatory | Description | Allowed range |
|-----|-----|-----|-----|
|order_id|string|Y||

Response：

| Field | Data type | Description |
|-----|-----|-----|
|symbol|string|Symbol name|
|order_id|string|order id|
|trade_type|string|trade type|
|quantity|string|deal quantity|
|price|string|deal price|
|amount|string|volume|
|fee|string|deal fee|
|fee_currency|string|fee currency|
|is_taker|bool|taker order or not|
|create_time|long|deal time|

## Cancel Orders By Symbol

> Response example

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

Request parameters：

| Parameter | Data type | Mandatory | Description | Allowed range |
| ---------- | ------------ | ------------ | -------- | ----- |
| symbol     | string       | Y | symbol name   | |

Response：

| Field | Data type | Description |
| ---------- | ------------ | -------------------- |
|data|map|order id and the relevant processing result|

<aside class="notice">
Either order_ids or client_order_ids have to be picked as parameter. When both of them exist, the client_order_ids will be ignored
</aside>

<aside class="notice">
When client recieves response from server, it only means the cancelling request has been accepted, doesn't mean the cancellation is finished
</aside>
# Asset

Only the endpoint handling the reading of deposit and withdrawal information is open currently, the withdrawal endpoint will be made available soon (Please contact the online customer service if you wish to access it now).

## Get Deposit Address

This endpoint is used to query the address of a specific currency in its block chain, which is available for both parent-account and  sub-account .

- **GET** ```/open/api/v2/asset/deposit/address/list```

<aside>
Rate Limit : 20times/2s
</aside>

**API Permission:** Read

**Request Parameters:**

| Parameter  | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| currency  | string  |  true  | Crypto currency |

**Response Parameters:**

| Parameter  | Data Type | Description  |
| ------------ | ------------ | ------------ |
| code  | int  | Status code |
| message  | string  | Misdescription (If there has )） |
| currency  | string  | Crypto currency |
| chain  | string  | Block chain name |
| address  | string   | Deposit address |

Note:
 1, Signature certification is required for the private endpoint ;
 2. Only return the generated address;

## Query Deposit Records

- **GET** ```/open/api/v2/asset/deposit/list```

<aside>
Rate Limit : 20times/2s
</aside>

**API Permission:** Read

**Request Parameters:**

| Parameter  | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| currency  | string  | false  | Crypto currency |
| state  | string  | false  | Status  |
| start_time  | long  | false  | The start time, unit:ms, defult:1 day. |
| end_time  | long  | false  | The ending time, unit:ms |
| page_num  | number  | false  | Number of pages, default 1 |
| page_size  | number  | false  | Size of pages, default 20, maximum 50 |

**Response Parameters:**

| Parameter  | Data Type | Description  |
| ------------ | ------------ | ------------ |
| code  | integer  | Status code |
| message  | string  | Misdescription (If there has ) |
| currency  | string  | Crypto currency |
| actual_amount  | number  | The actual received  amount |
| address  | string  | Deposit  address |
| amount  | number  | Deposit  amount |
| confirmations  | number  | Confirmation of blocks |
| require_confirmations  | number  | Minimum confirmation of blocks |
| create_time  | number  | Initiate withdraw time |
| explorer_url  | string  | Block browser address |
| fee   | string  | Fee |
| member_id   | string  | UserID |
| state  | string  | Status |
| txid  | string  | Trading hash |
| update_time  | string  | Update time |
| wallet_type  | string  | The wallet type |
| current_page  | number  | The current page |
| current_result  | number  | Size of the current page |
| total_result  | number  | The total size |
| total_page  | number  | The total pages |

Note: A single query can retrieve a maximum range of 10 days, and maximum retrieve records is the last 180 days.

## Query Withdraw Address List

- **GET** ```/open/api/v2/asset/address/list```

<aside>
Rate Limit : 20times/2s
</aside>

**API Permission:**Read

**Request Parameters:**

| Parameter  | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| currency  | string  | false  | Crypto currency |
| page_num  | number  | false  | Number of pages, default 1 |
| page_size  | number  | false  | Size of pages, default 20, maximum 50 |

**Response Parameters:**

| Parameter  | Data Type | Description  |
| ------------ | ------------ | ------------ |
| code  | integer  | Status code |
| message  | string  | Misdescription (If there has )） |
| chain  | string  | Block chain name |
| currency  | string  |Crypto currency |
| address  | string  | Address  |
| address_tab  | string  | Address tags | 
| current_page  | number  | The current page |
| current_result  | number  | Size of the current page |
| total_result  | number  | The total size |
| total_page  | number  | The total pages |

## Query Withdraw Records

- **GET** ```/open/api/v2/asset/withdraw/list```

<aside>
Rate Limit : 20times/2s
</aside>

**API Permission:**Read

**Request Parameters:**

| Parameter  | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| currency  | string  | false  | Crypto currency |
| withdraw_id  | string  | false  | Withdraw ID |
| state  | string  | false  | Status |
| start_time  | long  | false  | The start time, unit:ms, defult:1 day. |
| end_time  | long  | false  | The ending time, unit:ms |
| page_num  | number  | false  | Number of pages, default 1 |
| page_size  | number  | false  | Size of pages, default 20, maximum 50 |

**Response Parameters:**

| Parameter  | Data Type | Description  |
| ------------ | ------------ | ------------ |
| code  | integer  | Status code |
| msg | string  | Misdescription (If there has ) |
| currency  | string  | Crypto currency |
| actual_amount  | number  | The actual received amount |
| actual_fee  | number  | Withdraw fee |
| amount  | number  | Withdraw amount |
| create_time  | number  | Initiate withdraw time |
| explorer_url  | string  | Block browser address |
| fee   | string  | Fee |
| id  | string  | Withdraw ID |
| member_id   | string  | UserID |
| remark  | string  | Withdraw notes  |
| state  | string  | Status |
| txid  | string  | Trading hash |
| update_time  | string  | Update time |
| wallet_type  | string  | The wallet type |
| current_page  | number  | The current page |
| current_result  | number  | Size of the current page |
| total_result  | number  | The total size |
| total_page  | number  | The total pages |

Note: A single query can retrieve a maximum range of 10 days, and maximum retrieve records is the last 180 days.

## Withdraw

- **POST** ```/open/api/v2/asset/withdraw```

<aside>
Rate Limit : 20times/2s
</aside>

**API Permission:** Write 

**Request Parameters:**

| Parameter  | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| currency  | string  | true  | Crypto currency |
| chain | string  | false  | Chain name, reference the GET/open/API/v2 / market/coin/list (Get currency information), multiple chain required (such as withdraw  USDT to OMNI must set this parameter to "OMNI",  withdraw  USDT to TRX must set this parameter to  "TRC - 20", withdraw  USDT to ERC20 must set this parameter to  "ERC - 20"), do not need to set this parameter if there is single chain, when the more details reference to the endpoint of  “Get currency information”. |
| amount  | number  | true  | Withdraw amount  |
| address | string  | true  | withdraw address   Note: memo please use : for splicing |
| remark  | string  | false  | Note |


**Response Parameters:**

| Parameter  | Data Type | Description  |
| ------------ | ------------ | ------------ |
| code  | number  | Status code  |
| msg | string  | Misdescription (If there has ) |
| data  | object  |  |
| withdrawId  | string  | Withdraw ID |

## Cancel a withdraw request

- **DELETE** ```/open/api/v2/asset/withdraw```

<aside>
Rate Limit : 20times/2s
</aside>

**API Permission:** Write

**Request Parameters:**

| Parameter  | Data Type   | Mandatory  |  Description |
| ------------ | ------------ | ------------ | ------------ |
| withdraw_id  | string  | true  | Withdraw ID |

**Response Parameters:**

| Parameter  | Data Type | Description  |
| ------------ | ------------ | ------------ |
| code  | number  | Status code |
| msg | string  | Misdescription (If there has ) |

## Internal assets transfer

Support the transfer between Spot and Contract accounts in parent-account.

Support the transfer between Spot and Contract accounts in sub-account.

- **POST** ```/open/api/v2/asset/internal/transfer```

<aside>
Rate Limit : 2 times/s
</aside>

**API Permission:** Write

**Request Parameters:**

| Parameter | Data Type | Mandatory  | Description |
| ------------ | ------------ | ------------ | ------------ |
| currency | string | true | Currency，Ex. usdt|
| amount | number | true | Transfer amount |
| from | string | true | Transfer-out account，spot account MAIN，Contract account CONTRACT|
| to | string | true | Transfer-in account，spot account MAIN，futures account CONTRACT|

**Response Parameters:**

| Parameter | Data Type | Description |
| ------------ | ------------ | ------------ |
| code | number  | Status code |
| msg | string | Error message (if any) |
| result_list | object |  | 
| transact_id | string | Transfer id |
| currency | string | Currency  |
| amount | string | Amount  |
| from | string | Transfer-out account |
| to | string | Transfer-in account |
| transact_state | string | Transaction status |


Note：

1.Transfer is not available for isolated-margin account. 

2. Successful submission does not mean successful transfer. You can check whether the transfer is successful through the transfer order query endpoint. 

## Get internal assets transfer records

It supports the query of internal asset transfer records, and up to 10 days through a single query, and records of the past 180 days can be inquired.

- **GET** ```/open/api/v2/asset/internal/transfer/record```

<aside>
Rate Limit : 2 times/s
</aside>

**API Permission:** Read

**Request Parameters:**

| Parameter | Data Type | Mandatory  | Description |
| ------------ | ------------ | ------------ | ------------ |
| currency | string | false | Currency  （Return all currencies without filling）|(delete space)
| from | string | false | Transfer-out account ，spot account 、isolated-margin account 、futures account ，return all without filling |
| to | string | false | Transfer-in account，spot account, isolated-margin account, futures account，return all without filling |
| start_time | long | false | Start time|
| end_time | long | false | End time
| page_num | number | false | default 1 |
| page_size | number | false | Page size，default 20, maximum 50 |

**Response Parameters:**

| Parameter | Data Type | Description |
| code | number  | Status code |
| msg | string | Error message (if any) |
| currency | string | Currency  |
| amount | string| Amount  |
| from | string | Transfer-out account，spot account, isolated-margin account, contract account |
| to | string | Transfer-in account ，spot account、isolated-margin account、futures account  |
| transact_state | string | Transfer status  Success SUCCESS、Fail  FAILED、Transferring WAIT|
| transact_id | string | Transfer id |
| total_size | int | The total size |
| total_page | int | The total pages |

## Get transferable assets

This endpoint can obtain transferable assets in a specified account and currency.

- **GET** ```/open/api/v2/account/balance```

<aside>
Rate Limit : 2 times/s
</aside>

**API Permission:** Read

**Request Parameters:**

| Parameter | Data Type | Mandatory  | Description |
| ------------ | ------------ | ------------ | ------------ |
| currency | string | true | Currency  |
| account_type | string | false |  Account type：All、spot account 、futures account ，default spot account  |
| sub_uid | long | false | Sub- account uid，type is invalid with any filling|

**Response Parameters:**

| Parameter | Data Type | Description |
| ------------ | ------------ | ------------ |
| code  | number  | Status code  |
| msg | string  | Misdescription (If there has ) |
| data  | object  |  |
| account_type| string | Account  type |
| currency | string | Currency  |
| balance | string | Asset amount  |
| available | string | Available asset |
| frozen| string | Frozen asset |

## Internal assets transfer order inquiry

Through transfer ID query internal asset transfer order details.

- **GET** ```/open/api/v2/asset/internal/transfer/info```

<aside>
Rate Limit : 2 times/s
</aside>

**API Permission:** Read

**Request Parameters:**

| Parameter | Data Type | Mandatory  | Description |
| ------------ | ------------ | ------------ | ------------ |
| transact_id | String| ture | Transfer id |

**Response Parameters:**

| Parameter | Data Type | Description |
| ------------ | ------------ | ------------ |
| code | number  | Status code |
| msg | string | Error message (if any) |
| transact_id | string | Transfer id |
| currency | String | Currency  |
| amount | String | Transfer amount  |
| from | string | Transfer-out account ，spot account 、isolated-margin account 、futures account  |
| to | string | Transfer-in account ，spot account 、isolated-margin account 、futures account  |
| transact_state | string | Transfer status  Success 、Fail  、Transferring |
