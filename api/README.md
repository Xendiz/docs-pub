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
        "username": "Lorem Ipsum",
        "password": "pass",
        "apiKey": "apikey",
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
                "name": "Lorem "
            },
            {}
        ]
    }
}
```

## Example requests

### Authorization
Request made with cURL:
`curl -d '{"username": "Lorem Ipsum","password":"pass"}' -H "Content-Type: application/json" -X POST http://api.xendiz.com:3002/auth`

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
                "name": "Demo SSP #11"
            },
            {}
        ],
        "Dsps": [
            {
                "id": 1,
                "name": "Lorem "
            },
            {}
        ]
    }
}
```

### Sample request


## Overview
todo description
