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
	{
    "data": {
        "username": "Lorem Ipsum"",
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
}
```

## Overview
todo description
