# Partners API
* [Overview](#overview)
* [DSP API](./dsp)
* [SSP API](./ssp)
* [Trends API](./trends)

**API ENDPOINT: api.xendiz.com**

## Authorization

`POST` /auth

Request: 
```json
{
	"username": "Lorem Ipsum",
	"password": "pass"
}
```

Response:
```json
{
    "data": {
        "username": "demo",
        "password": "demoe",
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

## Example requests

### Authorization

* Send json with your username and password
* Receive your `api_key` and list with ids and names of your company SSPs and DSPs

Request made with cURL:
`curl -d '{"username": "Lorem Ipsum","password":"pass"}' -H "Content-Type: application/json" -X POST http://api.xendiz.com/auth`

Response:
```json
{
    "data": {
        "username": "Lorem Ipsum",
        "password": "pass",
        "apiKey": "apikey",
        "Ssps": [
            {
                "id": 5,
                "name": "Some SSP"
            },
            {}
        ],
        "Dsps": [
            {
                "id": 1,
                "name": "Getcha DSP"
            },
            {}
        ]
    }
}
```

### Sample request

* Pass `api_key` which you received in previous step to authorization header and get access to API

`PUT` /dsp/`:id`/block

`curl -d '[{"type":"app","source":"com.test.bundle"},{"type":"publisher","source":"some_publisher"}]' -H "Content-Type: application/json" -H "Authorization: Bearer api_key" -X PUT http://api.xendiz.com/dsp/1/block`

Response: 
* STATUS CODE 204

## Overview
todo description
