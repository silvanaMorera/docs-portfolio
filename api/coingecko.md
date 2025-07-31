---
layout: page
title: CoinGecko API Sample
permalink: /api/coingecko/
---

The CoinGecko API provides cryptocurrency market data, including token prices, volume, market capitalization, and historical charts. It’s widely used for analytics dashboards, fintech apps, and market tracking tools. This page covers authentication, usage examples, query parameters, and sample responses.

---

## Table of Contents

- [Table of Contents](#table-of-contents)
- [Authentication](#authentication)
- [When to Use](#when-to-use)
- [Use Case Example](#use-case-example)
- [Endpoint Reference](#endpoint-reference)
- [Required Parameters](#required-parameters)
- [Sample Request](#sample-request)
- [Sample Response JSON](#sample-response-json)
- [Key Response Fields](#key-response-fields)
- [Rate Limits](#rate-limits)
- [Common Errors](#common-errors)
- [Best Practices](#best-practices)

---

## Authentication

The public CoinGecko API does **not require authentication**. However, [CoinGecko Premium (Pro/VIP)](https://www.coingecko.com/en/api/pricing) offers authenticated access with higher rate limits and faster performance for enterprise use.

---

## When to Use

Use this API if:
- You’re building a crypto dashboard or portfolio tracker
- You want up-to-date market prices and token metadata
- You need data without the friction of API key registration
- You're integrating with DeFi or blockchain analytics tools

---

## Use Case Example

You're developing a mobile app that lets users view the current price of Bitcoin, Ethereum, and Solana in USD. The CoinGecko API allows you to retrieve all three prices with a single request and display the results in your UI.

---

## Endpoint Reference

**GET** `/api/v3/simple/price`

Returns the current price of one or more cryptocurrencies in any supported fiat or cryptocurrency.

---

## Required Parameters

| Name        | Type   | Required | Description                                               |
|-------------|--------|----------|-----------------------------------------------------------|
| `ids`       | string | Yes      | Comma-separated list of coin IDs (e.g. `bitcoin,ethereum`)|
| `vs_currencies` | string | Yes  | Comma-separated list of currencies to compare (e.g. `usd`)|
| `include_market_cap` | bool | No | If true, include market cap                               |
| `include_24hr_vol`   | bool | No | If true, include 24-hour volume                          |
| `include_24hr_change`| bool | No | If true, include 24-hour price change                    |

---

## Sample Request

```bash
curl "https://api.coingecko.com/api/v3/simple/price?ids=bitcoin,ethereum,solana&vs_currencies=usd&include_market_cap=true&include_24hr_change=true"
```

---

## Sample Response JSON

<details>
<summary>Click to view JSON</summary>

<pre><code class="language-json">
{
  "bitcoin": {
    "usd": 29654,
    "usd_market_cap": 580000000000,
    "usd_24h_change": 1.25
  },
  "ethereum": {
    "usd": 1847,
    "usd_market_cap": 220000000000,
    "usd_24h_change": 0.98
  },
  "solana": {
    "usd": 26.45,
    "usd_market_cap": 11200000000,
    "usd_24h_change": -0.62
  }
}
</code></pre>

</details>

---

## Key Response Fields

| Field                     | Type    | Description                              |
|---------------------------|---------|------------------------------------------|
| `coin_id.usd`             | float   | Current price in USD                     |
| `coin_id.usd_market_cap`  | float   | Market capitalization in USD             |
| `coin_id.usd_24h_change`  | float   | 24-hour price change in percentage       |

---

## Rate Limits

* **Public Tier:** 10–30 requests per minute
* **VIP Tier:** Up to 100+ requests per minute (requires subscription)

---

## Common Errors

| Status | Meaning              | Fix                                   |
|--------|----------------------|----------------------------------------|
| 400    | Invalid ID or currency | Check spelling and valid query pairs  |
| 429    | Rate limit exceeded    | Wait or upgrade to VIP                |
| 500    | Internal server error  | Retry later, CoinGecko may be down    |

---

## Best Practices

* Limit the number of coins requested per call for speed
* Use `vs_currency=usd` for compatibility with most financial data
* Cache frequent requests to reduce load
* Do not over-poll; respect the rate limits
* Use `/coins/list` to dynamically retrieve all available coin IDs

---

> *This documentation is part of my API Writing Portfolio. See also: [Weather API Sample](/api/weather/)*  
> Version: v1.0 • Status: Stable • Updated: July 2025