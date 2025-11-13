---
title: Notes API
description: FluentCart Notes API for attaching notes to orders.
---

# Notes API

The Notes API provides endpoints for attaching notes to orders in FluentCart.

## Base URL

All Notes API endpoints are prefixed with the same base URL as the core API:

```
/wp-json/fluent-cart/v2/
```

## Authentication

All Notes API endpoints require:
- **Policy**: `AdminPolicy`

## Order Notes

### Attach Note to Order

Attach or update a note on an order.

**Endpoint:** `POST /notes/attach`

**Permission Required**: `AdminPolicy`

#### Request Body

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `order_id` | int | Yes | Order ID |
| `note` | string | Yes | Note text content |

```json
{
  "order_id": 123,
  "note": "Customer requested expedited shipping. Contacted via email."
}
```

#### Response

```json
{
  "success": true,
  "data": {
    "message": "Order Note Updated successfully."
  }
}
```

#### Example Request

```bash
curl -X POST "https://yoursite.com/wp-json/fluent-cart/v2/notes/attach" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ=" \
  -H "Content-Type: application/json" \
  -d '{
    "order_id": 123,
    "note": "Customer requested expedited shipping."
  }'
```

## Error Handling

### Common Error Responses

#### Order Not Found

```json
{
  "success": false,
  "data": {
    "message": "Order not found"
  }
}
```

#### Failed to Update

```json
{
  "success": false,
  "data": {
    "message": "Failed to update order note."
  }
}
```

## Notes

- Notes are stored directly on the order record
- Notes are sanitized as text before saving
- Notes can be updated by sending a new note for the same order
- Notes are visible in the order details view

---

**Related Documentation:**
- [Orders API](./orders) - Order management

