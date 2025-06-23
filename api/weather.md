---
layout: page
title: Weather API Sample
permalink: /api/weather/
---

# Weather API Overview

The **Weather API** allows developers to access real time weather data for any city using a simple HTTP request. You can retrieve current temperature, humidity levels, and a short weather description by city name or geographic coordinates.

This API is ideal for apps that need to display local weather conditions, trigger weather-based events, or enrich user experiences with contextual climate data, without relying on a bulky SDK.

---

## Authentication

To access the API, you must include an API key (`appid`) as a query parameter in your request URL.

### How to Get an API Key

1. Go to the [API Console](https://home.openweathermap.org/)
2. Sign up or log in to your developer account
3. Generate a new API key from the **API Keys** tab
4. Copy and securely store your key

> Example API key: `123456abcde` (do not share this publicly)

### How to Use It

Include the `appid` in each request like this:

```https
GET https://api.openweathermap.org/data/2.5/weather?zip=10111&units=imperial&appid=APIKEY
```

### Quick Start
Try a simple `curl` request 

```bash
curl "https://api.openweathermap.org/data/2.5/weather?zip=10001&units=imperial&appid=APIKEY"
```

> Replace `APIKEY` with your valid token. 
> This returns the current temperature in Fahrenheit, along with humidity and weather descriptions for New York.

### Endpoint Reference
```bash 
GET /data/2.5/weather 
```
You must include one of the following to specify a location:

- **q**: City name (e.g. q=London)
- **zip**: ZIP code and country code (e.g. zip=10001,us)
- **lat + lon**: Geographic coordinates

### Required Parameters

The following parameters are accepted in GET `/weather` requests:

| Name    | Type   | Required | Description |
|---------|--------|----------|-------------|
| `appid` | string | Yes   | Your API key |
| `q`     | string | No       | City name (e.g. `London`). Not used with `zip` or `lat/lon`. |
| `zip`   | string | No       | ZIP code and country code (e.g. `10001,us`). |
| `lat`   | float  | No       | Latitude — must be used with `lon`. |
| `lon`   | float  | No       | Longitude — must be used with `lat`. |
| `units` | string | No       | Unit system:<br>– `standard` (Kelvin, default)<br>– `metric` (Celsius)<br>– `imperial` (Fahrenheit) |


### Other Examples

#### By City Name 
```bash 
curl "https://api.openweathermap.org/data/2.5/weather?q=London&units=metric&appid=YOUR_API_KEY"
```

#### By Coordinates
```bash 
curl "https://api.openweathermap.org/data/2.5/weather?lat=51.5074&lon=-0.1278&units=metric&appid=YOUR_API_KEY"
```

##### Note
> Don’t combine q, zip, and lat/lon — use only one location method per request.

### Sample Response JSON

This is how a JSON response looks like using the request by city name: 
``` json 
{
  "name": "London",
  "main": {
    "temp": 17.72,
    "humidity": 55
  },
  "weather": [
    { "main": "Clouds", "description": "broken clouds" }
  ]
}
```

### Key Response Fields
Below are the most commonly used fields in the response:

| Field                    | Type    | Description                                   |
|--------------------------|---------|-----------------------------------------------|
| `name`                   | string  | City name                                     |
| `coord.lat`              | float   | Latitude of the location                      |
| `coord.lon`              | float   | Longitude of the location                     |
| `main.temp`              | float   | Current temperature                           |
| `main.feels_like`        | float   | "Feels like" temperature                      |
| `main.humidity`          | integer | Humidity percentage                           |
| `weather[0].main`        | string  | Weather group (e.g., "Rain", "Clouds")        |
| `weather[0].description` | string  | Human-readable description (e.g., "mist")     |
| `wind.speed`             | float   | Wind speed (in m/s or mph depending on units) |

> For a full list of response fields, see [OpenWeather’s full schema documentation](https://openweathermap.org/current)

### Rate Limits

- Free tier: 60 requests/minute
- Pro tier: 600 requests/minute

### Common Errors

| Status  | Meaning            | Fix                             |
|-------- | ------------------ | ------------------------------- |
| 401     | Unauthorized       | Missing or invalid API key      |
| 403     | Forbidden          | Your key is inactive or blocked |
| 429     | Too Many Requests  | You've exceeded your rate limit |

