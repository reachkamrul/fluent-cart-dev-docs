---
title: Options/Attributes API
description: FluentCart Options/Attributes API for managing product attribute groups and terms.
---

# Options/Attributes API

The Options/Attributes API provides endpoints for managing product attribute groups and attribute terms in FluentCart. These are used to create product variations and options.

## Base URL

All Options/Attributes API endpoints are prefixed with the same base URL as the core API:

```
/wp-json/fluent-cart/v2/
```

## Authentication

All Options/Attributes API endpoints require:
- **Policy**: `ProductPolicy`
- **Permissions**: Varies by endpoint (see individual endpoints)

## Attribute Groups

Attribute groups define categories of attributes (e.g., "Color", "Size", "Material").

### List Attribute Groups

Retrieve all attribute groups.

**Endpoint:** `GET /options/attr/groups`

**Permission Required**: `products/view`

#### Query Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `search` | string | No | Search term for filtering groups |
| `per_page` | int | No | Number of items per page |
| `page` | int | No | Page number |

#### Response

```json
{
  "groups": [
    {
      "id": 1,
      "title": "Color",
      "slug": "color",
      "description": "Product color options",
      "settings": {},
      "created_at": "2024-01-01 10:00:00",
      "updated_at": "2024-01-01 10:00:00"
    }
  ]
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v2/options/attr/groups" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Get Attribute Group

Retrieve details for a specific attribute group.

**Endpoint:** `GET /options/attr/group/{group_id}`

**Permission Required**: `products/view`

#### Route Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `group_id` | int | Yes | Attribute group ID (route parameter) |

#### Response

```json
{
  "group": {
    "id": 1,
    "title": "Color",
    "slug": "color",
    "description": "Product color options",
    "settings": {},
    "terms": [
      {
        "id": 1,
        "title": "Red",
        "slug": "red"
      }
    ],
    "created_at": "2024-01-01 10:00:00",
    "updated_at": "2024-01-01 10:00:00"
  }
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v2/options/attr/group/1" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Create Attribute Group

Create a new attribute group.

**Endpoint:** `POST /options/attr/group/`

**Permission Required**: `products/create`

#### Request Body

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `title` | string | Yes | Group title |
| `slug` | string | No | Group slug (auto-generated from title if not provided) |
| `description` | string | No | Group description |
| `settings` | object | No | Group settings |

```json
{
  "title": "Size",
  "slug": "size",
  "description": "Product size options",
  "settings": {}
}
```

#### Response

```json
{
  "success": true,
  "data": {
    "id": 2,
    "title": "Size",
    "slug": "size",
    "description": "Product size options",
    "created_at": "2024-01-01 10:00:00",
    "updated_at": "2024-01-01 10:00:00"
  }
}
```

#### Example Request

```bash
curl -X POST "https://yoursite.com/wp-json/fluent-cart/v2/options/attr/group/" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ=" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Size",
    "description": "Product size options"
  }'
```

### Update Attribute Group

Update an existing attribute group.

**Endpoint:** `PUT /options/attr/group/{group_id}`

**Permission Required**: `products/edit`

#### Route Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `group_id` | int | Yes | Attribute group ID (route parameter) |

#### Request Body

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `title` | string | Yes | Group title |
| `slug` | string | No | Group slug |
| `description` | string | No | Group description |
| `settings` | object | No | Group settings |

```json
{
  "title": "Size - Updated",
  "description": "Updated description"
}
```

#### Response

```json
{
  "success": true,
  "data": {
    "id": 2,
    "title": "Size - Updated",
    "slug": "size",
    "description": "Updated description",
    "updated_at": "2024-01-15 11:30:00"
  }
}
```

### Delete Attribute Group

Delete an attribute group. The group can only be deleted if its terms are not in use.

**Endpoint:** `DELETE /options/attr/group/{group_id}`

**Permission Required**: `products/delete`

#### Route Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `group_id` | int | Yes | Attribute group ID (route parameter) |

#### Response

```json
{
  "success": true,
  "data": {
    "message": "Attribute group deleted successfully"
  }
}
```

## Attribute Terms

Attribute terms are the individual values within an attribute group (e.g., "Red", "Blue", "Green" for the "Color" group).

### List Attribute Terms

Retrieve all terms for a specific attribute group.

**Endpoint:** `GET /options/attr/group/{group_id}/terms`

**Permission Required**: `products/view`

#### Route Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `group_id` | int | Yes | Attribute group ID (route parameter) |

#### Query Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `search` | string | No | Search term for filtering terms |
| `per_page` | int | No | Number of items per page |
| `page` | int | No | Page number |

#### Response

```json
{
  "terms": [
    {
      "id": 1,
      "group_id": 1,
      "title": "Red",
      "slug": "red",
      "description": "",
      "serial": 1,
      "settings": {},
      "created_at": "2024-01-01 10:00:00",
      "updated_at": "2024-01-01 10:00:00"
    },
    {
      "id": 2,
      "group_id": 1,
      "title": "Blue",
      "slug": "blue",
      "serial": 2,
      "created_at": "2024-01-01 10:00:00",
      "updated_at": "2024-01-01 10:00:00"
    }
  ]
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v2/options/attr/group/1/terms" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Create Attribute Term

Create a new attribute term within an attribute group.

**Endpoint:** `POST /options/attr/group/{group_id}/term`

**Permission Required**: `products/create`

#### Route Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `group_id` | int | Yes | Attribute group ID (route parameter) |

#### Request Body

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `title` | string | Yes | Term title |
| `slug` | string | No | Term slug (auto-generated from title if not provided) |
| `description` | string | No | Term description |
| `serial` | int | No | Display order |
| `settings` | object | No | Term settings |

```json
{
  "title": "Green",
  "slug": "green",
  "description": "Green color option",
  "serial": 3
}
```

#### Response

```json
{
  "success": true,
  "data": {
    "id": 3,
    "group_id": 1,
    "title": "Green",
    "slug": "green",
    "serial": 3,
    "created_at": "2024-01-01 10:00:00",
    "updated_at": "2024-01-01 10:00:00"
  }
}
```

#### Example Request

```bash
curl -X POST "https://yoursite.com/wp-json/fluent-cart/v2/options/attr/group/1/term" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ=" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Green",
    "serial": 3
  }'
```

### Update Attribute Term

Update an existing attribute term.

**Endpoint:** `POST /options/attr/group/{group_id}/term/{term_id}`

**Permission Required**: `products/edit`

#### Route Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `group_id` | int | Yes | Attribute group ID (route parameter) |
| `term_id` | int | Yes | Attribute term ID (route parameter) |

#### Request Body

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `title` | string | Yes | Term title |
| `slug` | string | No | Term slug |
| `description` | string | No | Term description |
| `serial` | int | No | Display order |
| `settings` | object | No | Term settings |

```json
{
  "title": "Dark Green",
  "description": "Dark green color option",
  "serial": 3
}
```

#### Response

```json
{
  "success": true,
  "data": {
    "id": 3,
    "group_id": 1,
    "title": "Dark Green",
    "slug": "green",
    "serial": 3,
    "updated_at": "2024-01-15 11:30:00"
  }
}
```

### Delete Attribute Term

Delete an attribute term.

**Endpoint:** `DELETE /options/attr/group/{group_id}/term/{term_id}`

**Permission Required**: `products/delete`

#### Route Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `group_id` | int | Yes | Attribute group ID (route parameter) |
| `term_id` | int | Yes | Attribute term ID (route parameter) |

#### Response

```json
{
  "success": true,
  "data": {
    "message": "Attribute term deleted successfully"
  }
}
```

### Change Term Serial (Order)

Update the display order (serial) of an attribute term.

**Endpoint:** `POST /options/attr/group/{group_id}/term/{term_id}/serial`

**Permission Required**: `products/edit`

#### Route Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `group_id` | int | Yes | Attribute group ID (route parameter) |
| `term_id` | int | Yes | Attribute term ID (route parameter) |

#### Request Body

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `direction` | string | Yes | Direction to move: `'up'` or `'down'` |

```json
{
  "direction": "up"
}
```

#### Response

```json
{
  "success": true,
  "data": {
    "message": "Term serial updated successfully"
  }
}
```

#### Example Request

```bash
curl -X POST "https://yoursite.com/wp-json/fluent-cart/v2/options/attr/group/1/term/3/serial" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ=" \
  -H "Content-Type: application/json" \
  -d '{
    "direction": "up"
  }'
```

## Error Handling

### Common Error Responses

#### Validation Error

```json
{
  "success": false,
  "data": {
    "message": "Title is required"
  }
}
```

#### Not Found Error

```json
{
  "success": false,
  "data": {
    "message": "Attribute group not found"
  }
}
```

#### Cannot Delete (In Use)

```json
{
  "success": false,
  "data": {
    "message": "Cannot delete attribute group. Terms are in use."
  }
}
```

## Notes

- Attribute groups define categories of product attributes
- Attribute terms are the individual values within each group
- Terms have a `serial` field that determines their display order
- Groups can only be deleted if their terms are not in use
- Terms are used to create product variations
- The `slug` field is auto-generated from the `title` if not provided

---

**Related Documentation:**
- [Products API](./products) - Product management and variations
- [Settings API](./settings) - Store settings

