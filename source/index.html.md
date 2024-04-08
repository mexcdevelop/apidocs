---
title: API Document

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

includes:

search: true

meta:
  - name: description
    content: Documentation for the mexc API
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

[https://github.com/mexcdevelop/mexc-api-sdk](https://github.com/mexcdevelop/mexc-api-sdk)

<aside class="notice">
Any problem please submit <a href="https://github.com/mexcdevelop/mexc-api-sdk/issues" target="_blank"> feedback</a>
</aside>
### Postman Collections

There is now a Postman collection containing the API endpoints for quick and easy use.

This is recommended for new users who want to get a quick-start into using the API.

For more information please refer to this page: [MEXC API Postman](https://github.com/mexcdevelop/mexc-api-postman)

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

## **2024-04-04**

- Update response params of Get Withdraw History endpoint

## **2024-01-12**

- Add query sub-account asset endpoint

## **2024-01-01**

- Kline support interval: week
- Deposit and withdraw history endpoint update the query timestamp range

## **2023-12-11**

- Query Sub-account List endpoint add response params:uid

## **2023-11-10**

- Add user internal transfer endpoint and query internal transfer history endpoint.
- Add ws miniTicker and miniTickers channels.

## **2023-10-17**

- Add Get Affiliate Referral Data endpoint and Get Subaffiliates Data endpoint

## **2023-09-27**

- Add Get Affiliate Withdraw Record endpoint and Get Affiliate Commission Detail Record endpoint

## **2023-08-15**

- Add Get Affiliate Commission Record endpoint

## **2023-06-13**

- Add query all listenKey endpoint

## **2023-05-21**

- Add Download Historical Market Data

## **2023-03-16**

- Add:Query User Universal Transfer History (by tranId) endpoint

- ws spot@private.deals.v3.api channel add params:"commission","commissionAsset"and"deals amount"

## 

## **2023-03-12**

- Add:API default symbol,User API default symbol,cancel withdraw,Deposit Address endpoints.

## **2023-03-07**

- ws add channel:Account Update

## **2023-02-13**

- Add:Get Assets That Can Be Converted Into MX,Dust Transfer,Dust Log endpoints

## **2023-02-07**

- ws add channel:Individual Symbol Book Ticker Streams

## **2023-01-06**

- [Update Limits Info](https://mexcdevelop.github.io/apidocs/spot_v3_en/#limits)

## **2022-12-29**

- [ETF](https://mexcdevelop.github.io/apidocs/spot_v3_en/#etf) remove some response params:

| Name       | type | Description          |
| :------------- | :------- | :------------ |
| preBasket      | string   | preBasket  |
| preLeverage    | string   | preLeverage  |

## **2022-12-28**

- websocket add Partial Book Depth Streams

## **2022-12-13**

- Add params: avgPrice,cumulativeQuantity,cumulativeAmount for `spot@private.orders.v3.api` channel
- Add Query ReferCode Endpoint

## **2022-11-24**

- Add MEXC Broker Introduction
- Add "Enable MX Deduct" and "Query MX Deduct Status" Endpoints

## **2022-10-14**

- Update Endpoints [Wallet Endpoints](https://mexcdevelop.github.io/apidocs/spot_v3_en/#wallet-endpoints):

  1.[Withdraw](https://mexcdevelop.github.io/apidocs/spot_v3_en/#withdraw): When do a withdraw, `address` and `memo` should be passed separate (The previous version the memo is joined with a ":" after address).

  2.[Withdraw History](https://mexcdevelop.github.io/apidocs/spot_v3_en/#withdraw-history-supporting-network): Parameters `address` and `memo` should be returned separate (The previous version the memo is joined with a ":" after address).

  3.[Deposit Address](https://mexcdevelop.github.io/apidocs/spot_v3_en/#deposit-history-supporting-network): The return parameter  `tag` is changed to `memo`, and the memo required for deposite is returned in the `memo` parameter.

  4.[Deposit History](https://mexcdevelop.github.io/apidocs/spot_v3_en/#deposit-history-supporting-network): The return parameter  `addressTag` is changed to `memo`, and the memo required for deposite is returned in the `memo` parameter.

  5.Add [Generate deposit address](https://mexcdevelop.github.io/apidocs/spot_v3_en/#withdraw-history-supporting-network)

  6.[Query the currency information](https://mexcdevelop.github.io/apidocs/spot_v3_en/#query-the-currency-information): add `withdrawTips` and `depositTips` params。


## **2022-09-06**

- Add [Rebate Endpoints](https://mexcdevelop.github.io/apidocs/spot_v3_en/#rebate-endpoints):

  1.[Get Rebate History Records](https://mexcdevelop.github.io/apidocs/spot_v3_en/#get-rebate-history-records):Get the rebates from friends you invited and the transactions they make.

  2.[Get Rebate Records Detail](https://mexcdevelop.github.io/apidocs/spot_v3_en/#get-rebate-records-detail):You can query the records of each rebate generated by contracts and spot (non-leveraged) transactions made by your friends and their sub-accounts.

  3.[Get Self Rebate Records Detail](https://mexcdevelop.github.io/apidocs/spot_v3_en/#get-self-rebate-records-detail):You can query the each contract and spot (no margin) your invited friend made as the self-commission record generated from it.

## **2022-09-02**

- Add v3 websocket:

  1.Websocket Market Streams:[Trade Streams](https://mexcdevelop.github.io/apidocs/spot_v3_en/#trade-streams),[Kline Streams](https://mexcdevelop.github.io/apidocs/spot_v3_en/#kline-streams),[Diff.Depth Stream](https://mexcdevelop.github.io/apidocs/spot_v3_en/#diff-depth-stream);

  2.Websocket User Data Streams:[Account Deals](https://mexcdevelop.github.io/apidocs/spot_v3_en/#account-deals),[Account Orders](https://mexcdevelop.github.io/apidocs/spot_v3_en/#account-orders).

## **2022-08-26**

- [ETF](https://mexcdevelop.github.io/apidocs/spot_v3_en/#etf) add some response params:

| Name       | type | Description          |
| :------------- | :------- | :------------ |
| preBasket      | string   | preBasket  |
| preLeverage    | string   | preLeverage  |
| basket         | string   | basket   |

## **2022-08-15**

- Update for Sub-account endpoints:

  1.[Universal Transfer](https://mexcdevelop.github.io/apidocs/spot_v3_en/#universal-transfer-for-master-account)

  2.[Query Universal Transfer History](https://mexcdevelop.github.io/apidocs/spot_v3_en/#query-universal-transfer-history-for-master-account)


## **2022-08-03**

- Add [Wallet Endpoints](https://mexcdevelop.github.io/apidocs/spot_v3_en/#wallet-endpoints):

  1.[Query the currency information](https://mexcdevelop.github.io/apidocs/spot_v3_en/#query-the-currency-information)

  2.[Withdraw](https://mexcdevelop.github.io/apidocs/spot_v3_en/#withdraw)

  3.[Deposit History](https://mexcdevelop.github.io/apidocs/spot_v3_en/#deposit-history-supporting-network)

  4.[Withdraw History](https://mexcdevelop.github.io/apidocs/spot_v3_en/#withdraw-history-supporting-network)

  5.[Deposit Address](https://mexcdevelop.github.io/apidocs/spot_v3_en/#deposit-address-supporting-network)

  6.[User Universal Transfer](https://mexcdevelop.github.io/apidocs/spot_v3_en/#user-universal-transfer)

  7.[Query User Universal Transfer History](https://mexcdevelop.github.io/apidocs/spot_v3_en/#query-user-universal-transfer-history)

## **2022-07-27**

- Spot [New Order](https://mexcdevelop.github.io/apidocs/spot_v3_en/#new-order) Order type add: IOC and FOK

## **2022-07-15**

- [Account Trade List](https://mexcdevelop.github.io/apidocs/spot_v3_en/#account-trade-list) add params: isSelfTrade

| Name          | Description              |
| :-------------- | :---------------- |
| isSelfTrade     | isSelfTrade        |

## **2022-07-08**

- Add [Batch Orders](https://mexcdevelop.github.io/apidocs/spot_v3_en/#batch-orders) Supports 20 orders in a batch,rate limit: 2 times/s.

## **2022-07-03**

- Add [Query the currency information](https://mexcdevelop.github.io/apidocs/spot_v3_en/#query-the-currency-information),Query currency details and the smart contract address.


## **2022-05-22**

- Optimize exchangeInfo Endpoints
- Optimize order Endpoints,add parameter: order id

## **2022-04-25**

- [Exchange Info](https://mexcdevelop.github.io/apidocs/spot_v3_en/#exchange-information) add parameters:

| Name                     | type | Description                |
| :------------------------- | :------- | :------------------ |
| isSpotTradingAllowed       | Boolean  | isSpotTradingAllowed |
| isMarginTradingAllowed     | Boolean  | isMarginTradingAllowed |


- [Current Open Orders](https://mexcdevelop.github.io/apidocs/spot_v3_en/#current-open-orders) Optimize: Get all open orders on multiple symbols,maximun support 5 symbols for one request.

## **2022-03-29**

- Add [Sub-Account Endpoints](https://mexcdevelop.github.io/apidocs/spot_v3_en/#sub-account-endpoints):

  1.[Create a Sub-account](https://mexcdevelop.github.io/apidocs/spot_v3_en/#create-a-sub-account-for-master-account)

  2.[Query Sub-account List](https://mexcdevelop.github.io/apidocs/spot_v3_en/#query-sub-account-list-for-master-account)

  3.[Create an APIKey for a sub-account](https://mexcdevelop.github.io/apidocs/spot_v3_en/#create-an-apikey-for-a-sub-account-for-master-account)

  4.[Query the APIKey of a sub-account](https://mexcdevelop.github.io/apidocs/spot_v3_en/#query-the-apikey-of-a-sub-account-for-master-account)

  5.[Delete the APIKey of a sub-account](https://mexcdevelop.github.io/apidocs/spot_v3_en/#delete-the-apikey-of-a-sub-account-for-master-account)

  6.[Universal Transfer](https://mexcdevelop.github.io/apidocs/spot_v3_en/#universal-transfer-for-master-account)

  7.[Query Universal Transfer History](https://mexcdevelop.github.io/apidocs/spot_v3_en/#query-universal-transfer-history-for-master-account)


## **2022-03-25**

- Add [Postman collection](https://mexcdevelop.github.io/apidocs/spot_v3_en/#api-library)

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

- Add [ETF](https://mexcdevelop.github.io/apidocs/spot_v3_en/#etf)

## **2022-02-11**

- New version API

# FAQs

## Q1: How many API Keys can a user apply?

Each account can create up to 30 API Keys. The validity of an API Key without a linked IP address is 90 days, and the API Key will expire automatically. Each API Key can be linked to a maximum of 10 IP addresses.

## Q2: How many sub-accounts can a main account apply?

Each main account can create up to 30 sub-accounts. The sub-accounts will automatically inherit the main account rates. However, sub-accounts created via API cannot be logged in on Web.

## Q3: Why are there often issues of disconnections and expired sessions?

If stable access is not possible, it is recommended to use Japan or Singapore AWS cloud servers for access.

## Q4: What should I do after an error is reported for exceeding the limit frequency?

After exceeding the interface access frequency limit, you will not be able to continue accessing the interface. It will resume to normal after 10 minutes to keep the interface access frequency below the limit.

## Q5: How many orders can an account place?

Each account can hold up to 500 valid orders that are not completely filled.

## Q6:Why does WebSocket always disconnect?

1. If there is no valid subscription, it will disconnect in 30 seconds.
2. If the subscription is successful, and there is no traffic in 60 seconds, it will automatically disconnect.
3. To ensure a stable connection, a Pong reply is required upon receiving the Ping message sent from the server.

## Q7: Why am I unable to subcribe to multiple channels on WebSocket?

WebSocket currently allows subscription to up to 30 channels via a single link. Any subscription will be invalid after the limit is exceeded. To subscribe to more channels, it is recommended to create multiple links.

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
- For POST, PUT, and DELETE endpoints, the parameters may be sent as a query string with content type application/x-www-form-urlencoded,or in the request body with content type application/json. You may mix parameters between both the query string and request body if you wish to do so.
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

## LIMITS

There is rate limit for API access frequency, upon exceed client will get code 429: Too many requests.
The account is used as the basic unit of speed limit for the endpoints that need to carry access keys. For endpoints that do not need to carry access keys, IP addresses are used as the basic unit of rate limiting.

### Limits Description

- According to the two modes of IP and UID (account) limit, each are independent.
- Endpoints are marked according to IP or UID limit and their corresponding weight value.
- Each endpoint with IP limits has an independent 20000 per minute limit.
- Each endpoint with UID limits has an independent 240000 per minute limit.

### Limits Error

- When a 429 is received, it's your obligation as an API to back off and not spam the API.
- Repeatedly violating rate limits and/or failing to back off after receiving 429s will result in an automated IP ban .
- IP bans are tracked and scale in duration for repeat offenders, from 2 minutes to 3 days.
- A Retry-After header is sent with a 418 or 429 responses and will give the number of seconds required to wait, in the case of a 429, to prevent a ban, or, in the case of a 418, until the ban is over.

### Websocket Limits

- The Websocket limits is: 100times/s.
- A connection that goes beyond the limit will be disconnected; IPs that are repeatedly disconnected may be banned.
- A single connection can listen to a maximum of 30 streams.

## Error Code

The following error information can be returend

| Code      | Description                                                                           |
|-----------|---------------------------------------------------------------------------------------|
| -2011  | Unknown order sent                                           | 
| 26     | operation not allowed                                        | 
| 400    | api key required                                             | 
| 401    | No authority                                                 | 
| 403    | Access Denied                                                | 
| 429    | Too Many Requests                                            | 
| 500    | Internal error                                               | 
| 503    | service not available, please try again                      | 
| 504    | Gateway Time-out                                             | 
| 602    | Signature verification failed                                | 
| 10001  | user does not exist                                          | 
| 10007  | bad symbol                                                   | 
| 10015  | user id cannot be null                                       | 
| 10072  | invalid access key                                           | 
| 10073  | invalid Request-Time                                         | 
| 10095  | amount cannot be null                                        | 
| 10096  | amount decimal places is too long                            | 
| 10097  | amount is error                                              | 
| 10098  | risk control system detected abnormal                        | 
| 10099  | user sub account does not open                               | 
| 10100  | this currency transfer is not supported                      | 
| 10101  | Insufficient balance                                         | 
| 10102  | amount cannot be zero or negative                            | 
| 10103  | this account transfer is not supported                       | 
| 10200  | transfer operation processing                                | 
| 10201  | transfer in failed                                           | 
| 10202  | transfer out failed                                          | 
| 10206  | transfer is disabled                                         | 
| 10211  | transfer is forbidden                                        | 
| 10212  | This withdrawal address is not on the commonly used address list or has been invalidated | 
| 10216  | no address available. Please try again later                 | 
| 10219  | asset flow writing failed please try again                   | 
| 10222  | currency cannot be null                                      | 
| 10232  | currency does not exist                                      | 
| 10259  | Intermediate account does not configured in redisredis       | 
| 10265  | Due to risk control, withdrawal is unavailable, please try again later | 
| 10268  | remark length is too long                                    | 
| 20001  | subsystem is not supported                                   | 
| 20002  | Internal system error please contact support                 | 
| 22222  | record does not exist                                        | 
| 30000  | suspended transaction for the symbol                         | 
| 30001  | The current transaction direction is not allowed to place an order | 
| 30002  | The minimum transaction volume cannot be less than :         | 
| 30003  | The maximum transaction volume cannot be greater than :      | 
| 30004  | Insufficient position                                        | 
| 30005  | Oversold                                                     | 
| 30010  | no valid trade price                                         | 
| 30014  | invalid symbol                                               | 
| 30016  | trading disabled                                             | 
| 30018  | market order is disabled                                     | 
| 30019  | api market order is disabled                                 | 
| 30020  | no permission for the symbol                                 | 
| 30021  | invalid symbol                                               | 
| 30025  | no exist opponent order                                      | 
| 30026  | invalid order ids                                            | 
| 30027  | The currency has reached the maximum position limit, the buying is suspended | 
| 30028  | The currency triggered the platform risk control, the selling is suspended | 
| 30029  | Cannot exceed the maximum order limit                        | 
| 30032  | Cannot exceed the maximum position                           | 
| 30041  | current order type can not place order                       | 
| 33333  | param is error                                               | 
| 44444  | param cannot be null                                         | 
| 60005  | your account is abnormal                                     | 
| 70011  | Pair user ban trade apikey                                   | 
| 700001 | API-key format invalid                                       | 
| 700002 | Signature for this request is not valid                      | 
| 700003 | Timestamp for this request is outside of the recvWindow      | 
| 700004 | Param 'origClientOrderId' or 'orderId' must be sent, but both were empty/null | 
| 700005 | recvWindow must less than 60000                              | 
| 700006 | IP non white list                                            | 
| 700007 | No permission to access the endpoint                         | 
| 700008 | Illegal characters found in parameter                        |   
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
| 140001 | sub account does not exist                                   |
| 140002 | sub account is forbidden                                     |

# Market Data Endpoints

## Download Historical Market Data

Provides kline and trading data for all Spot pairs since 01-01-2023:[Historical Market Data](https://www.mexc.co/zh-CN/market-data-download)

## Test Connectivity

> Response

```json
{}
```

- **GET** ```/api/v3/ping```

Test connectivity to the Rest API.

**Weight(IP):** 1

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
  
**Weight(IP):** 1

Parameter:

NONE

## API default symbol

> Request

```
GET /api/v3/defaultSymbols
```

> Response

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


- **GET** ```/api/v3/defaultSymbols ```
  
**Weight(IP):** 1

**Request**

NONE

**Response**

| Name       | Type | Description                       |
| :------------ | :-------- |:-------------------------|
| symbol | string | symbol  |

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
        "LIMIT"
    ],
    "filters": [],
    "maxQuoteAmount": "5000000",
    "makerCommission": "0.002",
    "takerCommission": "0.002"
}

```

- **GET** ```/api/v3/exchangeInfo```

Current exchange trading rules and symbol information

**Weight(IP):** 10

**Parameter**:

There are 3 possible options:

| Method       | **Example**                                                                   |
| ------------ | ----------------------------------------------------------------------------- |
| No parameter | curl -X GET "https://api.mexc.com/api/v3/exchangeInfo"                        |
| symbol       | curl -X GET "https://api.mexc.com/api/v3/exchangeInfo?symbol=MXUSDT"          |
| symbols      | curl -X GET "https://api.mexc.com/api/v3/exchangeInfo?symbols=MXUSDT,BTCUSDT" |

**Response:**

| Name       | Type | Description                      |
| :------------ | :-------- |:-------------------------|
| timezone | string | timezone                       |
| serverTime | long | server Time                    |
| rateLimits | Array | rate Limits                     |
| exchangeFilters | Array | exchange Filters                     |
| symbol | String | symbol                      |
| status | String | status                       |
| baseAsset | String | base Asset                      |
| baseAssetPrecision | Int | base Asset Precision                   |
| quoteAsset | String | quote Asset                      |
| quotePrecision | Int | quote Precision                 |
| quoteAssetPrecision | Int | quote Asset Precision                  |
| baseCommissionPrecision | Int | base Commission Precision                 |
| quoteCommissionPrecision | Int | quote Commission Precision                |
| orderTypes | Array | <a href="#order_type">Order Type</a> |
| quoteOrderQtyMarketAllowed | Boolean | quoteOrderQtyMarketAllowed                |
| isSpotTradingAllowed | Boolean |   allow api spot trading            |
| isMarginTradingAllowed | Boolean | allow api margin trading               |
| permissions | Array | permissions                       |
| maxQuoteAmount | String | max Quote Amount                  |
| makerCommission | String | marker Commission                |
| takerCommission | String | taker Commission                 |
| quoteAmountPrecision|string|  min order amount                 |
| baseSizePrecision|string|  min order quantity                 |
| quoteAmountPrecisionMarket |string| min order amount  in market order       |
| maxQuoteAmountMarket | String | max quote Amount in market order       |




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

**Weight(IP):** 1

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

**Weight(IP):** 5

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

<!-- ## Old Trade Lookup

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

**Weight(IP):** 1

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
| isBestMatch  | Was the trade the best price match? | -->

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
  
**Weight(IP):** 1

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
  
**Weight(IP):** 1

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

**Weight(IP):** 1

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

**Weight(IP):** 

| Parameter	   | Symbols Provided   |  Weight  |
| ------ | ------ | ------  |
| symbol | 1 |  1 |
| symbols | all |  40 |

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

**Weight(IP):** 

| Parameter	   | Symbols Provided   |  Weight  |
| ------  | ------ | ------  |
| symbol  | 1      |  1      |
| symbols | all    |  2      |

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

**Weight(IP):** 1

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

**Permission:** SPOT_ACCOUNT_READ

**Weight(IP):** 1

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
            "createTime":1544433328000,
            "uid": "49910511"
        },
        {
            "subAccount":"mexc888",
            "isFreeze":false,
            "createTime":1544433328000,
            "uid": "91921059"
        }
    ]
}
```

- GET / api/v3/sub-account/list   

**Permission:** SPOT_ACCOUNT_READ

**Weight(IP):** 1

Parameters:

| Name       | Type   | Mandatory | Description                       |
| ---------- | ------ | --------- | --------------------------------- |
| subAccount | STRING | NO        | Sub-account Name                  |
| isFreeze   | STRING | NO        | true or false                     |
| page       | INT    | NO        | Default value: 1                  |
| limit      | INT    | NO        | Default value: 10, Max value: 200 |
| timestamp  | LONG   | YES       |                                   |
| recvWindow | LONG   | NO        |                                   |

Response:

| Name     | Description       |
| -------- | ----------------- |
| subAccount | subAccount name            |
| isFreeze  | isFreeze   |
| createTime   | createTime  |
| uid  | subaccount uid    |





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

**Permission:** SPOT_ACCOUNT_READ

**Weight(IP):** 1

Parameters:

| Name        | Type   | Mandatory | Description                                                  |
| ----------- | ------ | --------- | ------------------------------------------------------------ |
| subAccount  | STRING | YES       | Sub-account Name                                             |
| note        | STRING | YES       | APIKey note                                                  |
| permissions | STRING | YES       | Permission of APIKey:<br/>SPOT_ACCOUNT_READ,<br/>SPOT_ACCOUNT_WRITE,<br/>SPOT_DEAL_READ,<br/>SPOT_DEAL_WRITE,<br/>CONTRACT_ACCOUNT_READ,<br/>CONTRACT_ACCOUNT_WRITE,<br/>CONTRACT_DEAL_READ,<br/>CONTRACT_DEAL_WRITE,<br/>SPOT_TRANSFER_READ,<br/>SPOT_TRANSFER_WRITE| 
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

**Permission:** SPOT_ACCOUNT_READ

**Weight(IP):** 1

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

**Permission:** SPOT_ACCOUNT_READ

**Weight(IP):** 1

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

**Permission:**  SPOT_TRANSFER_WRITE

**Weight(IP):** 1

**Parameters:**

| Name | Type| Mandatory  | Description |  
| :------ | :-------- | :-------- | :---------- |
|fromAccount|string|NO|Transfer from master account by default if fromAccount is not sent|
|toAccount|string|NO|Transfer to master account by default if toAccount is not sent|
|fromAccountType|string|YES|fromAccountType:"SPOT","FUTURES"|
|toAccountType|string|YES|toAccountType:"SPOT","FUTURES"|
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

**Permission:** SPOT_TRANSFER_READ

**Weight(IP):** 1

**Parameters:**

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
|fromAccount|string|NO|Transfer from master account by default if fromAccount is not sent|
|toAccount|string|NO|Transfer to master account by default if toAccount is not sent|
|fromAccountType|string|YES|fromAccountType:"SPOT","FUTURES"|
|toAccountType|string|YES|toAccountType:"SPOT","FUTURES"|
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

## Query Sub-account Asset

> request

```
get /api/v3/sub-account/asset?subAccount=account1&accountType=SPOT&timestamp={{timestamp}}&signature={{signature}}
```
> response

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

- **GET** ```/api/v3/sub-account/asset```  

**Permission:** SPOT_TRANSFER_READ

**Weight(IP):** 1

**request**

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
| subAccount | string | Yes       | subAccount name,only support query for single subaccount|
| accountType|string|Yes|account type:"SPOT","FUTURES",only support SPOT currently|
| timestamp|string|Yes|timestamp|
| signature|string|Yes|signature|


**response**

| Name  |Type | Description|
| :------------ | :-------- | :--------|
|balances|string|balance|
|asset|string|asset|
|free|string|free|
|locked|string|locked|




<!-- ## Enable Futures for Sub-account (For Master Account)

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

**Permission:** SPOT_ACCOUNT_READ

**Weight(IP):** 1

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
|timestamp|string|response time| -->

<!-- ## Enable Margin for Sub-account (For Master Account)

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

**Permission:** SPOT_ACCOUNT_READ

**Weight(IP):** 1

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

 -->

# Spot Account/Trade

## User API default symbol

> Request

```
GET /api/v3/selfSymbols?timestamp={{timestamp}}&signature={{signature}}
```

> Response

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


- **GET** ```/api/v3/selfSymbols ```

**Permission:**  SPOT_ACCOUNT_R

**Weight(IP):** 1

**Request**

NONE

**Response**

| Name       | Type | Description                       |
| :------------ | :-------- |:-------------------------|
| symbol | string | api trade symbol      |



## Test New Order

> Response

```json
{}
```

- **POST** ```/api/v3/order/test```  

**Permission:** SPOT_DEAL_WRITE

**Weight(IP):** 1

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

**Permission:** SPOT_DEAL_WRITE

**Weight(IP):** 1, **Weight(UID):** 1

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

Supports 20 orders with a same symbol in a batch,rate limit:2 times/s.

> Request

```
POST /api/v3/batchOrders?batchOrders=[{"type": "LIMIT_ORDER","price": "40000","quantity": "0.0002","symbol": "BTCUSDT","side": "BUY","newClientOrderId": 9588234},{"type": "LIMIT_ORDER","price": "4005","quantity": "0.0003","symbol": "BTCUSDT","side": "SELL"}]
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

**Permission:** SPOT_DEAL_WRITE

**Weight(IP):** 1,**Weight(UID):** 1

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

**Permission:** SPOT_DEAL_WRITE

**Weight(IP):** 1

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

**Permission:** SPOT_DEAL_WRITE

**Weight(IP):** 1

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

**Permission:** SPOT_DEAL_READ

**Weight(IP):** 2

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

**Permission:** SPOT_DEAL_READ

**Weight(IP):** 3

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

**Permission:** SPOT_DEAL_READ

**Weight(IP):** 10

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

**Permission:** SPOT_ACCOUNT_READ

**Weight(IP):** 10

Get current account information,rate limit:2 times/s.

Parameters:

| Name       | Type | Mandatory | Description |
| ---------- | ---- | --------- | ----------- |
| recvWindow | long | NO        |             |
| timestamp  | long | YES       |             |


Response:

| Name             | Description     |
| ---------------- | --------------- |
| canTrade         | Can Trade       |
| canWithdraw      | Can Withdraw    |
| canDeposit       | Can Deposit     |
| updateTime       | Update Time     |
| accountType      | Account type    |
| balances         | Balance         |
| asset            | Asset coin      |
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

**Permission:** SPOT_ACCOUNT_READ

**Weight(IP):** 10

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


- **POST** ```api/v3/mxDeduct/enable```  

**Permission:** SPOT_DEAL_WRITE

**Weight(IP):** 1

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

<aside class="notice">For Futures:Enjoy 10% off trading fees when you transfer MX into your futures account.</aside>


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

- **GET** ```api/v3/mxDeduct/enable```  

**Permission:** SPOT_DEAL_READ

**Weight(IP):** 1

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

**Permission:** SPOT_WITHDRAW_READ

**Weight(IP):** 10

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

**Permission:** SPOT_WITHDRAW_WRITE

**Weight(IP):** 1

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
 
Can get `network` via endpoints `Get /api/v3/capital/config/getall`'s response params `networkList`.

Response:

| Name | Description  |
| :------------ | :-------- | 
|id|withdraw ID|

## Cancel withdraw

> Request

```
delete /api/v3/capital/withdraw?id=ca7bd51895134fb5bd749f1cf875b8af&timestamp={{timestamp}}&signature={{signature}}
```
> Response

```json
{
    "id": "ca7bd51895134fb5bd749f1cf875b8af"
}
```


- **DELETE** ```/api/v3/capital/withdraw```  

**Permission:** SPOT_WITHDRAW_W

**Weight(IP):** 1

**Request**

| Name | Type| Mandatory | Description               | 
| :------ | :-------- |:-----|:-----------------|
|id|string| Yes    | withdraw id              |

**Response**

| Name | Description  |
| :------------ | :-------- | 
|id|withdraw id|

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

**Permission:** SPOT_WITHDRAW_READ

**Weight(IP):** 1

Parameters: 

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
|coin|string|NO|coin |
|status|string|NO|status|
|startTime|string|NO|default: 7 days ago from current time|
|endTime|string|NO|default:current time|
|limit|string|NO|default:1000,max:1000|
|timestamp|string|YES|timestamp|
|signature|string|YES|signature|

1. default return the records of the last 7 days.
2. Ensure that the default timestamp of 'startTime' and 'endTime' does not exceed 7 days.
3. can query 90 days data at most.

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
        "memo": "MX10086",
        "transHash": "0x0ced593b8b5adc9f600334d0d7335456a7ed772ea5547beda7ffc4f33a065c",
        "updateTime": 1712134082000,
        "coinId": "128f589271cb495b03e71e6323eb7be",
        "vcoinId": "af42c6414b9a46c8869ce30fd51660f"
  }
]
```


- **GET** ```/api/v3/capital/withdraw/history```  

**Permission:** SPOT_WITHDRAW_READ

**Weight(IP):** 1

Parameters: 

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
|coin|string|NO|coin |
|status|string|NO|withdraw status|
|limit|string|NO|default:1000, max:1000|
|startTime|string|NO|default: 7 days ago from current time|
|endTime|string|NO|default:current time|
|timestamp|string|YES|timestamp|
|signature|string|YES|signature|

1. default return the records of the last 7 days.
2. Ensure that the default timestamp of 'startTime' and 'endTime' does not exceed 7 days.
3. can query 90 days data at most.
4. Supported multiple network coins's withdraw history may not return the 'network' field.



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
|memo|memo|
|transHash|transaction Hash|
|coinId|asset id|
|vcoinId|currency id|


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

**Permission:** SPOT_WITHDRAW_WRITE

**Weight(IP):** 1

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

**Permission:** SPOT_WITHDRAW_READ

**Weight(IP):** 10

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

## Withdraw Address (supporting network)

> Request

```
get /api/v3/capital/withdraw/address?coin=USDT&timestamp={{timestamp}}&signature={{signature}}
```
> Response

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


- **GET** ```/api/v3/capital/withdraw/address```  

**Permission:**  SPOT_WITHDRAW_R

**Weight(IP):** 10

**Request**

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
|coin|string|No|coin|
|page|number|No|page,default 1|
|limit|number|No|limit for per page|
|timestamp|string|Yes|timestamp|
|signature|string|Yes|signature|

**Response**

| Name | Description  |
| :------------ | :-------- |
|coin|coin|
|network|network|
|address|address|
|addressTag|addressTag|
|memo|memo|
|totalRecords|totalRecords|
|totalPageNum|totalPageNum|
|page|page|

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

**Permission:** SPOT_TRANSFER_WRITE

**Weight(IP):** 1

Parameters: 

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
|fromAccountType|string|YES|fromAccountType:"SPOT","FUTURES"|
|toAccountType|string|YES|toAccountType:"SPOT","FUTURES"|
|asset|string|YES|asset|
|amount|string|YES|amount|
|timestamp|string|YES|timestamp|
|signature|string|YES|signature|


Response:

| Name | Description  |
| :------------ | :-------- | 
|tranId|tranId|

## Query User Universal Transfer History 

> Request

```
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

**Permission:** SPOT_TRANSFER_READ

**Weight(IP):** 1

Parameters: 

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
|fromAccountType|string|YES|fromAccountType:"SPOT","FUTURES"|
|toAccountType|string|YES|toAccountType:"SPOT","FUTURES"|
|startTime|string|NO|startTime|
|endTime|string|NO|endTime|
|page|string|NO|default:1|
|size|string|NO|default:10, max:100|
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

## Query User Universal Transfer History （by tranId）

> Request

```
get /api/v3/capital/transfer/tranId?tranId=cb28c88cd20c42819e4d5148d5fb5742&timestamp={{timestamp}}&signature={{signature}}
```

> Response

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

- **GET** ```/api/v3/capital/transfer/tranId```  

**Permission:**  SPOT_TRANSFER_R

**Weight(IP):** 1

**request**

| Name    | Type | Mandatory | Description   |
| :-------- | :------- | :------- | :----- |
| tranId    | string   | YES       | tranId  |
| timestamp | string   | YES       | timestamp |
| signature | string   | YES       | signature   |

Only can quary the data for the last six months

**response**

| Name          | Description         |
| :-------------- | :----------- |
|tranId|tranId|
|clientTranId|client ID|
|asset|coin |
|amount|amount|
|fromAccountType|fromAccountType|
|toAccountType|toAccountType|
|symbol|symbol|
|status|status|
|timestamp|timestamp|


## Get Assets That Can Be Converted Into MX

> Request

```
get {{api_url}}/api/v3/capital/convert/list?timestamp={{timestamp}}&signature={{signature}}
```
> Response

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


- **GET** ```/api/v3/capital/convert/list```  

**Permission:** SPOT_ACCOUNT_READ

**Weight(IP):** 1

Parameters:
  
| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
|timestamp|string|YES|timestamp|
|signature|string|YES|signature|

Response:

| Name | Description  |
| :------------ | :-------- | 
| convertMx|MX amount（Deducted commission fee）|
| convertUsdt | usdt amount     |
| balance|Convertible balance|
| asset|asset|
| code    | code     |
| message | message  |

## Dust Transfer

> Request

```
post {{api_url}}/api/v3/capital/convert?asset=BTC,FIL,ETH&timestamp={{timestamp}}&signature={{signature}}
```
> Response

```json
{
  "successList":["ALGO","OMG"],
  "failedList":[],
  "totalConvert":"0.07085578",
  "convertFee":"0.00071571"
  }
```

- **POST** ```/api/v3/capital/convert```  

**Permission:** SPOT_ACCOUNT_W

**Weight(IP):** 10

Parameters:
  
| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
|asset|string|YES|The asset being converted.(max 15 assert)eg:asset=BTC,FIL,ETH|
|timestamp|string|YES|timestamp|
|signature|string|YES|signature|

Response:

| Name | Description  |
| :------------ | :-------- | 
|totalConvert|Convert MX amount(Deducted commission fee)|
| convertFee  | convertFee     |
| successList | convert success List |
| failedList  | convert failed List |
| -asset     | asset         |
| -message   | message  |
| -code      | code   |

## DustLog

> Request

```
get {{api_url}}/api/v3/capital/convert?timestamp={{timestamp}}&signature={{signature}}
```
> Response

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


- **GET** ```/api/v3/capital/convert```  

**Permission:** SPOT_DEAL_READ

**Weight(IP):** 1

Parameters:
  
| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
|startTime|long|NO|startTime|
|endTime|long|NO|endTime|
|page|int|NO|page,default 1|
|limit|int|NO|limit,default 1; max 1000|
|timestamp|string|YES|timestamp|
|signature|string|YES|signature|

Response:

| Name |  Type|Description  |
| :------------ | :-------- | :-------- |
|totalConvert|string|Convert MX amount(Deducted commission fee)|
|totalFee|string|Total fee amount|
|convertTime|long|Convert time|
|convertDetails|object|Convert details|
|id|string|Convert id|
|convert|string|Convert mx|
|fee|string|fee amount|
|amount|string|amount|
|time|long|Convert time|
|asset|string|asset|
|page|int|page|
|totalRecords|int|totalRecords|
|totalPage|int|totalPage|

<!-- ## Internal Transfer

> Request

```
post /api/v3/capital/transfer/internal?&timestamp={{timestamp}}&signature={{signature}}
```
> Response

```json
  {
    "tranId": "c45d800a47ba4cbc876a5cd29388319"
  }

```

- **POST** ```/api/v3/capital/transfer/internal```  

**Permission:** SPOT_WITHDRAW_WRITE

**Weight(IP):** 1

**Parameters**

| Name | Type| Mandatory | Description               | 
| :------ | :-------- |:-----|:-----------------|
|toAccountType|string| Yes    | toAccountTyp:EMAIL/UID/MOBILE  |
|toAccount|string| Yes    | toAccount:EMAIL/UID/MOBILE   |
|areaCode|string| No    | areaCode of mobile            |
|asset|string| Yes    | asset        |
|amount|string| Yes    | amount       |
|timestamp|string| Yes    | timestamp        |
|signature|string| Yes    | signature      |

**Response**

| Name | Description  |
| :------------ | :-------- | 
|tranId|tranId|
 -->

## Query Internal Transfer history

> Request

```
get /api/v3/capital/transfer/internal?&timestamp={{timestamp}}&signature={{signature}}
```
> Response

```json
  {
    "page": 1,  
    "totalRecords": 1,  
    "totalPageNum": 1,  
    "data": [
             {
      "tranId":"11945860693",
      "asset":"BTC",
      "amount":"0.1",
      "toAccountType":"EMAIL",
      "toAccount":"156283619@outlook.com",
      "fromAccount":"156283618@outlook.com",
      "status":"SUCCESS",
      "timestamp":1544433325000
    },
    {
      "tranId":"",
      "asset":"BTC",
      "amount":"0.8",
      "toAccountType":"UID",
      "fromAccount":"156283619@outlook.com",
      "toAccount":"87658765",
      "status":"SUCCESS",
      "timestamp":1544433325000
    }
    ]
}

```

- **GET** ``` /api/v3/capital/transfer/internal```  

**Permission:** SPOT_WITHDRAW_READ

**Weight(IP):** 1

**Parameters**

|Name	|Type	|Mandatory	|Description|
| :------ | :-------- |:-----|:-----------------|
|startTime|	long|	No	|
|endTime|	long|	No	|
|page	|int|	No|	default 1|
|limit|	int	|No|	default 10|
|tranId|	string|	No	|tranid|
|timestamp|	string|	Yes|	timestamp|
|signature|	string|	Yes|	signature|

If startTime and endTime are not provided, will default to returning data from the last 7 days.


**Response**

| Name | Description  |
| :------------ | :-------- | 
|page	|page|
|totalRecords	|totalRecords|
|totalPage	|totalPage|
|tranId	|tranId|
|asset	|asset|
|amount	|amount|
|fromAccountType	|fromAccountType|
|toAccountType	|toAccountType|
|status	|status|
|timestamp	|timestamp|

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
  "basket": 24678.0916
}

```

- **GET** ```api/v3/etf/info```

**Weight(IP):** 1

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
|basket     |string  | Basket After  |

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

## Partial Book Depth Streams
Top bids and asks, Valid are 5, 10, or 20.

>**request:**

```
{
    "method": "SUBSCRIPTION",
    "params": [
                "spot@public.limit.depth.v3.api@BTCUSDT@5"

   ]
}
```

> **response:**

```

{
  "c":"spot@public.limit.depth.v3.api@BTCUSDT@5",  
  "d":{
    "asks":[{                 
            "p":"20290.89",   
            "v":"0.650000"}], 
    "e":"spot@public.limit.depth.v3.api",  
    "r":"3407459756"},  
  "s":"BTCUSDT",             
  "t":1661932660144          
}
```


**Request:** `spot@public.limit.depth.v3.api@<symbol>@<level>`

**Response:**

| Name      | Type   | Description |
| :-------- | :----- | :--- |
| p | string | price |
| v | string | quantity |
| e | string | eventType |
| r | string | version |
| s | string | symbol |
| t | long | eventTime |

## Individual Symbol Book Ticker Streams
Pushes any update to the best bid or ask's price or quantity in real-time for a specified symbol.

> **request:**

```
{
    "method": "SUBSCRIPTION",
    "params": [
                "spot@public.bookTicker.v3.api@BTCUSDT"
      ]
}
```

> **response:**

```

{
 "c":"spot@public.bookTicker.v3.api@<BTCUSDT>",
 "d":{
    
    "A":"40.66000000" 
    "B":"31.21000000",  
    "a":"25.36520000",
    "b":"25.35190000",},  
 "s":"BTCUSDT", 
 "t":1661932660144 
}
```


**Request:** `spot@public.bookTicker.v3.api@<symbol>`

**Response:**

| Name      | Type   | Description |
| :-------- | :----- | :--- |
| A | string | best ask qty |
| B | string | best bid qty |
| a | string | best ask price |
| b | string | best bid price |
| s | string | symbol |
| t | long | eventTime |

## MiniTicker

>**request:**

```
{
    "method": "SUBSCRIPTION",
    "params": [
        "spot@public.miniTicker.v3.api@BTCUSDT@UTC+8"
    ]
}
```
> **response:**

```
{
  "d":
   {"s":"BTCUSDT",
    "p":"36474.74",
    "r":"0.0354",
    "tr":"0.0354",
    "h":"36549.72",
    "l":"35101.68",
    "v":"375173478.65",
    "q":"10557.72895",
    "lastRT":"-1",
    "MT":"0",
    "NV":"--",
    "t":"1699502456050"},
  "c":"spot@public.miniTicker.v3.api@BTCUSDT@UTC+8",
  "t":1699502456051,
  "s":"BTCUSDT"
}								         
```

**Request:**   `spot@public.miniTicker.v3.api@<symbol>@<timezone>`


**Response:**

| Name     | Type   | Description |
| :-------- | :----- | :--- |
| c	| string	| channel name| 
| d	| data| data| 
| >s	| string	|symbol|
| >p	| string	|deal price|
| >r	| string	|price Change Percent in utc8|
| >tr	| string	|price Change Percent in time zone|
| >h	| string	|24h high price |
| >l	| string	|24h low price |
| >v	| string	|24h volume|
| >q	| string	|24h quote Volume|
| >lastRT	| string	|etf Last Rebase Time|
| >MT	| string	|etf Merge Times|
| >NV	| string	|etf Net Value|


## MiniTickers

>**request:**

```
{
    "method": "SUBSCRIPTION",
    "params": [
        "spot@public.miniTickers.v3.api@UTC+8"
    ]
}
```
> **response:**

```
{
  "d":
  [{"s":"SENSOUSDT",
    "p":"0.07642",
    "r":"-0.0383",
    "tr":"-0.0383",
    "h":"0.08032",
    "l":"0.07463",
    "v":"25052.6533",
    "q":"323777.17",
    "lastRT":"-1",
    "MT":"0",
    "NV":"--"},
   {"s":"BTCUSDT",
    "p":"36474.74",
    "r":"0.0354",
    "tr":"0.0354",
    "h":"36549.72",
    "l":"35101.68",
    "v":"375173478.65",
    "q":"10557.72895",
    "lastRT":"-1",
    "MT":"0",
    "NV":"--"},
  "c":"spot@public.miniTickers.v3.api@UTC+8",
  "t":1699502456051,
}								         
```

**Request:**   `spot@public.miniTickers.v3.api@<timezone>`


**Response:**

| Name     | Type   | Description |
| :-------- | :----- | :--- |
| c	| string	| channel name| 
| d	| data| data| 
| >s	| string	|symbol|
| >p	| string	|deal price|
| >r	| string	|24h price Change Percent in utc8|
| >tr	| string	|24h price Change Percent in time zone|
| >h	| string	|24h high price |
| >l	| string	|24h low price |
| >v	| string	|24h volume|
| >q	| string	|24h quote Volume|
| >lastRT	| string	|etf Last Rebase Time|
| >MT	| string	|etf Merge Times|
| >NV	| string	|etf Net Value|



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

- websocket baseurl: **wss://wbs.mexc.com/ws**

- User Data Streams are accessed at **/ws?listenKey=listenKey** <br/>eg:**wss://wbs.mexc.com/ws?listenKey=pqia91ma19a5s61cv6a81va65sd099v8a65a1a5s61cv6a81va65sdf19v8a65a1**

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

**Permission:**  SPOT_ACCOUNT_R

**HTTP**

- **POST**  ` /api/v3/userDataStream`

Start a new user data stream. The stream will close after 60 minutes unless a keepalive is sent. 

**request:**

NONE

### Query all ListenKey

> **Response**

```
{
    "listenKey": [
        "c285bc363cfeac6646576b801a2ed1f9523310fcda9e927e509aaaaaaaaaaaaaa",
        "87cb8da0fb150e36c232c2c060bc3848693312008caf3acae73bbbbbbbbbbbb",
        "dc027517ebee2328b75268461a9df4d21addfac6ebebab8f5a6cccccccccccccc"
    ]
}
```

**Permission:**  SPOT_ACCOUNT_R

**HTTP**

- **GET**  ` /api/v3/userDataStream`

get all valid listenKey

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


## Spot Account Upadte  

The server will push an update of the account assets when the account balance changes.  

>**request:**

```
{
    "method": "SUBSCRIPTION",
    "params": [
    "spot@private.account.v3.api"
    ]
}
```

> **response:**

```
{
    "c": "spot@private.account.v3.api",
    "d": {
        "a": "USDT",
        "c": 1678185928428,
        "f": "302.185113007893322435",
        "fd": "-4.990689704",
        "l": "4.990689704",
        "ld": "4.990689704",
        "o": "ENTRUST_PLACE"
    },
    "t": 1678185928435
}
```

**Request:** `spot@private.account.v3.api`

**Response:**

| Name      | Type   | Description |
| :-------- | :----- | :--- |
| d | json | account updates |
| > a | string | asset |
| > c | long | change time |
| > f | string | free balance |
| > fd | string | free changed amount |
| > l | string | frozen amount |
| > ld | string | frozen changed amount|
| > o | string | <a href="#account_position">changed type</a>|
| t | long | eventTime |



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
        "p": "1.804",
        "v": "0.31",
        "a": "0.55924",
        "S": 1,
        "T": 1678901086198,
        "t": "5bbb6ad8b4474570b155610e30d960cd",
        "c": "",
        "i": "2dd9655f9fa2438fa1709510d7c1afd9",
        "m": 0,
        "st": 0,
        "n": "0.000248206380027431",
        "N": "MX"
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
| > a | string | deals amount |
| > n | string | commission fee|
| > N | string | commissionAsset）|
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
        "T":1,
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

**Permission:** SPOT_ACCOUNT_READ

**Weight(IP):** 1

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
             "type": "spot", 
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

**Permission:** SPOT_ACCOUNT_READ

**Weight(IP):** 1

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
|type|string|rebate type: spot futures |
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
            "type": "spot", 
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

**Permission:** SPOT_ACCOUNT_READ

**Weight(IP):** 1

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
|type|string|rebate type: spot futures |
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

**Permission:** SPOT_ACCOUNT_READ

**Weight(IP):** 1

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


## Get Affiliate Commission Record (affiliate only)

> request

```
get /api/v3/rebate/affiliate/commission?timestamp={{timestamp}}&signature={{signature}}
```
> response

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
**HTTP Request**

- **GET** ```/api/v3/rebate/affiliate/commission```  

**Permission:** SPOT_ACCOUNT_READ

**Weight(IP):** 1

**Request**

| Name | Type | Mandatory  | Description  | 
| :------ | :-------- | :-------- | :---------- |
| startTime  | long    | No       | startTime |
| endTime    | long    | No       | endTime  |
| inviteCode | string  | No       | invite Code  |
| page       | int     | No       | page   |
| pageSize   | int     | No       | pageSize，default:10|
| timestamp  | long    | Yes       | timestamp   |
| signature  | string  | Yes       | signature  |


**Response**

| Name  | Type | Description |
| :------------ | :-------- | :--------|
| uid |string| user uid|
| account |string|account|
| inviteCode |string|inviteCode|
| inviteTime |long|inviteTime|
| spot |string|spot commission(usdt)|
| etf |string|ETF commission(usdt) |
| futures |string|futures commission(usdt) |
| total |string| total commission(usdt) |
| deposit |string|deposit amount(usdt)|
| firstDepositTime |string|first Deposit Time|

If startTime and endTime are not sent, default return the data of the last six months .


## Get Affiliate Withdraw Record (affiliate only)

> request

```
get /api/v3/rebate/affiliate/withdraw?timestamp={{timestamp}}&signature={{signature}}
```
> response

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
**HTTP Request**

- **GET** ```/api/v3/rebate/affiliate/withdraw```  

**Permission:** SPOT_ACCOUNT_READ

**Weight(IP):** 1

**Request**

| Name | Type| Mandatory  | Description  | 
| :------ | :-------- | :-------- | :---------- |
| startTime  | long    | No       | startTime |
| endTime    | long    | No       | endTime  |
| page       | int     | No       | page  |
| pageSize   | int     | No       | pageSize,default: 10  |
| timestamp  | long    | Yes       | timestamp   |
| signature  | string  | Yes       |  signature  |


**Response**

| Name  |Type | Description |
| :------------ | :-------- | :--------|
| withdrawTime |long|withdrawTime|
| asset |string|withdraw asset|
| amount |string|withdraw amount|

If startTime and endTime are not sent, the data of the last six months is returned.

## Get Affiliate Commission Detail Record (affiliate only)

> request

```
get /api/v3/rebate/affiliate/commission/detail?timestamp={{timestamp}}&signature={{signature}}
```
> response

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
**HTTP Request**

- **GET** ```/api/v3/rebate/affiliate/commission/detail```  

**Permission:** SPOT_ACCOUNT_READ

**Weight(IP):** 1

**Request**

| Name | Type| Mandatory  | Description  | 
| :------ | :-------- | :-------- | :---------- |
| startTime  | long    | No       | startTime |
| endTime    | long    | No       | endTime |
| inviteCode | string  | No       | inviteCode   |
| page       | int     | No       | page  |
| pageSize   | int     | No       | pageSize,default: 10  |
| type       | int     | No       | commission type,1:spot,2:futures,3:ETF  |
| timestamp  | long    | Yes       | timestamp   |
| signature  | string  | Yes       |  signature  |


**Response**

| Name  |Type | Description |
| :------------ | :-------- | :--------|
| totalCommissionUsdtAmount| string|total commission in usdt|
| totalTradeUsdtAmount|string|total trade volume in usdt |
| type|int| commission type,1:spot 2:futures 3:ETF|
| sourceType|int|sourceType,1:referral 2:sub-affiliate|
| state|int|commission state|
| date|long|trade date|
| uid |string|uid|
| rate|string|commission rate|
| symbol|string|symbol|
| takerAmount|string|taker amount|
| makerAmount|string|maker amount|
| amountCurrency|string|amount currency|
| usdtAmount|string|usdt amount|
| commission|string|commission amount|
| currency|string|commission currency|




If startTime and endTime are not sent, the data from T-7 to T is returned. If type is not sent, the data of all types is returned,maximum 30 days data can be queried at one time.

<!-- ## Get Affiliate Campaign Data (affiliate only)

> request

```
get /api/v3/rebate/affiliate/campaign?timestamp={{timestamp}}&signature={{signature}}
```
> response

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
**HTTP Request**

- **GET** ```/api/v3/rebate/affiliate/campaign```  

**Permission:** SPOT_ACCOUNT_READ

**Weight(IP):** 1

**Request**

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
| startTime  | long    | No       | startTime |
| endTime    | long    | No       | endTime  |
| page       | int     | No       | page |
| pageSize   | int     | No       | pageSize,default: 10  |
| timestamp  | long    | Yes       | timestamp   |
| signature  | string  | Yes       |  signature |

**Response**

| Name  |Type | Description|
| :------------ | :-------- | :--------|
| campaign|string|campaign name|
| inviteCode|string|campaign inviteCode|
| createTime|long|campaign createTime|
| clickTime|int|inviteCode clickTime|
| signup|int|signup number|
| deposited|int|deposited number|
| depositAmount|string|depositAmount(usdt)|
| tradingAmount|string|tradingAmount(usdt)|
| traded|int|traded number|
| commission|string|commission|


If startTime and endTime are not sent, the data from T-7 to T is returned. -->

## Get Affiliate Referral Data（affiliate only）

> request

```
get /api/v3/rebate/affiliate/referral?timestamp={{timestamp}}&signature={{signature}}
```
> response

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
**HTTP Request**

- **GET** ```/api/v3/rebate/affiliate/referral```  

**Permission:** SPOT_ACCOUNT_READ

**Weight(IP):** 1

**Request**

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
| startTime  | long    | No       | startTime  |
| endTime    | long    | No       | endTime   |
| uid        |  string | No       | uid|
| inviteCode |  string | No       | invite code|
| page       | int     | No       | page  |
| pageSize   | int     | No       | pageSize,default: 10  |
| timestamp  | long    | Yes       | timestamp    |
| signature  | string  | Yes       |  signature  |


**Response**

| Name  | Type | Description|
| :------------ | :-------- | :--------|
| uid | int | uid |
| account | string | account email|
| inviteCode | string | invite code |
| inviteTime | long | invite time |
| nickName | string | nickName  |
| firstDeposit | long | first deposit date|
| firstTrade | long | first trade date|
| lastDeposit | long | last deposit date|
| lastTrade | long | last trade date|
| depositAmount | string | deposit amount(USDT) |
| tradingAmount | string | trading amount(USDT) |
| amount | string | commission amount(USDT) |
| asset | string |  0 USDT、1-1,000 USDT、1,000 - 10,000 USDT、 10,000 - 50,000 USDT、50,000 - 100,000 USDT、 100,000 - 500,000 USDT、500,000 - 1,000,000 USDT、 1,000,000 - 5,000,000 USDT、>5,000,000 USDT |
| withdrawalAmount | string | withdrawal amount(USDT) |
| identification | int | identification,1: Uncertified, 2: primary, 3: Advanced, 4: Institutional |

If startTime and endTime are not sent, the data from T-7 to T is returned.

## Get Subaffiliates Data (affiliate only)

> request

```
get /api/v3/rebate/affiliate/subaffiliates?timestamp={{timestamp}}&signature={{signature}}
```
> response

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
**HTTP Request**

- **GET** ```/api/v3/rebate/affiliate/subaffiliates```  

**Permission:** SPOT_ACCOUNT_READ

**Weight(IP):** 1

**Request**

| Name | Type| Mandatory  | Description | 
| :------ | :-------- | :-------- | :---------- |
| startTime  | long    | No       | startTime |
| endTime    | long    | No       |  endTime  |
| inviteCode | string  | No       | inviteCode|
| page       | int     | No       | page  |
| pageSize   | int     | No       | pageSize,default: 10  |
| timestamp  | long    | Yes       | timestamp |
| signature  | string  | Yes       | signature |


**Response**

| Name  | Type | Description|
| :------------ | :-------- | :--------|
| subaffiliateName|string|subaffiliate name|
| subaffiliateMail|string|subaffiliate mail|
| campaign|string|campaign |
| inviteCode|string|inviteCode|
| activationTime|long|activation time|
| registered|int|registered number|
| deposited|int|deposited number|
| depositAmount|string|deposit amount|
| commission|string|commission |

If startTime and endTime are not sent, the data from T-7 to T is returned.




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
- 1W  1 week
- 1M  1 month

### <a id="account_position">changed type</a>

- WITHDRAW  withdraw
- WITHDRAW_FEE withdraw fee
- DEPOSIT deposit
- DEPOSIT_FEE deposit fee
- ENTRUST deal
- ENTRUST_PLACE place order
- ENTRUST_CANCEL cancel order
- TRADE_FEE trade fee
- ENTRUST_UNFROZEN return frozen order funds
- SUGAR airdrop
- ETF_INDEX ETF place order