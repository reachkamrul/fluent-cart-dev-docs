---
title: Checkout Fields API
description: FluentCart Checkout Fields API for managing custom checkout field configurations.
---

# Checkout Fields API

The Checkout Fields API provides endpoints for managing custom checkout field configurations in FluentCart.

## Base URL

All Checkout Fields API endpoints are prefixed with the same base URL as the core API:

```
/wp-json/fluent-cart/v2/
```

## Authentication

All Checkout Fields API endpoints require:
- **Policy**: `StoreSensitivePolicy`

## Checkout Fields

### Get Checkout Fields

Retrieve checkout field schema configuration and settings.

**Endpoint:** `GET /checkout-fields/get-fields`

**Permission Required**: `StoreSensitivePolicy`

#### Response

```json
{
  "fields": {
    "billing": {
      "first_name": {
        "label": "First Name",
        "required": true,
        "type": "text"
      },
      "last_name": {
        "label": "Last Name",
        "required": true,
        "type": "text"
      }
    },
    "shipping": {
      "first_name": {
        "label": "First Name",
        "required": true,
        "type": "text"
      }
    }
  },
  "settings": {
    "enable_shipping_fields": true,
    "enable_billing_fields": true
  }
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v2/checkout-fields/get-fields" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Save Checkout Fields

Update checkout field settings.

**Endpoint:** `POST /checkout-fields/save-fields`

**Permission Required**: `StoreSensitivePolicy`

#### Request Body

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `settings` | object | Yes | Checkout field settings object |

```json
{
  "settings": {
    "enable_shipping_fields": true,
    "enable_billing_fields": true,
    "billing_first_name_required": true,
    "billing_last_name_required": true
  }
}
```

#### Response

```json
{
  "message": "Checkout fields has been updated successfully."
}
```

#### Example Request

```bash
curl -X POST "https://yoursite.com/wp-json/fluent-cart/v2/checkout-fields/save-fields" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ=" \
  -H "Content-Type: application/json" \
  -d '{
    "settings": {
      "enable_shipping_fields": true,
      "enable_billing_fields": true
    }
  }'
```

## Error Handling

### Common Error Responses

#### Validation Error

```json
{
  "success": false,
  "data": {
    "message": "Invalid settings"
  }
}
```

## Notes

- Checkout fields configuration affects the checkout form display
- Settings are validated against existing field schema
- Only valid settings keys are saved (invalid keys are filtered out)
- Field requirements can be customized per field type

---

**Related Documentation:**
- [Orders API](./orders) - Order management
- [Settings API](./settings) - Store settings

