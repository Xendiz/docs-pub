### Bid Request sample
```json
{
    "at": 2,
    "id": "SyeGTfQIrG",
    "tmax": 600,
    "cur": ["USD"],
    "badv": ["appsary.com", "township.com"],
    "bcat": ["IAB9-7", "IAB14-1", "IAB14-3", "IAB25", "IAB24", "IAB26"],
    "device": {
        "ip": "174.206.0.198",
        "os": "Android",
        "osv": "6.0.1",
        "make": "Motorola",
        "model": "XT1609",
        "devicetype": 4,
        "ua": "Mozilla/5.0 (Linux; Android 6.0.1; XT1609 Build/MPIS24.241-2.35-1-17; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/62.0.3202.73 Mobile Safari/537.36",
        "dnt": 0,
        "lmt": 0,
        "js": 1,
        "connectiontype": 6,
        "ifa": "b20388cd-d241-4c8b-8342-7c67543cd838",
        "dpidsha1": "3741eecc0269481072f4c7b24e013b3db187bd5c",
        "dpidmd5": "9eb2c6cf4d36fa4f56a7838e0341cfbf",
        "carrier": "Verizon Wireless",
        "geo": {
            "type": 2,
            "lat": 37.751,
            "lon": -97.822,
            "country": "USA",
            "metro": "0"
        }
    },
    "app": {
        "name": "Derived",
        "storeurl": "http://www.xapads.com/",
        "cat": ["IAB1"],
        "bundle": "com.app.xapads",
        "publisher": {
            "id": "der"
        },
        "id": "051996842e"
    },
    "imp": [{
        "id": "1",
        "bidfloorcur": "USD",
        "instl": 0,
        "tagid": "default",
        "banner": {
            "w": 320,
            "h": 50,
            "topframe": 1,
            "pos": 0
        },
        "bidfloor": 0.206
    }],
    "user": {
        "id": "1516806841.001.1bb1296aaaf30c0621a004acb26d25fb",
        "buyeruid": ""
    }
}
```

### Bid Response sample

```json
{
    "id":"SyeGTfQIrG",
    "seatbid": [{
        "bid": [{
            "id":"HJlaMhLEDz-1518787604706",
            "impid":"1",
            "price":0.935,
            "crid":"cr1.7110eda4",
            "cid":"c1.06a1cad2",
            "adid":"670ee102bd",
            "adomain":["booking.com"],
            "bundle":["com.google"],
            "attr":[1],"qagmediarating":1,
            "language":"UKR",
            "w":320,
            "h":50,
            "wratio":1,
            "hratio":2,
            "adm":"<h1>ADM</h1><img src=\"http://localhost:3000/adm?price=1.0843156917264036\"></img><img src=\"http://localhost:8080/win?price=${AUCTION_PRICE}&bidid=HJlaMhLEDz-1518787604706\" border=\"0\" width=\"1\" height=\"1\">",
            "nurl":"http://localhost:8080/win?bidid=HJlaMhLEDz-1518787604706&price=${AUCTION_PRICE}&n=1",
            "iurl":"http://localhost:8080/show?adid=670ee102bd"
        }],
        "seat":"1"
    }],
    "bidid":"BkW6z2UVvf",
    "cur":"USD"
}
```