# Availables API
* [Overview](#overview)


## Overview
  This section of API lists two methods:
- First is used to fetch list of available OS in our system.
- Second is used to fetch lost of available sizes in our system.

`GET` /availables/os

Response
```json
{
    "data": [
        "ios",
        "android",
        ""
    ]
}
```

`GET` /availables/size

Response
```json
{
    "data": [
        {
            "height": 320,
            "width": 240
        },
        {}
    ]
}
```
