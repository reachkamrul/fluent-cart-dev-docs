---
title: Labels API
description: FluentCart Labels API for managing labels and label assignments.
---

# Labels API

The Labels API provides endpoints for managing labels and assigning them to orders, customers, and other entities in FluentCart.

## Base URL

All Labels API endpoints are prefixed with the same base URL as the core API:

```
/wp-json/fluent-cart/v2/
```

## Authentication

All Labels API endpoints require:
- **Policy**: `LabelPolicy`
- **Permissions**: Varies by endpoint (see individual endpoints)

## Labels

### List Labels

Retrieve all available labels.

**Endpoint:** `GET /labels/`

**Permission Required**: `labels/view`

#### Response

```json
{
  "labels": [
    {
      "id": 1,
      "value": "VIP Customer",
      "color": "#FF5733",
      "created_at": "2024-01-01 10:00:00",
      "updated_at": "2024-01-01 10:00:00"
    },
    {
      "id": 2,
      "value": "High Priority",
      "color": "#33FF57",
      "created_at": "2024-01-01 10:00:00",
      "updated_at": "2024-01-01 10:00:00"
    }
  ]
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v2/labels/" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Create Label

Create a new label.

**Endpoint:** `POST /labels/`

**Permission Required**: `labels/manage`

#### Request Body

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `value` | string | Yes | Label text/value |
| `color` | string | No | Label color (hex code) |

```json
{
  "value": "New Customer",
  "color": "#3366FF"
}
```

#### Response

```json
{
  "success": true,
  "data": {
    "id": 3,
    "value": "New Customer",
    "color": "#3366FF",
    "created_at": "2024-01-15 11:30:00",
    "updated_at": "2024-01-15 11:30:00"
  }
}
```

#### Example Request

```bash
curl -X POST "https://yoursite.com/wp-json/fluent-cart/v2/labels/" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ=" \
  -H "Content-Type: application/json" \
  -d '{
    "value": "New Customer",
    "color": "#3366FF"
  }'
```

### Update Label Selections

Update which labels are assigned to a specific entity (order, customer, etc.).

**Endpoint:** `POST /labels/update-selections`

**Permission Required**: `labels/manage`

#### Request Body

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `bind_to_type` | string | Yes | Model type (e.g., `'Order'`, `'Customer'`) |
| `bind_to_id` | int | Yes | Entity ID to attach labels to |
| `selectedLabels` | array | Yes | Array of label IDs to assign |

```json
{
  "bind_to_type": "Order",
  "bind_to_id": 123,
  "selectedLabels": [1, 2, 3]
}
```

#### Response

```json
{
  "success": true,
  "data": {
    "message": "Labels Updated Successfully"
  }
}
```

#### Example Request

```bash
curl -X POST "https://yoursite.com/wp-json/fluent-cart/v2/labels/update-selections" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ=" \
  -H "Content-Type: application/json" \
  -d '{
    "bind_to_type": "Order",
    "bind_to_id": 123,
    "selectedLabels": [1, 2]
  }'
```

## Error Handling

### Common Error Responses

#### Validation Error

```json
{
  "success": false,
  "data": {
    "message": "Validation failed"
  }
}
```

#### Failed to Update

```json
{
  "success": false,
  "data": {
    "message": "Failed To Update Labels"
  }
}
```

## Notes

- Labels can be assigned to multiple entity types (orders, customers, products, etc.)
- When updating label selections, provide the full array of label IDs you want assigned
- Labels are polymorphic and can be attached to any model that supports labels
- The `bind_to_type` can be a simple class name (e.g., `'Order'`) or a fully qualified class name

---

**Related Documentation:**
- [Orders API](./orders) - Order management
- [Customers API](./customers) - Customer management

