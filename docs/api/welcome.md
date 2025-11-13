---
title: Welcome API
description: FluentCart Welcome API for retrieving welcome message.
---

# Welcome API

The Welcome API provides an endpoint for retrieving a welcome message in FluentCart.

## Base URL

All Welcome API endpoints are prefixed with the same base URL as the core API:

```
/wp-json/fluent-cart/v2/
```

## Authentication

The Welcome API endpoint does not require authentication (public endpoint).

## Welcome Message

### Get Welcome Message

Retrieve the welcome message.

**Endpoint:** `GET /welcome`

**Permission Required**: None (public endpoint)

#### Response

The response structure depends on the WelcomeController implementation. Typically returns a welcome message or configuration.

```json
{
  "message": "Welcome to FluentCart API",
  "version": "2.0"
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v2/welcome"
```

## Notes

- This is a public endpoint that does not require authentication
- The welcome message may vary based on the implementation
- This endpoint is typically used for API health checks or initial connection testing

---

**Related Documentation:**
- [Authentication API](./authentication) - API authentication

