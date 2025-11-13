---
title: Widgets API
description: FluentCart Widgets API for retrieving dynamic widgets.
---

# Widgets API

The Widgets API provides an endpoint for retrieving dynamic widgets based on filters in FluentCart.

## Base URL

All Widgets API endpoints are prefixed with the same base URL as the core API:

```
/wp-json/fluent-cart/v2/
```

## Authentication

The Widgets API endpoint requires:
- **Permission**: At least one of `customers/view` or `orders/view`

## Widgets

### Get Widgets

Retrieve widgets based on a filter type.

**Endpoint:** `GET /widgets`

**Permission Required**: `customers/view` OR `orders/view`

#### Query Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `filter` | string | Yes | Widget filter identifier (e.g., `'fluent_cart_single_customer'`, `'fluent_cart_single_order'`) |
| `data` | object | No | Additional data to pass to the widget filter |

#### Response

```json
{
  "success": true,
  "data": {
    "widgets": [
      {
        "title": "Customer Overview",
        "body": "<div>Customer statistics...</div>"
      },
      {
        "title": "Recent Orders",
        "body": "<div>Order list...</div>"
      }
    ]
  }
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v2/widgets?filter=fluent_cart_single_customer&data[customer_id]=123" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

## Widget Filters

Widgets are retrieved through WordPress filters. Common filter names include:

- `fluent_cart_single_customer` - Widgets for a single customer view
- `fluent_cart_single_order` - Widgets for a single order view
- `fluent_cart_dashboard` - Dashboard widgets

The `fluent_cart_` prefix is automatically removed from the filter parameter.

## Error Handling

### Common Error Responses

#### Permission Denied

```json
{
  "success": false,
  "data": {
    "message": "You do not have permission to access this resource"
  }
}
```

## Notes

- Widgets are dynamically generated through WordPress filters
- The filter name should include the `fluent_cart_` prefix (it will be automatically removed)
- Widget content is typically HTML that can be rendered in the admin interface
- Different widget filters may require different data parameters
- Widgets can be extended by third-party plugins using WordPress filters

---

**Related Documentation:**
- [Customers API](./customers) - Customer management
- [Orders API](./orders) - Order management
- [Dashboard API](./dashboard) - Dashboard statistics

