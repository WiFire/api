# WiFire API documentation. For partner applications to access WiFire's public WiFi database

You will need an API key to access this service. Please email wifire.bizdev@mobstac.com to get an API key.

## Making a request

All URLs start with https://wifireapi.mobstac.com/api/v1/

We use HTTP Basic auth for request authorization.

## API Endpoints

### 1. Hotspots

Public WiFi networks are called Hotspots in the WiFire world. The following endpoints are available:

#### `GET /hotspots`

Returns a list of hotspots (limit: 5) of the nearest public WiFi networks to the user's location, passed in through the `latlong` parameter

_Parameters_:

* `latlong` (required) - Geo-location coordinates specified as [lat,long], for e.g., [12.84064832,77.66001497]

###### Example JSON Response
```json
[
]
```

###### Copy as cURL

``` shell
curl -H "" https://wifireapi.mobstac.com/api/v1/hotspots
```


#### `GET /hotspots/:id`

Returns detailed information about a specific hotspot, identified by the `id` path parameter

_Optional parameters_:

* None

###### Example JSON Response
```json
[
]
```

###### Copy as cURL

``` shell
curl -H "" https://wifireapi.mobstac.com/api/v1/hotspots/1234
```
