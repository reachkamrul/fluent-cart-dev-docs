---
title: Activity API
description: FluentCart Activity API for managing activity logs.
---

# Activity API

The Activity API provides endpoints for managing activity logs in FluentCart.

## Base URL

All Activity API endpoints are prefixed with the same base URL as the core API:

```
/wp-json/fluent-cart/v2/
```

## Authentication

All Activity API endpoints require:
- **Policy**: `AdminPolicy`

## Activities

### List Activities

Retrieve a paginated list of activity logs.

**Endpoint:** `GET /activity/`

**Permission Required**: `AdminPolicy`

#### Query Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `search` | string | No | Search term for filtering activities |
| `per_page` | int | No | Number of items per page (default: 10) |
| `page` | int | No | Page number (default: 1) |
| `log_type` | string | No | Filter by log type |
| `module_name` | string | No | Filter by module name |
| `module_id` | int | No | Filter by module ID |

#### Response

```json
{
  "success": true,
  "data": {
    "activities": {
      "data": [
        {
          "id": 1,
          "title": "Order Created",
          "description": "Order #1234 was created",
          "log_type": "info",
          "module_name": "order",
          "module_id": 1234,
          "read_status": "unread",
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
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v2/activity/?per_page=20&page=1" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Delete Activity

Delete a specific activity log entry.

**Endpoint:** `DELETE /activity/{id}`

**Permission Required**: `AdminPolicy`

#### Route Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | int | Yes | Activity ID (route parameter) |

#### Response

```json
{
  "success": true,
  "data": {
    "message": "Activity Deleted Successfully"
  }
}
```

#### Example Request

```bash
curl -X DELETE "https://yoursite.com/wp-json/fluent-cart/v2/activity/1" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Mark Activity as Read/Unread

Update the read status of an activity log entry.

**Endpoint:** `PUT /activity/{id}/mark-read`

**Permission Required**: `AdminPolicy`

#### Route Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | int | Yes | Activity ID (route parameter) |

#### Request Body

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `status` | string | Yes | Status: `'read'` or `'unread'` |

```json
{
  "status": "read"
}
```

#### Response

```json
{
  "success": true,
  "data": {
    "message": "Activity Marked as Read"
  }
}
```

#### Example Request

```bash
curl -X PUT "https://yoursite.com/wp-json/fluent-cart/v2/activity/1/mark-read" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ=" \
  -H "Content-Type: application/json" \
  -d '{
    "status": "read"
  }'
```

## Error Handling

### Common Error Responses

#### Not Found

```json
{
  "success": false,
  "data": {
    "message": "Activity not found"
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

- Activities are automatically created for various actions (order creation, customer updates, etc.)
- Activities can be filtered by module name and module ID
- Read/unread status helps track which activities have been reviewed
- Activities are paginated for performance

---

**Related Documentation:**
- [Orders API](./orders) - Order management
- [Customers API](./customers) - Customer management

