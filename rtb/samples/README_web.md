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
    "id":"SyeGTfQIrG",
    "seatbid": [{
        "bid": [{
            "id":"rkgXwpUNvG-1518787930705",
            "impid":"1",
            "price":0.935,
            "crid":"cr1.7110eda4",
            "cid":"c1.06a1cad2",
            "adid":"670ee102bd",
            "adomain":["lazada.com"],
            "bundle":["com.google"],
            "attr":[1],
            "qagmediarating":1,
            "language":"UKR",
            "w":320,
            "h":50,
            "wratio":1,
            "hratio":2,
            "adm":"<h1>ADM</h1><img src=\"http://localhost:3000/adm?price=1.052015202792925\"></img><img src=\"http://localhost:8080/win?price=${AUCTION_PRICE}&bidid=rkgXwpUNvG-1518787930705\" border=\"0\" width=\"1\" height=\"1\">",
            "nurl":"http://localhost:8080/win?bidid=rkgXwpUNvG-1518787930705&price=${AUCTION_PRICE}&n=1",
            "iurl":"http://localhost:8080/show?adid=670ee102bd"
        }],
        "seat":"1"
    }],
    "bidid":"rybXwaL4Pz",
    "cur":"USD"
}
```