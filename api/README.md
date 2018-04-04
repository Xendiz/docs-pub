# Partners API
* [Overview](#api-endpoint)
* [DSP API](./dsp)
* [SSP API](./ssp)
* [Trends API](./trends)
* [Availables API](./availables)

## Api Endpoint
DSP API: ``http://api.xendiz.com/dsp`` <br>SSP API: ``http://api.xendiz.com/ssp``<br>TRENDS API: ``http://api.xendiz.com/trends``

## Authorization

`POST` /auth

* Send json with your username and password
* Receive your `api_key` and list with ids and names of your company SSPs and DSPs
* Pass `api_key` which you received in previous step to authorization header and get access to API

```bash
curl -d '{"username": "demo", "password":"demo"}' -H "Content-Type: application/json" -X POST http://api.xendiz.com/auth
```

Response:
```json
{
  "data": {
    "apiKey": "01bde69ca3b11b8eaac505b63562hd0a",
    "Ssps": [
      {
        "id": 5,
        "name": "Demo SSP #11"
      },
      {}
    ],
    "Dsps": [
      {
        "id": 1,
        "name": "Demo DSP #1"
      },
      {}
    ]
  }
}
```

## Example
Campaign report `GET` /dsp/detailed/cid

```bash
curl -H "Content-Type: application/json" -H "Authorization: Bearer 01bde69ca3b11b8eaac505b63562hd0a" -X GET http://api.xendiz.com/dsp/detailed/cid/?campaign=cid-12345&from=2018-01-01&to=2018-01-10
```

Response: 
```json
{
  "data": [{
    "date": "2018-01-01",
    "spend": 40.21,
    "impressions": 1293811
  }, {
    "date": "2018-01-02",
    "spend": 60.90,
    "impressions": 1423811
  }]
}
```
