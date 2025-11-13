---
title: Address Info API
description: FluentCart Address Info API for retrieving country and address-related information.
---

# Address Info API

The Address Info API provides endpoints for retrieving country options, state/province information, and address locale data in FluentCart.

## Base URL

All Address Info API endpoints are prefixed with the same base URL as the core API:

```
/wp-json/fluent-cart/v2/
```

## Authentication

All Address Info API endpoints require:
- **Policy**: `CustomerPolicy`

## Countries

### Get Countries Options

Retrieve a list of all available countries as options.

**Endpoint:** `GET /address-info/countries`

**Permission Required**: `CustomerPolicy`

#### Response

```json
{
  "success": true,
  "data": [
    {
      "value": "US",
      "label": "United States"
    },
    {
      "value": "CA",
      "label": "Canada"
    },
    {
      "value": "GB",
      "label": "United Kingdom"
    }
  ]
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v2/address-info/countries" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

## Country Information

### Get Country Info

Retrieve detailed information about a specific country including states/provinces and address locale.

**Endpoint:** `GET /address-info/get-country-info`

**Permission Required**: `CustomerPolicy`

#### Query Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `country_code` | string | Yes* | ISO country code (required if timezone not provided) |
| `timezone` | string | Yes* | Timezone (required if country_code not provided, used to guess country) |

#### Response

```json
{
  "success": true,
  "data": {
    "country_code": "US",
    "country_name": "United States",
    "states": [
      {
        "value": "AL",
        "label": "Alabama"
      },
      {
        "value": "AK",
        "label": "Alaska"
      },
      {
        "value": "CA",
        "label": "California"
      }
    ],
    "address_locale": {
      "format": "{{first_name}} {{last_name}}\n{{address_line_1}}\n{{city}}, {{state}} {{postal_code}}\n{{country}}"
    }
  }
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v2/address-info/get-country-info?country_code=US" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

#### Example Request with Timezone

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v2/address-info/get-country-info?timezone=America/New_York" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

## Error Handling

### Common Error Responses

#### Missing Parameters

```json
{
  "success": false,
  "data": {
    "message": "Country code or timezone is required"
  }
}
```

## Notes

- If `timezone` is provided, the country is automatically guessed from the timezone
- States/provinces are only returned for countries that have them
- Address locale format defines how addresses should be displayed for that country
- Country codes should be ISO 3166-1 alpha-2 format (e.g., 'US', 'CA', 'GB')

---

**Related Documentation:**
- [Customers API](./customers) - Customer address management
- [Shipping API](./shipping) - Shipping zone management

