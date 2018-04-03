# Partners API
* [Overview](#overview)
* [DSP API](./dsp)
* [SSP API](./ssp)
* [Trends API](./trends)

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

## Overview
todo description
