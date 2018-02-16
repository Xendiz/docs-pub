### Bid Request sample
```json
{
    "id": "1234567893",
    "at": 2, "tmax": 120,
    "imp": [
    {
        "id": "1", "bidfloor": 0.03,
        "video": {
        "w": 640, "h": 480, "pos": 1,
        "startdelay": 0, "minduration": 5, "maxduration": 30,
        "maxextended": 30,
        "minbitrate": 300, "maxbitrate": 1500,
        "api": [ 1, 2 ],
        "protocols": [ 2, 3 ],
        "mimes": [
            "video/x-flv",
            "video/mp4",
            "application/x-shockwave-flash",
            "application/javascript"
        ],
        "linearity": 1,
        "boxingallowed": 1,
        "playbackmethod": [ 1, 3 ],
        "delivery": [ 2 ],
        "battr": [ 13, 14 ],
        "companionad": [
            {
            "id": "1234567893-1",
            "w": 300, "h": 250, "pos": 1,
            "battr": [ 13, 14 ],
            "expdir": [ 2, 4 ]
            },
            {
            "id": "1234567893-2",
            "w": 728, "h": 90, "pos": 1,
            "battr": [ 13, 14 ]
            }
        ],
        "companiontype": [ 1, 2 ]
        }
    }
    ],
    "site": {
        "id": "1345135123", "name": "Site ABCD",
        "domain": "siteabcd.com",
        "cat": [ "IAB2-1", "IAB2-2" ],
        "page": "http://siteabcd.com/page.htm",
        "ref": "http://referringsite.com/referringpage.htm",
        "privacypolicy": 1,
        "publisher": {
            "id": "pub12345", "name": "Publisher A" 
        },
        "content": {
            "id": "1234567",
            "series": "All About Cars",
            "season": "2", "episode": 23, "title": "Car Show",
            "cat": [ "IAB2-2" ],
            "keywords": "keyword-a,keyword-b,keyword-c"
        }
    },
    "device": {
    "ip": "64.124.253.1",
    "ua": "Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.6; en-US; rv:1.9.2.16)Gecko/20110319 Firefox/3.6.16",
    "os": "OS X",
    "flashver": "10.1", "js": 1
    },
    "user": {
        "id": "456789876567897654678987656789",
        "buyeruid": "545678765467876567898765678987654",
        "data": [{
            "id": "6", "name": "Data Provider 1",
            "segment": [
                {
                "id": "12341318394918", "name": "auto intenders"
                },
                {
                "id": "1234131839491234", "name": "auto enthusiasts"
            }]
        }]
    }
}
```

### Bid Response sample

```json
{
    "id":"1234567893",
    "seatbid": [{
        "bid": [{
            "id":"rygRiCDEwM-1518792357681",
            "impid":"1",
            "price":0.935,
            "crid":"cr1.7110eda4",
            "cid":"c1.06a1cad2",
            "adid":"670ee102bd",
            "adomain":["luvoinc.com"],
            "bundle":["com.google"],
            "attr":[1],
            "qagmediarating":1,
            "language":"UKR",
            "w":320,
            "h":50,
            "wratio":1,
            "hratio":2,
            "adm":"%3C%3Fxml%20version%3D%221.0%22%20encoding%3D%22UTF-8%22%3F%3E%3CVAST%20version%3D%222.0%22%3E%3CAd%20id%3D%221%22%3E%3CWrapper%3E%3CAdSystem%20version%3D%221.0%22%3Ebonadza.com%3C%2FAdSystem%3Ehttp%3A%2F%2Flocalhost%3A8080%2Fwin%3Fprice%3D%24%7BAUCTION_PRICE%7D%26bidid%3DrygRiCDEwM-1518792357681%5D%5D%3E%3C%2FImpression%3E%3CVASTAdTagURI%3E%3C!%5BCDATA%5Bhttp%3A%2F%2Flbe.bonadza.com%2FBonadzaAd%2Fview%3Fp%3DErSbzgPf-dBo-h44S0aBMNT7TM4uPStsFqKA4EoolxPhPrfKwegqJ4F6eg-i_CCGAkUuliRqlsRU4Qceu33w8kWFZ3hxEWuO6dTDWqN8-vw9uyhatnFmamBWdFJgM01VQFaXFNd3NaT5kbtpiE2RqcGWps5dpAERe2a-48V9ERJgNKB7Gloyaob9RZK6brDzDOAMXtfYOz8DiG2bZ3kn2cmJT7rqxHN0eIfBkILmxL_IPn90RF-VyxxCGYh7bWGL%26wp%3D7.54731%26ai%3Dbdd67e8d1fb1e3847540115b4bde9522%26vp%3DJmlwPTIwOS40Mi4yLjQyJnVhPU1vemlsbGElMkY1LjArJTI4V2luZG93cytOVCsxMC4wJTNCK1dpbjY0JTNCK3g2NCUyOStBcHBsZVdlYktpdCUyRjUzNy4zNislMjhLSFRNTCUyQytsaWtlK0dlY2tvJTI5K0Nocm9tZSUyRjYxLjAuMzE2My4xMDArU2FmYXJpJTJGNTM3LjM2JmRudD0wJmR0PTMmbGF0PTQxLjg5OTgmbG9uPS04Ny42MzY4JnVybD1odHRwJTNBJTJGJTJGc3VwZXJoZWFsdGh5a2lkcy5jb20lMkYmZG9tYWluPXN1cGVyaGVhbHRoeWtpZHMuY29tJnNpdGVpZD0yZjc1YzJmN2Q2ODQ%5D%5D%3E%3C%2FVASTAdTagURI%3E%3C!%5BCDATA%5Bhttp%3A%2F%2Fns10.clickkydsp.com%2F%3Ft%3Dwinv%26ob%3D7.54731%26cd%3D12c4210f349a420afe4a8ccc26bac506%5D%5D%3E%3C%2FImpression%3E%3CCreatives%3E%3C%2FCreatives%3E%3C%2FWrapper%3E%3C%2FAd%3E%3C%2FVAST%3E",
            "nurl":"http://undefined'}"
            }],
        "seat":"1"
        }],
    "bidid":"Bkb0jAwVDG",
    "cur":"USD"
}
```