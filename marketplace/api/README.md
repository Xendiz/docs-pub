# Partners API
* [Overview](#api-endpoint)
* [DSP API](./dsp)
* [SSP API](./ssp)
* [Trends API](./trends)

## Api Endpoint
DSP API: ``http://api.xendiz.com/dsp``  
SSP API: ``http://api.xendiz.com/ssp``  
TRENDS API: ``http://api.xendiz.com/trends``

## Authorization

`POST` /auth

* Send json with your username and password
* Receive your `apiKey` and list with ids and names of your company SSPs and DSPs
* Either pass `apiKey` which you received in previous step to authorization header or as URL parameter (e.g `/dsp?apiKey=yourApiKey` or `/dsp?api_key=yourApiKey`) and get access to API

```bash
curl -d '{"username": "demo", "password":"demo"}' -H "Content-Type: application/json" -X POST http://api.xendiz.com/auth
```

Response:
```json
{
  "data": {
    "name": "Demo Company",
    "apiKey": "01bde69ca3b11b8eaac505b63562hd0a",
    "Ssps": [
      {
        "id": 5,
        "name": "Demo SSP #11"
      }
    ],
    "Dsps": [
      {
        "id": 1,
        "name": "Demo DSP #1"
      }
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
