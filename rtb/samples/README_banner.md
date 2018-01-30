### Bid Request sample
```json
{
    "at": 2,
    "id": "SyXrk7h8vSG",
    "tmax": 410,
    "cur": ["USD"],
    "bcat": ["IAB24", "IAB25", "IAB26"],
    "device": {
        "ip": "90.212.104.28",
        "os": "iOS",
        "osv": "11.2.2",
        "make": "Apple",
        "model": "iPhone",
        "devicetype": 4,
        "ua": "Mozilla/5.0 (iPhone; CPU iPhone OS 11_2_2 like Mac OS X) AppleWebKit/604.4.7 (KHTML, like Gecko) Mobile/15C202",
        "dnt": 0,
        "lmt": 0,
        "connectiontype": 2,
        "ifa": "FE56A8E2-58F3-4F2F-9591-650380E7CBAB",
        "carrier": "Sky Broadband",
        "geo": {
            "type": 2,
            "lat": 51.5167,
            "lon": 0.0667,
            "country": "GBR",
            "city": "beckton"
        }
    },
    "app": {
        "keywords": "Music,Entertainment,video,search,listen,million,designed",
        "publisher": {
            "id": "4b71c1d107",
            "name": "Alexandra Lazarescu"
        },
        "paid": 0,
        "name": "Tubidy Unlimited",
        "bundle": "1218295205",
        "storeurl": "https://itunes.apple.com/us/app/tubidy-unlimited/id1218295205?mt=8&uo=4",
        "cat": ["IAB1"],
        "id": "f85b576ee9"
    },
    "imp": [{
        "id": "1",
        "bidfloorcur": "USD",
        "banner": {
            "w": 320,
            "h": 50
        },
        "bidfloor": 0.12
    }],
    "user": {
        "id": "1516887063.001.4f4f11df7b1801d99a26ec324d2e17ac",
        "buyeruid": ""
    }
}
```

### Bid Response sample

```json
{
    "id": "fb296d90b0994e7697085554afcd3da6",
    "seatbid": [{
        "bid": [{
            "id": "rydMHT3LwHz-1516887228940",
            "impid": "4dcc7a6a-9abc-41f3-8bb9-4c079f0fc25f",
            "price": 1.2,
            "crid": "cr38.e349adfb",
            "cid": "c38.877ccc2d",
            "adid": "e5a5fc5c38",
            "adomain": ["iheart.com"],
            "attr": [4],
            "adm": "<iframe src=\"https://mbsrvlnk.com/ad1/173000?p=468937&app=best.deals.compare.coupons.discounts.tracker.assistant.alert&udid=e3ceb4de-6fcd-40bf-b535-9fcd347f467c&dm={DOMAIN_NAME}\" width=\"320\" height=\"50\" frameBorder=\"0\" scrolling=\"no\"></iframe>",
            "nurl": "http://alan.imptracker.bid/win?bidid=rydMHT3LwHz-1516887228940&price=${AUCTION_PRICE}&n=1",
            "iurl": "http://alan.imptracker.bid/show?adid=e5a5fc5c38"
        }],
        "seat": "38"
    }],
    "bidid": "SJFfr6hLPrf",
    "cur": "USD"
}
```