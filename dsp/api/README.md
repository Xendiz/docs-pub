# Xendiz DSP API

## Endpoint
```bash
https://dsp-front-1.xendiz.com
```

# Xendiz DSP API

## Overview
  * [Auth](#auth)
  * [Dashboard](#dashboard)
    * [List top os](#top-os)
    * [List top geo](#top-geo)
    * [List top apps](#top-apps)
    * [List top spend](#top-spend)
  * [Manage accounts](#accounts)
    * [Get account info](#get)
    * [Create new account](#create)
    * [Update account info](#update)
  * [Manage transactions](#accounts-transactions)
    * [Get account transactions list](#list)
  * [Manage campaigns](#campaigns)
    * [Get account's campaigns list](#list-1)
    * [Get account's campaigns tiny list](#tiny-list)
    * [Enable campaign](#enable)
    * [Disable campaign](#disable)
    * [Get campaign info](#get-1)
    * [Get linked creatives list for campaign](#creatives-list)
    * [Create new campaign](#create-1)
    * [Create campaign's copy](#make-copy)
    * [Update campaign](#update-1)
    * [Archive campaign](#archive)
    * [Unarchive campaign](#unarchive)
    * [Link creatives to campaign](#link)
    * [Unlink creatives from campaign](#unlink)
  * [Manage creatives](#creatives)
    * [Get account's creatives list](#list-2)
    * [Get account's creatives tiny list](#tiny-list-1)
    * [Get creative info](#get-2)
    * [Create new tag creative](#create-tag)
    * [Create new banner creative](#create-banner)
    * [Create new video creative](#create-video)
    * [Update tag creative](#update-2)
    * [Update banner](#update-banner)
    * [Update video](#update-video)
    * [Disable creative](#disable-1)
    * [Archive creative](#archive-1)
    * [Unarchive creative](#unarchive-1)
    * [Delete creative](#delete)
    * [Link creative to campaigns](#link-1)
    * [Unlink creative from campaigns](#unlink-1)
  * [User lists management](#lists)
    * [Get all lists](#get-all-account-lists)
    * [Create new list](#create-new-list)
    * [Work with list in bulk](#bulk-work)
    * [Update list name](#update-list)
    * [Delete list](#delete-list)
    * [Delete list entries](#delete-entry)
  * Availables
    * [OS](#available-os)
    * [Creative size](#available-sizes)
    * [ISP](#available-isp)
    * [City](#available-cities)
  * Reports
    * [Financial](#financial)
    * [Custom](#custom-report)
    * [Inventory Overview](#inventory-overview)

## Auth
`POST` /auth

Authorization on Xendiz DSP  

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
            "companyName": "Demo",
            "username": "test",
            "name": "Name Surname",
            "apiKey": "123",
            "balance": 100.5,
            "spendToday": 0,
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

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 403          | Invalid username or password | Wrong username or password
| 403          | Account deactivated          |Account with provided credentials has been deactivated

## Dashboard
### Top Os
`GET` /top/os

* Date fields `from` and `to` must be in format `YYYY-MM-DD`

Query params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| from         | Date | No         | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date | No         | End date. Example: `&to=2018-01-10`
| campId       | Int  | No         | Specific campaign id. If the param is not specified, a full report will be created for all the campaigns. Example: `&campId=21`
| cridId       | Int  | No         | Specific creative id. If the param is not specified, a full report will be created for all the creatives. Example: `&cridId=21`

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
| campId       | Int  | No         | Specific campaign id. If the param is not specified, a full report will be created for all the campaigns. Example: `&campId=21`
| cridId       | Int  | No         | Specific creative id. If the param is not specified, a full report will be created for all the creatives. Example: `&cridId=21`

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
| campId       | Int  | No         | Specific campaign id. If the param is not specified, a full report will be created for all the campaigns. Example: `&campId=21`
| cridId       | Int  | No         | Specific creative id. If the param is not specified, a full report will be created for all the creatives. Example: `&cridId=21`

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
                "storeUrl": "https://play.google.com/store/apps/details?id=com.outfit7.mytalkingtomfree&hl=en&gl=us",
                "iconUrl": "https://lh3.googleusercontent.com/3s2Ll-HtFiscV33KBhqJj5IOPAUi9XN_TiNZLV1jWHYJZFeLDrwie_lw4HwFCek26g"
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
| campId       | Int  | No         | Specific campaign id. If the param is not specified, a full report will be created for all the campaigns. Example: `&campId=21`
| cridId       | Int  | No         | Specific creative id. If the param is not specified, a full report will be created for all the creatives. Example: `&cridId=21`

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

Sign Up on Xendiz DSP  

Body params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| firstName    | String | No       | Users's first name
| lastName     | String | No       | User's last name
| companyName  | String | No       | User's company name  
| username     | String | Yes      | Username
| password     | String | Yes      | Preferrable password        
| email        | String | Yes      | User's email
| country      | String | No       | User's county in ISO-3166-1-alpha-3 format e.g `EST for Estonia`


Request:
```json
{
    "firstName": "first",
    "lastName": "last",
    "companyName": "Xendiz",
    "username": "test",
    "password": "test123",
    "email": "email@test.com",
    "country": "EST"
}
```

Response:
* Status code 200

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 400          | Missing one or more required fields | Request missing one or more of following fields: `firstName`, `lastName`, `password`
| 400          | Missing login information           | Request should at least have `email` property filled
| 400          | Account with provided email or username already exists | As stated in message

## Accounts
### Get
`GET` /accounts/me

Get data about currently logged in account  

Response:
```json
{
    "data": {
        "id": 1,
        "status": 1,
        "companyName": "Demo",
        "username": "demo",
        "name": "Dima Shirokov",
        "email": "email@xendiz.com",
        "country": "EST",
        "apiKey": "us-east-1.mgmuqofj9m0zwch257b9",
        "balance": 337.404,
        "spendToday": 0,
        "defaults": null,
        "regId": null,
        "timestamp": "2018-01-13T06:14:36.000Z"
    }
}
```

### Create
`POST` /accounts

Create new account  
* Note that you need to relogin to update created account data or act on it's behalf

Body params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| companyName  | String | No       | Account's company name
| name         | String | No       | Account's name
| username     | String | No       | Account's username that will be used to log in  
| password     | String | Yes      | Account's password
| email        | String | Yes      | Account's email
| country      | String | No       | User's county in ISO-3166-1-alpha-3 format e.g `EST for Estonia`

Request:
```json
{
    "companyName": "Demo",
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
        "apiKey": "49c2e273d075a1031c7600a20fcdbff8",
        "balance": 0,
        "spendToday": 0,
        "id": 3,
        "companyName": "Demo",
        "name": "DEM",
        "username": "test",
        "email": "mail@domain.com",
        "country": "UKR"
    }
}
```

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 400          | Missing one or more required fields | Request missing one or more of following fields: `company_name`, `name`, `username`, `password`

### Update

`PUT` /accounts

Update data of currently logged in account  

Body params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| companyName  | String | No       | Account's company name
| name         | String | No       | Account's name
| username     | String | No       | Account's username that will be used to log in  
| password     | String | Yes      | Account's password
| email        | String | Yes      | Account's email
| country      | String | No       | User's county in ISO-3166-1-alpha-3 format e.g `EST for Estonia`

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

Get list of transactions on this account  

Response:
```json
{
    "data": [
        {
            "id": 32,
            "accountId": 1,
            "orderId": 39,
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

Get list of this account's campaigns  

Query params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| all          | Int  | No         | Toggle to show or don't show archived campaigns

Response:
```json
{
    "data": [
        {
            "id": 2,
            "accountId": 2,
            "name": "test2",
            "labels": "",
            "status": 1,
            "adomain": "google.com",
            "bundle": null,
            "clickUrl": "http://google.com",
            "minCpm": 0.8,
            "maxCpm": 2,
            "dailyBudget": 100,
            "totalBudget": 1000,
            "spendToday": 100,
            "spendTotal": 1000,
            "clicksToday": 4347005,
            "clicksTotal": 4347113,
            "impsToday": 217743548,
            "impsTotal": 217773778,
            "impFrequency": 10,
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
            "startDate": "2018-04-10",
            "endDate": null,
            "timestamp": "2017-11-14T15:20:44.000Z"
        }
    ]
}
```

### Tiny List
`GET` /campaigns/tiny[?all=1]

Get minified version (id and name) of this account's campaigns

Query params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| all          | Int  | No         | Toggle to show or dont show archived campaigns

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

Enable campaign

Response:
* STATUS CODE 204

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 403          | Campaign unavailable    | Currently logged in account doesn't have access to campaign with provided id
| 400          | Archived campaign cannot be enabled | You can't set archived campaign active

### Disable
`PUT` /campaigns/`:id`/disable

Disable campaign  

Response:
* STATUS CODE 204

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 403          | Campaign unavailable    | Currently logged in account doesn't have access to campaign with provided id

### Get

`GET` /campaigns/:id

Get data about campaign  

Response:
```json
{
    "data": {
        "id": 45,
        "accountId": 1,
        "name": "test",
        "labels": "lorem,ipsum",
        "status": 1,
        "adomain": "google.com",
        "bundle": null,
        "clickUrl": "http://google.com",
        "minCpm": 1,
        "maxCpm": 5,
        "dailyBudget": 100,
        "totalBudget": 1000,
        "spendToday": 0,
        "spendTotal": 0,
        "clicksToday": 0,
        "clicksTotal": 0,
        "impsToday": 0,
        "impsTotal": 0,
        "impFrequency": 3,
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
        "startDate": "2018-04-10",
        "endDate": "2018-04-15",
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
                "name": "android",
                "max": 6,
                "min": 1
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

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 403          | Campaign unavailable    | Currently logged in account doesn't have access to campaign with provided id

### Creatives list

`GET` /campaigns/:id/creatives

Get creatives list for campaign  

Response:
```json
{
    "id": 1,
    "creatives": [
        {
            "id": 62,
            "name": "banner 728x90",
            "source": "http://res.cloudinary.com/xendiz-com/image/upload/c_fill,h_90,w_728/bhwjvoycmw14rix9g3ii",
            "type": "banner",
            "size": {
                "id": 4,
                "code": "728x90"
            }
        }
    ]
}
```

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 403          | Campaign unavailable    | Currently logged in account doesn't have access to campaign with provided id

### Create

`POST` /campaigns

Create new campaign  

Body params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| name             | String | Yes       | Campaign's name
| status           | Int    | Yes       | Set if campaign will be active right after creation
| labels           | String | Yes       | Optional field used for campaign search and grouping
| adomain          | String | Yes       | Advertiser's domain
| bundle           | String | Yes       | 
| clickUrl         | String | Yes       | Campaign's redirect url
| minCpm           | Int    | Yes       | Minimal CPM value
| maxCpm           | Int    | Yes       | Maximal CPM value
| dailyBudget      | Int    | Yes       | Daily campaign's budget
| totalBudget      | Int    | Yes       | Total campaign's budget
| impFrequency     | Int    | Yes       | The number of times (frequency) a specific visitor to a website/application is shown a particular advertisement
| inventory        | Object | Yes       | Campaign's inventory targeting settings
| device           | Object | Yes       | Campaign's device targeting settings
| connection       | Object | Yes       | Campaign's connection targeting settings
| startDate        | Date   | Yes       | Campaign's start date in `YYYY-MM-DD` format
| endDate          | Date   | Yes       | Campaign's end date in `YYYY-MM-DD` format
| classifications  | Array  | Yes       | Campaign's classification in format specified by IAB OpenRTB specification (List 5.1)
| categories       | Array  | Yes       | Campaign's targeting categories in format specified by IAB OpenRTB specification (List 5.1)
| countries        | Array  | Yes       | Campaign's country targeting
| cities           | Array  | Yes       | Campaign's city targeting in format of array of integers. Cities ID's you can fetch via [this](#available-isp) route
| isps             | Array  | Yes       | Campaign's ISP targeting in format of array of integers. ISP ID's you can fetch via [this](#available-cities) route
| blockedBundles   | Array  | Yes       | Blacklist of bundles formatted as array of bundle names
| blockedDomains   | Array  | Yes       | Blacklist of domains formatted as array of domain names
| blockedPublishers| Array  | Yes       | Blacklist of publishers formatted as array of publisher ids
| allowedDomains   | Array  | Yes       | Whitelist of domains formatted as array of domain names
| allowedBundles   | Array  | Yes       | Whitelist of bundles formatted as array of bundle names
| languages        | Array  | Yes       | Campaign's language targeting formatted as array of ISO 639-1 Code formatted strings
| os               | Array  | Yes       | Array of objects that describe campaign OS targeting
| schedules        | Array  | Yes       | Array of objects that describe campaign scheduling

Inventory object

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| web          | Bool | Yes        | Enable web traffic targeting
| inapp        | Bool | Yes        | Enable in-app traffic targeting

Device object

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| phone        | Bool | Yes        | Enable phone devices targeting
| tablet       | Bool | Yes        | Enable tablet devices targeting
| desktop      | Bool | Yes        | Enable desktop devices targeting
| other        | Bool | Yes        | Enable targeting on devices types that differ from three mentioned above

Inventory object

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| wifi         | Bool | Yes        | Enable targeting to devices that are connected to internet via wifi network
| cellular     | Bool | Yes        | Enable targeting to devices that are connected to internet via cellular network
| other        | Bool | Yes        | Enable targeting to devices that are connected to internet via other means

OS object

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| name         | String | Yes      | Campaign's targeting os name
| min          | Int    | Yes      | Minimal OS version
| max          | Int    | Yes      | Maximal OS version

Schedule object

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| day          | Int   | Yes       | Campaign's enable week day where 1 is Monday, 2 is Tuesday etc.
| hours        | Array | Yes       | Array of hours in which campaing will be active where 0 is 00:00 and 23 is 23:00



Request:
```json
{
    "name": "123",
    "status": 1,
    "labels": "123,321",
    "adomain": "google.com",
    "bundle": null,
    "clickUrl": "http://google.com",
    "minCpm": 1,
    "maxCpm": 5,
    "dailyBudget": 100,
    "totalBudget": 1000,
    "impFrequency": 3,
    "inventory": { "web": true, "inapp": true },
    "device": { "phone": true, "tablet": true, "desktop": true, "other": false },
    "connection": { "wifi": true, "cellular": true, "other": true },
    "startDate": "2018-04-10",
    "endDate": "2018-04-15",
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
    "os": [{"name": "ios", "min": 1, "max": 11}],
    "schedules": [{"day": 3, "hours": [0, 1, 3, 4, 5, 10, 15, 20, 21, 22, 23]}]
}
```

Response:
```json
{
    "data": {
        "spendTotal": 0,
        "clicksTotal": 0,
        "impsTotal": 0,
        "id": 46,
        "accountId": 1,
        "name": "123",
        "labels": "123,321",
        "status": 1,
        "adomain": "google.com",
        "bundle": null,
        "clickUrl": "http://google.com",
        "minCpm": 1,
        "maxCpm": 5,
        "dailyBudget": 100,
        "totalBudget": 1000,
        "impFrequency": 3,
        "inventory": "{\"web\":true,\"inapp\":true}",
        "device": "{\"phone\":true,\"tablet\":true,\"desktop\":true,\"other\":false}",
        "connection": "{\"wifi\":true,\"cellular\":true,\"other\":true}",
        "startDate": "2018-04-10",
        "endDate": "2018-04-15"
    }
}
```

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 400          | Budget preferences must be a number | Fields `daily_budget` and `total_budget` should be provided as numbers
| 400          | Budged preferences should be greater than 0 | Fields `daily_budget` and `total_budget` should be greated than 0
| 400          | Campaign should have name | Field `name` is required
| 400          | Missing campaign urls | Fields `adomain` and `click_url` are required
| 400          | Missing min/max cpm preferences | Fields `min_cpm` and `max_cpm` are required
| 400          | Missing campaign settings objects | Fields `inventory`, `connection` and `device` are required
| 400          | Validation Error: Wrong object format | Fields `inventory`, `connection` and `device` must be compiled as described above
| 400          | You provided doubling or unexisting entries | Request fields `cities` and `isps` are expected to be arrays of unique ids that you can get [here](#available-cities) and [here](#available-isp) respectively

### Make Copy

`GET` /campaigns/`:id`/copy

Makes campaign's copy  

Response:
```json
{
    "data": {
        "archived": 0,
        "spendToday": 0,
        "spendTotal": 0,
        "clicksToday": 0,
        "clicksTotal": 0,
        "impsToday": 0,
        "impsTotal": 0,
        "id": 0,
        "accountId": 2,
        "name": "test copy",
        "labels": "lorem,ipsum",
        "status": 0,
        "adomain": "google.com",
        "bundle": null,
        "clickUrl": "http://google.com",
        "minCpm": 1,
        "maxCpm": 5,
        "dailyBudget": 100,
        "totalBudget": 1000,
        "impFrequency": 3,
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
        "startDate": "2018-06-22",
        "endDate": null
    }
}
```

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 403          | Campaign unavailable    | Currently logged in account doesn't have access to campaign with provided id

### Update

`PUT` /campaigns/:id

Update campaign

Body params

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| name             | String | Yes       | Campaign's name
| status           | Int    | Yes       | Set if campaign will be active right after creation
| labels           | String | No        | Optional field used for campaign search and grouping
| adomain          | String | Yes       | Advertiser's domain
| bundle           | String | No        | 
| clickUrl         | String | Yes       | Campaign's redirect url
| minCpm           | Int    | Yes       | Minimal CPM value
| maxCpm           | Int    | Yes       | Maximal CPM value
| dailyBudget      | Int    | Yes       | Daily campaign's budget
| totalBudget      | Int    | Yes       | The number of times (frequency) a specific visitor to a website/application is shown a particular advertisement
| impFrequency     | Int    | Yes       | Campaign's impressions frequency
| inventory        | Object | Yes       | Campaign's inventory targeting settings
| device           | Object | Yes       | Campaign's device targeting settings
| connection       | Object | Yes       | Campaign's connection targeting settings
| startDate        | Date   | Yes       | Campaign's start date in `YYYY-MM-DD` format
| endDate          | Date   | Yes       | Campaign's end date in `YYYY-MM-DD` format
| classifications  | Array  | Yes       | Campaign's classification in format specified by IAB OpenRTB specification (List 5.1)
| categories       | Array  | Yes       | Campaign's targeting categories in format specified by IAB OpenRTB specification (List 5.1)
| countries        | Array  | Yes       | Campaign's country targeting
| cities           | Array  | Yes       | Campaign's city targeting in format of array of integers. Cities ID's you can fetch via [this](#available-isp) route
| isps             | Array  | Yes       | Campaign's ISP targeting in format of array of integers. ISP ID's you can fetch via [this](#available-cities) route
| blockedBundles   | Array  | Yes       | Blacklist of bundles in format of array of bundle names
| blockedDomains   | Array  | Yes       | Blacklist of domains in format of array of domain names
| blockedPublishers| Array  | Yes       | Blacklist of publishers in format of array of publisher ids
| allowedDomains   | Array  | Yes       | Whitelist of domains in format of array of domain names
| allowedBundles   | Array  | Yes       | Whitelist of bundles in format of array of bundle names
| languages        | Array  | Yes       | Campaign's language targeting in format of array of ISO 639-1 Code formatted strings
| os               | Array  | Yes       | Array of objects that describe campaign OS targeting
| schedules        | Array  | Yes       | Array of objects that describe campaign scheduling

Inventory object

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| web          | Bool | Yes        | Enable Web traffic
| inapp        | Bool | Yes        | Enable In-App traffic

Device object

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| phone        | Bool | Yes        | Enable phone devices targeting
| tablet       | Bool | Yes        | Enable tablet devices targeting
| desktop      | Bool | Yes        | Enable desktop devices targeting
| other        | Bool | Yes        | Enable targeting on devices that differ from three mentioned above

Inventory object

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| wifi         | Bool | Yes        | Enable targeting to devices that are connected to internet via wifi network
| cellular     | Bool | Yes        | Enable targeting to devices that are connected to internet via cellular network
| other        | Bool | Yes        | Enable targeting to devices that are connected to internet via other means

OS object

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| name      | String | Yes        | Campaign's targeting os name
| min       | Int    | Yes        | Minimal OS version
| max       | Int    | Yes        | Maximal OS version

Schedule object

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| day          | Int   | Yes       | Campaign's enable week day where 1 is Monday, 2 is Tuesday etc.
| hours        | Array | Yes       | Array of hours in which campaing will be active where 0 is 00:00 and 23 is 23:00

Request:
```json
{
    "name": "test",
    "labels": "lorem,ipsum",
    "adomain": "google.com",
    "bundle": null,
    "clickUrl": "http://google.com",
    "minCpm": 1,
    "maxCpm": 5,
    "dailyBudget": 100,
    "totalBudget": 1000,
    "impFrequency": 3,
    "inventory": { "web": true, "inapp": true },
    "device": { "phone": true, "tablet": true, "desktop": true, "other": false },
    "connection": { "wifi": true, "cellular": true, "other": true },
    "startDate": "2018-04-10",
    "endDate": "2018-04-15",
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
    "os": [{"name": "ios", "min": 1, "max": 11}],
    "schedules": [{"day": 3, "hours": [0, 1, 3, 4, 5, 10, 15, 20, 21, 22, 23]}]
}
```

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 403          | Campaign unavailable    | Currently logged in account doesn't have access to campaign with provided id
| 400          | You provided doubling or unexisting entries | Request fields `cities` and `isps` are expected to be arrays of unique ids that you can get [here](#available-cities) and [here](#available-isp) respectively

Response:
* STATUS CODE 204

### Archive

`PUT` /campaigns/:id/archive

Archive campaign

Response:
* STATUS CODE 204

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 403          | Campaign unavailable    | Currently logged in account doesn't have access to campaign with provided id
| 400          | Cannot archive enabled campaign    | As stated in message

### Unarchive

`PUT` /campaigns/:id/unarchive

Unarchive campaign

Respinse:
* STATUS CODE 204

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 403          | Campaign unavailable    | Currently logged in account doesn't have access to campaign with provided id

### Link

`PUT` /campaigns/:id/link

Link creatives to campaign

Body parameters

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| creatives    | Array| Yes        | Array of creative objects

Creative object

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| id           | Int  | Yes        | Creative ID
| order        | Int  | Yes        | 

Request: 
```json
{
    "creatives": [
        { "id": 1, "order": 0  },
        { "id": 2, "order": 0  },
        { "id": 3, "order": 0  },
        { "id": 4, "order": 0  }
    ]
}
```

Response:
* STATUS CODE 204

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 403          | Campaign unavailable    | Currently logged in account doesn't have access to campaign with provided id
| 400          | Creatives array missing | Crid is required to be in request and must be an array
| 400          | Creatives array is empty | Crids array should have at least one valid entry
| 400          | You provided doubling or unexisting entries | `id` property of each object should be unique and lead to existing creative

### Unlink

`PUT` /campaigns/:id/unlink

Unlink creatives from campaign

Body parameters

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| creatives    | Array| Yes        | Array of creative IDs as numbers

Request: 
```json
{
    "creatives": [1,2,3,4]
}
```
Response:
* STATUS CODE 204

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 403          | Campaign unavailable    | Currently logged in account doesn't have access to campaign with provided id
| 400          | Creatives array missing | Crid is required to be in request and must be an array
| 400          | Creatives array is empty | Crids array should have at least one valid entry

## Creatives
### List

`GET` /creatives/list[?all=1&adType=(tag|video|banner)]

Get this account's creatives list  

Query parameters

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| all          | Int  | No         | Toggle to show archived creatives. Defaults to 0
| adType       | String | No         | Select which creative type to show. This URL parameter supports multiple, comma separated, types entry e.g `&type=video,banner,tag`

Response:
```json
{
    "data": [
        {
            "id": 132,
            "hashedId": "fde1d6e00",
            "status": 1,
            "archived": 0,
            "approved": 1,
            "name": "test_post_new_banners",
            "isSecure": 1,
            "timestamp": "2018-06-19T10:43:39.000Z",
            "accountId": 2,
            "type": "banner",
            "size": {
                "id": 2,
                "code": "300x250"
            },
            "campaigns": [
                {
                    "id": 70,
                    "name": "dsad",
                    "spendToday": 0
                }
            ]
        }
    ]
}
```

### Tiny List

`GET` /creatives/tiny[?source=1&size=1&type=1&all=1&adType=(tag|video|banner)]

Get minified version of this account's creatives list

Query parameters

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| source       | Int  | No         | Toggle to add creative source to response. Defaults to 0
| size         | Int  | No         | Toggle to add creative size to response. Defaults to 0
| type         | Int  | No         | Toggle to add creative type to response. Defaults to 0
| all          | Int  | No         | Toggle to add archived creatives to response. Defaults to 0
| adType       | String | No       | Select which creative type to show. This URL parameter supports multiple, comma separated, types entry e.g `&type=video,banner,tag`

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

Get data about creative  
* Second example is for video creatives  

Response:
```json
{
    "data": {
        "id": 151,
        "hashedId": "a457a3302",
        "status": 1,
        "archived": 0,
        "approved": 0,
        "name": "qwerty2",
        "isSecure": 1,
        "timestamp": "2018-06-27T07:20:27.000Z",
        "accountId": 2,
        "type": "tag",
        "source": "<h1>Lorem Ipsum Dolor Sit Amet</h1>",
        "size": {
            "id": 2,
            "code": "300x250"
        }
    }
}
```

```json
{
    "data": {
        "id": 1,
        "hashedId": "f7edbfd8a",
        "status": 1,
        "archived": 0,
        "approved": 0,
        "name": "erw",
        "isSecure": 1,
        "timestamp": "2018-08-29T12:00:58.000Z",
        "accountId": 2,
        "type": "video",
        "source": "URL-to-video",
        "size": {
            "id": 0,
            "code": "0x0"
        },
        "assets": [
            {
                "name": "test",
                "id": 1,
                "source": "URL-to-asset",
                "type": "companion",
                "size": {
                    "id": 2,
                    "code": "300x250"
                }
            }
        ]
    }
}
```

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 400          | Specified creative does no exist or you don't have access to it | As stated by message

### Create tag

`POST` /creatives

Create creative with `tag` type

Body parameters

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| campaigns    | Array  | No       | Array of campaign IDs to link this creative to
| name         | String | No       | Creative name. If not set then generated based on creative data
| source       | String | Yes      | Creative source code
| isSecure     | Int    | Yes      | 
| size         | String | Yes      | Creative size code. You can get it [here](#available-sizes)


Request:
```json
{
    "campaigns": [16,17],
    "name": "asdf",
    "source": "<h1 style=\"background-color: red; padding: 15px;\"><a href=\"http://google.com\" target=\"_blank\">Google</a></h1>",
    "isSecure": 1,
    "size": "320x50"
}
```

Response:
```json
{
    "data": {
        "status": 0,
        "archived": 0,
        "approved": 0,
        "isSecure": 0,
        "id": 237,
        "name": "demo",
        "type": "tag",
        "source": "<h1 style=\"background-color: red; padding: 15px;\"><a href=\"http://google.com\" target=\"_blank\">Google</a></h1>",
        "accountId": 2,
        "hashedId": "31613a26f",
        "campaigns": [
            {
                "id": 53,
                "name": "test"
            },
            {
                "id": 65,
                "name": "Qwerty"
            }
        ],
        "size": {
            "id": 1,
            "code": "320x50"
        }
    }
}
```

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 400          | Invalid size | You provided size code that isn't supported in Xendiz DSP
| 400          | You provided doubling or unexisting entries | Request field `campaigns` is expected to be array of unique ids that lead to existing campaign


### Create banner

`POST` /creatives/banner<br>

Create new creative with `banner` type

Body parameters

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| campaigns    | Array  | No       | Array of campaign IDs to link this creative to
| name         | String | No       | Creative name. If not set then generated based on creative data
| source       | File   | Yes      | Banner image
| size         | String | Yes      | Creative size code. You can get it [here](#available-sizes)

Request:
```json
{   
    "name": "somename",
    "campaigns": [16,17],
    "source": "file",
    "size": "320x50"
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
        "accountId": 2,
        "isSecure": 1,
        "hashedId": "7c01f4189",
        "campaigns": [
            {
                "id": 16,
                "name": "name"
            }
        ],
        "size": {
            "id": 2,
            "code": "300x250"
        }
    }
}
```

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 400          | Missing image data | File is requeired in request
| 400          | Invalid size | You provided size code that isn't supported in Xendiz DSP
| 400          | You provided doubling or unexisting entries | Request field `campaigns` is expected to be array of unique ids that lead to existing campaign

### Create video

`POST` /creatives/video

Create new creative with `video` type

Body parameters

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| campaigns    | Array  | No       | Array of campaign IDs to link this creative to
| name         | String | No       | Creative name. If not set then generated based on creative data
| source       | File   | Yes      | Video file
| assets       | Array  | Yes      | Array of objects that describes video companion ads

Assets object  

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| id           | Int  | Yes        | Banner ID to attach as companion
| type         | String | Yes      | Companion type. Currently only `companion` type supported

Request:
```json
{
    "source": "file",
    "name": "Test",
    "assets": "[{id: \"1\", type: \"companion\"}]",
    "campaigns": "[1,2,3,4]"
}
```

Response:
```json
{
    "data": {
        "status": 0,
        "archived": 0,
        "approved": 0,
        "isSecure": 1,
        "id": 1,
        "name": "123video",
        "accountId": 2,
        "type": "video",
        "hashedId": "1111111",
        "source": "URL-to-video",
        "size": {
            "id": 0,
            "code": "0x0"
        },
        "assets": [
            {
                "name": "test",
                "id": 1,
                "source": "URL-to-asset",
                "type": "companion",
                "size": {
                    "id": 2,
                    "code": "300x250"
                }
            }
        ],
        "campaigns": [
            {
                "id": 1,
                "name": "test"
            }
        ]
    }
}
```

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 400          | Missing video data | File is requeired in request
| 400          | Video should be shorter than 30s | Video ad duration is limited to 30 seconds
| 400          | You provided doubling or unexisting entries | Request fields `campaigns` and `assets` is expected to be array with unique ids that lead to existing entities

### Update

`PUT` /creatives/`:id/tag`

Update creative with `tag` type  

Body parameters

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| isSecure     | Int    | No       | 
| name         | String | No       | Creative name. If not set then generated based on creative data
| source       | String | No       | Creative source code

Request:
```json
{   
    "isSecure": 0,
    "name": "somename",
    "source": "<h1 style=\"background-color: red; padding: 15px;\">TAG</h1>"
}
```

Response:
* STATUS CODE 204

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 400          | Creative not found | Creative with provided id doesn't exist in Xendiz DSP

### Update banner

`PUT` /creatives/`:id`/banner

Update creative with `banner` type  

Body parameters

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| name         | String | No       | Creative name. If not set then generated based on creative data
| source       | File   | Yes      | New image

Request:
```json
{   
    "name": "somename",
    "source": "file",
    "size": "size_code"
}
```

Response:
* STATUS CODE 204

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 400          | Creative not found | Creative with provided id doesn't exist in Xendiz DSP
| 400          | Invalid size | You provided size code that isn't supported in Xendiz DSP

### Update video

`PUT` /creatives/`:id`/video

Update creative with `video` type  

Body parameters

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| name         | String | No       | Creative name. If not set then generated based on creative data
| source       | File   | No      | New video ad
| assets       | Array  | No      | Array of objects that describes video companion ads

Assets object  

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| id           | Int  | Yes        | Banner ID to attach as companion
| type         | String | Yes      | Companion type. Currently only `companion` type supported

Request:
```json
{
    "source": "file",
    "name": "Test",
    "assets": "[{id: \"1\", type: \"companion\"}]"
}
```

Response

* STATUS CODE 204

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 400          | Video should be shorter than 30s | Video ad duration is limited to 30 seconds
| 400          | You provided doubling or unexisting entries | Request fields `assets` is expected to be array of objects with unique ids that lead to existing entities

### Disable

`PUT` /creatives/`:id`/disable

Disable creative  

Response:
* STATUS CODE 200

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 400          | Creative not found | Creative with provided id doesn't exist in Xendiz DSP

### Archive

`PATCH` /creatives/`:id`/archive

Archive creative  

Response:
* STATUS CODE 200

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 400          | Creative not found | Creative with provided id doesn't exist in Xendiz DSP
| 400          | Cannot archive enabled creative | As stated in message

### Unarchive

Unarchive creative  

`PATCH` /creatives/`:id`/unarchive

Response:
* STATUS CODE 200

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 400          | Creative not found | Creative with provided id doesn't exist in Xendiz DSP

### Delete

`DELETE` /creatives/`:id`

Delete creative  

Response:
* STATUS CODE 204

### Link

`PUT` /creatives/:id/link

Link creative to provided campaigns

Body parameters

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| campaigns    | Array| Yes        | Array of campaign objects

Campaign object

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| id           | Int  | Yes        | Campaign ID
| order        | Int  | Yes        | Set to 0   

Request: 
```json
{
    "campaigns": [
        { "id": 1, "order": 0  },
        { "id": 2, "order": 0  },
        { "id": 3, "order": 0  },
        { "id": 4, "order": 0  }
    ]
}
```

Response:
* STATUS CODE 204

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 400          | Creative not found | Creative with provided id doesn't exist in Xendiz DSP
| 400          | Campaigns array missing | Cid is required to be in request and must be an array
| 400          | Campaigns array is empty | Cids array should have at least one valid entry
| 400          | You provided doubling or unexisting entries | `id` property of each object should be unique and lead to existing campaign


### Unlink

`PUT` /creatives/:id/unlink

Unlink creative from provided campaigns  

Body parameters

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| campaigns    | Array| Yes        | Array of campaign IDs


Request: 
```json
{
    "campaigns": [1,2,3,4]
}
```
Response:
* STATUS CODE 204

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 400          | Creative not found | Creative with provided id doesn't exist in Xendiz DSP
| 400          | Campaigns array missing | Cid is required to be in request and must be an array
| 400          | Campaigns array is empty | Cids array should have at least one valid entry

## Lists

### Get all account lists

`GET` /lists

Response:
```json
{
    "data": [
        {
            "id": 2,
            "name": "New List",
            "entries": [
                {
                    "id": 2,
                    "text": "This is testing entry"
                }
            ]
        },
        {
            "id": 3,
            "name": "New List",
            "entries": []
        },
        {
            "id": 4,
            "name": "New List",
            "entries": []
        }
    ]
}
```

### Create new list

`POST` /lists

Body parameters

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| name         | Array  | Yes        | New list name
| entries      | Object | Yes        | Array of entry objects

Creative object

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| text         | String | Yes        | Entry text

Request:
```json
{
  "name": "New List",
  "entries": [
    { "text": "Samp List creation text" },
    { "text": "Samp List creation text" },
    { "text": "Samp List creation text" },
    { "text": "Samp List creation text" },
    { "text": "Samp List creation text" },
    { "text": "Samp List creation text" }
  ]
}
```

Response:
```json
{
    "data": {
        "id": 13,
        "name": "New List",
        "entries": [
            {
                "id": 129,
                "text": "Samp List creation text"
            }
        ]
    }
}
```

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 400          | List name required | As stated in message


### Bulk work

`POST` /lists/`id`/bulk

Method to work with list entries in bulk mode.

Body parameters

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| data         | Array | Yes        | Array of entry objects

Body parameters

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| id           | Int    | Yes        | Entry ID. Set to 0 if this is new entry
| text         | String | Yes        | Entry text

Request:
```json
{
    "data": [
        {
            "id": 13,
            "text": "Bulk Sample text 13"
        },
        {
            "id": 14,
            "text": "Bulk Sample text 14"
        },
        {
            "id": 15,
            "text": "Bulk Sample text 15"
        },
        {
            "id": 0,
            "text": "Lorem Ipsum"
        },
        {
            "id": 0,
            "text": "Dolor Sit Amet"
        }
    ]
}
```

Response:
```json
{
    "data": [
        {
            "id": 18,
            "text": "Lorem Ipsum"
        },
        {
            "id": 19,
            "text": "Dolor Sit Amet"
        }
    ]
}
```

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 400          | Jobs array missing | Request property `data` should be present in request and be an array
| 400          | Jobs array empty | Request property `data` is empty or doesn't have any valid entries
| 400          | List not found   | List with provided id doesn't exist

### Update list

`PUT` /lists/`:id`

Body parameters

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| name         | String | Yes        | New list name

Request:
```json
{
    "name": "New Name"
}
```

Response:
* STATUS CODE 204

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 400          | List name required | As stated in message

### Delete list

`DELETE` /lists/`:id`

Response:
* STATUS CODE 204

### Delete entry

`DELETE` /lists/`:id`/entries

Delete list entries

Body parameters

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| entries      | Array | Yes        | Array of entry IDs to delete


Request: 
```json
{
    "entries": [2,13,14,15]
}
```

Response:
* STATUS CODE 204

## Available OS
### List

`GET` /available/os

Get list of all available OS names with minimal and maximal versions in Xendiz DSP

Response:
```json
{
    "data": [
        {
            "id": 1,
            "name": "android",
            "min": 0,
            "max": 0
        }
    ]
}
```

## Available sizes
### List

`GET` /available/sizes

Get list of all available sizes supported by Xendiz DSP

Response:
```json
{
    "data": [
        {
            "id": 1,
            "code": "320x50"
        }
    ]
}
```

## Available ISP

`GET` /available/isp

Get list of ISP names along with ID that match your provided string

Query parameters

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| query        | Array | Yes        | Word to search ISP by

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
| country      | String | Yes         | Country name in ISO-3166-1-alpha-3 format to search divided by `,`. Example: `&country=USA,UKR`
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

Possible error responses:

Each 4XX error response is provided with `message` property which describes error nature.

| Code         | Message      |Description   |
| -------------|------------- |------------- |
| 400          | Country name and city string search are required | Both `country` and `query` parameters are required

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
| allDay  | Int  | Yes         | Search on span of previous 24h if both `hour` and this field are selected.
| campId    | Int | Yes         | Add campaign id to report
| cridId  | Int  | Yes         | Add creative id to report

Search object

| Name         | Type | isRequired | Description   |
| -------------| ---- | ---------- | ------------- |
| from     | String | No         | Exact date to begin search from (e.g `2018-05-01`, defaults to today's date)
| to       | String  | No         | Exact date where search must stop (e.g `2018-05-02`, defaults to today's date)
| campId    | Int | No         | Search by specific campaign id
| cridId  | Int  | No         | Search by specific creative id


Example:

`POST` /financial

Request: 
```json
{
    "selection": {
        "date": 1, 
        "hour": 1,
        "allDay": 0,
        "campId": 1, 
        "cridId": 1
        
    },
    "search": {
        "from": "2018-05-01",
        "to": "2018-05-10",
        "campId": 1,
        "cridId": 2
    }
}
```

Response:
```json
{
    "data": {
        "fields": [
            "Date",
            "Hour of Day",
            "Campaign",
            "Creative",
            "impressions",
            "clicks",
            "CTR",
            "spend"
        ],
        "data": [
            [
                "2018-07-10",
                "0:00 UTC",
                "test (id3)",
                "Demo tag 320x480 (id3)",
                79290,
                1824,
                "2.30%",
                "$ 20.91"
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
        "campId": 1, 
        "cridId": 1
        
    },
    "search": {
        "from": "2018-05-01",
        "to": "2018-05-02",
        "campId": 2,
        "cridId": 4
    }
}
```

Response:

```json
{
    "data": {
        "fields": [
            "Date",
            "Hour of Day",
            "Campaign",
            "Creative",
            "impressions",
            "clicks",
            "CTR",
            "spend"
        ],
        "data": [
            [
                "2018-07-10",
                "0:00 UTC",
                "test (id3)",
                "Demo tag 320x480 (id3)",
                79290,
                1824,
                "2.30%",
                "$ 20.91"
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
| adpos        | Bool   | No         | Ad position

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
