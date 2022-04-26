---
title: API Document

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

includes:

search: true

meta:
  - name: description
    content: Documentation for the mexc global API
---

# Introduction

## API Key Setup

- Some endpoints will require an API Key. Please refer to [this page](https://www.mexc.com/user/openapi) regarding API key creation.
- Once API key is created, it is recommended to set IP restrictions on the key for security reasons.
- Never share your API key/secret key to ANYONE.
  
<aside class="warning">If the API keys were accidentally shared, please delete them immediately and create a new key.</aside>

## API Key Restrictions

Check the required permissions when creating an API Key

## API Library

We provide developers with SDKs in five languages: Python, DotNET, Java, Javascript, and Go, and provide users with methods to call APIs directly through the SDK. Currently supports all interfaces in spot.

[https://github.com/mxcdevelop/mexc-api-sdk](https://github.com/mxcdevelop/mexc-api-sdk)

<aside class="notice">
Any problem please submit <a href="https://github.com/mxcdevelop/mexc-api-sdk/issues" target="_blank"> feedback</a>
</aside>
### Postman Collections

There is now a Postman collection containing the API endpoints for quick and easy use.

This is recommended for new users who want to get a quick-start into using the API.

For more information please refer to this page: [MEXC API Postman](https://github.com/mxcdevelop/mexc-api-postman)

## Contact us

- MEXC API Telegram Grop [MEXC API Support Group](https://t.me/MEXCAPIsupport)
  - For any general questions about the API not covered in the documentation.
  - For any MM questions
- MEXC Customer Support *website、app online customer server*
  -  For cases such as missing funds, help with 2FA, etc.

# Change Log

## **2022-03-29**

- Add Sub-Account Endpoints

## **2022-03-25**

- Add Postman collection

## **2022-03-24**

- Add information of market order 

## **2022-03-21**

- Add order state

## **2022-03-18**

- Add new order type：Market
- Add time page info：startTime and endTime need to the same time

## **2022-03-09**

- Add kline interval

## **2022-02-19**

- Add ETF 
## **2022-02-11**
- New version api

# General Info

## Base endpoint

The base endpoint is：

- ```https://api.mexc.com```

## HTTP Return Codes

- HTTP 4XX return codes are used for malformed requests; the issue is on the sender's side.
- HTTP 403 return code is used when the WAF Limit (Web Application Firewall) has been violated.
- HTTP 429 return code is used when breaking a request rate limit.
- HTTP 5XX return codes are used for internal errors; the issue is on MEXC's side. It is important to NOT treat this as a failure operation; the execution status is UNKNOWN and could have been a success.
## General Information on Endpoints

The API accepts requests of type GET, POST or DELETE

- For GET endpoints, parameters must be sent as a query string.
- For POST, PUT, and DELETE endpoints, the parameters may be sent as a query string or in the request body with content type application/x-www-form-urlencoded. You may mix parameters between both the query string and request body if you wish to do so.
- Parameters may be sent in any order.
- If a parameter sent in both the query string and request body, the query string parameter will be used.


## Header

Relevant parameters in the header

| key                 | Description            |
| ------------------- | ---------------------- |
| ```X-MEXC-APIKEY``` | Access key             |
| ```Content-Type```  | ```application/json``` |

## SIGNED
- SIGNED endpoints require an additional parameter, signature, to be sent in the query string or request body.
- Endpoints use HMAC SHA256 signatures. The HMAC SHA256 signature is a keyed HMAC SHA256 operation. Use your secretKey as the key and totalParams as the value for the HMAC operation.
- The signature is not case sensitive.
- totalParams is defined as the query string concatenated with the request body.

### Timing security

> The logic is as follows:

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

- A SIGNED endpoint also requires a parameter, timestamp, to be sent which should be the millisecond timestamp of when the request was created and sent.
- An additional parameter, recvWindow, may be sent to specify the number of milliseconds after timestamp the request is valid for. If recvWindow is not sent, it defaults to 5000.


Serious trading is about timing. Networks can be unstable and unreliable, which can lead to requests taking varying amounts of time to reach the servers. With recvWindow, you can specify that the request must be processed within a certain number of milliseconds or be rejected by the server.

<aside class="notice"> It is recommended to use a small recvWindow of 5000 or less! The max cannot go beyond 60,000!</aside>

### SIGNED Endpoint Examples for POST /api/v3/order

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

Here is a step-by-step example of how to send a vaild signed payload from the Linux command line using echo, openssl, and curl.

| Key       | Value                            |
| --------- | -------------------------------- |
| apiKey    | mx0aBYs33eIilxBWC5               |
| secretKey | 45d0b3c26f2644f19bfb98b07741b2f5 |



| Parameter  | Value         |
| ---------- | ------------- |
| symbol     | BTCUSDT       |
| side       | BUY           |
| type       | LIMIT         |
| quantity   | 1             |
| price      | 11            |
| recvWindow | 5000          |
| timestamp  | 1644489390087 |

#### **Example 1: As a request body**

- requestBody:
symbol=BTCUSDT&side=BUY&type=LIMIT&quantity=1&price=11&recvWindow=5000&timestamp=1644489390087

**Example 2: As a query string**

- queryString:
symbol=BTCUSDT&side=BUY&type=LIMIT&quantity=1&price=11&recvWindow=5000&timestamp=1644489390087

**Example 3: Mixed query string and request body**

- queryString:
symbol=BTCUSDT&side=BUY&type=LIMIT

- requestBody:
quantity=1&price=11&recvWindow=5000&timestamp=1644489390087

Note that the signature is different in example 3. There is no & between "LIMIT" and "quantity=1".
## Limits


There is rate limit for API access frequency, upon exceed client will get code 429: Too many requests.

The account is used as the basic unit of speed limit for the endpoints that need to carry access keys. For endpoints that do not need to carry access keys, IP addresses are used as the basic unit of rate limiting.

The default rate limiting rule for an endpoint is 20 times per second.

# Market Date Endpoints

## Test Connectivity

> Response

```json
{}
```

- **GET** ```/api/v3/ping```

Test connectivity to the Rest API.

Parameter：

NONE

## Check Server Time

> Response

```json
{
    "serverTime" : 1645539742000
}
```

- **GET** ```/api/v3/time ```
  

Parameter：

NONE

## Exchange Information

> Response

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
      "orderTypes": ["LIMIT", "MARKET", "LIMIT_MAKER"],
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

Current exchange trading rules and symbol information

**Parameter**：

There are 3 possible options:

| Method       | **Example**                                                                   |
| ------------ | ----------------------------------------------------------------------------- |
| No parameter | curl -X GET "https://api.mexc.com/api/v3/exchangeInfo"                        |
| symbol       | curl -X GET "https://api.mexc.com/api/v3/exchangeInfo?symbol=MXUSDT"          |
| symbols      | curl -X GET "https://api.mexc.com/api/v3/exchangeInfo?symbols=MXUSDT,BTCUSDT" |

## Order Book

> Response

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

Parameter：

| name   | Type    | Mandatory | Description     | Scope                 |
| ------ | ------- | --------- | --------------- | --------------------- |
| symbol | string  | YES       | Symbol          |                       |
| limit  | integer | NO        | Returen  number | default 100; max 5000 |

Response：

| name         | Type | Description            |
| ------------ | ---- | ---------------------- |
| lastUpdateId | long | Deal time              |
| bids         | list | Bid [Price, Quantity ] |
| asks         | list | Ask [Price, Quantity ] |

## Recent Trades List

> Response

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

Parameter：

| name   | Type    | Mandatory | Description | Scope                  |
| ------ | ------- | --------- | ----------- | ---------------------- |
| symbol | string  | YES       |             |                        |
| limit  | integer | NO        |             | Default  500; max 1000 |


Response:

| name         | Description                         |
| ------------ | ----------------------------------- |
| id           | Trade id                            |
| price        | Price                               |
| qty          | Number                              |
| quoteQty     | Trade total                         |
| time         | Trade time                          |
| isBuyerMaker | Was the buyer the maker?            |
| isBestMatch  | Was the trade the best price match? |

## Old Trade Lookup

> Response

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

Parameters:

| name   | Type    | Mandatory | Description   | Scope                 |
| ------ | ------- | --------- | ------------- | --------------------- |
| symbol | string  | YES       | Symbol        |                       |
| limit  | integer | NO        | Return number | Default 500; max 1000 |


Response:

| name         | Description                         |
| ------------ | ----------------------------------- |
| id           | Trade id                            |
| price        | Price                               |
| qty          | Number                              |
| quoteQty     | Trade total                         |
| time         | Trade time                          |
| isBuyerMaker | Was the buyer the maker?            |
| isBestMatch  | Was the trade the best price match? |

## Compressed/Aggregate Trades List

> Response

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
  

Get compressed, aggregate trades. Trades that fill at the time, from the same order, with the same price will have the quantity aggregated.

Parameters:

| name      | Type    | Mandatory | Description                                              | Scope                  |
| --------- | ------- | --------- | -------------------------------------------------------- | ---------------------- |
| symbol    | string  | YES       |                                                          |                        |
| startTime | long    | NO        | Timestamp in ms to get aggregate trades from INCLUSIVE.  |                        |
| endTime   | long    | NO        | Timestamp in ms to get aggregate trades until INCLUSIVE. |                        |
| limit     | integer | NO        |                                                          | Default 500; max 1000. |


Response:

| name | Description                         |
| ---- | ----------------------------------- |
| a    | Aggregate tradeId                   |
| f    | First tradeId                       |
| l    | Last tradeId                        |
| p    | Price                               |
| q    | Quantity                            |
| T    | Timestamp                           |
| m    | Was the buyer the maker?            |
| M    | Was the trade the best price match? |

## Kline/Candlestick Data

> Response

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

- **GET** ```/api/v3/klines```
  

Kline/candlestick bars for a symbol.
Klines are uniquely identified by their open time.

Parameters:

| name      | Type    | Mandatory | Description            |
| --------- | ------- | --------- | ---------------------- |
| symbol    | string  | YES       |                        |
| interval  | ENUM    | YES       | ENUM: Kline interval   |
| startTime | long    | NO        |                        |
| endTime   | long    | NO        |                        |
| limit     | integer | NO        | Default 500; max 1000. |


Response:

| Index | Description        |
| ----- | ------------------ |
| 0     | Open time          |
| 1     | Open               |
| 2     | High               |
| 3     | Low                |
| 4     | Close              |
| 5     | Volume             |
| 6     | Close time         |
| 7     | Quote asset volume |

## Current Average Price


> Response

```json
{
  "mins": 5,
  "price": "9.35751834"
}
```

- **GET** ```/api/v3/avgPrice```

Parameters:

| name   | Type   | Mandatory | Description |
| ------ | ------ | --------- | ----------- |
| symbol | string | YES       |             |


Response:

| name  | Description              |
| ----- | ------------------------ |
| mins  | Average price time frame |
| price | Price                    |

## 24hr Ticker Price Change Statistics


> Response

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

- **GET** ```/api/v3/ticker/24hr```

Parameters:

| name   | Type   | Mandatory | Description                                                                      |
| ------ | ------ | --------- | -------------------------------------------------------------------------------- |
| symbol | string | NO        | If the symbol is not sent, tickers for all symbols will be returned in an array. |


Response:

| name               | Description           |
| ------------------ | --------------------- |
| symbol             | Symbol                |
| priceChange        | price Change          |
| priceChangePercent | price change percent  |
| prevClosePrice     | Previous  close price |
| lastPrice          | Last price            |
| lastQty            | Last quantity         |
| bidPrice           | Bid best price        |
| bidQty             | Bid best quantity     |
| askPrice           | Ask best price        |
| askQty             | Ask best quantity     |
| openPrice          | Open                  |
| highPrice          | High                  |
| lowPrice           | Low                   |
| volume             | Deal volume           |
| quoteVolume        | Quote asset volume    |
| openTime           | Start time            |
| closeTime          | Close time            |
| count              |                       |

## Symbol Price Ticker

> Response

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

- **GET** ```/api/v3/ticker/price```

Parameters:

| name   | Type   | Mandatory | Description                                                          |
| ------ | ------ | --------- | -------------------------------------------------------------------- |
| symbol | string | NO        | If the symbol is not sent, all symbols will be returned in an array. |


Response:

| name   | Description |
| ------ | ----------- |
| symbol |             |
| price  | Last price  |

## Symbol Order Book Ticker

> Response

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


Best price/qty on the order book for a symbol or symbols.

Parameters:

| name   | Type   | Mandatory | Description                                                          |
| ------ | ------ | --------- | -------------------------------------------------------------------- |
| symbol | string | NO        | If the symbol is not sent, all symbols will be returned in an array. |


Response:

| name     | Description       |
| -------- | ----------------- |
| symbol   | Symbol            |
| bidPrice | Best bid price    |
| bidQty   | Best bid quantity |
| askPrice | Best ask price    |
| askQty   | Best ask quantity |


# Sub-Account Endpoints

## Create a Sub-account(For Master Account)

Create a sub-account from the master account.

> Response

```json
{
    "subAccount":"mexc1",
    "note":"1"
}
```

- POST / api/v3/sub-account/virtualSubAccount



Parameters:

| name       | Type   | Mandatory | Description       |
| ---------- | ------ | --------- | ----------------- |
| subAccount | STRING | YES       | Sub-account name  |
| note       | STRING | YES       | Sub-account notes |
| recvWindow | LONG   | NO        |                   |
| timestamp  | LONG   | YES       |                   |



## Query Sub-account List (For Master Account)

Get details of the sub-account list

> Response

```json
{
    "subAccounts":[
        {
            "subAccount":"mexc666",
            "isFreeze":false,
            "createTime":1544433328000
        },
        {
            "subAccount":"mexc888",
            "isFreeze":false,
            "createTime":1544433328000
        }
    ]
}
```

- GET / api/v3/sub-account/list 



Parameters:

| name       | Type   | Mandatory | Description                       |
| ---------- | ------ | --------- | --------------------------------- |
| subAccount | STRING | NO        | Sub-account name                  |
| isFreeze   | STRING | NO        | true or false                     |
| page       | INT    | NO        | Default value: 1                  |
| limit      | INT    | NO        | Default value: 10, Max value: 200 |
| timestamp  | LONG   | YES       |                                   |
| recvWindow | LONG   | NO        |                                   |




## Create an APIKey for a sub-account (For Master Account)

> Response

```json
    {
        "subAccount": "mexc1",
        "note": "1",
        "apiKey": "arg13sdfgs",
        "secretKey": "nkjwn21973ihi",
        "permissions": "SPOT_ACCOUNT_READ",
        "ip": "135.181.193",
        "creatTime": 1597026383085
    }
```

- POST /api/v3/sub-account/apiKey



Parameters:

| name        | Type   | Mandatory | Description                                                  |
| ----------- | ------ | --------- | ------------------------------------------------------------ |
| subAccount  | STRING | YES       | Sub-account name                                             |
| note        | STRING | YES       | APIKey note                                                  |
| permissions | STRING | YES       | permission of APIKey,SPOT_ACCOUNT_READ,SPOT_ORDER_READ,SPOT_ORDER, ,SPOT_WITHDRAW_READ,SPOT_WITHDRAW,SPOT_TRANSFER_READ,SPOT_TRANSFER,FUTURES_ACCOUNT_READ,FUTURES_ORDER_READ,FUTURES_ORDER |
| ip          | STRING | NO        | Link IP addresses, separate with commas if more than one. Support up to 20 addresses. |
| recvWindow  | LONG   | NO        |                                                              |
| timestamp   | LONG   | YES       |                                                              |




## Query the APIKey of a sub-account (For Master Account)

Applies to master accounts only

> Response

```json
   {
       "subAccount":[
        {
            "note":"v5",
            "apiKey":"arg13sdfgs",
            "permissions":"SPOT_ACCOUNT_READ,SPOT_ACCOUNT_WRITE",
            "ip":"1.1.1.1,2.2.2.2",
            "creatTime":1597026383085
        },
        {
            "note":"v5.1",
            "apiKey":"arg13sdfgs12",
            "permissions":"SPOT_ACCOUNT_READ,SPOT_ACCOUNT_WRITE",
            "ip":"1.1.1.1,2.2.2.2",
            "creatTime":1597026383085
        }
        ]
   }
```

- GET/api/v3/sub-account/apiKey

Parameters:

| name       | Type   | Mandatory | Description      |
| ---------- | ------ | --------- | ---------------- |
| subAccount | STRING | YES       | Sub-account name |
| recvWindow | LONG   | NO        |                  |
| timestamp  | LONG   | YES       |                  |




## Delete the APIKey of a sub-account (For Master Account)

> Response

```json
  {
           "subAccount":"mexc1"
}
```

- DELETE /api/v3/sub-account/apiKey



Parameters:

| name       | Type   | Mandatory | Description      |
| ---------- | ------ | --------- | ---------------- |
| subAccount | STRING | YES       | Sub-account name |
| apiKey     | STRING | YES       | API public key   |
| recvWindow | LONG   | NO        |                  |
| timestamp  | LONG   | YES       |                  |





# Spot Account/Trade

## Test New Order

> Response

```json
{}
```

- **POST** ```/api/v3/order/test```

Creates and validates a new order but does not send it into the matching engine.

Parameters:

同于 POST /api/v3/order

## New Order

> Response

```json
{
    "symbol": "BTCUSDT",
    "orderId": "1196315350023612316",
    "orderListId": -1
}
```

- **POST** ```/api/v3/order```

Parameters:

| 名称             | 类型    | YES否必需 | 描述                 |
| ---------------- | ------- | --------- | -------------------- |
| symbol           | STRING  | YES       |                      |
| side             | ENUM    | YES       | ENUM：Order Side     |
| type             | ENUM    | YES       | ENUM：Order Type     |
| quantity         | DECIMAL | NO        | Quantity             |
| quoteOrderQty    | DECIMAL | NO        | Quote order quantity |
| price            | DECIMAL | NO        | Price                |
| newClientOrderId | STRING  | NO        |                      |
| recvWindow       | LONG    | NO        | Max 60000            |
| timestamp        | LONG    | YES       |                      |

Additional mandatory parameters based on `type`:

| Type     | Additional mandatory parameters |
| :------- | :------------------------------ |
| `LIMIT`  | `quantity`, `price`             |
| `MARKET` | `quantity` or `quoteOrderQty`   |

Other info:

MARKET: When type is market, if it is a buy order, `quoteOrderQty` is a required. If it is a sell order, `quantity` is a required.

- `MARKET` orders using the `quantity` field specifies the amount of the `base asset` the user wants to sell at the market price
  - For example, sending a `MARKET` order on BTCUSDT will specify how much BTC the user is selling.
- `MARKET` orders using `quoteOrderQty` specifies the amount the user wants to spend (when buying) the `quote` asset; the correct `quantity` will be determined based on the market liquidity 
  - Using BTCUSDT as an example:
    - On the `BUY` side, the order will buy as many BTC as `quoteOrderQty` USDT can.
    - On the `SELL` side, the order will sell the `quantity` of  BTC.

## Cancel Orde

> Response

```json
{
  "symbol": "LTCBTC",
  "origClientOrderId": "myOrder1",
  "orderId": 4,
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

Cancel an active order.

Parameters:

| name              | Type   | Mandatory | Description |
| ----------------- | ------ | --------- | ----------- |
| symbol            | string | YES       |             |
| orderId           | string | NO        | Order id    |
| origClientOrderId | string | NO        |             |
| newClientOrderId  | string | NO        |             |
| recvWindow        | long   | NO        |             |
| timestamp         | long   | YES       |             |

Either `orderId` or `origClientOrderId` must be sent.

Response:

| name                | Description                |
| ------------------- | -------------------------- |
| symbol              | Symbol                     |
| origClientOrderId   | Original client order id   |
| orderId             | order id                   |
| clientOrderId       | client order id            |
| price               | Price                      |
| origOty             | Original order quantity    |
| executedQty         | Executed order quantity    |
| cummulativeQuoteQty | Cummulative quote quantity |
| status              | Order status               |
| timeInForce         |                            |
| type                | Order type                 |
| side                | Order side                 |
## Cancel all Open Orders on a Symbol 

> Response

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

Cancel all pending orders for a single  symbol, including OCO pending orders.

Parameters:

| name       | Type   | Mandatory | Description |
| ---------- | ------ | --------- | ----------- |
| symbol     | string | YES       |             |
| recvWindow | long   | NO        |             |
| timestamp  | long   | YES       |             |


Response:

| name                | Description                |
| ------------------- | -------------------------- |
| symbol              | Symbol                     |
| origClientOrderId   | Original client order id   |
| orderId             | order id                   |
| clientOrderId       | client order id            |
| price               | Price                      |
| origOty             | Original order quantity    |
| executedQty         | Executed order quantity    |
| cummulativeQuoteQty | Cummulative quote quantity |
| status              | Order status               |
| timeInForce         |                            |
| type                | Order type                 |
| side                | Order side                 |

## Query Order

> Response

```json
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
  "time": 1499827319559,
  "updateTime": 1499827319559,
  "isWorking": true,
  "origQuoteOrderQty": "0.000000"
}
```

- **GET** ```/api/v3/order```

Check an order's status.

Parameters:

| name              | Type   | Mandatory | Description |
| ----------------- | ------ | --------- | ----------- |
| symbol            | String | YES       |             |
| origClientOrderId | String | NO        |             |
| orderId           | String | NO        |             |
| recvWindow        | long   | NO        |             |
| timestamp         | long   | YES       |             |


Response:

| name                | Description                |
| ------------------- | -------------------------- |
| symbol              | Symbol                     |
| origClientOrderId   | Original client order id   |
| orderId             | order id                   |
| clientOrderId       | client order id            |
| price               | Price                      |
| origOty             | Original order quantity    |
| executedQty         | Executed order quantity    |
| cummulativeQuoteQty | Cummulative quote quantity |
| status              | Order status               |
| timeInForce         |                            |
| type                | Order type                 |
| side                | Order side                 |
| stopPrice           | stop price                 |
| time                | Order created time         |
| updateTime          | Last update time           |
| isWorking           | is orderbook               |

## Current Open Orders

> Response

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

Get all open orders on a symbol. **Careful** when accessing this with no symbol.

Parameters:

| name       | Type   | Mandatory | Description |
| ---------- | ------ | --------- | ----------- |
| symbol     | string | YES       |             |
| recvWindow | long   | NO        |             |
| timestamp  | long   | YES       |             |


Response:

## All Orders

> Response

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

Get all account orders; active, cancelled or completed

Parameters:

| name       | Type   | Mandatory | Description             |
| ---------- | ------ | --------- | ----------------------- |
| symbol     | string | YES       | Symbol                  |
| orderId    | string | NO        | Order id                |
| startTime  | long   | NO        |                         |
| endTime    | long   | NO        |                         |
| limit      | int    | NO        | Default  500; max 1000; |
| recvWindow | long   | NO        |                         |
| timestamp  | long   | YES       |                         |


Response:

| name                | Description                |
| ------------------- | -------------------------- |
| symbol              | Symbol                     |
| origClientOrderId   | Original client order id   |
| orderId             | order id                   |
| clientOrderId       | client order id            |
| price               | Price                      |
| origOty             | Original order quantity    |
| executedQty         | Executed order quantity    |
| cummulativeQuoteQty | Cummulative quote quantity |
| status              | Order status               |
| timeInForce         |                            |
| type                | Order type                 |
| side                | Order side                 |
| stopPrice           | stop price                 |
| time                | Order created time         |
| updateTime          | Last update time           |
| isWorking           | is orderbook               |
| origQuoteOrderQty   |                            |
## Account Information

> Response

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

Get current account information

Parameters:

| name       | Type | Mandatory | Description |
| ---------- | ---- | --------- | ----------- |
| recvWindow | long | NO        |             |
| timestamp  | long | YES       |             |


Response:

| name             | Description     |
| ---------------- | --------------- |
| makerCommission  | maker fee       |
| takerCommission  | taker fee       |
| buyerCommission  |                 |
| sellerCommission |                 |
| canTrade         | Can Trade       |
| canWithdraw      | Can Withdraw    |
| canDeposit       | Can Deposit     |
| updateTime       | Update Time     |
| accountType      | Account type    |
| balances         | Balance         |
| asset            | Aseet coin      |
| free             | Available  coin |
| locked           | Forzen coin     |
| permissions      | Permission      |
## Account Trade List

> Response

```json
[
  {
    "symbol": "BNBBTC",
    "id": 28457,
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


Get trades for a specific account and symbol.

Parameters:

| name       | Type   | Mandatory | Description            |
| ---------- | ------ | --------- | ---------------------- |
| symbol     | string | YES       |                        |
| orderId    | string | NO        | order Id               |
| startTime  | long   | NO        |                        |
| endTime    | long   | NO        |                        |
| limit      | int    | NO        | Default 500; max 1000; |
| recvWindow | long   | NO        |                        |
| timestamp  | long   | YES       |                        |


Response:

| name            | Description   |
| --------------- | ------------- |
| symbol          |               |
| id              | deal id       |
| orderId         | order id      |
| price           | Price         |
| qty             | Quantity      |
| quoteQty        | Deal quantity |
| time            | Deal time     |
| commission      |               |
| commissionAsset |               |
| time            | trade time    |
| isBuyerMaker    |               |
| isBestMatch     |               |

# ETF

## Get ETF info

> Response

```json
{

"symbol": "BTC3LUSDT", 

"netValue": "0.147", 

"feeRate":" 0.00001", 

"timestamp": `1507725176595`

}

```

- **GET** ```api/v3/etf/info```

Get information on ETFs, such as symbol, netValue and fund fee.

Parameters:

| name   | Type   | Mandatory | Description |
| ------ | ------ | --------- | ----------- |
| symbol | string | No        | ETF symbol  |


Response:

| name      | Type   | Description |
| --------- | ------ | ----------- |
| symbol    | string | ETF symbol  |
| netValue  | string | Net Value   |
| feeRate   | string | Fund Fee    |
| timestamp | long   |             |


# Public API Definitions

### ENUM definitions

### **Order side**

- BUY
- SELL

### Order type

- LIMIT    Limit order
- MARKET Market order
- LIMIT_MAKER   Limit maker order

### Order State

- NEW   Uncompleted
- FIELLD  Filled
- PARTIALLY_FILLED  Partially filled
- CANCELED  Canceled
- PARTIALLY_CANCELED  Partially canceled

### Kline Interval

- 1m  1 minute
- 3m  3 minute
- 5m  5 minute
- 15m  15 minute
- 30m  30 minute
- 1h  1 hour
- 2h  2 hour
- 4h  4 hour
- 6h  6 hour
- 8h  8 hour
- 12h  12 hour
- 1d  1 day
- 3d  3 day
- 1w  1 week
- 1M  1 month
