# DSP API
todo links

* [Overview](#overview)
* [Profile](#profile-api)
  * [Company DSP endpoints](#company-dsp-endpoints) 
  * [DSP endpoint details](#dsp-endpoint-details)
  * Add item to block list
  * [DSP campaigns target](#dsp-campaigns-target)
  * [Add DSP campaign target](#add-dsp-campaign-target)
  * [Delete DSP campaign target](#delete-dsp-campaign-target)
  * [Change DSP endpoint URL](#change-dsp-endpoint-url)
* [Financial](#financial-api)
* [Detailed](#detailed-reports-api)
  * [ampaign report](#campaign-report)
  * [Creative report](#creative-report)
  * [Domain list](#domain-list)
  * [Bundle list](#bundle-list)
  * [Specific domain report](#specific-domain-report)
  * [Specific bundle report](#specific-bundle-report)
  * [OS report](#os-report)
  * [Geo report](#geo-report)
  * [Users report](#user-report)
  * [Custom report](#custom-report)

## Overview
todo description

## Profile API

### Company DSP endpoints 
`GET` /dsp

Response:

```json
{
  "data": {
    "name": "Demo company",
    "endpoints": [{
      "id": 21,
      "name": "Demo banner"
    }, {
      "id": 22,
      "name": "Demo native"
    }, {
      "id": 23,
      "name": "Demo video"
    }]
  }
}
```

### DSP endpoint details
`GET` /dsp/`:id`

Path params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| id           | Int  | Yes        | Specific endpoint id. Example: `/21`

Response:

```json
{
  "data": {
    "id": 21,
    "name": "Demo banner",
    "token": "2330c0eef8d4ee649c8e8b6cefd2d9a3",
    "endpoint": "http://dsp.com/bid",
    "region": "us-east-1",
    "isBanner": 1,
    "isNative": 0,
    "isVideo": 0,
    "isAudio": 0,
    "qpsLimit": 1000,
    "bidQps": 100,
    "sumReq": 123420199321,
    "sumRes": 221342132,
    "sumImp": 200210,
    "manager": {
      "name": "John Doe",
      "email": "john.doe@xendiz.com"
    },
    "blockedPlatforms": [{
      "type": "site",
      "source": "google.com"
    }, {
      "type": "app",
      "source": "com.google"
    }, {
      "type": "publisher",
      "source": "eef8d4ee64"
    }]
  }
}
```

### Add item to block list

`POST` /dsp/`:id`/block

Path params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| id           | Int  | Yes        | Specific endpoint id. Example: `/21`

Body params

| Name         | Type    | isRequired | Description   |
| -------------| ------- | ---------- | ------------- |
| type         | String  | Yes        | One of `app`, `site`, `publisher`
| source       | Object  | No         | App bundle, site domain or Xendiz publisher ID

Request:
```json
[{
  "type": "app",
  "source": "com.test.bundle"
}, {
  "type": "publisher",
  "source": "eef8d4ee64"
}]
```

### DSP campaigns target

`GET` /dsp/`:id`/campaigns

Path params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| id           | Int  | Yes        | Specific endpoint id. Example: `/21`

Response:

```json
{
  "data": [{
    "campaignId": "cid1234",
    "device": {
      "mobile": true,
      "desktop": true,
      "tablet": true
    },
    "platform": {
      "web": true,
      "app": true
    },
    "os": ["android", "ios"],
    "connection": {
      "ethernet": true,
      "wifi": true,
      "cellular": true
    },
    "sizes": [{
      "w": 320,
      "h": 250
    }, {
      "w": 320,
      "h": 50
    }],
    "countries": ["USA", "RUS", "ITA", "GBR"]
  }]
}
```

### Add DSP campaign target

`POST` /dsp/`:id`/campaigns

Path params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| id           | Int  | Yes        | Specific endpoint id. Example: `/21`

Body params

| Name         | Type    | isRequired | Description   |
| -------------| ------- | ---------- | ------------- |
| campaignId   | String  | Yes        | Dsp specific campaign ID. Example: `cid-2234`
| device       | Object  | No         | Device target
| platform     | Object  | No         | Platform target
| os           | Array   | No         | OS target. See suported os list (link).
| countries    | Array   | No         | Country target. Array of ISO 3 country codes.
| connection   | Object  | No         | Connection target. See connection object (link)
| sizes        | Array   | No         | Size target. See size object.

Connection Object

| Name         | Type    | isRequired | Description   |
| -------------| ------- | ---------- | ------------- |
| ethernet     | Bool    | No         | Allow ethernet connection. `true` by default
| wifi         | Bool    | No         | Allow wi-fi connection. `true` by default
| cellular     | Bool    | No         | Allow cellular connection. `true` by default

Size Object

| Name         | Type    | isRequired | Description   |
| -------------| ------- | ---------- | ------------- |
| w            | Int     | Yes        | Width. Example: `320`
| h            | Int     | Yes        | Height. Example: `50`

Request

```json
[{
  "campaignId": "cid1234",
  "device": {
    "mobile": true,
    "desktop": true,
    "tablet": true
  },
  "platform": {
    "web": true,
    "app": true
  },
  "os": ["android", "ios"],
  "connection": {
    "ethernet": true,
    "wifi": true,
    "cellular": true
  },
  "sizes": [{
    "w": 320,
    "h": 250
  }, {
    "w": 320,
    "h": 50
  }],
  "countries": ["USA", "RUS", "ITA", "GBR"]
}]
```

### Delete DSP campaign target

`DELETE` /dsp/`:id`/campaigns/`:target_id`

Path params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| id           | Int  | Yes        | Specific endpoint id. Example: `/21`
| target_id    | Int  | Yes        | Dsp specific campaign ID. Example: `cid-2234`

### Change DSP endpoint URL

`PUT` /dsp/`:id`/endpoint

Path params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| id           | Int  | Yes        | Specific endpoint id. Example: `/21`

Body params

| Name         | Type    | isRequired | Description   |
| -------------| ------- | ---------- | ------------- |
| endpoint     | String  | Yes        | Endoint URL. Example: `http://dsp.com/bid?s=1`

Request:
```json
{
  "endpoint": "http://dsp.com/bid?s=1"
}
```

## Financial API
`GET` /dsp/financial

Query params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| from         | Date | No         | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date | No         | End date. Example: `&to=2018-01-10`
| endpoint_id  | Int  | No         | Specific endpoint id. If the param is not specified, a full report will be created for all the endpoints of the company. Example: `&endpoint_id=21`
| hour         | Bool | No         | Hour aggregated report. Example: `&hour=1`

`GET` /dsp/financial/?from=2018-01-01&to=2018-02-02
Response:

```json
{
  "data": [{
    "date": "2018-01-01",
    "spend": 40.21,
    "impressions": 1293811
  }, {
    "date": "2018-01-02",
    "spend": 60.90,
    "impressions": 1423811
  }]
}
```

`GET` /dsp/financial/?from=2018-01-02&hour=1
Response:

```json
{
    "data": [{
       "hour": "00:00",
       "spend": 2.21,
       "impressions": 2021
    }, {
       "hour": "00:01",
       "spend": 20.90,
       "impressions": 221132
    }, {
       "hour": "00:02",
       "spend": 21.5,
       "impressions": 222191
    }]
}
```

## Detailed reports API

### Campaign report

`GET` /dsp/detailed/cid

Query params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| campaign     | String | Yes        | Campaign ID. Example: `&campaign=cid-12345`
| from         | Date   | No        | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date   | No         | End date. Example: `&to=2018-01-10`
| endpoint_id  | Int    | No         | Specific endpoint id. If the param is not specified, a full report will be created for all the endpoints of the company. Example: `&endpoint_id=21`

Response:

```json
{
  "data": [{
    "date": "2018-01-01",
    "spend": 40.21,
    "impressions": 1293811
  }, {
    "date": "2018-01-02",
    "spend": 60.90,
    "impressions": 1423811
  }]
}
```

### Creative report

`GET` /dsp/detailed/crid

Query params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| creative     | String | Yes        | Creative ID. Example: `&creative=crid-12345`
| from         | Date   | No        | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date   | No         | End date. Example: `&to=2018-01-10`
| endpoint_id  | Int    | No         | Specific endpoint id. If the param is not specified, a full report will be created for all the endpoints of the company. Example: `&endpoint_id=21`

Response:

```json
{
  "data": [{
    "date": "2018-01-01",
    "spend": 40.21,
    "impressions": 1293811
  }, {
    "date": "2018-01-02",
    "spend": 60.90,
    "impressions": 1423811
  }]
}
```

### Domain list 

`GET` /dsp/detailed/domains

Query params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| from         | Date   | No        | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date   | No         | End date. Example: `&to=2018-01-10`
| endpoint_id  | Int    | No         | Specific endpoint id. If the param is not specified, a full report will be created for all the endpoints of the company. Example: `&endpoint_id=21`

Response:

```json
{
  "data": [{
    "date": "2018-01-01",
    "domain": "domain.com",
    "spend": 40.21,
    "impressions": 1293811
  }, {
    "date": "2018-01-01",
    "domain": "domain2.com",
    "spend": 22.21,
    "impressions": 13371337
  }]
}
```

### Bundle list 

`GET` /dsp/detailed/bundles

Query params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| from         | Date   | No        | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date   | No         | End date. Example: `&to=2018-01-10`
| endpoint_id  | Int    | No         | Specific endpoint id. If the param is not specified, a full report will be created for all the endpoints of the company. Example: `&endpoint_id=21`

Response

```json
{
  "data": [{
    "date": "2018-01-01",
    "bundle": "com.test.bundle",
    "name": "Test bundle",
    "spend": 40.21,
    "impressions": 1293811
  }, {
    "date": "2018-01-01",
    "bundle": "com.test.bundle2",
    "name": "Test bundle",
    "spend": 22.21,
    "impressions": 13371337
  }]
}
```

### Specific domain report

`GET` /dsp/detailed/domain/`:domain`

Path params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| domain       | String | Yes        | Domain for which you want to receive the report

Query params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| from         | Date   | No        | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date   | No         | End date. Example: `&to=2018-01-10`
| endpoint_id  | Int    | No         | Specific endpoint id. If the param is not specified, a full report will be created for all the endpoints of the company. Example: `&endpoint_id=21`

```json
{
  "data": [{
    "date": "2018-01-01",
    "spend": 40.21,
    "impressions": 1293811
  }, {
    "date": "2018-01-01",
    "spend": 22.21,
    "impressions": 13371337
  }]
}
```

### Specific bundle report
`GET` /dsp/detailed/bundle/`:bundle`

Path params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| bundle       | String | Yes        | Bundle for which you want to receive the report

Query params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| from         | Date   | No        | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date   | No         | End date. Example: `&to=2018-01-10`
| endpoint_id  | Int    | No         | Specific endpoint id. If the param is not specified, a full report will be created for all the endpoints of the company. Example: `&endpoint_id=21`

```json
{
  "data": [{
    "date": "2018-01-01",
    "spend": 40.21,
    "impressions": 1293811
  }, {
    "date": "2018-01-01",
    "spend": 22.21,
    "impressions": 13371337
  }]
}
```

### OS report

`GET` /dsp/detailed/os

Query params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| from         | Date   | No        | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date   | No         | End date. Example: `&to=2018-01-10`
| endpoint_id  | Int    | No         | Specific endpoint id. If the param is not specified, a full report will be created for all the endpoints of the company. Example: `&endpoint_id=21`

```json
{
  "data": [{
    "date": "2018-01-01",
    "os": "android",
    "spend": 40.21,
    "impressions": 1293811
  }, {
    "date": "2018-01-01",
    "os": "ios",
    "spend": 22.21,
    "impressions": 13371337
  }]
}
```

### Geo report

`GET` /dsp/detailed/geo

Query params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| from         | Date   | No        | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date   | No         | End date. Example: `&to=2018-01-10`
| endpoint_id  | Int    | No         | Specific endpoint id. If the param is not specified, a full report will be created for all the endpoints of the company. Example: `&endpoint_id=21`

```json
{
  "data": [{
    "date": "2018-01-01",
    "country": "USA",
    "spend": 40.21,
    "impressions": 1293811
  }, {
    "date": "2018-01-01",
    "country": "UKR",
    "spend": 22.21,
    "impressions": 13371337
  }]
}
```

### User report

You should intargate cookie sync with Xendiz SSP to use this method

`GET` /dsp/detailed/users

Query params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| from         | Date   | No        | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date   | No         | End date. Example: `&to=2018-01-10`
| endpoint_id  | Int    | No         | Specific endpoint id. If the param is not specified, a full report will be created for all the endpoints of the company. Example: `&endpoint_id=21`

```json
{
  "data": [{
    "date": "2018-01-01",
    "user": "1515751091.001.2e4668d7ba11eacfb7edca41c28ec842",
    "spend": 0.0002,
    "impressions": 12
  }, {
    "date": "2018-01-01",
    "user": "1516281837.001.fc5b8c8c4d0f2f8817ae848660efe971",
    "spend": 0.0001,
    "impressions": 5
  }]
}
```

### Custom report

`POST` /dsp/detailed/custom

Query params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| from         | Date   | No        | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date   | No         | End date. Example: `&to=2018-01-10`
| endpoint_id  | Int    | No         | Specific endpoint id. If the param is not specified, a full report will be created for all the endpoints of the company. Example: `&endpoint_id=21`

Body Params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| adtype       | String | No         | Platfrom type. `app` or `site`
| platform     | Object | No         | Platfrom Object
| device       | Object | No         | Device Object
| select    | Object | No         | Selection Object

Platfrom Object

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| domain       | Bool   | No         | Platfrom domain
| bundle       | Bool   | No         | Platfrom bundle
| name         | Bool   | No         | Platfrom name
| id           | Bool   | No         | Platfrom id

Device Object

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| ip           | Bool   | No         | Device ip
| os           | Bool   | No         | Device os
| type         | Bool   | No         | Device type
| vendor       | Bool   | No         | Device vendor
| ct           | Bool   | No         | Device connection type
| country      | Bool   | No         | Device country

Select

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| date         | Bool   | No         | Date
| size         | Bool   | No         | Size
| campaign     | Bool   | No         | Dsp campaign
| creative     | Bool   | No         | Dsp creative
| category     | Bool   | No         | Content category
| price        | Object | No         |
| price.on     | Bool   | No         | Add cost to selection
| price.value  | String | No         | Aggregate function: `median`, `sum`, `average`

Example request

```json
{
    "adType": "app",
    "platform": {
        "domain": false,
        "bundle": false,
        "name": false,
        "id": false
    },
    "device": {
        "ip": false,
        "os": true,
        "type": false,
        "vendor": false,
        "ct": true,
        "country": false
    },
    "select": {
        "date": false,
        "size": true,
        "campaign": false,
        "creative": false,
        "category": false,
        "price": {
            "on": true,
            "value": "median"
        }
    }
}
```

Response
```json
{
    "fields": [
        "OS",
        "Connection Type",
        "Date",
        "Size",
        "Price",
        "Impressions"
    ],
    "data": [
        [
            "android",
            "WIFI",
            "320x50",
            0.58792,
            "290112"
        ],
        []
    ]
}
```
