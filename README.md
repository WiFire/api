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

* `latlong` (required) - Geo-location coordinate array specified as [lat,long], for e.g., [12.84064832,77.66001497].
* `radius` (optional) - Radius in meters, up to 3 km. Default: 3000
* `limit` (optional) - Number of closest hotspots to return, up to 5. Default: 5

###### Example JSON Response
```json
{
  "count": 5,
  "data": [
    {
      "id": 10860825,
      "body": {
        "g": "tdr4he8fvd",
        "l": [
          13.0275244,
          77.54277259999999
        ],
        "speed": [
          0,
          0
        ],
        "placeID": "ChIJB8kXjms9rjsRQ9CZSbMQbVw",
        "placeName": "Sparsh Hospital",
        "aggregateRating": 0
      }
    },
    {
      "id": 10860824,
      "body": {
        "g": "tdr1v9qmx5",
        "l": [
          12.9716981,
          77.5943417
        ],
        "placeID": "ChIJ-VrecmkWrjsRtN8D7e0Ddcc",
        "placeName": "Café Coffee Day The Square",
        "aggregateRating": 0
      }
    },
    {
      "id": 10860823,
      "body": {
        "g": "tdr1qzq7dw",
        "l": [
          12.91644003243457,
          77.64907624579747
        ],
        "aggregateRating": 0
      }
    },
    {
      "id": 10530811,
      "body": {
        "g": "tdr4hb9fe1",
        "l": [
          13.0109961,
          77.5550236
        ],
        "speed": [
          841000,
          3350000
        ],
        "placeID": "ChIJQZkOs3g9rjsRlhZ6dYyogHA",
        "placeName": "PVR",
        "aggregateRating": 0
      }
    },
    {
      "id": 10530591,
      "body": {
        "g": "tdr4nexxu",
        "l": [
          13.028388,
          77.63988569999992
        ],
        "placeID": "ChIJS9mI-ToXrjsRYc-bOMD0gPc",
        "placeName": "Bangalore city college",
        "aggregateRating": 0
      }
    }
  ]
}
```

###### Copy as cURL

``` shell
curl -u username:password -G https://wifireapi.mobstac.com/api/v1/hotspots -d latlong=12.82 -d latlong=77.41
```


#### `GET /hotspots/:id`

Returns detailed information about a specific hotspot, identified by the `id` path parameter

_Optional parameters_:

* None

###### Example JSON Response
```json
{
 "data": {
    "g": "tdr4he8fvd",
    "l": [
      13.0275244,
       77.54277259999999
    ],
    "speed": [
      0,
      0
    ],
    "placeID": "ChIJB8kXjms9rjsRQ9CZSbMQbVw",
    "placeName": "Sparsh Hospital",
    "aggregateRating": 0
  }
}
```

###### Copy as cURL

``` shell
curl -u username:password -G https://wifireapi.mobstac.com/api/v1/hotspots/10860825
```

### Glossary of JSON fields

- `g` - geohash
- `l` - coordinate array [lat,long]
- `speed` - Avg speed of network in bytes per sec [download,upload]
- `placeID` - Google place ID
- `aggregateRating` - Average user rating of the hotspot
