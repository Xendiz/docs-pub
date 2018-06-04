# Xendiz DSP API

## Endpoint
```bash
http://dsp-front-1.xendiz.com
```

## Auth

## Dashboard
### Top Os
`GET` /top/os

* Date fields `from` and `to` must be in format `YYYY-MM-DD`

Query params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| from         | Date | No         | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date | No         | End date. Example: `&to=2018-01-10`
| camp_id  | Int  | No         | Specific campaign id. If the param is not specified, a full report will be created for all the campaigns. Example: `&camp_id=21`
| crid_id  | Int  | No         | Specific creative id. If the param is not specified, a full report will be created for all the creatives. Example: `&crid_id=21`

`GET` /top/os?from=2018-05-07

Response:
```json
{
    "data": [
        {
            "impressions": "9",
            "clicks": "9",
            "os": "android",
            "spend": 0.01899000210687518
        }
    ]
}
```
### Top Geo

`GET` /top/geo

* Date fields `from` and `to` must be in format `YYYY-MM-DD`

Query params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| from         | Date | No         | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date | No         | End date. Example: `&to=2018-01-10`
| camp_id  | Int  | No         | Specific campaign id. If the param is not specified, a full report will be created for all the campaigns. Example: `&camp_id=21`
| crid_id  | Int  | No         | Specific creative id. If the param is not specified, a full report will be created for all the creatives. Example: `&crid_id=21`

`GET` /top/geo?from=2018-05-07

Response:
```json
{
    "data": [
        {
            "countryCode": "JPN",
            "impressions": "9",
            "clicks": "9",
            "spend": 0.01899000210687518
        }
    ]
}
```

### Top Apps
`GET` /top/apps

* Date fields `from` and `to` must be in format `YYYY-MM-DD`
* Fields `bundle`, `name`, `os` always will be in response

Query params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| from         | Date | No         | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date | No         | End date. Example: `&to=2018-01-10`
| camp_id  | Int  | No         | Specific campaign id. If the param is not specified, a full report will be created for all the campaigns. Example: `&camp_id=21`
| crid_id  | Int  | No         | Specific creative id. If the param is not specified, a full report will be created for all the creatives. Example: `&crid_id=21`

`GET` /top/apps?from=2018-05-07

Response:
```json
{
    "data": [
        {   
            "app": {
                "bundle": "com.cleanmaster.mguard",
                "name": "com.cleanmaster.mguard",
                "os": "android",
                "price": 123,
                "score": 4.5,
                "store_url": "url.com",
                "icon_url": "url.com"
            },
            "impressions": "9",
            "clicks": "9",
            "spend": 0.01899000210687518
        }
    ]
}
```

## Accounts
### Get
`GET` /accounts/me

Response:
```json
{
    "data": {
        "id": 1,
        "status": 1,
        "company_name": "Demo",
        "username": "demo",
        "name": "Demo User",
        "email": "email@xendiz.com",
        "country": "EST",
        "api_key": "us-east-1.mgmuqofj9m0zwch257b9",
        "balance": 337.404,
        "spend_today": 0,
        "defaults": null,
        "timestamp": "2018-01-13T06:14:36.000Z"
    }
}
```

### List
`GET` /accounts/list

Response:
```json
{
    "data": [
        {
            "id": 1,
            "name": "Name Surname",
            "email": "email@domain.com"
        },
        {
            "id": 2,
            "name": "Test Account",
            "email": "email@domain.com"
        }
    ]
}
```

### Create
`POST` /accounts

Request:
```json
{
    "company_name": "Demo",
    "name": "Demo User",
    "username": "test",
    "password": "pass",
    "email": "mail@domain.com",
    "country": "EST"
}
```
Response:
```json
{
    "data": {
        "api_key": "49c2e273d075a1031c7600a20fcdbff8",
        "balance": 0,
        "spend_today": 0,
        "id": 3,
        "company_name": "Demo",
        "name": "Demo User",
        "username": "test",
        "email": "mail@domain.com",
        "country": "EST"
    }
}
```

### Update

`PUT` /accounts

Request:
```json
{
    "company_name": "Demo",
    "name": "Demo User",
    "username": "test",
    "password": "123",
    "email": "mail@domain.com",
    "country": "EST"
}
```

Response:
* STATUS CODE 204

## Account Transactions
### List

`GET` /transactions/list

Response:
```json
{
    "data": [
        {
            "id": 2,
            "account_id": 2,
            "volume": 100.5,
            "method": 1,
            "timestamp": "2018-04-19T07:25:16.000Z"
        },
        {}
    ]
}
```

## Campaigns
### List
`GET` /campaigns/list

Response:
```json
{
    "data": [
        {
            "id": 2,
            "account_id": 2,
            "name": "test2",
            "labels": "",
            "status": 1,
            "adomain": "google.com",
            "bundle": null,
            "click_url": "http://google.com",
            "min_cpm": 0.8,
            "max_cpm": 2,
            "daily_budget": 100,
            "total_budget": 1000,
            "spend_today": 100,
            "spend_total": 1000,
            "clicks_today": 4347005,
            "clicks_total": 4347113,
            "imps_today": 217743548,
            "imps_total": 217773778,
            "imp_frequency": 10,
            "inventory": {
                "web": true,
                "inapp": true
            },
            "device": {
                "phone": true,
                "tablet": true,
                "desktop": false,
                "other": true
            },
            "connection": {
                "wifi": true,
                "cellular": true,
                "other": true
            },
            "start_date": "2018-04-10",
            "end_date": null,
            "timestamp": "2017-11-14T15:20:44.000Z"
        },
        {}
    ]
}
```

### Enable
`PUT` /campaigns/`:id`/enable

Response:
* STATUS CODE 204

### Disable
`PUT` /campaigns/`:id`/disable

Response:
* STATUS CODE 204

### Get

`GET` /campaigns/:id

Response:
```json
{
    "data": {
        "id": 45,
        "account_id": 1,
        "name": "test",
        "labels": "lorem,ipsum",
        "status": 1,
        "adomain": "google.com",
        "bundle": null,
        "click_url": "http://google.com",
        "min_cpm": 1,
        "max_cpm": 5,
        "daily_budget": 100,
        "total_budget": 1000,
        "spend_today": 0,
        "spend_total": 0,
        "clicks_today": 0,
        "clicks_total": 0,
        "imps_today": 0,
        "imps_total": 0,
        "imp_frequency": 3,
        "inventory": {
            "web": true,
            "inapp": true
        },
        "device": {
            "phone": true,
            "tablet": true,
            "desktop": true,
            "other": false
        },
        "connection": {
            "wifi": true,
            "cellular": true,
            "other": true
        },
        "start_date": "2018-04-10",
        "end_date": "2018-04-15",
        "timestamp": "2018-05-31T09:33:38.000Z",
        "classification": [
            "IAB1",
            "IAB2",
            "IAB2-1"
        ],
        "categories": [
            "IAB123",
            "IAB2-12",
            "IAB21"
        ],
        "languages": [
            "en",
            "es",
            "uk"
        ],
        "countries": [
            "UKR",
            "USA"
        ],
        "os": [
            {
                "os_name": "android",
                "os_max": 6,
                "os_min": 1
            },
            {
                "os_name": "ios",
                "os_max": 11,
                "os_min": 1
            }
        ],
        "schedules": [
            {
                "day": 3,
                "hours": [
                    0,
                    1,
                    5,
                    6,
                    7
                ]
            }
        ],
        "cities": [
            {
                "cityId": 5,
                "cityName": "Bloemfontein"
            },
            {
                "cityId": 6,
                "cityName": "Durban"
            },
            {
                "cityId": 1234,
                "cityName": "Tonkawa"
            }
        ],
        "blockedPublishers": [
            "pub2"
        ],
        "blockedDomains": [
            "google.com"
        ],
        "blockedBundles": [
            "com.yandex.app"
        ],
        "allowedDomains": [
            "xendiz.com"
        ],
        "allowedBundles": [
            "com.best.app"
        ],
        "isps": [
            {
                "ispId": 4,
                "ispName": "i2ts,inc."
            },
            {
                "ispId": 5,
                "ispName": "TOT"
            }
        ]
    }
}
```

### Create

`POST` /campaigns

Request:
```json
{
    "name": "123",
    "labels": "123,321",
    "adomain": "google.com",
    "bundle": null,
    "click_url": "http://google.com",
    "min_cpm": 1,
    "max_cpm": 5,
    "daily_budget": 100,
    "total_budget": 1000,
    "spend_today": 0,
    "spend_total": 0,
    "clicks_today": 0,
    "clicks_total": 1123,
    "imp_frequency": 3,
    "inventory": { "web": true, "inapp": true },
    "device": { "phone": true, "tablet": true, "desktop": true, "other": false },
    "connection": { "wifi": true, "cellular": true, "other": true },
    "start_date": "2018-04-10",
    "end_date": "2018-04-15",
    "classification": ["IAB1", "IAB2", "IAB2-1"],
    "categories": ["IAB1", "IAB2", "IAB2-1"],
    "countries": ["USA", "UKR"],
    "cities": [1,2,3,4,5,6,1234],
    "isps": [1,2,3,4,5],
    "blockedBundles": ["com.google.app", "com.yandex.app"],
    "blockedDomains": ["google.com", "yandex.ru"],
    "blockedPublishers": ["pub1", "pub2"],
    "allowedDomains": ["xendiz.com"],
    "allowedBundles": ["com.best.app"],
    "languages": ["en", "es", "uk"],
    "os": [{"os_name": "ios", "os_min": 1, "os_max": 11}, {"os_name": "android", "os_min": 1, "os_max": 6}],
    "schedules": [{"day": 3, "hours": [0, 1, 3, 4, 5, 10, 15, 20, 21, 22, 23]}]
}
```

Response:
```json
{
    "data": {
        "spend_total": 0,
        "clicks_total": 0,
        "imps_total": 0,
        "id": 46,
        "account_id": 1,
        "name": "123",
        "labels": "123,321",
        "status": 1,
        "adomain": "google.com",
        "bundle": null,
        "click_url": "http://google.com",
        "min_cpm": 1,
        "max_cpm": 5,
        "daily_budget": 100,
        "total_budget": 1000,
        "imp_frequency": 3,
        "inventory": "{\"web\":true,\"inapp\":true}",
        "device": "{\"phone\":true,\"tablet\":true,\"desktop\":true,\"other\":false}",
        "connection": "{\"wifi\":true,\"cellular\":true,\"other\":true}",
        "start_date": "2018-04-10",
        "end_date": "2018-04-15"
    }
}
```
### Update

`PUT` /campaigns/:id

Request:
```json
{
    "name": "test",
    "labels": "lorem,ipsum",
    "adomain": "google.com",
    "bundle": null,
    "click_url": "http://google.com",
    "min_cpm": 1,
    "max_cpm": 5,
    "daily_budget": 100,
    "total_budget": 1000,
    "spend_today": 0,
    "spend_total": 0,
    "clicks_today": 0,
    "clicks_total": 1123,
    "imp_frequency": 3,
    "inventory": { "web": true, "inapp": true },
    "device": { "phone": true, "tablet": true, "desktop": true, "other": false },
    "connection": { "wifi": true, "cellular": true, "other": true },
    "start_date": "2018-04-10",
    "end_date": "2018-04-15",
    "classification": ["IAB1", "IAB2", "IAB2-1"],
    "categories": ["IAB123", "IAB21", "IAB2-12"],
    "countries": ["USA", "UKR"],
    "cities": [5,6,1234],
    "isps": [4,5],
    "blockedBundles": ["com.yandex.app"],
    "blockedDomains": ["google.com"],
    "blockedPublishers": ["pub2"],
    "allowedDomains": ["xendiz.com"],
    "allowedBundles": ["com.best.app"],
    "languages": ["en", "es", "uk"],
    "os": [{"os_name": "ios", "os_min": 1, "os_max": 11}, {"os_name": "android", "os_min": 1, "os_max": 6}],
    "schedules": [{"day": 3, "hours": [0, 1, 3, 4, 5, 10, 15, 20, 21, 22, 23]}]
}
```

Response:
* STATUS CODE 204

### Link

`PUT` /campaigns/:id/link

Request: 
```json
{
    "crid": [
        { "id": 1, "order": 0  },
        { "id": 2, "order": 0  },
        { "id": 3, "order": 0  },
        { "id": 4, "order": 0  }
    ]
}
```

Response:
* STATUS CODE 204

### Unlink

`PUT` /campaigns/:id/unlink

Request: 
```json
{
    "crid": [1,2,3,4]
}
```
Response:
* STATUS CODE 204

## Creatives
### List

`GET` /creatives/list

Response:
```json
{
    "data": [
        {
            "id": 1,
            "status": 0,
            "name": "asdf",
            "type": "banner",
            "size_id": 1,
            "source": "<h1 style=\"background-color: red; padding: 15px;\"><a href=\"http://google.com\" target=\"_blank\">Google</a></h1>",
            "size": {
                "id": 1,
                "size_code": "320x50"
            },
            "timestamp": "2012-02-24T09:51:39.000Z",
            "campaigns": [
                {
                    "id": 1,
                    "name": "test",
                    "CampaignCreatives": {
                        "camp_id": 1,
                        "creative_id": 1,
                        "bid_order": 0
                    }
                },
                {
                    "id": 2,
                    "name": "test2",
                    "CampaignCreatives": {
                        "camp_id": 2,
                        "creative_id": 1,
                        "bid_order": 0
                    }
                },
                {
                    "id": 3,
                    "name": "test3",
                    "CampaignCreatives": {
                        "camp_id": 3,
                        "creative_id": 1,
                        "bid_order": 0
                    }
                }
            ]
        },
        {}
    ]
}
```

### Get

`GET` /creatives/`:id`

Response:
```json
{
    "data": {
        "id": 9,
        "status": 0,
        "name": "asdf",
        "account_id": 2,
        "type": "banner",
        "size_id": 1,
        "timestamp": "2012-02-24T09:51:39.000Z",
        "source": "<h1 style=\"background-color: red; padding: 15px;\"><a href=\"http://google.com\" target=\"_blank\">Google</a></h1>",
        "size": "320x50"
    }
}
```

### Create tag

`POST` /creatives

Request:
```json
{
    "campaign_id": 16,
    "name": "asdf",
    "source": "<h1 style=\"background-color: red; padding: 15px;\"><a href=\"http://google.com\" target=\"_blank\">Google</a></h1>",
    "is_secure": 1,
    "size_code": "320x50"
}
```

Response:
```json
{
    "data": {
        "status": 2,
        "is_secure": 0,
        "id": 17,
        "type": "tag",
        "source": "<h1 style=\"background-color: red; padding: 15px;\"><a href=\"http://google.com\" target=\"_blank\">Google</a></h1>",
        "size_id": 1,
        "account_id": 1
    }
}
```

### Create banner

`POST` /creatives/banner<br>

Request:
```json
{
    "campaign_id": 16,
    "source": "<img src=\"https://res.cloudinary.com/xendiz-com/image/upload/v1525946050/nqtbgrq9xvf7fkkeocbc.jpg\" width=\"300\" height=\"250\">",
    "size_code": "320x50"
}
```

Response:
* STATUS CODE 200

### Update

`PUT` /creatives/:id

Request:
```json
{
    "source": "<h1 style=\"background-color: red; padding: 15px;\">TAG</h1>",
    "size_code": "300x250"
}
```

Response:
* STATUS CODE 200

### Disable

`PUT` /creatives/:id/disable

Response:
* STATUS CODE 200

### Delete

`DELETE` /creatives/:id

Response:
* STATUS CODE 204

## Available OS
### List

`GET` /available/os

Response:
```json
{
    "data": [
        {
            "id": 1,
            "os_name": "android",
            "os_min": 0,
            "os_max": 0
        },
        {}
    ]
}
```

## Available sizes
### List

`GET` /available/sizes

Response:
```json
{
    "data": [
        {
            "id": 1,
            "size_code": "320x50"
        },
        {}
    ]
}
```

## Available ISP

`GET` /available/isp

Response:
```json
{
    "data": [
        {
            "id": 1,
            "name": "Google"
        },
        {
            "id": 2,
            "name": "China Telecom fujian"
        },
        {
            "id": 3,
            "name": "China Telecom Guangdong"
        },
        {
            "id": 4,
            "name": "i2ts,inc."
        },
        {
            "id": 5,
            "name": "TOT"
        }
    ]
}
```

## Financial
### Report

`POST` /financial

* Date fields `from` and `to` must be in format `YYYY-MM-DD`

Body params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| selection    | Object | Yes         | Query selection object
| search  | Object  | Yes         | Query search object

Selection object

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| date    | Int | Yes         | Add date to report
| hour  | Int  | Yes         | Add by hour grouping to report
| camp_id    | Int | Yes         | Add campaign id to report
| crid_id  | Int  | Yes         | Add creative id to report

Search object

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| from     | String | No         | Exact date to begin search from (e.g `2018-05-01`, defaults to today's date)
| to       | String  | No         | Exact date where search must stop (e.g `2018-05-02`, defaults to today's date)
| camp_id    | Int | No         | Search by specific campaign id
| crid_id  | Int  | No         | Search by specific creative id


Example:

`POST` /financial

Request: 
```json
{
    "selection": {
        "date": 1, 
        "hour": 0, 
        "camp_id": 1, 
        "crid_id": 1
        
    },
    "search": {
        "from": "2018-05-01",
        "to": "2018-05-02",
        "camp_id": 2,
        "crid_id": 4
    }
}
```

Response:
```json
{
    "data": {
        "fields": [
            "date",
            "camp_id",
            "crid_id",
            "impressions",
            "clicks",
            "spend"
        ],
        "data": [
            [
                "2018-05-01",
                2,
                4,
                "5692095",
                "110",
                713.7676296234131
            ],
            [
                "2018-05-02",
                2,
                4,
                "4924540",
                "130",
                565.6175422668457
            ]
        ]
    }
}
```

`POST` /financial

Request:
```json
{
    "selection": {
        "date": 1, 
        "hour": 1, 
        "camp_id": 1, 
        "crid_id": 1
        
    },
    "search": {
        "from": "2018-05-01",
        "to": "2018-05-02",
        "camp_id": 2,
        "crid_id": 4
    }
}
```

Response:

```json
{
    "data": {
        "fields": [
            "date",
            "hour",
            "camp_id",
            "crid_id",
            "impressions",
            "clicks",
            "spend"
        ],
        "data": [
            [
                "2018-05-01",
                0,
                2,
                4,
                "280104",
                "0",
                36.56417465209961
            ],
            [
                "2018-05-01",
                1,
                2,
                4,
                "259380",
                "0",
                31.8701229095459
            ],
            [
                "2018-05-01",
                2,
                2,
                4,
                "235356",
                "0",
                27.657794952392575
            ]
        ]
    }
}
```
## Cities

### List

`GET` /cities

Query params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| country      | String | Yes         | Country code in ISO-3166-1-alpha-3. Example: `&country=USA`

Request:  
`GET` /cities?country=USA

Response:
```json
{
    "data": [
        {
            "id": 639765,
            "name": "Aaron"
        },
        {
            "id": 404642,
            "name": "Aaronsburg"
        },
        {
            "id": 395813,
            "name": "Abbeville"
        },
        {
            "id": 502367,
            "name": "Abbot"
        }
    ]
}
```

### Custom report

`POST` /custom

This method is used to generate custom detailed report for your company based on account stats.  
Select which field to include to your report in body params objects, their contents are specified below.

* Date fields `from` and `to` must be in format `YYYY-MM-DD`

Query params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| from         | Date   | No         | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date   | No         | End date. Example: `&to=2018-01-10`

Body Params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| adtype       | Object | No         | Adv object
| platform     | Object | No         | Platform Object
| format       | Object | No         | Format Object
| device       | Object | No         | Device Object
| select       | Object | No         | Selection Object
| camps       | Array | No         | Array of campaign id's
| crids       | Array | No         | Array of creative id's
| limit        | Int    | No         | Number of rows in response. Default is 10

Adv object

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| site         | Bool   | No         | Advert in site
| app          | Bool   | No         | Advert in bundle


Platform Object

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| pubid       | Bool   | No         | Publisher id
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
| model       | Bool   | No         | Device model
| carrier       | Bool   | No         | Device carrier
| ct           | Bool   | No         | Device connection type
| country      | Bool   | No         | Device country
| city      | Bool   | No         | Device city
| ifa      | Bool   | No         | Device ifa
| dpid      | Bool   | No         | Device dpid
| did      | Bool   | No         | Device did

Select

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| date         | Bool   | No         | Date
| campaign     | Bool   | No         | Dsp campaign
| creative     | Bool   | No         | Dsp creative
| category     | Bool   | No         | Content category
| Adpos        | Bool   | No         | Ad position

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
        "pubid": true,
        "name": true,
        "id": true
    },
    "device": {
        "ip": false,
        "os": false,
        "type": false,
        "vendor": false,
        "model": false,
        "carrier": false,
        "ct": false,
        "country": false,
        "city": false,
        "ifa": false,
        "dpid": false,
        "did": false
    },
    "select": {
        "date": true,
        "category": false,
        "creative": false,
        "campaign": false,
        "adpos": true
    },
    "camps": [1,2,3,4,5,6],
    "crids": [1,2,3,4,5,6],
    "limit": 10
}
```

Response
```json
{
    "data": {
        "fields": [
            "Publisher",
            "Name",
            "ID",
            "Date",
            "Impressions",
            "Clicks",
            "Price"
        ],
        "data": [
            [
                "1006458",
                "Clean Master- Space Cleaner and Antivirus",
                "com.cleanmaster.mguard",
                "2018-05-07",
                "9",
                "9",
                "9"
            ]
        ]
    }
}
```

### Inventory overview

`POST` /inventory

This method is used to generate custom inventory report for your company based on account stats.  
Select which field to include to your report in body params objects, their contents are specified below.

* Date fields `from` and `to` must be in format `YYYY-MM-DD`

Query params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| from         | Date   | No         | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date   | No         | End date. Example: `&to=2018-01-10`

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
| pubid       | Bool   | No         | Publisher id
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
| model       | Bool   | No         | Device model
| carrier       | Bool   | No         | Device carrier
| ct           | Bool   | No         | Device connection type
| country      | Bool   | No         | Device country
| city      | Bool   | No         | Device city
| ifa      | Bool   | No         | Device ifa
| dpid      | Bool   | No         | Device dpid
| did      | Bool   | No         | Device did

Select

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| date         | Bool   | No         | Date

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
        "pubid": true,
        "name": true,
        "id": true
    },
    "device": {
        "ip": false,
        "os": false,
        "type": false,
        "vendor": false,
        "model": false,
        "carrier": false,
        "ct": false,
        "country": false,
        "city": false,
        "ifa": false,
        "dpid": false,
        "did": false
    },
    "select": {
        "date": true
    },
    "limit": 10
}
```

Response
```json
{
    "data": {
        "fields": [
            "Publisher",
            "Name",
            "ID",
            "Date",
            "Impressions",
            "Clicks",
            "Price"
        ],
        "data": [
            [
                "1006458",
                "Clean Master- Space Cleaner and Antivirus",
                "com.cleanmaster.mguard",
                "2018-05-07",
                "13",
                "13",
                "13"
            ],
            [
                "1006458",
                "Clean Master- Space Cleaner and Antivirus",
                "com.cleanmaster.mguard",
                "2018-05-09",
                "1",
                "1",
                "1"
            ]
        ]
    }
}
```