---
title: Onboarding API
description: FluentCart Onboarding API for managing the store setup and onboarding process.
---

# Onboarding API

The Onboarding API provides endpoints for managing the store onboarding process, including page creation and initial settings configuration.

## Base URL

All Onboarding API endpoints are prefixed with the same base URL as the core API:

```
/wp-json/fluent-cart/v2/
```

## Authentication

All Onboarding API endpoints require:
- **Policy**: `AdminPolicy`

## Onboarding Data

### Get Onboarding Data

Retrieve onboarding configuration including available pages, currencies, and default settings.

**Endpoint:** `GET /onboarding/`

**Permission Required**: `AdminPolicy`

#### Response

```json
{
  "success": true,
  "data": {
    "pages": [
      {
        "key": "checkout_page_id",
        "title": "Checkout Page",
        "page_id": null
      },
      {
        "key": "customer_profile_page_id",
        "title": "Customer Profile Page",
        "page_id": null
      }
    ],
    "currencies": [
      {
        "code": "USD",
        "name": "US Dollar",
        "symbol": "$"
      }
    ],
    "default_settings": {
      "store_name": "My Store",
      "store_email": "store@example.com"
    }
  }
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v2/onboarding/" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Save Onboarding Settings

Save initial store settings during onboarding.

**Endpoint:** `POST /onboarding/`

**Permission Required**: `AdminPolicy`

#### Request Body

The request body should contain store settings to save. Can include:
- Store name, email, address
- Currency settings
- Page IDs
- Category selection (optional, triggers dummy product creation)

```json
{
  "store_name": "My New Store",
  "store_email": "store@example.com",
  "currency": "USD",
  "category": "electronics"
}
```

#### Response

```json
{
  "success": true,
  "data": {
    "message": "Store has been updated successfully"
  }
}
```

#### Example Request

```bash
curl -X POST "https://yoursite.com/wp-json/fluent-cart/v2/onboarding/" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ=" \
  -H "Content-Type: application/json" \
  -d '{
    "store_name": "My New Store",
    "store_email": "store@example.com",
    "currency": "USD"
  }'
```

### Create Pages

Create all required FluentCart pages at once.

**Endpoint:** `POST /onboarding/create-pages`

**Permission Required**: `AdminPolicy`

#### Response

Returns the same structure as `GET /onboarding/` with updated page IDs.

```json
{
  "success": true,
  "data": {
    "pages": [
      {
        "key": "checkout_page_id",
        "title": "Checkout Page",
        "page_id": 123
      }
    ],
    "currencies": [],
    "default_settings": {}
  }
}
```

#### Example Request

```bash
curl -X POST "https://yoursite.com/wp-json/fluent-cart/v2/onboarding/create-pages" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Create Single Page

Create a single specific page.

**Endpoint:** `POST /onboarding/create-page`

**Permission Required**: `AdminPolicy`

#### Request Body

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `content` | string | Yes | Page key (e.g., `'checkout_page_id'`) |
| `page_name` | string | Yes | Page title/name |
| `save_settings` | boolean | No | Whether to save the page ID to settings (default: false) |

```json
{
  "content": "checkout_page_id",
  "page_name": "Checkout",
  "save_settings": true
}
```

#### Response

```json
{
  "success": true,
  "data": {
    "page_id": 123,
    "page_name": "Checkout",
    "link": "https://yoursite.com/checkout/"
  }
}
```

#### Example Request

```bash
curl -X POST "https://yoursite.com/wp-json/fluent-cart/v2/onboarding/create-page" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ=" \
  -H "Content-Type: application/json" \
  -d '{
    "content": "checkout_page_id",
    "page_name": "Checkout",
    "save_settings": true
  }'
```

## Error Handling

### Common Error Responses

#### Unable to Create Page

```json
{
  "success": false,
  "data": {
    "message": "Unable to create page"
  }
}
```

#### Failed to Update

```json
{
  "success": false,
  "data": {
    "errors": "Failed to update!"
  }
}
```

## Notes

- Pages are created as WordPress pages with the `'publish'` status
- If `save_settings` is true, the page ID is saved to store settings and rewrite rules are flushed
- Providing a `category` in save settings triggers creation of dummy products for that category
- Pages that already exist are excluded from bulk creation

---

**Related Documentation:**
- [Settings API](./settings) - Store settings management
- [Dashboard API](./dashboard) - Dashboard and onboarding status

