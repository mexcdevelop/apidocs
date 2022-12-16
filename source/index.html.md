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

## MEXC Broker Introduction

MEXC is committed to building crypto infrastructure, with API broker partners that provide valuable services being an essential part of the MEXC ecosystem. To reward the partners, MEXC now provides privileges for MEXC brokers, including trading rebates and marketing support.

**Broker Modes Supported by MEXC**

**1. API Broker**

This includes copy trade platforms, trading bots, quantitative strategy platforms, or other asset management platforms with more than 500 people, etc. Users can authorize the API key to the API broker, and the API broker will send the trading orders containing the broker ID on behalf of the user and receive profit shares from fees.

**2. Independent Broker**

This includes wallet platforms, market data platforms, aggregation trading platforms, stockbrokers, as well as stock and securities trading platforms, etc., all of which have their own independent users. MEXC can provide order matching systems, account management systems, settlement systems, as well as main and sub-account systems, etc. Independent brokers can share the trading fluidity and depth over the MEXC platform and receive profit shares from fees.

To apply for a partnership, please contact: **broker@mexc.com**

## Contact us

- MEXC API Telegram Group [MEXC API Support Group](https://t.me/MEXCAPIsupport)
  - For any general questions about the API not covered in the documentation.
  - For any MM questions
- MEXC Customer Support *website.app online customer server*
  -  For cases such as missing funds, help with 2FA, etc.

# Change Log

## **2022-12-13 **

- Add params: avgPrice,cumulativeQuantity,cumulativeAmount for `spot@private.orders.v3.api` channel
- Add Query ReferCode Endpoint

## **2022-11-29 **

- Add "Margin Account Orders" channel and "Margin Account Risk Rate" channel in Websocket

## **2022-11-24 **

- Add MEXC Broker Introduction
- Add "Enable MX Deduct" and "Query MX Deduct Status" Endpoints

## **2022-10-14 **

- Update Endpoints [Wallet Endpoints](https://mxcdevelop.github.io/apidocs/spot_v3_en/#wallet-endpoints):

  1.[Withdraw](https://mxcdevelop.github.io/apidocs/spot_v3_en/#withdraw): When do a withdraw, `address` and `memo` should be passed separate (The previous version the memo is joined with a ":" after address).

  2.[Withdraw History](https://mxcdevelop.github.io/apidocs/spot_v3_en/#withdraw-history-supporting-network): Parameters `address` and `memo` should be returned separate (The previous version the memo is joined with a ":" after address).

  3.[Deposit Address](https://mxcdevelop.github.io/apidocs/spot_v3_en/#deposit-history-supporting-network): The return parameter  `tag` is changed to `memo`, and the memo required for deposite is returned in the `memo` parameter.

  4.[Deposit History](https://mxcdevelop.github.io/apidocs/spot_v3_en/#deposit-history-supporting-network): The return parameter  `addressTag` is changed to `memo`, and the memo required for deposite is returned in the `memo` parameter.

  5.Add [Generate deposit address](https://mxcdevelop.github.io/apidocs/spot_v3_en/#withdraw-history-supporting-network)

  6.[Query the currency information](https://mxcdevelop.github.io/apidocs/spot_v3_en/#query-the-currency-information): add `withdrawTips` and `depositTips` params。


## **2022-09-06**

- Add [Rebate Endpoints](https://mxcdevelop.github.io/apidocs/spot_v3_en/#rebate-endpoints):

  1.[Get Rebate History Records](https://mxcdevelop.github.io/apidocs/spot_v3_en/#get-rebate-history-records):Get the rebates from friends you invited and the transactions they make.

  2.[Get Rebate Records Detail](https://mxcdevelop.github.io/apidocs/spot_v3_en/#get-rebate-records-detail):You can query the records of each rebate generated by contracts and spot (non-leveraged) transactions made by your friends and their sub-accounts.

  3.[Get Self Rebate Records Detail](https://mxcdevelop.github.io/apidocs/spot_v3_en/#get-self-rebate-records-detail):You can query the each contract and spot (no margin) your invited friend made as the self-commission record generated from it.

## **2022-09-02**

- Add v3 websocket:

  1.Websocket Market Streams:[Trade Streams](https://mxcdevelop.github.io/apidocs/spot_v3_en/#trade-streams),[Kline Streams](https://mxcdevelop.github.io/apidocs/spot_v3_en/#kline-streams),[Diff.Depth Stream](https://mxcdevelop.github.io/apidocs/spot_v3_en/#diff-depth-stream);

  2.Websocket User Data Streams:[Account Deals](https://mxcdevelop.github.io/apidocs/spot_v3_en/#account-deals),[Account Orders](https://mxcdevelop.github.io/apidocs/spot_v3_en/#account-orders).

## **2022-08-26**

- [ETF](https://mxcdevelop.github.io/apidocs/spot_v3_en/#etf) add some response params:

| Name       | type | Description          |
| :------------- | :------- | :------------ |
| preBasket      | string   | preBasket  |
| preLeverage    | string   | preLeverage  |
| basket         | string   | basket   |

## **2022-08-15**

- Update for Sub-account endpoints:

  1.[Universal Transfer](https://mxcdevelop.github.io/apidocs/spot_v3_en/#universal-transfer-for-master-account)

  2.[Query Universal Transfer History](https://mxcdevelop.github.io/apidocs/spot_v3_en/#query-universal-transfer-history-for-master-account)

  3.[Enable Futures for Sub-account](https://mxcdevelop.github.io/apidocs/spot_v3_en/#enable-futures-for-sub-account-for-master-account)

  4.[Enable Margin for Sub-account endpoints](https://mxcdevelop.github.io/apidocs/spot_v3_en/#enable-margin-for-sub-account-for-master-account)

## **2022-08-03**

- Add [Wallet Endpoints](https://mxcdevelop.github.io/apidocs/spot_v3_en/#wallet-endpoints):

  1.[Query the currency information](https://mxcdevelop.github.io/apidocs/spot_v3_en/#query-the-currency-information)

  2.[Withdraw](https://mxcdevelop.github.io/apidocs/spot_v3_en/#withdraw)

  3.[Deposit History](https://mxcdevelop.github.io/apidocs/spot_v3_en/#deposit-history-supporting-network)

  4.[Withdraw History](https://mxcdevelop.github.io/apidocs/spot_v3_en/#withdraw-history-supporting-network)

  5.[Deposit Address](https://mxcdevelop.github.io/apidocs/spot_v3_en/#deposit-address-supporting-network)

  6.[User Universal Transfer](https://mxcdevelop.github.io/apidocs/spot_v3_en/#user-universal-transfer)

  7.[Query User Universal Transfer History](https://mxcdevelop.github.io/apidocs/spot_v3_en/#query-user-universal-transfer-history)

## **2022-07-27**

- Spot [New Order](https://mxcdevelop.github.io/apidocs/spot_v3_en/#new-order) Order type add: IOC and FOK

## **2022-07-15**

- [Account Trade List](https://mxcdevelop.github.io/apidocs/spot_v3_en/#account-trade-list) add params: isSelfTrade

| Name          | Description              |
| :-------------- | :---------------- |
| isSelfTrade     | isSelfTrade        |

## **2022-07-08**

- Add [Batch Orders](https://mxcdevelop.github.io/apidocs/spot_v3_en/#batch-orders) Supports 20 orders in a batch,rate limit: 2 times/s.

## **2022-07-03**

- Add [Query the currency information](https://mxcdevelop.github.io/apidocs/spot_v3_en/#query-the-currency-information),Query currency details and the smart contract address.

## **2022-06-16**

- Add [Margin Account and Trading](https://mxcdevelop.github.io/apidocs/spot_v3_en/#margin-account-and-trading-interface)


## **2022-05-22**

- Optimize exchangeInfo Endpoints
- Optimize order Endpoints,add parameter: order id

## **2022-04-25**

- [Exchange Info](https://mxcdevelop.github.io/apidocs/spot_v3_en/#exchange-information) add parameters:

| Name                     | type | Description                |
| :------------------------- | :------- | :------------------ |
| isSpotTradingAllowed       | Boolean  | isSpotTradingAllowed |
| isMarginTradingAllowed     | Boolean  | isMarginTradingAllowed |


- [Current Open Orders](https://mxcdevelop.github.io/apidocs/spot_v3_en/#current-open-orders) Optimize: Get all open orders on multiple symbols,maximun support 5 symbols for one request.

## **2022-03-29**

- Add [Sub-Account Endpoints](https://mxcdevelop.github.io/apidocs/spot_v3_en/#sub-account-endpoints):

  1.[Create a Sub-account](https://mxcdevelop.github.io/apidocs/spot_v3_en/#create-a-sub-account-for-master-account)

  2.[Query Sub-account List](https://mxcdevelop.github.io/apidocs/spot_v3_en/#query-sub-account-list-for-master-account)

  3.[Create an APIKey for a sub-account](https://mxcdevelop.github.io/apidocs/spot_v3_en/#create-an-apikey-for-a-sub-account-for-master-account)

  4.[Query the APIKey of a sub-account](https://mxcdevelop.github.io/apidocs/spot_v3_en/#query-the-apikey-of-a-sub-account-for-master-account)

  5.[Delete the APIKey of a sub-account](https://mxcdevelop.github.io/apidocs/spot_v3_en/#delete-the-apikey-of-a-sub-account-for-master-account)

  6.[Universal Transfer](https://mxcdevelop.github.io/apidocs/spot_v3_en/#universal-transfer-for-master-account)

  7.[Query Universal Transfer History](https://mxcdevelop.github.io/apidocs/spot_v3_en/#query-universal-transfer-history-for-master-account)

  8.[Enable Futures for Sub-account](https://mxcdevelop.github.io/apidocs/spot_v3_en/#enable-futures-for-sub-account-for-master-account)

  9.[Enable Margin for Sub-account](https://mxcdevelop.github.io/apidocs/spot_v3_en/#enable-margin-for-sub-account-for-master-account)

## **2022-03-25**

- Add [Postman collection](https://mxcdevelop.github.io/apidocs/spot_v3_en/#api-library)

## **2022-03-24**

- Add information of market order

## **2022-03-21**

- Add order status

## **2022-03-18**

- Add new <a href="#order_type">Order Type</a>: Market
- Add time page info: startTime and endTime need to the same time

## **2022-03-09**

- Add <a href="#kline_interval">kline interval</a>

## **2022-02-19**

- Add [ETF](https://mxcdevelop.github.io/apidocs/spot_v3_en/#etf)

## **2022-02-11**

- New version API

# General Info

## Base endpoint

The base endpoint is:

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

- SIGNED endpoints require an additional parameter, signature, to be sent in the query string or request body(in the API of batch operation, if there are special symbols such as comma in the parameter value, these symbols need to be URL encoded when signing,and encode only support uppercase).
- Endpoints use HMAC SHA256 signatures. The HMAC SHA256 signature is a keyed HMAC SHA256 operation. Use your secretKey as the key and totalParams as the value for the HMAC operation.
- The signature is support lowercase only.
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

## Error Code

The following error information can be returend

| Code      | Description                                                                           |
|-----------|---------------------------------------------------------------------------------------|
| 400       | Invalid parameter                                                                     |
| 401       | Invalid signature, fail to pass the validation                                        |
| 429       | Too many requests, rate limit rule is violated                                        |
| 10072     | Invalid access key                                                                    |
| 10073     | Invalid request time                                                                  |
| 30000     | Trading is suspended for the requested symbol                                         |
| 30001     | Current trading type (bid or ask) is not allowed                                      |
| 30002     | Invalid trading amount, smaller than the symbol minimum trading amount                |
| 30003     | Invalid trading amount, greater than the symbol maximum trading amount                |
| 30004     | Insufficient balance                                                                  |
| 30005     | Oversell error                                                                        |
| 30010     | Price out of allowed range                                                            |
| 30016     | Market is closed                                                                      |
| 30019     | api market order is disabled                                                          |
| 30020     | Restricted symbol, API access is not allowed for the time being                       |
| 30021     | Invalid symbol                                                                        |
| 700001  | API-key format invalid                                                                |
| 700002  | Signature for this request is not valid                                               |
| 700003  | Timestamp for this request is outside of the recvWindow                               |
| 700004  | Mandatory parameter '%s' was not sent, was empty/null, or malformed.                  |
| 700005  | 'recvWindow' must be less than 60000                                                  |
| 700006  | IP non white list                                                                     |
| 700007  | No permission to access the endpoint                                                  |
| 700008  | Illegal characters found in parameter 's%'; legal range is '${regexp}"'               |
| 730001  | Pair not found                                                                        |
| 730002  | Your input param is invalid                                                           |
| 730000  | Request failed, please contact the customer service                                   |
| 730001  | User information error                                                                |
| 730002  | Parameter error                                                                       |
| 730003  | Unsupported operation, please contact the customer service                            |
| 730100  | Unusual user status                                                                   |
| 730600  | Sub-account Name cannot be null                                                       |
| 730601  | Sub-account Name must be a combination of 8-32 letters and numbers                    |
| 730602  | Sub-account remarks cannot be null                                                    |
| 730700  | API KEY remarks cannot be null                                                        |
| 730701  | API KEY permission cannot be null                                                     |
| 730702  | API KEY permission does not exist                                                     |
| 730703  | The IP information is incorrect, and a maximum of 10 IPs are allowed to be bound only |
| 730704  | The bound IP format is incorrect, please refill                                       |
| 730705  | At most 30 groups of Api Keys are allowed to be created only                            |
| 730706  | API KEY information does not exist                                                       |
| 730707  | accessKey cannot be null                                                                 |
| 730101  | The user Name already exists                                                                  |

# Market Data Endpoints

## Test Connectivity

> Response

```json
{}
```

- **GET** ```/api/v3/ping```

Test connectivity to the Rest API.

Parameter:

NONE

## Check Server Time

> Response

```json
{
    "serverTime" : 1645539742000
}
```

- **GET** ```/api/v3/time ```
  

Parameter:

NONE

## Exchange Information

> Response

```json
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

```

- **GET** ```/api/v3/exchangeInfo```

Current exchange trading rules and symbol information

**Parameter**:

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

Parameter:

| Name   | Type    | Mandatory | Description     | Scope                 |
| ------ | ------- | --------- | --------------- | --------------------- |
| symbol | string  | YES       | Symbol          |                       |
| limit  | integer | NO        | Returen  number | default 100; max 5000 |

Response:

| Name         | Type | Description            |
| ------------ | ---- | ---------------------- |
| lastUpdateId | long | Last Update Id       |
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

Parameter:

| Name   | Type    | Mandatory | Description | Scope                  |
| ------ | ------- | --------- | ----------- | ---------------------- |
| symbol | string  | YES       |             |                        |
| limit  | integer | NO        |             | Default  500; max 1000 |


Response:

| Name         | Description                         |
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

| Name   | Type    | Mandatory | Description   | Scope                 |
| ------ | ------- | --------- | ------------- | --------------------- |
| symbol | string  | YES       | Symbol        |                       |
| limit  | integer | NO        | Return number | Default 500; max 1000 |


Response:

| Name         | Description                         |
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

| Name      | Type    | Mandatory | Description                                              | Scope                  |
| --------- | ------- | --------- | -------------------------------------------------------- | ---------------------- |
| symbol    | string  | YES       |                                                          |                        |
| startTime | long    | NO        | Timestamp in ms to get aggregate trades from INCLUSIVE.  |                        |
| endTime   | long    | NO        | Timestamp in ms to get aggregate trades until INCLUSIVE. |                        |
| limit     | integer | NO        |                                                          | Default 500; max 1000. |

startTime and endTime must be used at the same time.

Response:

| Name | Description                         |
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

| Name      | Type    | Mandatory | Description                                        |
| --------- | ------- | --------- |----------------------------------------------------|
| symbol    | string  | YES       |                                                    |
| interval  | ENUM    | YES       | ENUM: <a href="#kline_interval">Kline Interval</a> |
| startTime | long    | NO        |                                                    |
| endTime   | long    | NO        |                                                    |
| limit     | integer | NO        | Default 500; max 1000.                             |


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

| Name   | Type   | Mandatory | Description |
| ------ | ------ | --------- | ----------- |
| symbol | string | YES       |             |


Response:

| Name  | Description              |
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

| Name   | Type   | Mandatory | Description                                                                      |
| ------ | ------ | --------- | -------------------------------------------------------------------------------- |
| symbol | string | NO        | If the symbol is not sent, tickers for all symbols will be returned in an array. |


Response:

| Name               | Description           |
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

| Name   | Type   | Mandatory | Description                                                          |
| ------ | ------ | --------- | -------------------------------------------------------------------- |
| symbol | string | NO        | If the symbol is not sent, all symbols will be returned in an array. |


Response:

| Name   | Description |
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

| Name   | Type   | Mandatory | Description                                                          |
| ------ | ------ | --------- | -------------------------------------------------------------------- |
| symbol | string | NO        | If the symbol is not sent, all symbols will be returned in an array. |


Response:

| Name     | Description       |
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

| Name       | Type   | Mandatory | Description       |
| ---------- | ------ | --------- | ----------------- |
| subAccount | STRING | YES       | Sub-account Name  |
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

| Name       | Type   | Mandatory | Description                       |
| ---------- | ------ | --------- | --------------------------------- |
| subAccount | STRING | NO        | Sub-account Name                  |
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

| Name        | Type   | Mandatory | Description                                                  |
| ----------- | ------ | --------- | ------------------------------------------------------------ |
| subAccount  | STRING | YES       | Sub-account Name                                             |
| note        | STRING | YES       | APIKey note                                                  |
| permissions | STRING | YES       | Permission of APIKey:<br/>SPOT_ACCOUNT_READ,<br/>SPOT_ACCOUNT_WRITE,<br/>SPOT_DEAL_READ,<br/>SPOT_DEAL_WRITE,<br/>ISOLATED_MARGIN_ACCOUNT_READ,<br/>ISOLATED_MARGIN_ACCOUNT_WRITE,<br/>ISOLATED_MARGIN_DEAL_READ,<br/>ISOLATED_MARGIN_DEAL_WRITE,<br/>CONTRACT_ACCOUNT_READ,<br/>CONTRACT_ACCOUNT_WRITE,<br/>CONTRACT_DEAL_READ,<br/>CONTRACT_DEAL_WRITE,<br/>SPOT_TRANSFER_READ,<br/>SPOT_TRANSFER_WRITE| 
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

| Name       | Type   | Mandatory | Description      |
| ---------- | ------ | --------- | ---------------- |
| subAccount | STRING | YES       | Sub-account Name |
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

| Name       | Type   | Mandatory | Description      |
| ---------- | ------ | --------- | ---------------- |
| subAccount | STRING | YES       | Sub-account Name |
| apiKey     | STRING | YES       | API public key   |
| recvWindow | LONG   | NO        |                  |
| timestamp  | LONG   | YES       |                  |


## Universal Transfer (For Master Account)

> Request

```
post /api/v3/capital/sub-account/universalTransfer
```

> Response

```json
 {
    "tranId":11945860693 
 }
```

- **POST** ```/api/v3/capital/sub-account/universalTransfer```

**Parameters:**

| Name | Type| Mandatory  | Description |  
| :------ | :-------- | :-------- | :---------- |
|fromAccount|string|NO|Transfer from master account by default if fromAccount is not sent|
|toAccount|string|NO|Transfer to master account by default if toAccount is not sent|
|fromAccountType|string|YES|fromAccountType:"SPOT","FUTURES","ISOLATED_MARGIN"|
|toAccountType|string|YES|toAccountType:"SPOT","FUTURES","ISOLATED_MARGIN"
|symbol|string|NO|Only supported under ISOLATED_MARGIN type,eg:ETHUSDT|
|asset|string|YES|asset,eg:USDT|
|amount|string|YES|amount,eg:1.82938475|
|timestamp|string|YES|timestamp|
|signature|string|YES|sign|

**Response:**

| Name  |Type | Description|
| :------------ | :-------- | :--------|
|tranId|string|transfer ID|

## Query Universal Transfer History (For Master Account)

> Request

```
get /api/v3/capital/sub-account/universalTransfer
```

> Response

```json
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
```
- **GET** ```/api/v3/capital/sub-account/universalTransfer```

**Parameters:**

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
|fromAccount|string|NO|Transfer from master account by default if fromAccount is not sent|
|toAccount|string|NO|Transfer to master account by default if toAccount is not sent|
|fromAccountType|string|YES|fromAccountType:"SPOT","FUTURES","ISOLATED_MARGIN"|
|toAccountType|string|YES|toAccountType:"SPOT","FUTURES","ISOLATED_MARGIN"|
|startTime|string|NO|startTime|
|endTime|string|NO|endTime|
|page|string|NO|default 1|
|limit|string|NO|default 500, max 500|
|timestamp|string|YES|timestamp|
|signature|string|YES|sign|

**Response:**

| Name  |Type | Description|
| :------------ | :-------- | :--------|
|tranId|string|transfer ID|
|fromAccount|string|fromAccount|
|toAccount|string|toAccount|
|clientTranId|string|clientTranId|
|asset|string|asset|
|amount|string|transfer amount|
|fromAccountType|string|fromAccountType|
|toAccountType|string|toAccountType|
|fromSymbol|string|fromSymbol|
|toSymbol|string|toSymbol|
|status|string|status|
|timestamp|number|timestamp|
|totalCount|number|total transfer|

## Enable Futures for Sub-account (For Master Account)

> Request

```
post /api/v3/sub-account/futures
```

> Response

```json
  {
    "code": "0",
    "message": "",
    "data": [{
        "subAccount": "mexc1",
        "isFuturesEnabled": true,
        "timestamp": "1597026383085"
    }]
  }
```

- **POST** ```/api/v3/sub-account/futures```

**Parameters:**

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
|subAccount|string|YES|subaccount Name|
|timestamp|string|YES|timestamp|
|signature|string|YES|sign|

**Response:**

| Name  |Type | Description|
| :------------ | :-------- | :--------|
|subAccount|string|subaccount Name|
|isFuturesEnabled|boolean|isFuturesEnabled:true|
|timestamp|string|response time|

## Enable Margin for Sub-account (For Master Account)

> Request

```
post /api/v3/sub-account/margin
```

> Response

```json
{
  "code": "0",
  "message": "",
  "data": [{
      "subAccount": "mexc1",
      "isMarginEnabled": true,
      "timestamp": "1597026383085"
  }]
}
```

- **POST** ```/api/v3/sub-account/margin```

**Parameters:**

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
|subAccount|string|YES|subaccount Name|
|timestamp|string|YES|timestamp|
|signature|string|YES|sign|

**Response:**

| Name  |Type | Description|
| :------------ | :-------- | :--------|
|subAccount|string|subaccount Name|
|isMarginEnabled|booleanisMarginEnabled:true or false|
|timestamp|string|response time|



# Spot Account/Trade

## Test New Order

> Response

```json
{}
```

- **POST** ```/api/v3/order/test```

Creates and validates a new order but does not send it into the matching engine.

Parameters:

equaled POST /api/v3/order

## New Order

> Request

```
POST /api/v3/order?symbol=MXUSDT&side=BUY&type=LIMIT&quantity=50&price=0.1&timestamp={{timestamp}}&signature={{signature}}
```

> Response

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

- **POST** ```/api/v3/order```

Parameters:

| Name             | type    | Mandatory | Description                               |
| ---------------- | ------- | --------- |-------------------------------------------|
| symbol           | STRING  | YES       |                                           |
| side             | ENUM    | YES       | ENUM:<a href="#order_side">Order Side</a> |
| type             | ENUM    | YES       | ENUM:<a href="#order_type">Order Type</a> |
| quantity         | DECIMAL | NO        | Quantity                                  |
| quoteOrderQty    | DECIMAL | NO        | Quote order quantity                      |
| price            | DECIMAL | NO        | Price                                     |
| newClientOrderId | STRING  | NO        |                                           |
| recvWindow       | LONG    | NO        | Max 60000                                 |
| timestamp        | LONG    | YES       |                                           |

Response:

| Name         | Description                          |
|--------------|--------------------------------------|
| symbol       | Symbol                               |
| orderId      | order id                             |
| orderListId  | order list id                        |
| price        | Price                                |
| origQty      | Original order quantity              |
| type         | <a href="#order_type">Order type</a> |
| side         | <a href="#order_side">order side</a> |
| transactTime | transactTime                         |


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

## Batch Orders

Supports 20 orders in a batch,rate limit:2 times/s.

> Request

```
POST /api/v3/batchOrders?batchOrders=[{"type": "LIMIT_ORDER","price": "40000","quantity": "0.0002","symbol": "BTCUSDT","side": "BID","newClientOrderId": 9588234},{"type": "LIMIT_ORDER","price": "4005","quantity": "0.0003","symbol": "BTCUSDT","side": "ASK"}]
```

> Response

```json
{
  { //success response:
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
   //error response:
   [
     { 
       "symbol": "BTCUSDT", 
       "orderId": "1196315350023612316", 
       "newClientOrderId": "hio8279hbdsds", 
       "orderListId": -1 
     },
     { 
       "newClientOrderId": "123456",
       "msg": "The minimum transaction volume cannot be less than:0.5USDT", 
       "code": 30002
     },
     { 
       "symbol": "BTCUSDT", 
       "orderId": "1196315350023612318", 
       "orderListId": -1 
     }
   ] 
 }
}
```

- **POST** ```/api/v3/batchOrders```

Parameters:

| Name             | type    | Mandatory | Description                                |
| :--------------- | :------ | :------- |:-------------------------------------------|
| batchOrders      | LIST  | YES      | list of batchOrders,supports max 20 orders |
| symbol           | STRING  | YES      | symbol                                     |
| side             | ENUM    | YES      | <a href="#order_side">order side</a>       |
| type             | ENUM    | YES      | <a href="#order_type">order type</a>       |
| quantity         | DECIMAL | NO       | quantity                                   |
| quoteOrderQty    | DECIMAL | NO       | quoteOrderQty                              |
| price            | DECIMAL | NO       | order price                                |
| newClientOrderId | STRING  | NO       | ClientOrderId                              |
| recvWindow       | LONG    | NO       | less than 60000                            |
| timestamp        | LONG    | YES      | order time                                 |

base on different`type`,some params are mandatory:

| type     | Mandatory   params      |
| :------- | :---------------------------- |
| `LIMIT`  | `quantity`, `price`           |
| `MARKET` | `quantity` or `quoteOrderQty` |

Response

| Name       | type | Description       |
| :------------ | :-------- | :------------------- |
| symbol | STRING | symbol |
| orderId | STRING | orderId |

## Cancel Order

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

| Name              | Type   | Mandatory | Description |
| ----------------- | ------ | --------- | ----------- |
| symbol            | string | YES       |             |
| orderId           | string | NO        | Order id    |
| origClientOrderId | string | NO        |             |
| newClientOrderId  | string | NO        |             |
| recvWindow        | long   | NO        |             |
| timestamp         | long   | YES       |             |

Either `orderId` or `origClientOrderId` must be sent.

Response:

| Name                | Description                          |
| ------------------- |--------------------------------------|
| symbol              | Symbol                               |
| origClientOrderId   | Original client order id             |
| orderId             | order id                             |
| clientOrderId       | client order id                      |
| price               | Price                                |
| origOty             | Original order quantity              |
| executedQty         | Executed order quantity              |
| cummulativeQuoteQty | Cummulative quote quantity           |
| status              | <a href="#order_status">order status</a> |
| timeInForce         |                                      |
| type                | <a href="#order_type">Order type</a> |
| side                | <a href="#order_side">order side</a> |

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

| Name       | Type   | Mandatory | Description |
| ---------- | ------ | --------- | ----------- |
| symbol     | string | YES       | maximum input 5 symbols,separated by ",". e.g. "BTCUSDT,MXUSDT,ADAUSDT"|
| recvWindow | long   | NO        |             |
| timestamp  | long   | YES       |             |


Response:

| Name                | Description                |
| ------------------- | -------------------------- |
| symbol              | Symbol                     |
| origClientOrderId   | Original client order id   |
| orderId             | order id                   |
| clientOrderId       | client order id            |
| price               | Price                      |
| origOty             | Original order quantity    |
| executedQty         | Executed order quantity    |
| cummulativeQuoteQty | Cummulative quote quantity |
| status              | <a href="#order_status">order status</a>               |
| timeInForce         |                            |
| type                | <a href="#order_type">Order type</a>                 |
| side                | <a href="#order_side">order side</a>                 |

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

| Name              | Type   | Mandatory | Description |
| ----------------- | ------ | --------- | ----------- |
| symbol            | String | YES       |             |
| origClientOrderId | String | NO        |             |
| orderId           | String | NO        |             |
| recvWindow        | long   | NO        |             |
| timestamp         | long   | YES       |             |


Response:

| Name                | Description                          |
| ------------------- |--------------------------------------|
| symbol              | Symbol                               |
| origClientOrderId   | Original client order id             |
| orderId             | order id                             |
| clientOrderId       | client order id                      |
| price               | Price                                |
| origOty             | Original order quantity              |
| executedQty         | Executed order quantity              |
| cummulativeQuoteQty | Cummulative quote quantity           |
| status              | <a href="#order_status">order status</a>                         |
| timeInForce         |                                      |
| type                | <a href="#order_type">Order type</a>                           |
| side                | <a href="#order_side">Order side</a> |
| stopPrice           | stop price                           |
| time                | Order created time                   |
| updateTime          | Last update time                     |
| isWorking           | is orderbook                         |

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

| Name       | Type   | Mandatory | Description |
| ---------- | ------ | --------- | ----------- |
| symbol     | string | YES       |             |
| recvWindow | long   | NO        |             |
| timestamp  | long   | YES       |             |


Response:

| Name                | Description                         |
| ------------------- |-------------------------------------|
| symbol              | Symbol                              |
| origClientOrderId   | Original client order id            |
| orderId             | order id                            |
| clientOrderId       | client order id                     |
| price               | Price                               |
| origOty             | Original order quantity             |
| executedQty         | Executed order quantity             |
| cummulativeQuoteQty | Cummulative quote quantity          |
| status              | <a href="#order_status">order status</a>                        |
| timeInForce         |                                     |
| type                | <a href="#order_type">Order type</a>                           |
| side                | <a href="#order_side">Order side</a> |
| stopPrice           | stop price                          |
| time                | Order created time                  |
| updateTime          | Last update time                    |
| isWorking           | is orderbook                        |

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

Get all account orders including active, cancelled or completed orders(the query period is the latest 24 hours by default). You can query a maximum of the latest 7 days.

Parameters:

| Name       | Type   | Mandatory | Description             |
| ---------- | ------ | --------- | ----------------------- |
| symbol     | string | YES       | Symbol                  |
| startTime  | long   | NO        |                         |
| endTime    | long   | NO        |                         |
| limit      | int    | NO        | Default  500; max 1000; |
| recvWindow | long   | NO        |                         |
| timestamp  | long   | YES       |                         |


Response:

| Name                | Description                          |
| ------------------- |--------------------------------------|
| symbol              | Symbol                               |
| origClientOrderId   | Original client order id             |
| orderId             | order id                             |
| clientOrderId       | client order id                      |
| price               | Price                                |
| origOty             | Original order quantity              |
| executedQty         | Executed order quantity              |
| cummulativeQuoteQty | Cummulative quote quantity           |
| status              | <a href="#order_status">order status</a>                         |
| timeInForce         |                                      |
| type                | <a href="#order_type">Order type</a>                           |
| side                | <a href="#order_side">Order side</a> |
| stopPrice           | stop price                           |
| time                | Order created time                   |
| updateTime          | Last update time                     |
| isWorking           | is orderbook                         |
| origQuoteOrderQty   |                                      |

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

Get current account information,rate limit:2 times/s.

Parameters:

| Name       | Type | Mandatory | Description |
| ---------- | ---- | --------- | ----------- |
| recvWindow | long | NO        |             |
| timestamp  | long | YES       |             |


Response:

| Name             | Description     |
| ---------------- | --------------- |
| makerCommission  | maker fee       |
| takerCommission  | taker fee       |
| buyerCommission  | buyer fee       |
| sellerCommission | seller fee      |
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
    "id": "fad2af9e942049b6adbda1a271f990c6",
    "orderId": "bb41e5663e124046bd9497a3f5692f39",
    "orderListId": -1,
    "price": "4.00000100", 
    "qty": "12.00000000", 
    "quoteQty": "48.000012", 
    "commission": "10.10000000", 
    "commissionAsset": "BNB", 
    "time": 1499865549590, 
    "isBuyer": true, 
    "isMaker": false, 
    "isBestMatch": true,
    "isSelfTrade": true,
    "clientOrderId": null
  }
]
```

- **GET** ```/api/v3/myTrades```


Get trades for a specific account and symbol,Only the transaction records in the past 1 month can be queried. If you want to view more transaction records, please use the export function on the web side, which supports exporting transaction records of the past 3 years at most.

Parameters:

| Name       | Type   | Mandatory | Description            |
| ---------- | ------ | --------- | ---------------------- |
| symbol     | string | YES       |                        |
| orderId    | string | NO        | order Id               |
| startTime  | long   | NO        |                        |
| endTime    | long   | NO        |                        |
| limit      | int    | NO        | Default 500; max 1000; |
| recvWindow | long   | NO        |                        |
| timestamp  | long   | YES       |                        |


Response:

| Name            | Description   |
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
| isSelfTrade     |   isSelfTrade |
| clientOrderId   | clientOrderId |

## Enable MX Deduct
Enable or disable MX deduct for spot commission fee

> Request

```
post api/v3/mxDeduct/enable
```
> Response

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

**Parameters:**

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
|mxDeductEnable|boolean|yes|true:enable,false:disable|
|recvWindow|long|no|recvWindow|
|timestamp|long|yes|timestamp|
|signature|string|yes|signature|

**Response:**

| Name  |Type | Description|
| :------------ | :-------- | :--------|
|mxDeductEnable|boolean|true:enable,false:disable|

<aside class="notice">For Futures:Enjoy 10% off trading fees when you transfer MX into your futures account and offset USDT-margined futures trading fees with MX.</aside>


## Query MX Deduct Status

> Request

```
get api/v3/mxDeduct/enable
```
> Response

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

- **GET** ```api/v3/mxDeduct/enableh```

**Parameters:**

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
|recvWindow|long|no|recvWindow|
|timestamp|long|yes|timestamp|
|signature|string|yes|signature|


**Response:**

| Name  |Type | Description|
| :------------ | :-------- | :--------|
|mxDeductEnable|boolean|true:enable,false:disable|

# Wallet Endpoints

## Query the currency information

> Request

```
Get /api/v3/capital/config/getall
```
> Response

```json
[
  {
    "coin": "EOS",
    "Name": "EOS",
    "networkList": [
      {
          "coin": "EOS",
          "depositDesc": null,
          "depositEnable": true,
          "minConfirm": 0,
          "Name": "EOS",
          "network": "EOS",
          "withdrawEnable": false,
          "withdrawFee": "0.000100000000000000",
          "withdrawIntegerMultiple": null,
          "withdrawMax": "10000.000000000000000000",
          "withdrawMin": "0.001000000000000000",
          "sameAddress": false,
          "contract": "TN3W4H6rK2ce4vX9YnFQHwKENnHjoxbm9",
          "withdrawTips": "Both a MEMO and an Address are required.",
          "depositTips": "Both a MEMO and an Address are required."
      },
      {
          "coin": "BTC",
          "depositDesc": null,
          "depositEnable": true,
          "minConfirm": 0,
          "Name": "BTC-BSC",
          "network": "BEP20(BSC)",
          "withdrawEnable": true,
          "withdrawFee": "0.000010000000000000",
          "withdrawIntegerMultiple": null,
          "withdrawMax": "100.000000000000000000",
          "withdrawMin": "0.000100000000000000",
          "sameAddress": false,
          "contract": "0x7130d2a12b9bcbfae4f2634d864a1ee1ce3ead9c",
          "withdrawTips": null,
          "depositTips": null
      }
    ]
  },
]
```

- **GET** ```/api/v3/capital/config/getall```

Query currency details and the smart contract address


Parameters:  

  None


Response:

| Name | Description  | 
| :------------ | :-------- | 
|depositEnable|depositEnable|
|network|withdraw network|
|withdrawEnable|withdrawEnable|
|withdrawFee|withdrawFee|
|withdrawMax|Max withdraw amount|
|withdrawMin|Min withdraw amount|
|contract|coin contract|
|withdrawTips|withdrawTips|
|depositTips|depositTips|

## Withdraw

> Request

```
post /api/v3/capital/withdraw/apply?coin=EOS&address=zzqqqqqqqqqq&amount=10&network=EOS&memo=MX10086&timestamp={{timestamp}}&signature={{signature}}
```
> Response

```json
[
  {
    "id":"7213fea8e94b4a5593d507237e5a555b"
  }
]
```


- **POST** ```/api/v3/capital/withdraw/apply```

Parameters: 

| Name | Type| Mandatory | Description                                                    | 
| :------ | :-------- |:----------|:---------------------------------------------------------------|
|coin|string| YES       | coin                                                           |
|withdrawOrderId|string| NO        | withdrawOrderId                                                |
|network|string| NO        | withdraw network                                               |
|address|string| YES       | withdraw address                                               |
|memo|string| NO        | memo(If memo is required in the address, it must be passed in) |
|amount|string| YES       | withdraw amount                                                |
|remark|string| NO        | remark                                                         |
|timestamp|string| YES       | timestamp                                                      |
|signature|string| YES       | signature                                                      |
 
1. If `network` is not sent, will return default network in that currency.
2. Can get `network` via endpoints `Get /api/v3/capital/config/getall`'s response params `networkList` and check whether is default network by response params`isDefault`
3. Withdraw address only support address which added in withdrawal settings on website.
Response:

| Name | Description  |
| :------------ | :-------- | 
|id|withdraw ID|

## Deposit History(supporting network) 

> Request

```
get /api/v3/capital/deposit/hisrec?coin=EOS&timestamp={{timestamp}}&signature={{signature}}
```
> Response

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


- **GET** ```/api/v3/capital/deposit/hisrec```

Parameters: 

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
|coin|string|NO|coin |
|status|string|NO|status|
|startTime|string|NO|default: 90 days ago from current time|
|endTime|string|NO|default:current time|
|limit|string|NO|default:1000,max:1000|
|timestamp|string|YES|timestamp|
|signature|string|YES|signature|

Ensure that the default timestamp of 'startTime' and 'endTime' does not exceed 90 days.

Response:

| Name | Description  |
| :------------ | :-------- |
|amount|deposit amount|
|coin|coin |
|network|deposit network|
|status|deposit status,1:SMALL,2:TIME_DELAY,3:LARGE_DELAY,<br/>4:PENDING,5:SUCCESS,6:AUDITING,7:REJECTED|
|address|deposit adress|
|addressTag|addressTag|
|txId|txId|
|insertTime|insertTime|
|unlockConfirm| unlockConfirm|
|confirmTimes|confirmTimes|
|memo|memo|

## Withdraw History (supporting network) 

> Request

```
get /api/v3/capital/withdraw/history?coin=USDT&timestamp={{timestamp}}&signature={{signature}}
```
> Response

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
        "memo": "MX10086"
  }
]
```


- **GET** ```/api/v3/capital/withdraw/history```

Parameters: 

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
|coin|string|NO|coin |
|status|string|NO|withdraw status|
|limit|string|NO|default:1000, max:1000|
|startTime|string|NO|default: 90 days ago from current time|
|endTime|string|NO|default:current time|
|timestamp|string|YES|timestamp|
|signature|string|YES|signature|

1. Supported multiple network coins'  withdraw history may not return the 'network' field.
2. Ensure that the default timestamp of 'startTime' and 'endTime' does not exceed 90 days.


Response:

| Name | Description  |
| :------------ | :-------- | 
|address|withdraw address|
|amount| withdraw amount|
|applyTime| apply time||
|coin|coin |
|id|withdraw id|
|withdrawOrderId| withdrawOrderId|
|network|withdraw network|
|transferType|transferType, 0: outside transfer,1: inside transfer  |
|status|withdraw status,1:APPLY,2:AUDITING,3:WAIT,4:PROCESSING,5:WAIT_PACKAGING,<br/>6:WAIT_CONFIRM,7:SUCCESS,8:FAILED,9:CANCEL,10:MANUAL|
|transactionFee| transactionFee|
|confirmNo| confirmNo|
|txId|txId|
|remark|remark|

## Generate deposit address (supporting network) 

> Request

```
post /api/v3/capital/deposit/address?coin=EOS&network=EOS&timestamp={{timestamp}}&signature={{signature}}
```
> Response

```json
[
  {
      "coin": "USDT",
      "network": "TRC20",
      "address": "TXobiKkdciupZrhdvZyTSSLjE8CmZAufS",
      "tag": null
  },
  {
     "coin": "EOS",
     "network": "EOS",
     "address": "zzqqqqqqqqqq",
     "memo": "MX10068"
  }
]
```


- **POST** ```/api/v3/capital/deposit/address```

Parameters: 

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
|coin|string|YES|coin |
|network|string|YES|deposit network|
|timestamp|string|YES|timestamp|
|signature|string|YES|signature|

Response:

| Name | Description  |
| :------------ | :-------- |
|address|deposit address|
|coin|coin |
|memo|memo|
|network|network|

## Deposit Address (supporting network) 

> Request

```
get /api/v3/capital/deposit/address?coin=USDT&timestamp={{timestamp}}&signature={{signature}}
```
> Response

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


- **GET** ```/api/v3/capital/deposit/address```

Parameters: 

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
|coin|string|YES|coin |
|network|string|NO|deposit network|
|timestamp|string|YES|timestamp|
|signature|string|YES|signature|

Response:

| Name | Description  |
| :------------ | :-------- |
|address|deposit address|
|coin|coin |
|memo|memo|
|network|network|

## User Universal Transfer

> Request

```
post /api/v3/capital/transfer?fromAccountType=FUTURES&toAccountType=SPOT&asset=USDT&amount=1&timestamp={{timestamp}}&signature={{signature}}
```
> Response

```json
[
  {
    "tranId": "c45d800a47ba4cbc876a5cd29388319"
  }
]
```


- **POST** ```/api/v3/capital/transfer```

Parameters: 

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
|fromAccountType|string|YES|fromAccountType:"SPOT","FUTURES",<br/>"ISOLATED_MARGIN"|
|toAccountType|string|YES|toAccountType:"SPOT","FUTURES",<br/>"ISOLATED_MARGIN"|
|asset|string|YES|asset|
|amount|string|YES|amount|
|symbol|string|NO|symbol,needed when`fromAccountType`is ISOLATED_MARGIN.eg:ETHUSDT|
|timestamp|string|YES|timestamp|
|signature|string|YES|signature|

When type is`ISOLATEDMARGIN`, `fromSymbol` and `toSymbol` must be sent.

Response:

| Name | Description  |
| :------------ | :-------- | 
|tranId|tranId|

## Query User Universal Transfer History 

> Request

```
get /api/v3/capital/transfer
get /api/v3/capital/transfer
```
> Response

```json
[
  {
    "rows":[
    {
      "tranId":"11945860693",
      "clientTranId":"test",
      "asset":"BTC",
      "amount":"0.1",
      "fromAccountType":"SPOT",
      "toAccountType":"FUTURE",
      "fromSymbol":"SPOT",
      "toSymbol":"FUTURE",
      "status":"SUCCESS",
      "timestamp":1544433325000
    },
    {
      "tranId":"11945860693",
      "clientTranId":"test",
      "asset":"BTC",
      "amount":"0.1",
      "fromAccountType":"SPOT",
      "toAccountType":"FUTURE",
      "fromSymbol":"SPOT",
      "toSymbol":"FUTURE",
      "status":"SUCCESS",
      "timestamp":1544433325000
    }],
    "total": 2,
  }
]
```


- **GET** ```/api/v3/capital/transfer```

Parameters: 

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
|fromAccountType|string|YES|fromAccountType:"SPOT","FUTURES",<br/>"ISOLATED_MARGIN"|
|toAccountType|string|YES|toAccountType:"SPOT","FUTURES",<br/>"ISOLATED_MARGIN"|
|startTime|string|NO|startTime|
|endTime|string|NO|endTime|
|page|string|NO|default:1|
|size|string|NO|default:10, max:100|
|symbol|string|YES|symbol,needed when`fromAccountType`is ISOLATED_MARGIN.eg:ETHUSDT|
|timestamp|string|YES|timestamp|
|signature|string|YES|signature|

1. Only can quary the data for the last six months
2. If 'startTime' and 'endTime' are not send, will return the last seven days' data by default

Response:

| Name | Description  |
| :------------ | :-------- | 
|total|total|
|tranId|tranId|
|clientTranId|client ID|
|asset|coin |
|amount|amount|
|fromAccountType|fromAccountType|
|toAccountType|toAccountType|
|symbol|symbol|
|status|status|
|timestamp|timestamp|

# ETF

## Get ETF info

> Response

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

- **GET** ```api/v3/etf/info```

Get information on ETFs, such as symbol, netValue and fund fee.

Parameters:

| Name   | Type   | Mandatory | Description |
| ------ | ------ | --------- | ----------- |
| symbol | string | No        | ETF symbol  |


Response:

| Name      | Type   | Description |
| --------- | ------ | ----------- |
| symbol    | string | ETF symbol  |
| netValue  | string | Net Value   |
| feeRate   | string | Fund Fee    |
| timestamp | long   |             |
|leverage    |string | target leverage  |
|realLeverage|string | real leverage    |
|mergedTimes |string | mergedTimes      |
|lastMergedTime|long | lastMergedTime   |
|preBasket  |string  | Basket Before   |
|preLeverage|string  | Leverage Before  |
|basket     |string  | Basket After  |

# Margin Account and Trading Interface

## TradeMode
switch trademode of margin account

> request

```
POST /api/v3/margin/tradeMode?tradeMode=0&symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> response

```json

{
"tradeMode": 0,
"symbol": "BTCUSDT"
}
```

**Http Request**

- **POST** ```/api/v3/margin/tradeMode```

**Request Parameter**

| Name | Description| Mandatory  | Type |  Sample            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
| tradeMode | tradeMode |YES|int|0: Normal 1:Auto|
| symbol | symbol |YES|string|BTCUSDT|
| timestamp | time | YES| string|1655143087012|
| signature | signature |YES|string|


**Response Parameter**

| Name | Description  |Type | Sample|
| :------------ | :-------- | :-------| :------ |
|tradeMode|tradeMode|int|0|
|symbol|symbol|string|BTCUSDT|



## Place Order

<aside class="warning">not support market order yet</aside>

> request

```
POST /api/v3/margin/order?symbol=BTCUSDT&side=BUY&type=LIMIT&quantity=0.0003&price=20000&timestamp={{timestamp}}&signature={{signature}}
```
> response

```json
  {
  "symbol": "BTCUSDT",
  "orderId": "693471305432961024",
  "isIsolated": true,       
  "transactTime": 1507725176595
  }

```
**Http Request**

- **POST** ```/api/v3/margin/order```

**Request Parameter**

| Name | Description                                          | Mandatory  | Type |  Sample  | 
| :------ |:-----------------------------------------------------| :-------- | :---------- | :------------------- |
|symbol| symbol                                               |YES|string|BTCUSDT|
|isIsolated| is Isolated,"TRUE", "FALSE", Default "TRUE"          |NO|string|TRUE|
|side| BUY SELL                                             |YES|string|BUY|
|type| API Definitions:<a href="#order_type">order type</a> |YES|string| 
|quantity| quantity                                             |NO|string| 
|quoteOrderQty| order quantity                                       |NO|string| 
|price| price                                                |NO|string|
|recvWindow|                                                      |NO|string| 
|timestamp| time                                                 |YES|string|timestamp|
|signature| signature                                            |YES|string|signature|


**Response Parameter**

| Name | Description  |Type | Sample |
| :------------ | :-------- | :-------- |:-------------- |
|symbol| |string|BTCUSDT|
|orderId| |string|693471305432961024|
|isIsolated| is Isolated|boolean|true|
|transactTime| |number|1507725176595|


## Loan

> request

```
post /api/v3/margin/loan?asset=BTC&amount=0.002&symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> response

```json

  {
    "tranId": 746784754145301480
  }

```
**Http Request**

- **POST** ```/api/v3/margin/loan```

**Request Parameter**

| Name | Description| Mandatory  | Type |  Sample |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|asset|asset|YES|string|BTC| 
|isIsolated|is Isolated,"TRUE", Default "TRUE"|NO|string| 
|symbol|symbol|YES|string| 
|amount| amount|YES|string| 
|recvWindow| |NO|string| 
|timestamp|time |YES|string|timestamp|
|signature|signature |YES|string|signature|


**Response Parameter**

| Name | Description  |Type | Sample |
| :------------ | :-------- | :-------- | :------------------- |
| tranId |transfer id |number|746784754145301480|

**Description**:

If isIsolated = "TRUE", means isolated mode,symbol must be filled in.


## Repayment

> request

```
post /api/v3/margin/repay?asset=BTC&symbol=BTCUSDT&isAllRepay=true&borrowId=746784754145300480&timestamp={{timestamp}}&signature={{signature}}
```
> response

```json

  {
    "tranId": 2597392
  }

```
**Http Request**

- **POST** ```/api/v3/margin/repay```

**Request Parameter**

| Name | Description| Mandatory  | Type |  Sample            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|asset|asset/btc|YES|string||
|isIsolated|is Isolated,"TRUE",  Default "TRUE"|NO|string||
|symbol|symbol|YES|string||
|amount|amount or isAllRepay|NO|string||
|borrowId|loan order id|YES|string||
|isAllRepay|all repay or portion repay|NO|string||
|recvWindow| |YES|string||
|timestamp| |YES|string|timestamp|
|signature| |YES|string|signature|

**Response Parameter**

| Name | Description  |Type | Sample|
| :------------ | :-------- | :--------| :------------------- |
|tranId|repay id|number|2597392|

**Description**:

If isIsolated = "TRUE", means isolated mode,symbol must be filled in.


## Cancel all Open Orders on a Symbol

> request

```
delete /api/v3/margin/openOrders?symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> response

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
       "status": "NEW",
       "type": "LIMIT",
       "side": "BUY",
       "isIsolated": true,
       "isWorking": true,
       "time": 1658212540000,
       "updateTime": 1658212540000
  }
]
```
**Http Request**

- **DELETE** ```/api/v3/margin/openOrders```

**Request Parameter**

| Name | Description| Mandatory  | Type |  Sample            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|symbol| |YES|string||
|isIsolated|is Isolated,"TRUE", Default "TRUE"|NO|string||
|recvWindow|less than `60000`|NO|string||
|timestamp| |YES|string|timestamp|
|signature| |YES|string|signature|

**Response Parameter**

| Name | Description  |Type | Sample|
| :------------ | :-------- | :--------| :------------------- |
|symbol| |string|BTCUSDT|
|isIsolated| is isolated symbol |boolean|true|
|clientOrderId||string|pXLV6Hz6mprAcVYpVMTGgx|
|price| |string|0.089853|
|origQty| |string|0.178622|
|executedQty||string|0.000000|
|cummulativeQuoteQty| |string|0.000000|
|status| |string|CANCELED|
|type| |string|LIMIT|
|side| |string|BUY|
|orderId||string| |
|orderListId|-1|string||



## Cancel Order

> request

```
delete /api/v3/margin/order?symbol=BTCUSDT&orderId=746777776866070528&timestamp={{timestamp}}&signature={{signature}}
```
> response

```json

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

```
**Http Request**

- **DELETE** ```/api/v3/margin/order```

**Request Parameter**

| Name | Description| Mandatory  | Type |  Sample            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|symbol| |YES|string|
|isIsolated|is Isolated,"TRUE", "FALSE", Default "FALSE"|NO|string|
|orderId| |YES|string|
|origClientOrderId|origClientOrderId|NO|string|
|recvWindow| |NO|string|
|timestamp| |YES|string|timestamp|
|signature| |YES|string|signature|

**Response Parameter**

| Name | Description  |Type | Sample|
| :------------ | :-------- | :--------| :------------------- |
|symbol| |string|LTCBTC|
|orderId| |string|693471305432961024|
|clientOrderId| |string|cancelMyOrder1|
|price| |string|1.00000000|
|origQty| |string|10.00000000|
|executedQty| |string|8.00000000|
|cummulativeQuoteQty|cummulativeQuoteQty|string|8.00000000|
|status| |string|CANCELED|
|type| |string|LIMIT|
|side| |string|SELL|
|isIsolated| is isolated symbol |boolean|true|

**Description**:

must send any one of orderId or origClientOrderId .


## Query Loan List


> request

```
get /api/v3/margin/loan?asset=BTC&symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> response

```json

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

```
**Http Request**

- **GET** ```/api/v3/margin/loan```

**Request Parameter**

| Name | Description| Mandatory  | Type |  Sample            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|asset|asset|YES|string|BTC|
|symbol|symbol|YES|string|
|tranId|tranId |NO|string|
|startTime| |NO|string|
|endTime| |NO|string|
|current|current page. Default:1|NO|string|
|size|Default:10 max:100|NO|string|
|recvWindow| |NO|string|
|timestamp| |YES|string|timestamp|
|signature| |YES|string|signature|

**Response Parameter**

| Name | Description  |Type | Sample|
| :------------ | :-------- | :--------| :------------------- |
|symbol| symbol|string|MXUSDT|
|tranId| |number|12807067523|
|asset| |string|MX|
|principal|principal|string|0.84624403|
|timestamp|time |number|1555056425000|
|remainAmount|remainAmount|string| |
|remainInterest|remainInterest|string| |
|repayAmount|repayAmount|string|300|
|repayInterest|repayInterest|string|1.96249686|
|status|status: PENDING , CONFIRMED, FAILED;|string|CONFIRMED|
|total| |number|1|

**Description**:

TranId or startTime must be sent, tranId takes precedence. Responses are returned in descending order. If you send isolatedSymbol, return the credit record for the specified store-by-store symbol specified asset.


## All Order

> request

```
get /api/v3/margin/allOrders?symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> response

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
**Http Request**

- **GET** ```/api/v3/margin/allOrders```

**Request Parameter**

| Name | Description| Mandatory  | Type |  Sample            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|symbol| |YES|string|
|isIsolated|is Isolated,"TRUE", "FALSE",Default "TRUE"|NO|string|
|orderId| |NO|string|
|startTime| |NO|string|
|endTime| |NO|string|
|limit|Default 500;max 500.|NO|string|
|timestamp| |YES|string|timestamp|
|signature| |YES|string|signature|

**Response Parameter**

| Name | Description  |Type | Sample|
| :------------ | :-------- | :--------| :------------------- |
|clientOrderId| |string|D2KDy4DIeS56PvkM13f8cP|
|cummulativeQuoteQty| |string|0.00000000|
|executedQty| |string|0.00000000|
|isWorking| |boolean|false|
|orderId| |number|41295|
|origQty| |string|5.31000000|
|price| |string|0.22500000|
|side| |string|SELL|
|status| |string|CANCELED|
|symbol| |string|MXBTC|
|isIsolated| is isolated symbol |boolean|false|
|time| |number|1565769338806|
|type| |string|TAKE_PROFIT_LIMIT|
|updateTime| |number|1565769342148|

**Description**:

If orderId is set, get the order &gt;= orderId, NO returns the recent order history. Some historical orders of cummulativeQuoteQty  &lt; 0: YES Indicates that the current data does not exist.



## Account Trade List


> request

```
get /api/v3/margin/myTrades?symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> response

```json
[

]
```
**Http Request**

- **GET** ```/api/v3/margin/myTrades```

**Request Parameter**

| Name | Description| Mandatory  | Type |  Sample            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|symbol| |YES|string|
|isIsolated|is Isolated,"TRUE", "FALSE",Default "TRUE"|NO|string|
|startTime| |NO|string|
|endTime| |NO|string|
|fromId|TradeId|NO|string|
|limit|Default 500; max 1000.|NO|string|
|timestamp| |YES|string|timestamp|
|signature| |YES|string|signature|

**Response Parameter**

| Name | Description  |Type | Sample|
| :------------ | :-------- | :--------| :------------------- |
|commission|commission|string|0.00006000|
|commissionAsset|commissionAsset|string|BTC|
|id|trade-id|number|34|
|isBuyer| |boolean|false|
|orderId| |number|39324|
|price| |string|0.02000000|
|qty| |string|3.00000000|
|symbol| |string|MXBTC|
|isIsolated| is isolated symbol|boolean|false|
|time| |number|1561973357171|

**Description**:

If fromId is set, get the order ID &gt; = fromId, NO Returns the recent order history.


## Current Open Orders

> request

```
get /api/v3/margin/openOrders?symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> response

```json
[
  {
    "rows": [
      {
          "isolatedSymbol": "MXUSDT", 
          "id": "12807067523",
          "asset": "MX",
          "timestamp": 1555056425000,
          "amount": "315.53307675",
          "dealAmount": "319.26088158",
          "dealQuantity": "23768.97",
          "fee": "0",
          "feeCurrency": "USDT",
          "orderType": "STOP_OUT",
          "price": "0.013275",
          "quantity": "23768.97",
	  			"remainQuantity": "0",
          "remainAmount": "300",
	  			"side": "SELL",
	  			"status": "FILLED"
      }
    ],
    "total": 1
  }
]
```
**Http Request**

- **GET** ```/api/v3/margin/openOrders```

**Request Parameter**

| Name | Description| Mandatory  | Type |  Sample            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|symbol|symbol|YES|string| 
|isIsolated|is Isolated,"TRUE", "FALSE",Default "TRUE"|NO|string|
|timestamp| |YES|string|timestamp|
|signature| |YES|string|signature|

**Response Parameter**

| Name | Description  |Type | Sample|
| :------------ | :-------- | :--------| :------------------- |
|clientOrderId| |string|qhcZw71gAkCCTv0t0k8LUK|
|cummulativeQuoteQty|cummulativeQuoteQty|string|0.00000000|
|executedQty| |string|0.00000000|
|isWorking| |boolean|true|
|orderId| |number|211842552|
|origQty| |string|0.30000000|
|price| |string|0.00475010|
|side| |string|SELL|
|status| |string|NEW|
|symbol| |string|MXBTC|
|isIsolated| is isolated symbol|boolean|true|
|time| |number|1562040170089|
|timeInForce| |string|GTC|
|type| |string|LIMIT|
|updateTime| |number|1562040170089|




## Account Max Transferable

> request

```
get /api/v3/margin/maxTransferable?asset=BTC&symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> response

```json

  {
     "amount": "0.00022998"
  } 

```
**Http Request**

- **GET** ```/api/v3/margin/maxTransferable```

**Request Parameter**

| Name | Description| Mandatory  | Type |  Sample            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|asset| |YES|string| 
|symbol|symbol|YES|string| 
|timestamp| |YES|string|timestamp|
|signature| |YES|string|signature|

**Response Parameter**

| Name | Description  |Type | Sample|
| :------------ | :-------- | :--------| :------------------- |
|amount| |string|0.00022998|


## Margin PriceIndex

> request

```
get /api/v3/margin/priceIndex?symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> response

```json

  {
     "price": "21823.45",
     "symbol": "BTCUSDT",
     "calcTime": 1658215048128
  }

```
**Http Request**

- **GET** ```/api/v3/margin/priceIndex```

**Request Parameter**

| Name | Description| Mandatory  | Type |  Sample            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|symbol| |YES|string| 
|timestamp| |YES|string|timestamp|
|signature| |YES|string|signature|  

**Response Parameter**

| Name | Description  |Type | Sample|
| :------------ | :-------- | :--------| :------------------- |
|calcTime| |number|1562046418000|
|price| |string|0.00333930|
|symbol| |string|MXBTC|



## Query Order

> request

```
get /api/v3/margin/order?symbol=BTCUSDT&orderId=746779360689786880&timestamp={{timestamp}}&signature={{signature}}
```
> response

```json

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

```
**Http Request**

- **GET** ```/api/v3/margin/order```

**Request Parameter**

| Name | Description| Mandatory  | Type |  Sample            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|symbol| |YES|string|
|isIsolated|is Isolated,"TRUE", "FALSE",Default "TRUE"|NO|string| |
|orderId| |NO|string| 
|timestamp| |YES|string|timestamp|
|signature| |YES|string|signature|

**Response Parameter**

| Name | Description  |Type | Sample|
| :------------ | :-------- | :--------| :------------------- |
|clientOrderId| |string|ZwfQzuDIGpceVhKW5DvCmO|
|cummulativeQuoteQty|cummulativeQuoteQty|string|0.00000000|
|executedQty|amount|string|0.00000000|
|isWorking| |boolean|true|
|orderId| |number|213205622|
|origQty|orign amount|string|0.30000000|
|price| |string|0.00493630|
|side| |string|SELL|
|status| |string|NEW|
|symbol| |string|MXBTC|
|isIsolated| is isolated symbol|boolean|true|
|time| |number|1562133008725|
|type| |string|LIMIT|
|updateTime| |number|1562133008725|

**Description**:

You must send either orderId or origClientOrderId. Some historical orders of cummulativeQuoteQty < 0: YES Indicates that the current data does not exist.


## Isolated Account

> request

```
get /api/v3/margin/isolated/account?symbols=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> response

```json

  {
   "assets":[
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

```
**Http Request**

- **GET** ```/api/v3/margin/isolated/account```

**Request Parameter**

| Name | Description| Mandatory  | Type |  Sample            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|symbols|max 5 symbols; String delimited by ",".|YES|string|"BTCUSDT,MXUSDT,ADAUSDT"|
|timestamp| |YES|string|timestamp|
|signature| |YES|string|signature|
**Response Parameter**

| Name | Description  |Type | Sample|
| :------------ | :-------- | :--------| :------------------- |
|asset| |string|BTC|
|borrowEnabled| |boolean|true|
|borrowed| |string|0.00000000|
|free| |string|0.00000000|
|interest| |string|0.00000000|
|locked| |string|0.00000000|
|netAsset| |string|0.00000000|
|netAssetOfBtc| |string|0.00000000|
|repayEnabled| |boolean|true|
|totalAsset| |string|0.00000000|
|isolatedCreated| |boolean|true|
|enabled| enabled|boolean|true|
|marginLevel| |string|0.00000000|
|marginRatio| |string|0.00000000|
|indexPrice| |string|10000.00000000|
|liquidatePrice| |string|1000.00000000|
|liquidateRate| |string|1.00000000|
|tradeEnabled| |boolean|true|




<!-- ## Query TrigerOrder

> request

```
get /api/v3/margin/trigerOrder
```
> response

```json
[

]
```
**Http Request**

- **GET** ```/api/v3/margin/trigerOrder```

**Request Parameter**

| Name | Description| Mandatory  | Type |  Sample            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|timestamp| |YES|string|{{timestamp}}|
|signature| |YES|string|{{signature}}|

**Response Parameter**

| Name | Description  |Type | Sample|
| :------------ | :-------- | :--------| :------------------- |

 -->

## MaxBorrowable

> request

```
get /api/v3/margin/maxBorrowable?asset=BTC&symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> response

```json

  {
     "amount": "0.00618914",
     "borrowLimit": "30"
  }

```
**Http Request**

- **GET** ```/api/v3/margin/maxBorrowable```

**Request Parameter**

| Name | Description| Mandatory  | Type |  Sample            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|asset| |YES|string| 
|symbol| symbol|YES|string| 
|timestamp| |YES|string|timestamp|
|signature| |YES|string|signature|

**Response Parameter**

| Name | Description  |Type | Sample|
| :------------ | :-------- | :--------| :------------------- |
|amount| max borrowable amount|string|1.69248805|
|borrowLimit| borrowLimit |string|60|


## Repay
Description

> request

```
get /api/v3/margin/repay?asset=BTC&symbol=BTCUSDT&tranId=2597392&timestamp={{timestamp}}&signature={{signature}}
```
> response

```json
[

]
```
**Http Request**

- **GET** ```/api/v3/margin/repay```

**Request Parameter**

| Name | Description| Mandatory  | Type |  Sample            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|asset| |YES|string| |
|symbol|symbol|YES|string| |
|tranId|transfer id|YES|string| |
|startTime| |NO|string| |
|endTime| |NO|string| |
|current|current page Default:1|NO|string| |
|size|Default:10 max:100|NO|string| |
|recvWindow| |NO|string| |
|timestamp| |YES|string|timestamp|
|signature| |YES|string|signature|

**Response Parameter**

| Name | Description  |Type | Sample|
| :------------ | :-------- | :--------| :------------------- |
|symbol| symbol|string|MXUSDT|
|amount| amount|string|14.00000000|
|asset| |string|MX|
|interest| interest|string|0.01866667|
|principal| principal|string|13.98133333|
|timestamp| |number|1563438204000|
|tranId| |number|2970933056|
|total| |number|1|

**Description**:

TranId or startTime must be sent, tranId takes precedence. Responses are returned in descending order. If a symbol is sent, returns the repayment record for the specified symbol specified asset on a store-by-store basis.



## Isolated Symbol

> request

```
get /api/v3/margin/isolated/pair?symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> response

```json

  {
   "symbol":"BTCUSDT",
   "base":"BTC",
   "quote":"USDT",
   "isMarginTrade":true
  }

```
**Http Request**

- **GET** ```/api/v3/margin/isolated/pair```

**Request Parameter**

| Name | Description| Mandatory  | Type |  Sample            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|symbol| |YES|string|| 
|timestamp| |YES|string|timestamp|
|signature| |YES|string|signature|

**Response Parameter**

| Name | Description  |Type | Sample|
| :------------ | :-------- | :--------| :------------------- |
|symbol| |string|BTCUSDT|
|base| |string|BTC|
|quote| |string|USDT|
|isMarginTrade|isMarginTrade   |boolean|true|



## Force Liquidation Record

> request

```
get /api/v3/margin/forceLiquidationRec?symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> response

```json
{

}

```
**Http Request**

- **GET** ```/api/v3/margin/forceLiquidationRec```

**Request Parameter**

| Name | Description| Mandatory  | Type |  Sample            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|startTime| |NO|string| |
|endTime| |NO|string|| 
|symbol| |YES|string|| 
|current|current page Default:1|NO|string|| 
|size|Default:10 max:100|NO|string|| 
|timestamp| |YES|string|timestamp|
|signature| |YES|string|signature|

**Response Parameter**

| Name | Description  |Type | Sample|
| :------------ | :-------- | :--------| :------------------- |
|avgPrice| |string|0.00388359|
|executedQty| |string|31.39000000|
|orderId|order id|string|180015097|
|price|price|string|0.00388110|
|qty| |string|31.39000000|
|side| |string|SELL|
|symbol| |string|MXBTC|
|isIsolated| is isolated|boolean|true|
|updatedTime| |number|1558941374745|
|total| |number|1|

**Description**:

Responses are returned in descending order.


## Isolated MarginData

> request

```
get /api/v3/margin/isolatedMarginData?symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> response

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
**Http Request**

- **GET** ```/api/v3/margin/isolatedMarginData```

**Request Parameter**

| Name | Description| Mandatory  | Type |  Sample            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|symbol| |YES|string|| 
|timestamp| |YES|string|timestamp|
|signature| |YES|string|signature|

**Response Parameter**

| Name | Description  |Type | Sample|
| :------------ | :-------- | :--------| :------------------- |
|symbol| |string|BTCUSDT|
|leverage| |string|10|
|coin| |string|BTC|
|hourInterest|hourInterest|string|0.00026125|
|borrowLimit|borrowLimit|string|270|



## Isolated MarginTier

> request

```
get /api/v3/margin/isolatedMarginTier?symbol=BTCUSDT&timestamp={{timestamp}}&signature={{signature}}
```
> response

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
**Http Request**

- **GET** ```/api/v3/margin/isolatedMarginTier```

**Request Parameter**

| Name | Description| Mandatory  | Type |  Sample            |
| :------ | :-------- | :-------- | :---------- | :------------------- |
|symbol| |YES|string|| 
|tier||NO|string|| 
|timestamp| |YES|string|timestamp|
|signature| |YES|string|signature|

**Response Parameter**

| Name | Description  |Type | Sample|
| :------------ | :-------- | :--------| :------------------- |
|symbol| |string|BTCUSDT|
|tier|tier|number|1|
|effectiveMultiple|effectiveMultiple|string|10|
|initialRiskRatio|initialRiskRatio|string|1.111|
|liquidationRiskRatio|liquidationRiskRatio|string|1.05|
|baseAssetMaxBorrowable|baseAssetMaxBorrowable|string|9|
|quoteAssetMaxBorrowable|quoteAssetMaxBorrowable|string|70000|

# Websocket Market Streams

- The base endpoint is: **wss://wbs.mexc.com/ws**.

- A single connection to **wbs.mexc.com** is only valid for 24 hours; expect to be disconnected at the 24 hour mark.

- All symbols are **Uppercase** <br/>eg:`spot@public.deals.v3.api@<symbol>`</br>->`spot@public.deals.v3.api@BTCUSDT`.

- If there is no valid websocket subscription, the server will disconnect in **30 seconds**. If the subscription is successful but there is no streams, the server will disconnect in **1 minute**. The client can send `PING` to maintain the connection.

- Every websocket connection maximun support 30 subscriptions at one time.

## Live Subscribing/Unsubscribing to streams

- The following data can be sent through the websocket instance in order to subscribe/unsubscribe from streams. Examples can be seen below.

- The id used in the JSON payloads is an unsigned INT used as an identifier to uniquely identify the messages going back and forth.

- In the response, if the `msg`  received is same as request params, this means the request sent was a success.

### Subscribe to a stream

> **Subscribe Response**

```
 {
  "id":0,
  "code":0,
  "msg":"spot@public.deals.v3.api@BTCUSDT"
 }
```

- **Request**


{
 "method":"SUBSCRIPTION",
 "params":["spot@public.deals.v3.api@BTCUSDT"]
}

### Unsubscribe to a stream

> **Unsubscribe Response**

```
 {
  "id":0,
  "code":0,
  "msg":"spot@public.increase.depth.v3.api@BTCUSDT,spot@public.deals.v3.api@BTCUSDT"
 }
```

- **Request**

{
 "method":"UNSUBSCRIPTION",
 "params":["spot@public.deals.v3.api@BTCUSDT","spot@public.increase.depth.v3.api@BTCUSDT"]
}

### PING/PONG

> **PING/PONG Response**

```
 {
  "id":0,
  "code":0,
  "msg":"PONG"
 }
```

- **Request**

{"method":"PING"}

## Trade Streams

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
					"S":2,                             //tradeType
					"p":"20233.84",                    //price
					"t":1661927587825,  				       //dealTime
					"v":"0.001028"}],  						     //quantity
			"e":"spot@public.deals.v3.api"},        //eventType			         
	"s":"BTCUSDT",  								           //symbol
	"t":1661927587836                          //eventTime
} 								         
```

**Request:**   `spot@public.deals.v3.api@<symbol>`

The Trade Streams push raw trade information; each trade has a unique buyer and seller.

**Response:**

| Name      | Type   | Description |
| :-------- | :----- | :--- |
| deals | array | dealsInfo  |
| > S | int | tradeType 1:buy 2:sell |
| > p | string | price |
| > t | long | dealTime |
| > v | string | quantity |
| e | string | eventType |
| s | string | symbol |
| t | long | eventTime |

## Kline Streams

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
				"T":1661931900,                     
				"a":29043.48804658,	 
				"c":20279.43,				 
				"h":20284.93,				 
				"i":"Min15",				 
				"l":20277.52,				 
				"o":20284.93,				 
				"t":1661931000,			 
				"v":1.43211},				 
			"e":"spot@public.kline.v3.api"},					
	"s":"BTCUSDT",						
	"t":1661931016878					 
}

```

The Kline/Candlestick Stream push updates to the current klines/candlestick every second.

**Request:** `spot@public.kline.v3.api@<symbol>@<interval>`

**Response:**

| Name      | Type   | Description |
| :-------- | :----- | :--- |
| k | object| klineInfo |
| > T | long | endTime |
| > a | bigDecimal | volume |
| > c | bigDecimal | closingPrice |
| > h | bigDecimal | highestPrice |
| > i | interval | interval |
| > l | bigDecimal | lowestPrice |
| > o | bigDecimal | openingPrice |
| > t | long | stratTime |
| > v | bigDecimal | quantity |
| s | string | symbol |
| t | long | eventTime |

**Kline chart intervals:**

Min -> minutes; Hour -> hours; Day -> days; Week -> weeks, M -> months

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

## Diff.Depth Stream

> **request:**

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
		"asks":[{									
			"p":"20290.89",		
			"v":"0.000000"}], 
		"e":"spot@public.increase.depth.v3.api", 
    "r":"3407459756"},	 
	"s":"BTCUSDT",						
	"t":1661932660144					
}
```

If the quantity is 0, it means that the order of the price has been cancel or traded,remove the price level.

**Request:** `spot@public.increase.depth.v3.api@<symbol>`

**Response:**

| Name      | Type   | Description |
| :-------- | :----- | :--- |
| p | string | price |
| v | string | quantity |
| e | string | eventType |
| r | string | version |
| s | string | symbol |
| t | long | eventTime |

**How is incremental depth information maintained:**

1. Though **spot@public.increase.depth.v3.api@<symbol>** to get full amount of depth information, save the current version.
2. Subscribe to ws depth information, if the received data version more than the current version after update,  the later received update cover the previous one at the same price.
3. Through **https://api.mexc.com/api/v3/depth?symbol=MXBTC&limit=1000** get  the latest 1000 depth snapshots.
4. Discard version data from the snapshot obtained by Version (less than step 3 )for the same price in the current cached depth information
5. Update the contents of the deep snapshots to the local cache and keep updating from the event received by the WS
6. The version of each new event should be exactly equal to version+1 of the previous event, otherwise packet loss may occur. In case of packet loss or discontinuous version of the event retrieved, please re-initialize from Step 3.
7. The amount of hanging orders in each event represents the **absolute value** of the current hanging orders of the price, rather than the relative change.
8. If the amount of a hanging order corresponding to a certain price is 0, it means that the hanging order at that price has been cancelled, the price should be removed.

# Websocket User Data Streams

- The base API endpoint is: **https://api.mexc.com**

- A User Data Stream `listenKey` is valid for 60 minutes after creation.

- Doing a `PUT` on a `listenKey` will extend its validity for 60 minutes.

- Doing a `DELETE` on a `listenKey` will close the stream and invalidate the `listenKey`.

- Doing a `POST` on an account with an active `listenKey` will return the currently active `listenKey` and extend its validity for 60 minutes.

- websocket baseurl: **wss://wbs.mexc.me/ws**

- User Data Streams are accessed at **/ws?listenKey=listenKey** <br/>eg:**wss://wbs.mexc.me/ws?listenKey=pqia91ma19a5s61cv6a81va65sd099v8a65a1a5s61cv6a81va65sdf19v8a65a1**

- A single connection is only valid for 24 hours; expect to be disconnected at the 24 hour mark.

- Each UID can apply for a maximum of 60 listen keys (excluding invalid listen keys).

- Each listen key maximum support  5 websocket connection (which means each uid can applies for a maximum of 60 listen keys and 300 ws links).

## Listen Key 

### Create a ListenKey

> **Response**

```
{
  "listenKey": "pqia91ma19a5s61cv6a81va65sdf19v8a65a1a5s61cv6a81va65sdf19v8a65a1"
}
```

**HTTP**

- **POST**  ` /api/v3/userDataStream`

Start a new user data stream. The stream will close after 60 minutes unless a keepalive is sent. If the account has an active `listenKey`, that `listenKey` will be returned and its validity will be extended for 60 minutes. 

**request:**

NONE

### Keep-alive a ListenKey 

> **Response**

```
{
    "listenKey": "pqia91ma19a5s61cv6a81va65sdf19v8a65a1a5s61cv6a81va65sdf19v8a65a1"
}
```
**HTTP**

- **PUT**  ` /api/v3/userDataStream`

Keepalive a user data stream to prevent a time out. User data streams will close after 60 minutes. It's recommended to send a ping about every 30 minutes.

**Request:**

| Name    | Type | Mandatory | Description |
| :-------- | :------- | :------- | :--- |
| listenKey | STRING   | YES      |      |

 ### Close a ListenKey  

 > **Response**

 ```
 {
     "listenKey": "pqia91ma19a5s61cv6a81va65sdf19v8a65a1a5s61cv6a81va65sdf19v8a65a1"
 }
 ```

 **HTTP**

 - **DELETE**  ` /api/v3/userDataStream`

 Close out a user data stream.


## Spot Account Deals

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

**Request:** `spot@private.deals.v3.api`

**Response:**

| Name      | Type   | Description |
| :-------- | :----- | :--- |
| d | json | dealsInfo |
| > S | int | tradetype 1:buy 2:sell |
| > T | long | tradeTime |
| > c | string | clientOrderId |
| > i | string | orderId |
| > m | int | isMaker |
| > p | string | price |
| > st | byte | isSelfTrade |
| > t | string | tradeId |
| > v | string | quantity |
| s | string | symbol |
| t | long |eventTime |

## Spot Account Orders

>**request:**

```
{
  "method": "SUBSCRIPTION",
  "params": [
      "spot@private.orders.v3.api"
  ]
}
```

**Request:** `spot@private.orders.v3.api`

### 1. Limit/Market Orders 

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
        "v":10,
        "ap":0,  
        "cv":0, 	
        "ca":0 
  },
  "s": "MXUSDT",
  "t": 1661938138193
}
```

**Response:**

| Name      | Type   | Description |
| :-------- | :----- | :--- |
| d | json | orderInfo |
| > A | bigDecimal | remainAmount |
| > O | long | createTime|
| > S | int | tradetype 1:buy 2:sell |
| > V | bigDecimal | remainQuantity |
| > a | bigDecimal | amount |
| > c | string | clientOrderId |
| > i | string | orderId |
| > m | int | isMaker |
| > o | int | LIMIT_ORDER(1),POST_ONLY(2),IMMEDIATE_OR_CANCEL(3),<br />FILL_OR_KILL(4),MARKET_ORDER(5);STOP_LIMIT(100) |
| > p | bigDecimal | PRICE |
| > s | int | status 1:New order 2:Filled 3:Partially filled 4:Order canceled 5:Order filled partially, and then the rest of the order is canceled |
| > v | bigDecimal | quantity |
| > ap | bigDecimal | avgPrice |
| > cv | bigDecimal | cumulativeQuantity |
| > ca | bigDecimal | cumulativeAmount |
| t | long | eventTime |
| s | string | symbol |

### 2. Stop Limit Order

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

**Response:**

|  Name      | Type   | Description |
| :-------- | :----- | :--- |
| d            | json | orderInfo |
| > N | string | commissionAsset |
|  > O | long | createTime |
|  > P | bigDecimal | triggerPrice |
|  > S | int | tradetype 1:buy 2:sell |
|  > T | int | 0: GE(price is higher than triggerPrice) 1: LE(price is lower than triggerPrice) |
|  > i | string | orderId |
| >  o | int | orderType LIMIT_ORDER(1),POST_ONLY(2),IMMEDIATE_OR_CANCEL(3),<br />FILL_OR_KILL(4),MARKET_ORDER(5);STOP_LIMIT(100) |
|  > p | bigDecimal | price |
| > s | string | state  NEW,CANCELED,EXECUTED,FAILED |
|  > v | bigDecimal | quantity |
| s | string | symbol |
| t | long | eventTime |

## Margin Account Orders

> **request:**

```
{
    "method": "SUBSCRIPTION",
    "params": [
        "margin@private.orders.v3.api"
    ]
}
```
> **response:**

```
{
    "c": "margin@private.orders.v3.api",
    "d":{
         "O":1661938138000,   
         "p":"0.8",           
         "a":"8",             
         "v":"10",            
        "da":"0",           
        "dv":"0",          
         "A":"8.0",           
         "V":"10",            
         "n": "0",            
         "N": "USDT",         
         "S":1,               
         "o":1,               
         "s":1,               
         "i":"e03a5c7441e44ed899466a7140b71391", 
    },
    "s": "MXUSDT",           
    "t":1661938138193       
}
```
**Request:** `margin@private.orders.v3.api`

**response:**

| Name | Type | Description          |
| :----- | :------- | :------------ |
| d      | json     | order info  |
| >O     | long     | createTime  |
| >p     | string   | price      |
| >a     | string   | amount    |
| >v     | string   | quantity      |
| >da     | string  | dealAmount    |
| >dv     | string  | dealQuantity      |
| >A     | string   | remainAmount|
| >V     | string   | remainQuantity|
| >n     | string   | fee   |
| >N     | string   | feeCurrency|
| >S     | int      | tradeType |
| >o     | int      | orderType   |
| >s     | int      | status    |
| >i     | string   | orderId        |
| s      | string   | symbol        |
| t      | long     | timestamp     |

## Margin Account Risk Rate

> **request:**

```
{
    "method": "SUBSCRIPTION",
    "params": [
        "margin@private.risk.rate.v3.api@BTCUSDT",
    ]
}
```
> **response:**

```
{
    "c": "margin@private.risk.rate.v3.api@BTCUSDT",
    "d":{
          "ba":{          
                 "a":"0.0", 
                 "b":"0.0", 
                 "f":"0.0", 
                 "i":"0.0", 
                 "n":"BTC",
                 "t":"0.0"},
          "qa":{           
                 "a":"1359.917312", 
                 "b":"1279.922176", 
                 "f":"0.0",         
                 "i":"8.44748637",  
                 "n":"USDT",      
                 "t":"1359.917312"},
          "l":"--",        
          "r":"1.05",      
          "sl":"1.05",     
     },
    "s":"BTCUSDT",  
    "t":1661938138193     
}
```
**Request:** `margin@private.risk.rate.v3.api@<symbol>`

**response:**

| Name      | Type   | Description |
| :-------- | :----- | :--- |
| d | json | riskRateInfo |
| >ba | json | currencyAsset |
| >qa | json | marketAsset |
| >>a | string | availableAmount|
| >>b | string | borrowAmount|
| >>f | string | frozenAmount |
| >>i | string | interest|
| >>n | string | name |
| >>t | string | totalAmount |
| >l | string | liquidationPrice |
| >r | string | riskRate|
| >sl | string |stopLine|
| s | string | symbol|
| t | long | timestamp |

# Rebate Endpoints

## Get Rebate History Records

> request

```
get /api/v3/rebate/taxQuery?timestamp={{timestamp}}&signature={{signature}}
```
> response

```json
{
    "page": 1,  
    "totalRecords": 1,  
    "totalPageNum": 1,  
    "data": [
        {
            "spot": "0.00082273",  
            "futures":"0.00022487",       
            "total": "0.00012126",  
            "uid": "221827",  
            "account": "154****291@qq.com",  
            "inviteTime": 1637651320000
        },
        ...
        {
            "spot": "0.00082273",  
            "futures":"0.00022487",    
            "total": "0.00012126",  
            "uid": "82937",  
            "account": "338****291@qq.com",  
            "inviteTime": 1637651320000
        }
    ]
}
```
**Http Request**

- **GET** ```/api/v3/rebate/taxQuery```

**Request**

| Name | Type|  Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
| startTime  | long | NO       |        |
| endTime    | long | NO       |        |
| page       | int  | NO       | default 1  |
| recvWindow | long | NO       |        |
| timestamp  | long | YES       |        |
| signature  | string | YES     |        |

**Response**

| Name  |Type | Description|
| :------------ | :-------- | :--------|
| spot |string|spot rebate,unit:usdt|
| futures |string|futures rebate,unit:usdt|
| total |string|total rebate,unit:usdt|
| uid |string|Invitee uid|
| account |string|Invitee account|
| inviteTime |long|invite time|

If startTime and endTime are not sent, the recent 1 year's data will be returned.

## Get Rebate Records Detail

> request

```
get /api/v3/rebate/detail?timestamp={{timestamp}}&signature={{signature}}
```
> response

```json
{
     "page": 1, 
     "totalRecords": 1, 
     "totalPageNum": 1, 
     "data": [
         {
             "asset": "USDT", 
             "type": "spot",       
             "rate": "0.3", 
             "amount": "0.0001126", 
             "uid": "2293729101827", 
             "account": "154****291@qq.com", 
             "tradeTime": 1637651320000,
             "updateTime": 1637651320000
         },
         ...
         {
             "asset": "ETH", 
             "type": "margin", 
             "rate": "0.3", 
             "amount": "0.00000056",
             "uid": "22937291018263", 
             "account": "154****291@qq.com", 
             "tradeTime": 1637651320000,
             "updateTime": 1637928379000
         }
     ]
}
​
```
**Http Request**

- **GET** ```/api/v3/rebate/detail```

**Request**

| Name | Type|  Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
| startTime  | long | NO       |        |
| endTime    | long | NO       |        |
| page       | int  | NO       | default 1  |
| recvWindow | long | NO       |        |
| timestamp  | long | YES       |        |
| signature  | string | YES     |        |


**Response**

| Name  |Type | Description|
| :------------ | :-------- | :--------|
|asset|string|rebate asset|
|type|string|rebate type: spot futures margin |
|rate|string|rebate rate|
|amount|string|rebate amount|
|uid|string|Invitee uid|
|account|string|Invitee account|
|tradeTime|long|trade time|
|updateTime|long|update time|

If startTime and endTime are not sent, the recent 1 year's data will be returned.

## Get Self Rebate Records Detail

> request

```
get /api/v3/rebate/detail/kickback?timestamp={{timestamp}}&signature={{signature}}
```
> response

```json
{
    "page": 1,  
    "totalRecords": 27,  
    "totalPageNum": 3,  
    "data": [
        {
            "asset": "USDT",  
            "type": "spot",        
            "rate": "0.3", 
            "amount": "0.0001126",  
            "uid": "2293729101827",  
            "account": "154****291@qq.com",  
            "tradeTime": 1637651320000,
            "updateTime": 1637651320000
        },
        ...
        {
            "asset": "ETH", 
            "type": "margin", 
            "rate": "0.3", 
            "amount": "0.00000056",
            "uid": "22937291018263",  
            "account": "154****291@qq.com",  
            "tradeTime": 1637651320000,
            "updateTime": 1637928379000
        }
    ]
}
```
**Http Request**

- **GET** ```/api/v3/rebate/detail/kickback```

**Request**

| Name | Type|  Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
| startTime  | long | NO       |        |
| endTime    | long | NO       |        |
| page       | int  | NO       | default 1  |
| recvWindow | long | NO       |        |
| timestamp  | long | YES       |        |
| signature  | string | YES     |        |


**Response**

| Name  |Type | Description|
| :------------ | :-------- | :--------|
|asset|string|rebate asset|
|type|string|rebate type: spot futures margin |
|rate|string|rebate rate|
|amount|string|rebate amount|
|uid|string|Invitee uid|
|account|string|Invitee account|
|tradeTime|long|trade time|
|updateTime|long|update time|

If startTime and endTime are not sent, the recent 1 year's data will be returned.

## Query ReferCode

> request

```
get /api/v3/rebate/referCode?timestamp={{timestamp}}&signature={{signature}}
```
> response

```json
{
    "referCode": "in3jd"
}
```
**HTTP Request**

- **GET** ```/api/v3/rebate/referCode```

**Request**

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
| recvWindow | long | NO       |        |
| timestamp  | long | YES       |        |
| signature  | string | YES     |        |


**Response**

| Name  |Type | Description|
| :------------ | :-------- | :--------|
|referCode|string|referCode|

# Public API Definitions

## ENUM definitions

### <a id="order_side">Order side</a>

- BUY
- SELL

### <a id="order_type">Order type</a>

- LIMIT (Limit order)   
- MARKET (Market order)
- LIMIT_MAKER   (Limit maker order)
- IMMEDIATE_OR_CANCEL (Immediate or cancel order)
- FILL_OR_KILL (Fill or kill order)

### <a id="order_status">Order Status</a>

- NEW   Uncompleted
- FILLED  Filled
- PARTIALLY_FILLED  Partially filled
- CANCELED  Canceled
- PARTIALLY_CANCELED  Partially canceled

### <a id="kline_interval">Kline Interval</a>

- 1m  1 minute
- 5m  5 minute
- 15m  15 minute
- 30m  30 minute
- 60m  60 minute
- 4h  4 hour
- 1d  1 day
- 1M  1 month

