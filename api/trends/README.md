# Trends API
* [Overview](#overview)
* [Applications](#applications)
* [Sites](#sites)
* [Formats](#formats)
* [Device](#device)

## Overview
### Ssp
Trends are something that is popular inside the Xendiz Marketplace right now. Open this traffic and increase your trading volumes.
### Dsp
Trading volumes and prices for the most popular traffic in real time. Set up your campaigns based on data.

This section's methods main purpose - is to provide you data about trends on our platform
All of methods are more or less self-descriptive:
- If you want to get data on trending applications then you should use first method.
- Second method is used when you want to get trends on sites.
- Third method will provide you with data on what ad types are popular right now.
- Fourth method will show you which platforms are currently trending.
- Last method is used when you want to generate custom trends report
  - First three parameters are send via URL and duplicate first three parameters for financial report:
    - First parameter is `from` and it is used to set beginning of date interval in format `YYYY-MM-DD`. If not set then date for current day will be used.
    - Second parameter is `to` and it is used to set end of date interval in format `YYYY-MM-DD`. If not set then date for current day will be used.

  - Next parameters are sent via body of POST request:
    - AdType is a parameter that describes platform that you want to do research for (site or application).
    - Platform is an object that describes which platform-specific parameters you want to include to your report. All of it's fields are boolean-typed.
    - Device is an object that describes which device-specific parameters you want to include to your report.  All of it's fields are boolean-typed.
    - Select is an object that describes fields that you want to group by and select for your report.
      - Almost all of it's parameters are boolean, exept for `price` - it's an object than has two fields: boolean flag which is used to add or remove this option from selection and second string-based one which describes function with which you want to aggregate your price by.
      


## Applications
`GET` /trends/app

Get the most trading applications.

Response:
```json
[{
  "app": {
    "bundle": "com.enflick.android.TextNow",
    "os": "android",
    "name": "TextNow - free text + calls",
    "price": 0,
    "score": 4.4,
    "store_url": "https://play.google.com/store/apps/details?id=com.enflick.android.TextNow",
    "icon_url": "//lh4.ggpht.com/nrNrI-mpolozU8SGzXEyZDRZvd2lsujq-2fbAhPT5ZK_H5P29rk4DNINhZCiJx9c8so0=w300"
  },
  "median_bidfloor": 0.12,
  "median_bidprice": 1.2,
  "imps_available": 129001211
}, {
  "app": {
    "bundle": "635896473",
    "os": "ios",
    "name": "ASKfm: Ask Anonymous Questions 12+",
    "price": 0,
    "score": 4,
    "store_url": "https://itunes.apple.com/us/app/askfm-ask-anonymous-question/id635896473?mt=8&uo=4",
    "icon_url": "http://is1.mzstatic.com/image/thumb/Purple128/v4/5b/28/32/5b2832b4-655e-a54e-1b74-2d9820086083/source/512x512bb.jpg"
  },
  "median_bidfloor": 0.281,
  "median_bidprice": 0.94,
  "imps_available": 12345321
}]
```

## Sites
`GET` /trends/site

Get the most trading web sites.

Response:
```json
[{
  "domain": "liberoquotidiano.it",
  "median_bidfloor": 0.12,
  "median_bidprice": 0.77,
  "imps_available": 129001211
}, {
  "domain": "msn.com",
  "median_bidfloor": 0.84,
  "median_bidprice": 2.2,
  "imps_available": 12345321
}]
```

## Formats
`GET` /trends/format

Get the most trading ad formats.

Response:
```json
[{
  "btype": "banner",
  "ptype": "app",
  "size": [300, 250],
  "geo": "USA",
  "median_bidfloor": 0.32,
  "median_bidprice": 0.45,
  "imps_available": 12345321,
  "position": 1
}]
```

## Device
`GET` /trends/device

Get the most trading devices.

Response:
```json
[{
  "vendor": "apple",
  "model": "iphone",
  "os": "ios",
  "connection_type": 3,
  "median_bidfloor": 0.32,
  "median_bidprice": 0.45,
  "imps_available": 12345321
}]
```

## Custom
`POST` /trends/custom

Get custom trends report.

**Difference between dates shouldn't be greater than 1 month**  
* Date fields `from` and `to` must be in format `YYYY-MM-DD`


Query params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| from         | Date   | No        | Start date. If not set then current day will be chosen. Example: `&from=2018-01-01`
| to           | Date   | No         | End date. Example: `&to=2018-01-10`

**Date difference between from and to must be lesser than month**

Body Params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| adtype       | Object | No         | Adv object
| platform     | Object | No         | Platform Object
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
