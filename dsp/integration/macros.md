# DSP Macros List
These Macros allow you to pass info to the advertiser with the click or impression.

| Macro           | Type    | Description
| -------------   | :-----: | :-------------:  
`{SEAT}`          | String  | Xendiz Advertiser ID (e.g. "1292")
`{IMP_ID}`        | String  | Impression ID (e.g. "H1xjIoDVvz")
`{CLICK_ID}`      | String  | Click ID (e.g. "SyeGTfQIrG")
`{EXCHANGE}`      | String  | Exchange name (e.g. "Xendiz")
`{CREATIVE_ID}`   | Integer | Creative ID (e.g. "121131")
`{CAMPAIGN_ID}`   | Integer | Campaign ID (e.g. "244314")
`{PUBLISHER_ID}`  | String  | Publisher ID (e.g. "9eb2c6cf4")
`{TYPE}`          | Enum(app, site)| Platform type 
`{SITE_DOMAIN}`   | String  | Site domain (e.g. "msn.com")
`{SITE_PAGEURL}`  | String  | Site page url (e.g. "https://www.msn.com/en-us/news/world/syrian-president-to-meet-kim-jong-un-in-north-korea-report-says/ar-AAyaeOb?li=BBnbfcL")
`{APP_BUNDLE}`    | String  | Application bundle (e.g "591560124")
`{DEVICE_TYPE}`   | String  | OpenRTB Device Type (e.g "2")
`{DEVICE_VENDOR}` | String  | OpenRTB Device Type (e.g "Apple")
`{DEVICE_MODEL}`  | String  | Device model (e.g. "iPhone")
`{DEVICE_OS}`     | String  | Device Os (e.g. "iOS")
`{DEVICE_CARRIER}`| String  | Device carrier (e.g. "Verizon")
`{DEVICE_CONTYPE}`| String  | OpenRTB Device Connection Type (e.g. "3")
`{LAT}`           | Float   | Latitude from -90.0 to +90.0, where negative is south.
`{LON}`           | Float   | Longitude from -180.0 to +180.0, where negative is west.
`{COUNTRY}`       | String  | Country code using ISO-3166-1-alpha-3. (e.g. "USA")
`{CITY}`          | String  | City using United Nations Code for Trade & Transport
Locations. 
`{IPSHA1}`        | String  | Device IP, hashed via SHA1.
`{IFA}`           | String  | ID sanctioned for advertiser use in the clear (i.e., not hashed).
`{DPIDSHA1}`      | String  | Platform device ID (e.g., Android ID); hashed via SHA1.
`{DIDSHA1}`       | String  | Hardware device ID (e.g., IMEI); hashed via SHA1.
`{TIMESTAMP}`     | Integer | Event Unix Timestamp