# WiFire API documentation. For partner applications to access WiFire's public WiFi database

You will need a username and password to access this service. Please email wifire.bizdev@mobstac.com to get credentials generated and assigned to your organization.

## Making a request

All URLs start with https://wifireapi.mobstac.com/api/v1/. We use HTTP Basic auth for request authorization.

*NOTE:* All API requests must come from a pre-whitelisted public IP address that belongs to your server. Your API key is tied to the IP address, so requests from other IPs are automatically rejected.

We also rate-limit API requests to ensure you don't overload our server.

## API Endpoints

### 1. Hotspots

Public WiFi networks in the WiFire database are called Hotspots. The following endpoints are available:

#### `GET /hotspots`

Returns a list of hotspots (limit: 5) of the nearest public WiFi networks to the user's location, passed in through the `latlong` parameter

_Parameters_:

* `latlong` (required) - Geo-location coordinate. To pass lat & long, use this parameter twice, for e.g., `latlong=12.84064832&latlong=77.66001497` to pass in [12.84064832,77.66001497]
* `radius` (optional) - Radius in meters, up to 3 km. Default: 3000
* `limit` (optional) - Number of closest hotspots to return, up to 5. Default: 5

###### Example JSON Response
```json
{
  "count": 5,
  "data": [
    {
      "id": "-Kegzar5AQbrp99neN3N",
      "g": "tdr1yfb5sv",
      "l": [
        12.979605,
        77.6405906
      ],
      "placeID": "ChIJc0JAFaUWrjsRRXSXJPX7YFo",
      "placeName": "Toit Brewpub",
      "speed": [
        7713500,
        435500
      ],
      "distance": 77.6,
      "aggregateRating": 3.8,
      "url": "http://hotspot.findwifi.co/vDxgGIrwASWx5xdY"
    },
    {
      "id": "-K46isqY4D7NcssaVH3q",
      "g": "tdr1yfbq2h",
      "l": [
        12.9800695,
        77.6407289
      ],
      "placeID": "ChIJwyjjN6UWrjsRmofzxcCt3_I",
      "placeName": "3oh'3",
      "speed": [
        978977.0064571049,
        237842.9379574884
      ],
      "distance": 79.5,
      "url": "http://hotspot.findwifi.co/TbcgfgN6vGHweFLc"
    },
    {
      "id": "-KE5iKsLLxtxofeec-7t",
      "g": "tdr1wxw7yh",
      "l": [
        12.980799999999999,
        77.640468
      ],
      "placeID": "ChIJ7_gUy7oWrjsRkOIJEP5qtV8",
      "placeName": "The Beer Cafe",
      "speed": [
        77323.75553776497,
        22549.557096725704
      ],
      "aggregateRating": 4,
      "distance": 102,
      "url": "http://hotspot.findwifi.co/ooLaW-l8nWq6xXzk"
    },
    {
      "id": "-KSVcKyctzLkonWmfp6J",
      "g": "tdr1yfb0k9",
      "l": [
        12.9790266,
        77.640579
      ],
      "placeID": "ChIJYyvzFKUWrjsRQxHn48rD5T8",
      "placeName": "Glen's Bakehouse",
      "distance": 124.7,
      "url": "http://hotspot.findwifi.co/YHuhN5aRrqZtgBfg"
    },
    {
      "id": "-KSBY-V6z1_ouTEewROh",
      "g": "tdr1yf85u",
      "l": [
        12.9782791,
        77.64057869999999
      ],
      "placeID": "ChIJX-547aQWrjsRenl27sGSY6s",
      "placeName": "Pizza Hut",
      "distance": 200.5,
      "url": "http://hotspot.findwifi.co/TzHho0cYrfSXr1cO"
    }
  ]
}
```

###### Copy as cURL

``` shell
curl -u username:password -G https://wifireapi.mobstac.com/api/v1/hotspots -d latlong=12.82 -d latlong=77.41
```

### Glossary of JSON fields

- `id` - unique identifier for this hotspot
- `g` - geohash
- `l` - coordinate array [lat,long]
- `placeID` - Google place ID
- `placeName` - name of the place hosting this hotspot
- `speed` (optional) - average network speed in bytes per sec [download,upload]
- `aggregateRating` (optional) - average user rating for the hotspot
- `url` - unique user-friendly rendered web page for the hotspot that can be rendered in a WebView

**Note:** The `url` has a validity of 15 minutes.
