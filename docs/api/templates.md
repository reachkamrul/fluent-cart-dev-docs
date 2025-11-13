---
title: Templates API
description: FluentCart Templates API for managing print templates (invoices, packing slips, etc.).
---

# Templates API

The Templates API provides endpoints for managing print templates such as invoices, packing slips, and shipping labels in FluentCart.

## Base URL

All Templates API endpoints are prefixed with the same base URL as the core API:

```
/wp-json/fluent-cart/v2/
```

## Authentication

All Templates API endpoints require:
- **Policy**: `AdminPolicy`

## Print Templates

### Get Print Templates

Retrieve all available print templates.

**Endpoint:** `GET /templates/print-templates`

**Permission Required**: `AdminPolicy`

#### Response

```json
{
  "success": true,
  "data": {
    "templates": [
      {
        "key": "invoice_template",
        "title": "Invoice Template",
        "content": "<html>...</html>"
      },
      {
        "key": "packing_slip",
        "title": "Packing Slip Template",
        "content": "<html>...</html>"
      },
      {
        "key": "delivery_slip",
        "title": "Delivery Slip Template",
        "content": "<html>...</html>"
      },
      {
        "key": "shipping_slip",
        "title": "Shipping Slip Template",
        "content": "<html>...</html>"
      },
      {
        "key": "dispatch_slip",
        "title": "Dispatch Slip Template",
        "content": "<html>...</html>"
      }
    ]
  }
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v2/templates/print-templates" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Save Print Templates

Update print template content.

**Endpoint:** `PUT /templates/print-templates`

**Permission Required**: `AdminPolicy`

#### Request Body

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `templates` | array | Yes | Array of template objects |

Each template object should contain:
- `key` (string, required): Template key identifier
- `content` (string, required): HTML content of the template

```json
{
  "templates": [
    {
      "key": "invoice_template",
      "content": "<html><body><h1>Invoice</h1>...</body></html>"
    },
    {
      "key": "packing_slip",
      "content": "<html><body><h1>Packing Slip</h1>...</body></html>"
    }
  ]
}
```

#### Response

```json
{
  "success": true,
  "data": {
    "message": "Template saved successfully"
  }
}
```

#### Example Request

```bash
curl -X PUT "https://yoursite.com/wp-json/fluent-cart/v2/templates/print-templates" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ=" \
  -H "Content-Type: application/json" \
  -d '{
    "templates": [
      {
        "key": "invoice_template",
        "content": "<html><body><h1>Invoice</h1></body></html>"
      }
    ]
  }'
```

## Available Template Keys

- `invoice_template` - Invoice template
- `packing_slip` - Packing slip template
- `delivery_slip` - Delivery slip template
- `shipping_slip` - Shipping slip template
- `dispatch_slip` - Dispatch slip template

## Error Handling

### Common Error Responses

#### Validation Error

```json
{
  "success": false,
  "data": {
    "message": "Invalid template data"
  }
}
```

## Notes

- Template content is sanitized using `wp_kses_post` before saving
- If a template doesn't exist, the default template content is returned
- Templates support HTML and can include shortcodes for dynamic content
- Template content is stored in WordPress options

---

**Related Documentation:**
- [Orders API](./orders) - Order management
- [Settings API](./settings) - Store settings

