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
Trading volumes and prices for the most popular traffic in real time. Set up your campaigns based on data.

## Applications
`GET` /trends/app
Get data on trending applications then you should use first method.

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
Generate custom trends report 
`POST` /trends/custom

Get custom trends report.
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
            "sizes": ["728x90"]
        },
        "campaign": true,
        "creative": false,
        "category": false,
        "price": {
            "on": false,
            "value": "median"
        }
    }
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
            "Impressions"
        ],
        "data": [
            [
                "Ethernet",
                "RUS",
                "2018-03-20",
                "crid",
                "2.32M"
            ],
            []
        ]
    }
}
```
