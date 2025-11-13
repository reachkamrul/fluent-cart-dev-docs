---
title: Variants API
description: FluentCart Variants API for listing product variants.
---

# Variants API

The Variants API provides endpoints for retrieving product variants in FluentCart.

## Base URL

All Variants API endpoints are prefixed with the same base URL as the core API:

```
/wp-json/fluent-cart/v2/
```

## Authentication

All Variants API endpoints require:
- **Policy**: `ProductPolicy`

## Variants

### List Variants

Retrieve all product variants.

**Endpoint:** `GET /variants/`

**Permission Required**: `ProductPolicy`

#### Query Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `params` | object | No | Optional parameters for filtering/searching |

#### Response

```json
[
  {
    "id": 1,
    "post_id": 100,
    "variation_title": "Product Variant 1",
    "serial_index": 1,
    "stock_status": "in-stock",
    "available": 1,
    "total_stock": 10,
    "payment_type": "onetime",
    "fulfillment_type": "physical",
    "created_at": "2024-01-01 10:00:00",
    "updated_at": "2024-01-01 10:00:00"
  },
  {
    "id": 2,
    "post_id": 100,
    "variation_title": "Product Variant 2",
    "serial_index": 2,
    "stock_status": "in-stock",
    "available": 1,
    "total_stock": 5,
    "payment_type": "onetime",
    "fulfillment_type": "physical",
    "created_at": "2024-01-01 10:00:00",
    "updated_at": "2024-01-01 10:00:00"
  }
]
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v2/variants/" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

## Notes

- This endpoint returns all product variants in the system
- Variants are linked to products via `post_id`
- The `serial_index` determines the display order of variants
- For more detailed variant management (create, update, delete), see the Products API variant endpoints

---

**Related Documentation:**
- [Products API](./products) - Product and variant management

