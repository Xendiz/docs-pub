# DSP API
* [Overview](#overview)
* [Profile](#profile-api)
  * [Company DSP endpoints](#company-dsp-endpoints) 
  * [DSP endpoint details](#dsp-endpoint-details)
  * [Add item to block list](#add-items-to-block-list)
  * [Remove item from block list](#remove-items-from-block-list)
  * [DSP campaigns target](#dsp-campaigns-target)
  * [Add DSP campaign target](#add-dsp-campaign-target)
  * [Update DSP campaign](#update-dsp-campaign)
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
- Profile-based data that is used for work with your endpoints.
- Financial report generation that is used when you want to get financial report of your company.
- Detailed report generation that is used when you need to generate report with fields that interests you.

## Profile API

### Company DSP endpoints 
`GET` /dsp

This route is used to fetch all company's DSP enpoints.

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

This route is used to get more detailed info about specific endpoint.

Path params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| id           | Int  | Yes        | Specific endpoint id. Example: `/21`

Response:

```json
{
    "data": {
        "id": 1,
        "name": "Lorem ",
        "token": "2330c0eef8d4ee649c8e8b6cefd2d9a3",
        "endpoint": "http://dsp.com/bid/xendiz",
        "isBanner": 1,
        "isAudio": 0,
        "isVideo": 1,
        "isNative": 1,
        "qpsLimit": 500,
        "bidQps": 1,
        "sumReq": 2000014,
        "sumRes": 1000004,
        "sumImp": 2440931,
        "realQps": 1024,
        "spendToday": 122.2,
        "manager": {
            "name": "John Doe",
            "email": "hello@xendiz.com"
        },
        "blockedPlatforms": [
            {
                "type": "app",
                "source": "com.app.awesome"
            },
            {}
        ],
        "region": "us-east-1"
    }
}
```

### Add items to block list

`PUT` /dsp/`:id`/block

This route is used to add new items to DSP's block list.  
Request's body must be array of objects.  
Each object's contents are listed below in `Body params` section.

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

### Remove items from block list

`DELETE` /dsp/`:id`/block

This route is used to remove items from DSP's block list.  
Request's body must be array of objects.  
Each object's contents are listed below in `Body params` section.

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

This route is used to fetch all target campaigns for selected DSP.  
* First element of response array always will be default target for selected DSP.

Path params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| id           | Int  | Yes        | Specific endpoint id. Example: `/21`

Response:

```json
{
    "data": [
        {
            "campaignId": "default",
            "cost": 0,
            "device": {
                "mobile": false,
                "desktop": true,
                "tablet": false
            },
            "platform": {
                "web": false,
                "app": false
            },
            "format": {
                "banner": true,
                "video": true,
                "native": true
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
                "windows"
            ],
            "countries": [
                "ALA",
                "RUS"
            ],
            "sizes": [
                {
                    "w": 325,
                    "h": 333
                },
                {
                    "w": 336,
                    "h": 445
                },
                {
                    "w": 345,
                    "h": 333
                }
            ],
            "blockedPlatforms": [
                {
                    "type": "app",
                    "source": "com.app.awesome"
                },
                {
                    "type": "app",
                    "source": "com.app.sampblock"
                },
                {
                    "type": "app",
                    "source": "com.app.test"
                },
                {
                    "type": "app",
                    "source": "com.app.wew"
                },
                {
                    "type": "app",
                    "source": "com.test.bundle"
                },
                {
                    "type": "site",
                    "source": "google.com"
                },
                {
                    "type": "site",
                    "source": "sample.domain"
                },
                {
                    "type": "site",
                    "source": "yandex.ru"
                }
            ]
        },
        {
            "campaignId": "cid-1234",
            "cost": 123.22,
            "device": {
                "mobile": false,
                "desktop": true,
                "tablet": false
            },
            "platform": {
                "web": false,
                "app": true
            },
            "format": {
                "banner": true,
                "native": false,
                "video": false
            },
            "connection": {
                "ethernet": true,
                "wifi": false,
                "cellular": true
            },
            "os": [
                "android",
                "ios"
            ],
            "countries": [
                "GBR",
                "ITA",
                "USA"
            ],
            "sizes": [
                {
                    "w": 320,
                    "h": 50
                },
                {
                    "w": 320,
                    "h": 250
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
            "format": {
                "banner": true,
                "native": false,
                "video": false
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
        },
        {
            "campaignId": "cid1234",
            "cost": 23452.4,
            "device": {
                "mobile": true,
                "desktop": true,
                "tablet": true
            },
            "platform": {
                "web": true,
                "app": true
            },
            "format": {
                "banner": true,
                "native": false,
                "video": false
            },
            "connection": {
                "ethernet": false,
                "wifi": false,
                "cellular": false
            },
            "os": [
                "blackberry",
                "ios"
            ],
            "countries": [
                "GBR",
                "ITA",
                "RUS",
                "USA"
            ],
            "sizes": [
                {
                    "w": 320,
                    "h": 250
                },
                {
                    "w": 320,
                    "h": 450
                }
            ]
        }
    ]
}
```

### Add DSP campaign target

`POST` /dsp/`:id`/campaigns

This route is used to create new target campaigns for selected DSP.  
Request's body must be array of objects. 
Each object contents are specified below in `Body params` section.  

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
| format       | Object  | No         | Format target
| os           | Array   | No         | OS target. See suported os list (link).
| countries    | Array   | No         | Country target. Array of ISO 3 country codes.
| connection   | Object  | No         | Connection target. See connection object (link)
| sizes        | Array   | No         | Size target. See size object.

Device Object

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| mobile       | Bool   | No         | Mobile target
| desktop      | Bool   | No         | Desktop target
| tablet       | Bool   | No         | Tablet target

Platform Object

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| web          | Bool   | No         | Platform domain
| app          | Bool   | No         | Platform bundle

Format object

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| banner       | Bool   | No         | Banner format
| native       | Bool   | No         | Native format
| video        | Bool   | No         | Video format

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
  "campaignId": "cid22234",
  "cost": 123.22,
  "device": {
    "mobile": false,
    "desktop": true,
    "tablet": false
  },
  "format": {
    "banner": true,
    "video": false,
    "native": false
  },
  "platform": {
    "web": false,
    "app": true
  },
  "os": ["android", "ios"],
  "connection": {
    "ethernet": true,
    "wifi": false,
    "cellular": true
  },
  "sizes": [{
    "w": 320,
    "h": 250
  }, {
    "w": 320,
    "h": 50
  }],
  "countries": ["USA", "RUR", "ITA", "GBR"]
}]
```

### Update DSP campaign

`PUT` /dsp/`:id`/campaigns/

This route is used to update target campaign for selected DSP.

Path params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| id           | Int  | Yes        | Specific endpoint id. Example: `/21`
| target_id    | String  | Yes        | Dsp specific campaign ID. Example: `cid-2234`

Body params

| Name         | Type    | isRequired | Description   |
| -------------| ------- | ---------- | ------------- |
| device       | Object  | No         | Device target
| platform     | Object  | No         | Platform target
| format       | Object  | No         | Format target
| os           | Array   | No         | OS target. See suported os list (link).
| countries    | Array   | No         | Country target. Array of ISO 3 country codes.
| connection   | Object  | No         | Connection target. See connection object (link)
| sizes        | Array   | No         | Size target. See size object.

Device Object

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| mobile       | Bool   | No         | Mobile target
| desktop      | Bool   | No         | Desktop target
| tablet       | Bool   | No         | Tablet target

Platform Object

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| web          | Bool   | No         | Platform domain
| app          | Bool   | No         | Platform bundle

Format object

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| banner       | Bool   | No         | Banner format
| native       | Bool   | No         | Native format
| video        | Bool   | No         | Video format

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


Request:

`/dsp/1/campaigns/default`

{
    "device": {
        "mobile": false,
        "desktop": true,
        "tablet": false
    },
    "platform": {
        "web": false,
        "app": false
    },
    "format": {
        "banner": true,
        "video": false,
        "native": false
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
        "windows"
    ],
    "countries": [
        "ALA",
        "RUS"
    ],
    "sizes": [
        {
            "w": 325,
            "h": 333
        }
    ],
    "blockedPlatforms": [
        {
            "type": "app",
            "source": "com.app.awesome"
        }
    ]
}

`/dsp/1/campaigns/cid1234`

```json
{
        "cost": 23452.4,
        "device": {
            "mobile": true,
            "desktop": true,
            "tablet": true
        },
        "platform": {
            "web": true,
            "app": true
        },
        "format": {
            "banner": true,
            "native": true,
            "video": true
        },
        "connection": {
            "ethernet": false,
            "wifi": false,
            "cellular": false
        },
        "os": [
            "blackberry",
            "ios"
        ],
        "countries": [
            "GBR",
            "ITA",
            "RUS",
            "USA"
        ],
        "sizes": [
            {
                "w": 320,
                "h": 250
            }
        ]
    }
```

Response:

* STATUS CODE 200

### Delete DSP campaign target

`DELETE` /dsp/`:id`/campaigns/`:target_id`

This route is used to delete target campaign with id `:targed_id` from selected DSP.

Path params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| id           | Int  | Yes        | Specific endpoint id. Example: `/21`
| target_id    | Int  | Yes        | Dsp specific campaign ID. Example: `cid-2234`

Response:

* STATUS CODE 204

### Change DSP endpoint URL

`PUT` /dsp/`:id`/endpoint

This route is used to update endpoint URL for selected DSP.

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

Response:

* STATUS CODE 204

## Financial API
`GET` /dsp/financial

This route is used to generate financial report based on either one specific endpoint id or all of your company's endpoints.

* Date fields `from` and `to` must be in format `YYYY-MM-DD`

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

This method is used generate detailed report based company's campaign id.

* Date fields `from` and `to` must be in format `YYYY-MM-DD`

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

This method is used generate detailed report based company's creative id.

* Date fields `from` and `to` must be in format `YYYY-MM-DD`

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

This method is used to generate detailed report about domains in your company based on either one specific `endpoint_id` or all of your company's endpoints.

* Date fields `from` and `to` must be in format `YYYY-MM-DD`

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

This method is used to generate detailed report about bundles in your company based on either one specific `endpoint_id` or all of your company's endpoints.

* Date fields `from` and `to` must be in format `YYYY-MM-DD`

Query params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| from         | Date   | No        | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date   | No         | End date. Example: `&to=2018-01-10`
| endpoint_id  | Int    | No         | Specific endpoint id. If the param is not specified, a full report will be created for all the endpoints of the company. Example: `&endpoint_id=21`
| detailed     | int   | No         | Set to 1 if you want detailed data about each bundle
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

This method is used to generate detailed report about specific domain in your company based on either one `endpoint_id` or all of your company's endpoints.

* Date fields `from` and `to` must be in format `YYYY-MM-DD`

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
| limit        | Int    | No         | Number of rows in response. Default is 10. Example `&limit=15`.

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

This method is used to generate detailed report about specific bundle in your company based on either one `endpoint_id` or all of your company's endpoints.

* Date fields `from` and `to` must be in format `YYYY-MM-DD`

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
| limit        | Int    | No         | Number of rows in response. Default is 10. Example `&limit=15`.

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

This method is used to generate detailed report about operational systems in your company based on either one specific `endpoint_id` or all of your company's endpoints.

* Date fields `from` and `to` must be in format `YYYY-MM-DD`

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

This method is used to generate detailed report about geos in your company based on either one specific `endpoint_id` or all of your company's endpoints.

* Date fields `from` and `to` must be in format `YYYY-MM-DD`

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

* You should intergate cookie sync with Xendiz SSP to use this method

`GET` /dsp/detailed/users

This method is used to generate detailed report about users in your company based on either one specific `endpoint_id` or all of your company's endpoints.

* Date fields `from` and `to` must be in format `YYYY-MM-DD`

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

This method is used to generate custom detailed report for your company based on either one specific `endpoint_id` or all of your company's endpoints.  
Select which field to include to your report in body params objects, their contents are specified below.

* Date fields `from` and `to` must be in format `YYYY-MM-DD`

Query params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| from         | Date   | No         | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date   | No         | End date. Example: `&to=2018-01-10`
| endpoint_id  | Int    | No         | Specific endpoint id. If the param is not specified, a full report will be created for all the endpoints of the company. Example: `&endpoint_id=21`

Body Params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| adtype       | Object | No         | Adv object
| platform     | Object | No         | Platform Object
| format       | Object | No         | Format Object
| device       | Object | No         | Device Object
| select       | Object | No         | Selection Object
| limit        | Int    | No         | Number of rows in response. Default is 10

Adv object

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| site         | Bool   | No         | Advert in site
| app          | Bool   | No         | Advert in bundle


Platform Object

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| domain       | Bool   | No         | Platform domain
| bundle       | Bool   | No         | Platform bundle
| name         | Bool   | No         | Platform name
| id           | Bool   | No         | Platform id

Format object

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| banner       | Bool   | No         | Banner format
| native       | Bool   | No         | Native format
| video        | Bool   | No         | Video format

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
| size         | Object | No         | Size
| campaign     | Bool   | No         | Dsp campaign
| creative     | Bool   | No         | Dsp creative
| category     | Bool   | No         | Content category
| price        | Object | No         |
| price.on     | Bool   | No         | Add cost to selection
| price.value  | String | No         | Aggregate function: `median`, `sum`, `average`

Size Object

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| on           | Bool   | No         | Add size to selection
| sizes        | Array  | No         | Array of strings in format `WxH` (e.g `350x70` etc.)

Example request

```json
{
    "adType": {
      "app": true,
      "site": true
    },
    "format": {
        "banner": true,
        "native": true,
        "video": true
    },
    "platform": {
        "domain": false,
        "bundle": false,
        "name": false,
        "id": false
    },
    "device": {
        "ip": false,
        "os": false,
        "type": false,
        "vendor": false,
        "ct": true,
        "country": true
    },
    "select": {
        "date": true,
        "size": {
            "on": true,
            "sizes": ["300x250","728x90","320x50"]
        },
        "campaign": true,
        "creative": false,
        "category": false,
        "price": {
            "on": false,
            "value": "median"
        }
    },
    "limit": 10
}
```

Response
```json
{
    "data": {
        "fields": [
            "Connection Type",
            "Country",
            "Date",
            "Campaign",
            "Size",
            "Impressions"
        ],
        "data": [
            [
                "Cellular Network - Unknown",
                "USA",
                "2018-03-13",
                "234|479",
                "728x90",
                "3.117k"
            ],
            []
        ]
    }
}
```
