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
- Last method will show you which platforms are currently trending.

## Applications
Get the most trading applications.

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
