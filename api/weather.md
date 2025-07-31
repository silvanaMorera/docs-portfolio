---
layout: page
title: Weather API Sample
permalink: /api/weather/
---

This API provides real-time weather data by location, supporting city names, ZIP codes, or geographic coordinates. It’s ideal for developers building climate-aware apps, dashboards, or automation tools. This page covers authentication, query parameters, sample requests, response handling, and common errors.

---

## Table of Contents

- [Table of Contents](#table-of-contents)
- [Authentication](#authentication)
  - [How to Get an API Key](#how-to-get-an-api-key)
- [Quick Start](#quick-start)
- [When to Use](#when-to-use)
- [Endpoint Reference](#endpoint-reference)
- [Required Parameters](#required-parameters)
- [Other Examples](#other-examples)
  - [By City Name](#by-city-name)
  - [By Coordinates](#by-coordinates)
- [Sample Response JSON](#sample-response-json)
- [Key Response Fields](#key-response-fields)
- [Rate Limits](#rate-limits)
- [Common Errors](#common-errors)
- [Best Practices](#best-practices)

---

## Authentication

To access the API, include your API key (`appid`) as a query parameter in the request URL.

### How to Get an API Key

1. Go to the [OpenWeather API Console](https://home.openweathermap.org/)
2. Log in or create a developer account
3. Navigate to API Keys tab
4. Generate and copy your new key securely

> Example API Key: `123456abcde` (do not share this publicly)

---

## Quick Start

Use this simple `curl` request:

```bash
curl "https://api.openweathermap.org/data/2.5/weather?zip=10001,us&units=imperial&appid=YOUR_API_KEY"
```

> **Tip:** Replace `YOUR_API_KEY` with your actual key. This returns current temperature in Fahrenheit, humidity, and weather description for New York.

---

## When to Use

Use this API if:
- You want to display current weather in your app or device
- You’re triggering logic based on local conditions (e.g., automation or alerts)
- You’re building a climate aware UI or dashboard
- You want to experiment with geolocation based data

## Endpoint Reference

**GET** `/data/2.5/weather`

You must include one of the following to specify the location:

* `q`: City name (e.g. `q=London`)
* `zip`: ZIP code and country (e.g. `zip=10001,us`)
* `lat + lon`: Geographic coordinates

> **Note:** Do not combine `q`, `zip`, and `lat/lon` — use only one method per request.

---

## Required Parameters

| Name    | Type   | **Required** | Description                                                         |
| ------- | ------ | ------------ | ------------------------------------------------------------------- |
| `appid` | string | Yes          | Your API key                                                        |
| `q`     | string | No           | City name (not used with `zip` or `lat/lon`)                        |
| `zip`   | string | No           | ZIP and country code (e.g. `10001,us`)                              |
| `lat`   | float  | No           | Latitude (used with `lon`)                                          |
| `lon`   | float  | No           | Longitude (used with `lat`)                                         |
| `units` | string | No           | `standard` (Kelvin), `metric` (Celsius), or `imperial` (Fahrenheit) |

---

## Other Examples

### By City Name

```bash
curl "https://api.openweathermap.org/data/2.5/weather?q=London&units=metric&appid=YOUR_API_KEY"
```

### By Coordinates

```bash
curl "https://api.openweathermap.org/data/2.5/weather?lat=51.5074&lon=-0.1278&units=metric&appid=YOUR_API_KEY"
```

---

## Sample Response JSON

<details>
<summary>Click to view full JSON response</summary>

<pre><code class="language-json">
{
  "name": "London",
  "main": {
    "temp": 17.72,
    "humidity": 55
  },
  "weather": [
    {
      "main": "Clouds",
      "description": "broken clouds"
    }
  ]
}
</code></pre>

</details>


---

## Key Response Fields

| Field                    | Type    | Description                      |
| ------------------------ | ------- | -------------------------------- |
| `name`                   | string  | City name                        |
| `coord.lat`              | float   | Latitude                         |
| `coord.lon`              | float   | Longitude                        |
| `main.temp`              | float   | Current temperature              |
| `main.feels_like`        | float   | Feels-like temperature           |
| `main.humidity`          | integer | Humidity percentage              |
| `weather[0].main`        | string  | Weather group (e.g., "Clouds")   |
| `weather[0].description` | string  | Human-readable weather condition |
| `wind.speed`             | float   | Wind speed                       |

---

## Rate Limits

* **Free Tier:** 60 requests per minute
* **Pro Tier:** 600 requests per minute

---

## Common Errors

| Status | Meaning           | Fix                             |
| ------ | ----------------- | ------------------------------- |
| 401    | Unauthorized      | Missing or invalid API key      |
| 403    | Forbidden         | API key is inactive or blocked  |
| 429    | Too Many Requests | You’ve exceeded your rate limit |

---

## Best Practices

* Cache API results to minimize repeat calls
* Always include `units` parameter for clarity
* Validate input before querying (city, ZIP, lat/lon)
* Handle `429` with exponential backoff or retry logic

---

> *This documentation is part of my API Writing Portfolio. See also: [CoinGecko API Sample](/api/coingecko/)*

> Version: v1.0 • Status: Stable • Updated: July 2025
