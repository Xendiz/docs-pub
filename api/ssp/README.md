# SSP API
* [Overview](#overview)
* [Profile](#profile-api)
  * [Company SSP endpoints](#company-ssp-endpoints)
  * [SSP endpoint details](#ssp-endpoint-details)
  * [Block creative](#block-creative)
  * [Unblock creative](#unblock-creative)
* [Financial](#financial-api)
* [Custom report](#custom-report)

## Overview
This section of describes API routes for supply-side platforms.

### This part of API is divided into 3 general sections:
- Profile-based data
- Financial report generation
- Custom report generation

### First section is used for work with your endpoints
- First method of this section helps you to see all of your company's endpoints
- Second method is used when you need more detailed information for specific endpoint
- Last two methods are used to block and unblock your creative campaign, while latter method only requires your SSP id and Creative id, former also is able to recieve reason for your campaign blockage though it's optional

### Second section is used when you want to get financial report of your company
It's only method recieves up to 4 parameters which are fully optional
- First parameter is `from` and it is used to set beginning of date interval in format `YYYY-MM-DD`. If not set then date for current day will be used.
- Second parameter is `to` and it is used to set end of date interval in format `YYYY-MM-DD`. If not set then date for current day will be used.
- Third parameter is `endpoint_id` which is used to choose one distinct endpoint for report generation. If not set then report will be generated based on all of your company's endpoints.
- Fourth and last parameter is `hour` and it is used to switch report to hourly format

All of these parameters are sent via URL.

### Third section is used when you need to generate custom report with fields that interests you

First three parameters are send via URL and duplicate first three parameters for financial report:
- First parameter is `from` and it is used to set beginning of date interval in format `YYYY-MM-DD`. If not set then date for current day will be used.
- Second parameter is `to` and it is used to set end of date interval in format `YYYY-MM-DD`. If not set then date for current day will be used.
- Third parameter is `endpoint_id` which is used to choose one distinct endpoint for report generation. If not set then report will be generated based on all of your company's endpoints.

Next parameters are sent via body of POST request:
- AdType is a parameter that describes platform that you want to do research for (site or application).
- Platform is an object that describes which platform-specific parameters you want to include to your report. All of it's fields are boolean-typed.
- Device is an object that describes which device-specific parameters you want to include to your report.  All of it's fields are boolean-typed.
- Select is an object that describes fields that you want to group by and select for your report.
  - Almost all of it's parameters are boolean, exept for `price` - it's an object than has two fields: boolean flag which is used to add or remove this option from selection and second string-based one which describes function with which you want to aggregate your price by.

**You cannot set more than five flags to true at the same time.**


## Profile API

### Company SSP endpoints
`GET` /ssp

```json
{
  "data": {
    "name": "Demo company",
    "endpoints": [{
      "id": 1,
      "name": "Demo banner"
    }, {
      "id": 2,
      "name": "Demo native"
    }, {
      "id": 3,
      "name": "Demo video"
    }]
  }
}
```

### SSP endpoint details
`GET` /ssp/`:id`

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
    "region": "us-east-1",
    "isActive": 1,
    "qps": 1000,
    "bidQps": 121,
    "sumReq": 123420199321,
    "sumRes": 221342132,
    "sumImp": 200210,
    "manager": {
      "name": "John Doe",
      "email": "john.doe@xendiz.com"
    },
    "blockedCreatives": [{
      "id": "cr8.qwerty",
      "reason": ""
    }, {
      "id": "cr8.qwerty2",
      "reason": ""
    }]
  }
}
```

### Block creative
`POST` /ssp/`:id`/crid

Path params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| id           | Int  | Yes        | Specific endpoint id. Example: `/21`

Body params

| Name         | Type    | isRequired | Description   |
| -------------| ------- | ---------- | ------------- |
| crid         | String  | Yes        | Xendiz creative ID. Example: `cr8.qwerty`
| reason       | String  | No         | Reason for block creative (optional)

Request
```json
[{
  "crid": "cr8.qwerty",
  "reason": ""
}, {
  "crid": "cr8.qwerty2",
  "reason": ""
}]
```

### Unblock creative
`DELETE` /ssp/`:id`/crid

Path params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| id           | Int  | Yes        | Specific endpoint id. Example: `/21`

Body params

| Name         | Type    | isRequired | Description   |
| -------------| ------- | ---------- | ------------- |
| crid         | String  | Yes        | Xendiz creative ID. Example: `cr8.qwerty`

Request
```json
[{
  "crid": "cr8.qwerty"
}, {
  "crid": "cr8.qwerty2"
}]
```

## Financial API
`GET` /ssp/financial

Query params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| from         | Date | No         | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date | No         | End date. Example: `&to=2018-01-10`
| endpoint_id  | Int  | No         | Specific endpoint id. If the param is not specified, a full report will be created for all the endpoints of the company. Example: `&endpoint_id=21`
| hour         | Bool | No         | Hour aggregated report. Example: `&hour=1`

`GET` /ssp/financial/?from=2018-01-01&to=2018-02-02
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

`GET` /ssp/financial/?from=2018-01-02&hour=1
Response:

```json
{
    "data": [{
       "hour": "01:00",
       "spend": 2.21,
       "impressions": 2021
    }, {
       "hour": "02:00",
       "spend": 20.90,
       "impressions": 221132
    }, {
       "hour": "03:00",
       "spend": 21.5,
       "impressions": 222191
    }]
}
```

## Custom report
`POST` /ssp/detailed/custom

Query params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| from         | Date   | No         | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date   | No         | End date. Example: `&to=2018-01-10`
| endpoint_id  | Int    | No         | Specific endpoint id. If the param is not specified, a full report will be created for all the endpoints of the company. Example: `&endpoint_id=21`

Body Params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| adtype       | String | No         | Platfrom type. `app` or `site`
| platform     | Object | No         | Platfrom Object
| device       | Object | No         | Device Object
| select       | Object | No         | Selection Object

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
