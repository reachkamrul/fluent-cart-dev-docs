---
title: Dashboard API
description: FluentCart Dashboard API for retrieving dashboard statistics and onboarding data.
---

# Dashboard API

The Dashboard API provides endpoints for retrieving dashboard statistics and onboarding data in FluentCart.

## Base URL

All Dashboard API endpoints are prefixed with the same base URL as the core API:

```
/wp-json/fluent-cart/v2/
```

## Authentication

Dashboard API endpoints require:
- **Policy**: `AdminPolicy` or `DashboardPolicy`
- **Permissions**: Varies by endpoint (see individual endpoints)

## Dashboard Statistics

### Get Dashboard Stats

Retrieve dashboard statistics and widgets.

**Endpoint:** `GET /dashboard/stats`

**Policy**: `DashboardPolicy`

**Permission Required**: `dashboard_stats/view`

#### Query Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `params` | object | No | Optional parameters for filtering stats |

#### Response

```json
{
  "success": true,
  "data": {
    "stats": [
      {
        "title": "Total Revenue",
        "value": "10000.00",
        "currency": "USD"
      }
    ]
  }
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v2/dashboard/stats" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

## Onboarding

### Get Onboarding Data

Retrieve onboarding steps and completion status.

**Endpoint:** `GET /dashboard/`

**Policy**: `AdminPolicy`

#### Response

```json
{
  "steps": {
    "page_setup": {
      "title": "Setup Pages",
      "text": "Customers to find what they're looking for by organising.",
      "icon": "Cart",
      "completed": false,
      "url": "https://yoursite.com/wp-admin/admin.php?page=fluent-cart#/settings/store-settings/pages_setup"
    },
    "store_info": {
      "title": "Add Details to Store",
      "text": "Store details such as addresses, company info etc.",
      "icon": "StoreIcon",
      "completed": false,
      "url": "https://yoursite.com/wp-admin/admin.php?page=fluent-cart#/settings/store-settings/"
    },
    "product_info": {
      "title": "Add Your First Product",
      "text": "Share your brand story and build trust with customers.",
      "icon": "ShoppingCartIcon",
      "completed": false,
      "url": "https://yoursite.com/wp-admin/admin.php?page=fluent-cart#/products"
    },
    "setup_payments": {
      "title": "Setup Payment Methods",
      "text": "Choose from fast & secure online and offline payment.",
      "icon": "PaymentIcon",
      "completed": true,
      "url": "https://yoursite.com/wp-admin/admin.php?page=fluent-cart#/settings/payments"
    }
  },
  "completed": 1
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v2/dashboard/" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

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

- Dashboard stats are filtered based on user permissions
- Onboarding steps are automatically marked as completed based on store configuration
- The onboarding endpoint checks for:
  - Page setup completion
  - Store information completion
  - Product creation
  - Payment method setup

---

**Related Documentation:**
- [Reports API](./reports) - Detailed reporting endpoints
- [Settings API](./settings) - Store settings management

