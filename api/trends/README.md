# Trends API
* [Overview](#overview)
* [Applications](#applications)
* [Sites](#sites)
* [Formats](#formats)
* [Device](#device)

## Overview
This section's methods main purpose - is to provide you data about trends on Xendiz platform.
### Ssp
Trends are something that is popular inside the Xendiz Marketplace right now. Open this traffic and increase your trading volumes.
### Dsp
Trading volumes and prices for the most popular traffic in real time. Set up your campaigns based on data.<br>

## Applications
Get data on trending applications then you should use first method.

`GET` /trends/app
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
Get the most trading web sites.

`GET` /trends/site
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
Get the most trading ad formats.

`GET` /trends/format
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
Get the most trading devices.

`GET` /trends/device
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
Generate custom trends report 
`POST` /trends/custom

Query params

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| from         | Date   | No         | Set beginning of date interval in format `YYYY-MM-DD`. If not set then date for current day will be used. Example: `&from=2018-01-01`
| to           | Date   | No         | End date. Example: `&to=2018-01-10`

Body Params<br>
All of it's fields are boolean-typed.

| Name         | Type   | isRequired | Description   |
| -------------| ------ | ---------- | ------------- |
| adtype       | Object | No         | Describes platform that you want to do research for (site or application). 
| platform     | Object | No         | Describes which platform-specific parameters you want to include to your report.
| device       | Object | No         | Describes which device-specific parameters you want to include to your report.
| select       | Object | No         | Describes fields that you want to group by and select for your report.

Adtype object

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
    "adtype": {
      "app": true,
      "site": false
    },
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
