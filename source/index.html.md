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
# MEXC Boker 介绍

**MEXC致力于构建加密货币基础设施，提供有价值服务的API 经纪商合作伙伴是MEXC生态系统中的重要参与部分。MEXC推出了MEXC经纪商权益，包括交易返佣和营销支持，以奖励合作伙伴。**

**合作请联系：broker@mexc.com**

## MEXC支持的经纪商模式

**1. API 经纪商：**</br>
包括集跟单平台、交易机器人、量化策略平台或其他500人以上资产管理平台等，用户可以将API key授权给API经纪商，API经纪商代替用户发送含有经济商ID的交易订单，获取手续费分润。

**2. 独立经纪商：**</br>
包括钱包商、行情资讯平台、聚合交易平台、券商和股票证券交易平台等，有自己独立用户，MEXC可以提供订单撮合系统、账户管理系统、结算系统以及母子账户系统等，独立经纪商可共享全站流动性和深度，获得高额手续费分润。

## MEXC提供的经纪商服务内容

**1. API 经纪商：**</br>
用户在MEXC注册账号</br>
用户在MEXC申请API Key并提供给经纪商</br>
经纪商通过Broker ID + 用户API Key下单</br>

   * 支持用户自定义设置可交易币对</br>
   * 支持API Key续签，避免多次绑定
    

**2. 独立经纪商：**</br>
经纪商拥有自主品牌和独立的账户系统</br>
经纪商在MEXC母账号下为用户创建独立子账号进行交易

   * 支持子账号充提
   * 支持子账号划转



## MEXC 经纪商合作模式

**1. API 经纪商：** 

<img src="../images/broker.png">

**2. 独立经纪商：**

<img src="../images/broker-2.png">


# Broker 接口

## 查询母子万向划转历史-broker用户

> 请求示例

```

get  /api/v3/broker/sub-account/universalTransfer

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
  },
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

**HTTP请求：**

- **GET** ```/api/v3/broker/sub-account/universalTransfer```

**权限：现货划转读取**

**请求参数：**

| 参数名 | 数据类型| 是否必须 | 说明 |
| ------ | -------- | -------- | ---------- |
|fromAccount|string|no|转出账户，不填默认母账户|
|toAccount|string|no|转入账户，不填默认母账户|
|fromAccountType|string|yes|<a href="#from_account">划出账户类型</a>|
|toAccountType|string|yes|<a href="#to_account">划入账户类型</a>|
|startTime|string|no|起始时间, 13位|
|endTime|string|no|结束时间, 13位|
|page|string|no|默认 1|
|limit|string|no|默认 500, 最大 500|
|timestamp|string|yes|时间|
|signature|string|yes|签名|

**返回参数：**

| 参数名 | 类型 | 说明 |
| ------ | ---- | ---- |
| tranId |string| 划转ID|
|fromAccount|string|划出账户|
|toAccount|string|划入账户|
| clientTranId |string| client ID|
|asset|string| 币种 |
| amount |string| 划转数量|
| fromAccountType |string|转出账户|
|toAccountType|string|划入账户|
| fromsymbol|string| 转出交易对 |
| tosymbol|string| 转入交易对 |
| status |string|划转状态【成功，失败，划转中，中断】|
| timestamp|number|划转时间|

<!-- ##  查询子账户的once token

> 请求示例

```

get  /api/v3/broker/sub-account/onceToken

```

> 返回示例

```json
{
    "onceToken": "lksod273hsbqi90ljiha"
}

```

**HTTP请求：**

- **GET** ```/api/v3/broker/sub-account/onceToken```

**权限：现货账户读取**

**请求参数：**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| ------ | -------- | -------- | ---------- |
|subAccount|string|yes|子账户名称|
|timestamp|string|yes|时间|
|signature|string|yes|签名|

**返回参数：**

| 参数名 | 类型 | 说明 |
| ------ | ---- | ---- |
|onceToken|string| 子账户onceToken| -->

##  创建子账户

> 请求示例

```

post  /api/v3/broker/sub-account/virtualSubAccount

```

> 返回示例

```json
{
    "code": "0",
    "message": "",
    "data": [{
        "subAccount": "mexc1",
        "note": "1",
        "timestamp": "1597026383085"
    }]
}
```

**HTTP请求：**

- **POST** ```/api/v3/broker/sub-account/virtualSubAccount```

**Query参数：**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| ------ | -------- | -------- | ---------- |
|timestamp|string|yes|时间|
|signature|string|yes|签名|

**Body请求参数：**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| ------ | -------- | -------- | ---------- |
|subAccount|string|yes|子账户名称|
|note|string|yes|备注|
|password|string|yes|资金密码【资金密码要求：MD5加密的16进制字符串过来】|

**返回参数：**

| 参数名 | 类型 | 说明 |
| ------ | ---- | ---- |
|subAccount|string|子账户名称|
|note|string|备注|

##  查看子账户列表

> 请求示例

```

get  /api/v3/broker/sub-account/list

```

> 返回示例

```json
{
    "code": "0",
    "message": "",
    "data": [{
        "isFreeze": true,
        "subAccount": "mexc1",
        "note": "1",
        "timestamp": "1597026383085"
    }, {
        "isFreeze": true,
        "subAccount": "mexc2",
        "note": "2",
        "timestamp": "1597026383787"
    }]
```

**HTTP请求：**

- **GET** ```/api/v3/broker/sub-account/list```

**请求参数：**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| ------ | -------- | -------- | ---------- |
|isFreeze|string|no|子账户状态，true:正常使用 false:冻结|
|subAccount|string|no|子账户名称|
|page|string|no|分页参数：页码。默认: 1|
|limit|string|no|分页参数：页容量。默认: 10, 最大: 200|
|timestamp|string|yes|时间|
|signature|string|yes|签名|

<aside class="notice">【subaccount和isFreeze ，二选一传，都不传时返回所有subaccount的list.】</aside>
<aside class="notice">【subaccount和isFreeze都传，且不匹配，返回空.】</aside>

**返回参数：**

| 参数名 | 类型 | 说明 |
| ------ | ---- | ---- |
|subAccount	|string| 子账户名称|
|isFreeze	|boolean| 是否冻结|
|timestamp	|number| 创建时间|
|note	|string| 备注|

##  创建子账户的APIKey

> 请求示例

```

post  /api/v3/broker/sub-account/apiKey

```

> 返回示例

```json
{
    "subAccount": "4Eb8rPPhpsAL",
    "permissions": "SPOT_ACCOUNT_READ,SPOT_ACCOUNT_WRITE",
    "note": "note2",
    "apikey": "mx0npKfh57kEEVmyLa",
    "secretKey": "51f38875ebe0475dad6236783a95cc19",
    "createTime": 1646291300120
}
```

**HTTP请求：**

- **POST** ```/api/v3/broker/sub-account/apiKey```

**Query参数：**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| ------ | -------- | -------- | ---------- |
|timestamp|string|yes|时间|
|signature|string|yes|签名|

**Body请求参数：**

| 参数名 | 数据类型| 是否必须 | 说明 |
| ------ | -------- | -------- | ---------- |
|subAccount|string|yes|子账户名称|
|permissions|string|yes|<a href="#permissions">权限</a> |
|ip|string|no|ip白名单，多个用逗号隔开，目前最大支持4个IP，可选|
|note|string|yes|备注|

**返回参数：**

| 参数名 | 类型 | 说明 |
| ------ | ---- | ---- |
|subAccount|string|子账户名称|
|note|string|APIKey的备注|
|apikey|string|API公钥|
|secretKey|string|API私钥|
|permissions|string|APIKey权限|
|ip|string|APIKey绑定的ip地址|
|createTime|number|创建时间|

##  查询子账户的APIKey

> 请求示例

```

get  /api/v3/broker/sub-account/apiKey

```

> 返回示例

```json
{
    "subAccount": [{
        "note": "v5",
        "apiKey": "arg13sdfgs",
        "permissions": "SPOT_ACCOUNT_READ,SPOT_ACCOUNT_WRITE",
        "ip": "1.1.1.1,2.2.2.2",
        "creatTime": 1597026383085
    }, {
        "note": "v5.1",
        "apiKey": "arg13sdfgs",
        "permissions": "read_only",
        "ip": "1.1.1.1,2.2.2.2",
        "creatTime": 1597026383085
    }]
}

```

**HTTP请求：**

- **GET** ```/api/v3/broker/sub-account/apiKey```

**请求参数：**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| ------ | -------- | -------- | ---------- |
|subAccount|string|yes|子账户名称|
|timestamp|string|yes|时间|
|signature|string|yes|签名|

**返回参数：**

| 参数名 | 类型 | 说明 |
| ------ | ---- | ---- |
|note|string| 子账户备注|
|apikey|string| API公钥|
|permissions|string|APIKey权限|
|ip|string| APIKey绑定的ip地址|
|creatTime|number| 创建时间|

##  删除子账户的APIKey

> 请求示例

```

delete  /api/v3/broker/sub-account/apiKey

```

> 返回示例

```json
{
    "subAccount": "mexc1"
}
```

**HTTP请求：**

- **DELETE** ```/api/v3/broker/sub-account/apiKey```

**Query参数：**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| ------ | -------- | -------- | ---------- |
|timestamp|string|yes|时间|
|signature|string|yes|签名|

**Body请求参数：**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| ------ | -------- | -------- | ---------- |
|subAccount|string|yes|子账户名称|
|apiKey|string|yes|API公钥|

**返回参数：**

| 参数名 | 类型 | 说明 |
| ------ | ---- | ---- |
|subAccount|string|子账户名称|

##  生成子账户充值地址

> 请求示例

```

post  /api/v3/broker/capital/deposit/subAddress

```

> 返回示例

```json
{
    "address": "TDunhSa7jkTNuKrusUTU1MUHtqXoBPKETV",
    "coin": "USDT",
    "network": "ERC-20",
    "memo": ""
}
```

**HTTP请求：**

- **POST** ```/api/v3/broker/capital/deposit/subAddress```

**权限：现货充值写**

**Query参数：**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| ------ | -------- | -------- | ---------- |
|recvWindow|string|no|同步时间|
|timestamp|string|yes|时间|
|signature|string|yes|签名|

**Body请求参数：**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| ------ | -------- | -------- | ---------- |
|coin|string|yes|充值币种|
|network|string|yes|充值网络|

**返回参数：**

| 参数名 | 类型 | 说明 |
| ------ | ---- | ---- |
|address|string|充值地址|
|coin|string|充值币种|
|network|string|充值网络|
|memo|string|memo值|

##  获取子账户充值地址

> 请求示例

```

get  /api/v3/broker/capital/deposit/subAddress

```

> 返回示例

```json
[{
    "address": "TDunhSa7jkTNuKrusUTU1MUHtqXoBPKETV",
    "coin": "USDT",
    "network": "ERC-20",
    "memo": ""
}, {
    "address": "TDunhSa7jkTNuKrusUTU1MUHtqXoBPKETV",
    "coin": "USDT",
    "network": "TRC-20",
    "memo": ""
}]

```

**HTTP请求：**

- **GET** ```/api/v3/broker/capital/deposit/subAddress```

**权限：现货充值读取**

**请求参数：**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| ------ | -------- | -------- | ---------- |
|coin|string|yes|充值币种|
|recvWindow|string|no|同步时间|
|timestamp|string|yes|时间|
|signature|string|yes|签名|


**返回参数：**

| 参数名 | 类型 | 说明 |
| ------ | ---- | ---- |
|address|string|充值地址|
|coin|string|充值币种|
|network|string|充值网络|
|memo|string|memo值|

<!-- ##  broker 母查所有子的所有充值记录

> 请求示例

```

get  /api/v3/broker/capital/deposit/subHisrec/getall

```

> 返回示例

```json
[
    {
        "amount":"0.00999800",
        "coin":"PAXG",
        "network":"ETH",
        "status":,
        "address":"0x788cabe9236ce061e5a892e1a59395a81fc8d62c",
        "addressTag":"",
        "txId":"0xaad4654a3234aa6118af9b4b335f5ae81c360b2394721c019b5d1e75328b09f3",
        "unlockConfirm":"12", 
        "confirmTimes":"7"
    },
    {
        "amount":"0.50000000",
        "coin":"IOTA",
        "network":"IOTA",
        "status":1,
       "address":"SIZ9VLMHWATXKV99LH99CIGFJFUMLEHGWVZVNNZXRJJVWBPHYWPPBOSDORZ9EQSHCZAMPVAPGFYQAUUV9DROOXJLNW",
        "addressTag":"",
        "txId":"ESBFVQUTPIWQNJSPXFNHNYHSQNTGKRVKPRABQWTAXCDWOAKDKYWPTVG9BGXNVNKTLEJGESAVXIKIZ9999",
         "unlockConfirm":"12", 
         "confirmTimes":"7"
    }
]
```

**HTTP请求：**

- **GET** ```/api/v3/broker/capital/deposit/subHisrec/getall```

**权限：现货充提读取**

**请求参数：**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| ------ | -------- | -------- | ---------- |
|coin|string|no|币种|
|status|string|no|<a href="#status">状态</a> |
|startTime|string|no|开始时间，如果没有传，默认查询10天|
|endTime|string|no|结束时间，如果没有传，取当前时间|
|limit|string|no|默认值20，目前无最大值限制|
|page|string|no|默认值1|
|recvWindow|string|no|同步时间|
|timestamp|string|yes|时间|
|signature|string|yes|签名|

**返回参数：**

| 参数名 | 类型 | 说明 |
| ------ | ---- | ---- |
|amount|string| 充值数量|
|coin|string| 充值币种|
|network|string|充值网络|
|status|number| <a href="#status">状态</a> |
|address|string| 充值地址|
|addressTag|string| 地址标签|
|txId|string| txid|
|unlockConfirm|string|解锁需要的网络确认次数|
|confirmTimes|string| 确认进度| -->

##  获取子账户充值记录

> 请求示例

```

get  /api/v3/broker/capital/deposit/subHisrec

```

> 返回示例

```json
[
    {
        "amount":"0.00999800",
        "coin":"PAXG",
        "network":"ETH",
        "status":,
        "address":"0x788cabe9236ce061e5a892e1a59395a81fc8d62c",
        "addressTag":"",
        "txId":"0xaad4654a3234aa6118af9b4b335f5ae81c360b2394721c019b5d1e75328b09f3",
        "unlockConfirm":"12", 
        "confirmTimes":"7"
    },
    {
        "amount":"0.50000000",
        "coin":"IOTA",
        "network":"IOTA",
        "status":1,
"address":"SIZ9VLMHWATXKV99LH99CIGFJFUMLEHGWVZVNNZXRJJVWBPHYWPPBOSDORZ9EQSHCZAMPVAPGFYQAUUV9DROOXJLNW",
        "addressTag":"",    		"txId":"ESBFVQUTPIWQNJSPXFNHNYHSQNTGKRVKPRABQWTAXCDWOAKDKYWPTVG9BGXNVNKTLEJGESAVXIKIZ9999",
         "unlockConfirm":"12",
         "confirmTimes":"7"
    }
]

```

**HTTP请求：**

- **GET** ```/api/v3/broker/capital/deposit/subHisrec```

**请求参数：**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| ------ | -------- | -------- | ---------- |
|coin|string|no|币种|
|status|string|no|<a href="#status">状态</a> |
|startTime|string|no|开始时间，如果没有传，默认查询10天|
|endTime|string|no|结束时间，如果没有传，取当前时间|
|limit|string|no|默认值20，目前无最大值限制|
|page|string|no|默认值1|
|recvWindow|string|no|同步时间|
|timestamp|string|yes|时间|
|signature|string|yes|签名|

**返回参数：**

| 参数名 | 类型 | 说明 |
| ------ | ---- | ---- |
|amount|string| 充值数量|
|coin|string| 充值币种|
|network|string|充值网络|
|status|number| <a href="#status">状态</a> |
|address|string| 充值地址|
|addressTag|string| 地址标签|
|txId|string| txid|
|unlockConfirm|string|解锁需要的网络确认次数|
|confirmTimes|string| 确认进度|

##  提币
【只支持子账号提币，不支持母提子】

> 请求示例

```

post  /api/v3/broker/capital/withdraw/apply

```

> 返回示例

```json
{
    "id":"7213fea8e94b4a5593d507237e5a555b"
}
```

**HTTP请求：**

- **POST** ```/api/v3/broker/capital/withdraw/apply```

**权限：现货划转读取**

**Query参数：**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| ------ | -------- | -------- | ---------- |
|recvWindow|string|no|同步时间|
|timestamp|string|yes|时间|
|signature|string|yes|签名|

**Body请求参数：**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| ------ | -------- | -------- | ---------- |
|coin|string|yes|提币币种|
|network|string|yes|提币网络|
|address|string|yes|提币地址|
|amount|string|yes|数量|
|password|string|no|资金密码【传此参数不交验提现地址簿】【资金密码要求：MD5加密的16进制字符串过来】|
|remark|string|no|标记|

**返回参数：**

| 参数名 | 类型 | 说明 |
| ------ | ---- | ---- |
|id|string|提币ID|

##  母子用户万向划转
只支持broker账户使用

> 请求示例

```

post  /api/v3/broker/sub-account/universalTransfer

```

> 返回示例

```json
{
    "tranId": "7213fea8e94b4a5593d507237e5a555b"
}
```

**HTTP请求：**

- **POST** ```/api/v3/broker/sub-account/universalTransfer```

**权限：现货划转读取**

**Query参数：**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| ------ | -------- | -------- | ---------- |
|timestamp|string|yes|时间|
|signature|string|yes|签名|

**Body请求参数：**

| 参数名 | 数据类型| 是否必须 | 说明 |
| ------ | -------- | -------- | ---------- |
|fromAccount|string|no|母子账户，可填subAccout账户名，不填默认母账户|
|toAccount|string|no|母子账户，可填subAccout账户名，不填默认母账户|
|fromAccountType|string|yes|<a href="#from_account">划出账户类型</a>|
|toAccountType|string|yes|<a href="#to_account">划入账户类型</a>|
|symbol|string|yes|币对，当fromAccountType为逐仓杠杆（ISOLATED_MARGIN）时必传，eg：ETHUSDT|
|asset|string|yes|划转资产，eg：USDT|
|amount|string|yes|划转数量，eg：1.82938475|

**返回参数：**

| 参数名 | 类型 | 说明 |
| ------ | ---- | ---- |
|tranId|string|划转ID|

##  开通子账户的合约业务

> 请求示例

```

post  /api/v3/broker/sub-account/futures

```

> 返回示例

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

**HTTP请求：**

- **POST** ```/api/v3/broker/sub-account/futures```

**Query参数：**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| ------ | -------- | -------- | ---------- |
|timestamp|string|yes|时间|
|signature|string|yes|签名|

**Body请求参数：**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| ------ | -------- | -------- | ---------- |
|subAccount|string|yes|子账户名称|

**返回参数：**

| 参数名 | 类型 | 说明 |
| ------ | ---- | ---- |
|subAccount|string|子账户名称|
|isFuturesEnabled|boolean|开通合约业务，开通：true|
|timestamp|string|返回时间|

##  开通子账户的杠杆业务

> 请求示例

```

post  /api/v3/broker/sub-account/margin

```

> 返回示例

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

**HTTP请求：**

- **POST** ```/api/v3/broker/sub-account/margin```

**Query参数：**

| 参数名 | 数据类型| 是否必须 | 说明 | 
| ------ | -------- | -------- | ---------- |
|subAccount|string|yes|子账户名称|
|timestamp|string|yes|时间|
|signature|string|yes|签名|

**返回参数：**

| 参数名 | 类型 | 说明 |
| ------ | ---- | ---- |
|subAccount|string|子账户名称|
|isMarginEnabled|boolean|是否开通杠杆业务：true or false|
|timestamp|string|返回时间|
# 公开API参数

## Broker 枚举定义

### <a id="from_account">划出账户类型</a>

- SPOT 现货
- FUTURES 合约
- ISOLATED_MARGIN 杠杆

### <a id="to_account">划入账户类型</a>

- SPOT 现货
- FUTURES 合约
- ISOLATED_MARGIN 杠杆

### <a id="permissions">权限</a>

- SPOT_ACCOUNT_READ 账户读
- SPOT_ACCOUNT_WRITE 账户写
- SPOT_DEAL_READ 现货交易信息读
- SPOT_DEAL_WRITE 现货交易信息写
- ISOLATED_MARGIN_ACCOUNT_READ 杠杆账户信息读
- ISOLATED_MARGIN_ACCOUNT_WRITE 杠杆账户信息写
- ISOLATED_MARGIN_DEAL_READ 杠杆交易信息读
- ISOLATED_MARGIN_DEAL_WRITE 杠杆交易信息写
- CONTRACT_ACCOUNT_READ 合约账户信息读
- CONTRACT_ACCOUNT_WRITE 合约账户信息写
- CONTRACT_DEAL_READ 合约交易信息读
- CONTRACT_DEAL_WRITE 合约交易信息写
- SPOT_WITHDRAW_READ 钱包提现相关读
- SPOT_WITHDRAW_WRITE 钱包提现相关写
- SPOT_TRANSFER_READ 资金划转读
- SPOT_TRANSFER_WRITE 资金划转写
- SPOT_DEPOSIT_READ 现货充值读
- SPOT_DEPOSIT_WRITE 现货充值写

### <a id="status">状态</a>

- SMALL 小额充值，不入账 
- TIME_DELAY 延迟到账币种
- LARGE_DELAY 大额充值，审核中
- PENDING 入账中
- SUCCESS 入账成功
- AUDITING 审核中
- REJECTED 驳回
