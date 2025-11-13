---
title: Taxes API
description: FluentCart Taxes API for managing tax filing and tax records.
---

# Taxes API

The Taxes API provides endpoints for managing tax records and marking taxes as filed. This is different from the Tax API which manages tax rates and classes.

## Base URL

All Taxes API endpoints are prefixed with the same base URL as the core API:

```
/wp-json/fluent-cart/v2/
```

## Authentication

All Taxes API endpoints require:
- **Policy**: `AdminPolicy`

## Tax Records

### List Tax Records

Retrieve a paginated list of tax records.

**Endpoint:** `GET /taxes/`

**Permission Required**: `AdminPolicy`

#### Query Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `search` | string | No | Search term for filtering taxes |
| `per_page` | int | No | Number of items per page (default: 10) |
| `page` | int | No | Page number (default: 1) |
| `filed` | boolean | No | Filter by filed status |
| `country` | string | No | Filter by country code |

#### Response

```json
{
  "success": true,
  "data": {
    "taxes": {
      "data": [
        {
          "id": 1,
          "order_id": 123,
          "country": "US",
          "state": "CA",
          "rate": 7.5,
          "amount": 7.50,
          "filed_at": null,
          "created_at": "2024-01-01 10:00:00"
        },
        {
          "id": 2,
          "order_id": 124,
          "country": "US",
          "state": "NY",
          "rate": 8.0,
          "amount": 8.00,
          "filed_at": "2024-01-15 10:00:00",
          "created_at": "2024-01-01 10:00:00"
        }
      ],
      "total": 100,
      "per_page": 10,
      "current_page": 1,
      "last_page": 10
    }
  }
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v2/taxes/?per_page=20&page=1" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Mark Taxes as Filed

Mark one or more tax records as filed.

**Endpoint:** `POST /taxes/`

**Permission Required**: `AdminPolicy`

#### Request Body

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `ids` | array | Yes | Array of tax record IDs to mark as filed |

```json
{
  "ids": [1, 2, 3, 4, 5]
}
```

#### Response

```json
{
  "success": true,
  "data": {
    "message": "Taxes marked as filed successfully"
  }
}
```

#### Example Request

```bash
curl -X POST "https://yoursite.com/wp-json/fluent-cart/v2/taxes/" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ=" \
  -H "Content-Type: application/json" \
  -d '{
    "ids": [1, 2, 3]
  }'
```

## Error Handling

### Common Error Responses

#### No IDs Provided

```json
{
  "success": false,
  "data": {
    "message": "No IDs provided to mark!"
  }
}
```

#### Permission Denied

```json
{
  "success": false,
  "data": {
    "message": "You do not have permission to perform this action"
  }
}
```

## Notes

- Tax records are automatically created when orders are placed
- Only unfiled taxes can be marked as filed
- The `filed_at` timestamp is set to the current GMT time when marked as filed
- Tax records are linked to orders and include country, state, rate, and amount information
- This API is for tax filing management, not tax rate configuration (see [Tax API](./tax))

---

**Related Documentation:**
- [Tax API](./tax) - Tax rates and classes management
- [Orders API](./orders) - Order management

