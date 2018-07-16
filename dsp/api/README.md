# Xendiz DSP API

## Endpoint
```bash
https://dsp-front-1.xendiz.com
```

## Auth
`POST` /auth

Request:
```json
{
    "username": "name",
    "password": "pass"
}
```

Response:
```json
{   
    "data":{
        "token": "token",
        "user": {
            "id": 2,
            "status": 1,
            "company_name": "Demo",
            "username": "test",
            "name": "Name Surname",
            "api_key": "123",
            "balance": 100.5,
            "spend_today": 0,
            "defaults": null,
            "timestamp": "2018-04-13T05:14:36.000Z",
            "campaigns": [
                1,
                2,
                3,
                4,
                14,
                15,
                16,
                17,
                18,
                19,
                20,
                22,
                23,
                26
            ]
        }
    }
}
```

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
            "os": "android",
            "impressions": 93193458,
            "clicks": 1984422,
            "spend": 0
        },
        {
            "os": "ios",
            "impressions": 92861639,
            "clicks": 1984529,
            "spend": 24507.05
        },
        {
            "os": "windows",
            "impressions": 92845239,
            "clicks": 1982675,
            "spend": 24502.64
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
            "country": "Georgia",
            "impressions": 28045935,
            "clicks": 593115,
            "spend": 7401.56
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
                "bundle": "com.outfit7.mytalkingtomfree",
                "os": "android",
                "name": "My Talking Tom",
                "price": 0,
                "score": 4.48421,
                "store_url": "https://play.google.com/store/apps/details?id=com.outfit7.mytalkingtomfree&hl=en&gl=us",
                "icon_url": "https://lh3.googleusercontent.com/3s2Ll-HtFiscV33KBhqJj5IOPAUi9XN_TiNZLV1jWHYJZFeLDrwie_lw4HwFCek26g"
            },
            "impressions": 580577,
            "clicks": 12636,
            "spend": 153.22
        }
    ]
}
```

### Top Spend
`GET` /top/spend

* Date fields `from` and `to` must be in format `YYYY-MM-DD`
* Fields `bundle`, `name`, `os` always will be in response

Query params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| from         | Date | No         | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date | No         | End date. Example: `&to=2018-01-10`
| camp_id  | Int  | No         | Specific campaign id. If the param is not specified, a full report will be created for all the campaigns. Example: `&camp_id=21`
| crid_id  | Int  | No         | Specific creative id. If the param is not specified, a full report will be created for all the creatives. Example: `&crid_id=21`

* First elemtent in array comes as sum of params between `from` and `to`
* Second element in array comes as sum of params between `from` date minus difference between `from` and `to`

Response:
```json
{
    "data": [
        {
            "impressions": 243231480,
            "clicks": 5281702,
            "spend": 64152.309198914096
        },
        {
            "impressions": 77078925,
            "clicks": 1681492,
            "spend": 20329.56853437424
        }
    ]
}
```

## Signup
### Post

`POST` /signup

Request:
```json
{
    "firstName": "first",
    "lastName": "last",
    "companyName": "Xendiz",
    "username": "test",
    "password": "test123",
    "email": "demo@xendiz.com",
    "country": "EST"
}
```

Response:
* Status code 200

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
    "name": "DEM",
    "username": "test",
    "password": "pass",
    "email": "mail@domain.com",
    "country": "UKR"
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
        "name": "DEM",
        "username": "test",
        "email": "mail@domain.com",
        "country": "UKR"
    }
}
```

### Update

`PUT` /accounts

Request:
```json
{
    "company_name": "Demo",
    "name": "DEM",
    "username": "test",
    "password": "123",
    "email": "mail@domain.com",
    "country": "UKR"
}
```

Response:
* STATUS CODE 204

## Accounts Transactions
### List

`GET` /transactions/list

Response:
```json
{
    "data": [
        {
            "id": 32,
            "account_id": 1,
            "order_id": 39,
            "volume": 120.5,
            "method": "worldhand",
            "timestamp": "2018-06-06T06:44:48.000Z",
            "getaway": "paysera"
        }
    ]
}
```

## Campaigns
### List
`GET` /campaigns/list[?all=1]

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

### Tiny List
`GET` /campaigns/tiny[?all=1]

Response:
```json
{
    "data" :[
        {
            "id": 10449,
            "name": "demo camp"
        },
        {
            "id": 10450,
            "name": "demo camp"
        }
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
                "id": 5,
                "name": "Bloemfontein"
            },
            {
                "id": 6,
                "name": "Durban"
            },
            {
                "id": 1234,
                "name": "Tonkawa"
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
                "id": 4,
                "name": "i2ts,inc."
            },
            {
                "id": 5,
                "name": "TOT"
            }
        ]
    }
}
```

### Creatives list

`GET` /campaigns/:id/creatives

Response:
```json
{
    "id": 1,
    "creatives": [
        {
            "id": 62,
            "name": "banner 728x90",
            "source": "<img src='http://res.cloudinary.com/xendiz-com/image/upload/c_fill,h_90,w_728/bhwjvoycmw14rix9g3ii' height='90' width='728'/>",
            "type": "banner",
            "size": {
                "id": 4,
                "size_code": "728x90"
            }
        }
    ]
}
```

### Create

`POST` /campaigns

Request:
```json
{
    "name": "123",
    "status": 1,
    "labels": "123,321",
    "adomain": "google.com",
    "bundle": null,
    "click_url": "http://google.com",
    "min_cpm": 1,
    "max_cpm": 5,
    "daily_budget": 100,
    "total_budget": 1000,
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

### Archive

`PATCH` /campaigns/:id/archive

Respinse:
* STATUS CODE 204

### Unarchive

`PATCH` /campaigns/:id/unarchive

Respinse:
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

`GET` /creatives/list[?all=1]

Response:
```json
{
    "data": [
        {
            "id": 132,
            "hashed_id": "fde1d6e00",
            "status": 1,
            "archived": 0,
            "approved": 1,
            "name": "test_post_new_banners",
            "is_secure": 1,
            "timestamp": "2018-06-19T10:43:39.000Z",
            "account_id": 2,
            "type": "banner",
            "size": {
                "id": 2,
                "size_code": "300x250"
            },
            "campaigns": [
                {
                    "id": 70,
                    "name": "dsad",
                    "spend_today": 0
                }
            ]
        }
    ]
}
```

### Tiny List

`GET` /creatives/tiny[?source=1&size=1&type=1&all=1]

Response:
```json
{
    "data": [
        {
            "id": 12,
            "name": "somename"
        },
        {
            "id": 13,
            "name": "somename"
        },
        {
            "id": 14,
            "name": "somename"
        }
    ]
}
```

### Get

`GET` /creatives/`:id`

Response:
```json
{
    "data": {
        "id": 151,
        "hashed_id": "a457a3302",
        "status": 1,
        "archived": 0,
        "approved": 0,
        "name": "qwerty2",
        "is_secure": 1,
        "timestamp": "2018-06-27T07:20:27.000Z",
        "account_id": 2,
        "type": "tag",
        "source": "<h1>Lorem Ipsum Dolor Sit Amet</h1>",
        "size": {
            "id": 2,
            "size_code": "300x250"
        }
    }
}
```

### Create tag

`POST` /creatives

Request:
```json
{
    "campaign_id": [16,17],
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
        "id": 136,
        "name": "demo",
        "type": "tag",
        "source": "<h1 style=\"background-color: red; padding: 15px;\"><a href=\"http://google.com\" target=\"_blank\">Google</a></h1>",
        "size_id": 1,
        "account_id": 2,
        "hashed_id": "71a3a594a",
        "size": {
            "id": 1,
            "size_code": "320x50"
        }
    }
}
```

### Create banner

`POST` /creatives/banner<br>

Request:
```json
{   
    "name": "somename",
    "campaign_id": [16,17],
    "source": "file",
    "size_code": "320x50"
}
```

Response:
```json
{
    "data": {
        "status": 2,
        "id": 135,
        "name": "test_post",
        "type": "banner",
        "source": "<img src='link.com' height='250' width='300'/>",
        "size_id": 2,
        "account_id": 2,
        "is_secure": 1,
        "hashed_id": "7c01f4189",
        "size": {
            "id": 2,
            "size_code": "300x250"
        }
    }
}
```

### Update

`PUT` /creatives/`:id`

Request:
```json
{   
    "name": "somename",
    "source": "<h1 style=\"background-color: red; padding: 15px;\">TAG</h1>",
    "size_code": "300x250"
}
```

Response:
* STATUS CODE 204

### Update banner

`PUT` /creatives/`:id`/banner

Request:
```json
{   
    "name": "somename",
    "source": "file",
    "size_code": "300x250"
}
```

Response:
* STATUS CODE 204

### Disable

`PUT` /creatives/`:id`/disable

Response:
* STATUS CODE 200

### Archive

`PATCH` /creatives/`:id`/archive

Response:
* STATUS CODE 200

### Unarchive

`PATCH` /creatives/`:id`/unarchive

Response:
* STATUS CODE 200

### Delete

`DELETE` /creatives/`:id`

Response:
* STATUS CODE 204

### Link

`PUT` /creatives/:id/link

Request: 
```json
{
    "cid": [
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

`PUT` /creatives/:id/unlink

Request: 
```json
{
    "cid": [1,2,3,4]
}
```
Response:
* STATUS CODE 204

## Lists

`GET` /lists

Response:
```json
{
    "data": [
        {
            "id": 2,
            "name": "New List"
        }
    ]
}
```

`POST` /lists

Request:
```json
{
    "name": "New List"
}
```

Response:
```json
{
    "data": {
        "id": 4,
        "name": "New List"
    }
}
```

`PUT` /lists/`:id`

Request:
```json
{
    "name": "New Name"
}
```

Response:
* STATUS CODE 204

`DELETE` /lists/`:id`

Response:
* STATUS CODE 204

`GET` /lists/`:id`

Response:
```json
{
    "data": [
        {
            "id": 2,
            "text": "This is testing entry"
        }
    ]
}
```

`PUT` /lists/`:id`/`:entry_id`

Request:
```json
{
    "text": "Lorem Ipsum"
}
```

Response:
* STATUS CODE 204

`DELETE` /lists/`:id`/`:entry_id`

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

Request:

`GET` /available/isp?query=1

Response:
```json
{
    "data": [
        {
            "id": 12046,
            "name": "# 1 Firma Handlowa Giga Arkadiusz Kocma"
        },
        {
            "id": 6151,
            "name": "#1 Tele 2 Nederland B.V."
        }
    ]
}
```

## Available cities

### List

`GET` /available/cities

Query params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| country      | String | Yes         | Country name to search divided by `,`. Example: `&country=USA,UKR`
| query      | String | Yes         | City name to search. Example: `&query=br`

Request:  
`GET` /available/cities?query=br&country=USA,UKR,RUS

Response:
```json
{
    "data": [
        {
            "id": 27,
            "name": "Braamfontein"
        },
        {
            "id": 132,
            "name": "Bryanston"
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
| all_day  | Int  | Yes         | Search on span of previous 24h if both `hour` and this field are selected.
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
        "hour": 1,
        "all_day": 0,
        "camp_id": 1, 
        "crid_id": 1
        
    },
    "search": {
        "from": "2018-05-01",
        "to": "2018-05-10",
        "camp_id": 1,
        "crid_id": 2
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
                9,
                9,
                9
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
| os           | Bool   | No         | Device os
| type         | Bool   | No         | Device type
| vendor       | Bool   | No         | Device vendor
| model       | Bool   | No         | Device model
| carrier       | Bool   | No         | Device carrier
| ct           | Bool   | No         | Device connection type
| country      | Bool   | No         | Device country
| city      | Bool   | No         | Device city

Select

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| date         | Bool   | No         | Date
| price         | Object   | No         | Price
| size         | Object   | No         | Size

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
        "os": false,
        "type": false,
        "vendor": false,
        "model": false,
        "carrier": false,
        "ct": false,
        "country": false,
        "city": false
    },
    "select": {
        "date": true,
        "price": {"on": true, "fn": "sum"},
        "size": {"on": true, "sizes": ["...id"]}
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
                13,
                13,
                13
            ],
            [
                "1006458",
                "Clean Master- Space Cleaner and Antivirus",
                "com.cleanmaster.mguard",
                "2018-05-09",
                1,
                1,
                1
            ]
        ]
    }
}
```