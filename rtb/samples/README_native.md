### Bid Request sample
```json
{
    "id": "80ce30c53c16e6ede735f123ef6e32361bfc7b22",
    "at": 1, "cur": [ "USD" ],
    "imp": [
        {
            "id": "1", "bidfloor": 0.03,
            "banner": {
            "h": 250, "w": 300, "pos": 0
            },
            "native": {
                "request": "...Native Spec request as an encoded string...",
                "ver": "1.0",
                "api": [ 3 ], "battr": [ 13, 14 ]
            }
        }
    ],
    "site": {
    "id": "102855",
    "domain": "www.foobar.com",
    "cat": [ "IAB3-1" ],
    "page": "http://www.foobar.com/1234.html",
    "publisher": {
        "id": "8953", "name": "foobar.com",
        "cat": [ "IAB3-1" ],
        "domain": "foobar.com"
    }
    },
    "device": {
        "ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_6_8) AppleWebKit/537.13(KHTML, like Gecko) Version/5.1.7 Safari/534.57.2",
        "ip": "123.145.167.10"
    },
    "user": {
    "id": "55816b39711f9b5acf3b90e313ed29e51665623f"
    }
}
```

### Bid Response sample

```json
{
    "id":"80ce30c53c16e6ede735f123ef6e32361bfc7b22",
    "seatbid": [{
        "bid": [{
            "id":"H1x1BaDNPG-1518791991357",
            "impid":"1",
            "price":0.935,
            "crid":"cr1.7110eda4",
            "cid":"c1.06a1cad2",
            "adid":"670ee102bd",
            "adomain":["singtel.com"],
            "bundle":["com.google"],
            "attr":[1],
            "qagmediarating":1,
            "language":"UKR",
            "w":320,
            "h":50,
            "wratio":1,
            "hratio":2,
            "adm":"<h1>ADM</h1><img src=\"http://localhost:3000/adm?price=1.0490140830849086\"></img><img src=\"http://localhost:8080/win?price=${AUCTION_PRICE}&bidid=H1x1BaDNPG-1518791991357\" border=\"0\" width=\"1\" height=\"1\">",
            "nurl":"http://localhost:8080/win?bidid=H1x1BaDNPG-1518791991357&price=${AUCTION_PRICE}&n=1",
            "iurl":"http://localhost:8080/show?adid=670ee102bd"
            }],
        "seat":"1"
        }]
}
```