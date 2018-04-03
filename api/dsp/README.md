# DSP API
* [Overview](#overview)
* [Profile](#profile-api)
  * [Company DSP endpoints](#company-dsp-endpoints) 
  * [DSP endpoint details](#dsp-endpoint-details)
  * [Add item to block list](#add-item-to-block-list)
  * [DSP campaigns target](#dsp-campaigns-target)
  * [Add DSP campaign target](#add-dsp-campaign-target)
  * [Delete DSP campaign target](#delete-dsp-campaign-target)
  * [Change DSP endpoint URL](#change-dsp-endpoint-url)
* [Financial](#financial-api)
* [Detailed](#detailed-reports-api)
  * [Campaign report](#campaign-report)
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
This section of describes API routes for demand-side platforms.

### This part of API is divided into 3 general sections:
- Profile-based data
- Financial report generation
- Detailed report generation

### First section is used for work with your endpoints
- First method of this section helps you to see all of your company's endpoints
- Second method is used when you need more detailed information for specific endpoint
- Third method is used to add new items to blacklist for specific endpoint. It receives two parameters in body of `POST` request:
  - type - sets type of blocked item. Can be set to `app` to block bundle, `site` to block  domain or `publisher` to block publisher.
  - source - that describes blocked entity and could be app bundle, site domain or Xendiz publisher ID
- Fourth method is used to get list of all targeting campaigns for specific endpoint

### Second section is used when you want to get financial report of your company
It's only method recieves up to 4 parameters which are fully optional
- First parameter is `from` and it is used to set beginning of date interval in format `YYYY-MM-DD`. If not set then date for current day will be used.
- Second parameter is `to` and it is used to set end of date interval in format `YYYY-MM-DD`. If not set then date for current day will be used.
- Third parameter is `endpoint_id` which is used to choose one distinct endpoint for report generation. If not set then report will be generated based on all of your company's endpoints.
- Fourth and last parameter is `hour` and it is used to switch report to hourly format

All of these parameters are sent via URL.

### Third section is used when you need to generate custom report with fields that interests you
**All methods in this section are accepting optional url parameter which limits amount of rows in response, if not set then default value will be used (10 rows)**
- First method of this section generates report based on your ad campaign
  - The only required paramater here is `cid` - that is id of your campaign
  - `from` and `to` parameters are optional and used to set beginning and end of date period for your report respectively in `YYYY-MM-DD` format. If either or both of them aren't set, then date for current day will be used.
  - Last parameter, which is `endpoint_id` is used when you want to get report for specific enpoint. If not set, then full report for all of your endpoints will be generated.
- Second method of this section generates report based on your creative identifier.
  - The only required paramater here is `crid` - that is your creative identifier
  - `from` and `to` parameters are optional and used to set beginning and end of date period for your report respectively in `YYYY-MM-DD` format. If either or both of them aren't set, then date for current day will be used.
  - Last parameter, which is `endpoint_id` is used when you want to get report for specific enpoint. If not set, then full report for all of your endpoints will be generated.
- Next two methods are used when you want to get report based on either your domains or bundles.
  - Both methods may receive up to three parameters, all of them are fully optional.
    - `from` and `to` parameters are optional and used to set beginning and end of date period for your report respectively in `YYYY-MM-DD` format. If either or both of them aren't set, then date for current day will be used.
    - `endpoint_id` parameter is used to choose one distinct endpoint for report generation. If not set then report will be generated based on all of your company's endpoints.
    - if you want to get detailed data about each bundle set url parameter `detailed` to 1
- Next two methods are used when you want to get report based on either one specific domain or bundle.
  - Necessary domain or bundle should be set in route's path
  - As URL parameters you can set up to three parameters which are fully optional
    - `from` and `to` parameters are optional and used to set beginning and end of date period for your report respectively in `YYYY-MM-DD` format. If either or both of them aren't set, then date for current day will be used.
    - `endpoint_id` parameter is used to choose one distinct endpoint for report generation. If not set then report will be generated based on all of your company's endpoints.
- Two following methods are used when you want to get report based on os or geo.
  - Both methods may receive up to three parameters, all of them are fully optional.
    - `from` and `to` parameters are optional and used to set beginning and end of date period for your report respectively in `YYYY-MM-DD` format. If either or both of them aren't set, then date for current day will be used.
    - `endpoint_id` parameter is used to choose one distinct endpoint for report generation. If not set then report will be generated based on all of your company's endpoints.
- Next method is used when you want to get report based on users.
  - **To use this method you shoul integrate your cookie sync with Xendiz SSP**
  - This method may receive up to three parameters, all of them are fully optional.
    - `from` and `to` parameters are optional and used to set beginning and end of date period for your report respectively in `YYYY-MM-DD` format. If either or both of them aren't set, then date for current day will be used.
    - `endpoint_id` parameter is used to choose one distinct endpoint for report generation. If not set then report will be generated based on all of your company's endpoints.
- Last method is used when you need to generate custom report with fields that interests you
  - First three parameters are send via URL and duplicate first three parameters for financial report:
    - First parameter is `from` and it is used to set beginning of date interval in format `YYYY-MM-DD`. If not set then date for current day will be used.
    - Second parameter is `to` and it is used to set end of date interval in format `YYYY-MM-DD`. If not set then date for current day will be used.
    - Third parameter is `endpoint_id` which is used to choose one distinct endpoint for report generation. If not set then report will be generated based on all of your company's endpoints.

  - Next parameters are sent via body of POST request:
    - AdType is a parameter that describes platform that you want to do research for (site or application).
    - Platform is an object that describes which platform-specific parameters you want to include to your report. All of it's fields are boolean-typed.
    - Device is an object that describes which device-specific parameters you want to include to your report.  All of it's fields are boolean-typed.
    - Select is an object that describes fields that you want to group by and select for your report.
      - Almost all of it's parameters are boolean, exept for `price` - it's an object than has two fields: boolean flag which is used to add or remove this option from selection and second string-based one which describes function with which you want to aggregate your price by.

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

### Add items to block list

`PUT` /dsp/`:id`/block

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

Response: 
* STATUS CODE 204

### Remove items to block list

`DELETE` /dsp/`:id`/block

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

Response: 
* STATUS CODE 204

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
        "campaignId": "default",
        "cost": 0,
        "device": {
            "mobile": false,
            "desktop": true,
            "tablet": false
        },
        "platform": {
            "web": true,
            "app": true
        },
        "connection": {
            "ethernet": true,
            "wifi": true,
            "cellular": true
        },
        "os": [
            "android",
            "blackberry",
            "ios",
            "windows",
            "windows mobile"
        ],
        "countries": [
            "ALA"
        ],
        "sizes": [
            {
                "w": 336,
                "h": 445
            },
            {
                "w": 345,
                "h": 333
            }
        ]
    },
    {
        "campaignId": "cid-2234",
        "cost": 0,
        "device": {
            "mobile": true,
            "desktop": true,
            "tablet": true
        },
        "platform": {
            "web": true,
            "app": true
        },
        "connection": {
            "ethernet": true,
            "wifi": true,
            "cellular": true
        },
        "os": [
            "android",
            "ios",
            "windows"
        ],
        "countries": [
            "AUS",
            "JAP",
            "RUS",
            "USA"
        ],
        "sizes": [
            {
                "w": 150,
                "h": 150
            },
            {
                "w": 300,
                "h": 400
            }
        ]
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
| limit        | Int    | No         | Number of rows in response. Default is 10

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
| limit        | Int    | No         | Number of rows in response. Default is 10

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
| limit        | Int    | No         | Number of rows in response. Default is 10

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
| detailed     | int   | No         | Set to 1 if you want detailed data about bundle
| limit        | Int    | No         | Number of rows in response. Default is 10

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
| limit        | Int    | No         | Number of rows in response. Default is 10

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
| limit        | Int    | No         | Number of rows in response. Default is 10

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
| limit        | Int    | No         | Number of rows in response. Default is 10

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
| limit        | Int    | No         | Number of rows in response. Default is 10

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

You should intergate cookie sync with Xendiz SSP to use this method

`GET` /dsp/detailed/users

Query params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| from         | Date   | No        | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date   | No         | End date. Example: `&to=2018-01-10`
| endpoint_id  | Int    | No         | Specific endpoint id. If the param is not specified, a full report will be created for all the endpoints of the company. Example: `&endpoint_id=21`
| limit        | Int    | No         | Number of rows in response. Default is 10

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
| limit        | Int    | No         | Number of rows in response. Default is 10

Body Params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| adtype       | Object | No         | Adv object
| platform     | Object | No         | Platfrom Object
| device       | Object | No         | Device Object
| select    | Object | No         | Selection Object

Adv object

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| site         | Bool   | No         | Advert in site
| app          | Bool   | No         | Advert in bundle


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
