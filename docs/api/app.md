---
title: App API
description: FluentCart App API for application initialization and attachment management.
---

# App API

The App API provides endpoints for application initialization, retrieving configuration, and managing attachments in FluentCart.

## Base URL

All App API endpoints are prefixed with the same base URL as the core API:

```
/wp-json/fluent-cart/v2/
```

## Authentication

All App API endpoints require:
- **Policy**: `AdminPolicy`

## Application Initialization

### Initialize App

Retrieve application initialization data including REST API info, asset URLs, translations, and shop configuration.

**Endpoint:** `GET /app/init`

**Permission Required**: `AdminPolicy`

#### Response

```json
{
  "success": true,
  "data": {
    "rest": {
      "namespace": "fluent-cart/v2",
      "base_url": "https://yoursite.com/wp-json/fluent-cart/v2"
    },
    "asset_url": "https://yoursite.com/wp-content/plugins/fluent-cart/assets/",
    "trans": {
      "common": {
        "save": "Save",
        "cancel": "Cancel"
      }
    },
    "shop": {
      "name": "My Store",
      "currency": "USD"
    }
  }
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v2/app/init" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

## Attachments

### Get Attachments

Retrieve all image attachments from the WordPress media library.

**Endpoint:** `GET /app/attachments`

**Permission Required**: `AdminPolicy`

#### Response

```json
{
  "success": true,
  "data": {
    "attachments": [
      {
        "id": 123,
        "title": "Product Image",
        "url": "https://yoursite.com/wp-content/uploads/2024/01/image.jpg"
      },
      {
        "id": 124,
        "title": "Logo",
        "url": "https://yoursite.com/wp-content/uploads/2024/01/logo.png"
      }
    ]
  }
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v2/app/attachments" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Upload Attachments

Upload an image file to the WordPress media library.

**Endpoint:** `POST /app/upload-attachments`

**Permission Required**: `AdminPolicy`

#### Request Body

This endpoint accepts multipart/form-data with a file field.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `file` | file | Yes | Image file to upload |

#### Response

```json
{
  "id": 125,
  "title": "uploaded-image",
  "url": "https://yoursite.com/wp-content/uploads/2024/01/uploaded-image.jpg"
}
```

#### Example Request

```bash
curl -X POST "https://yoursite.com/wp-json/fluent-cart/v2/app/upload-attachments" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ=" \
  -F "file=@/path/to/image.jpg"
```

## Error Handling

### Common Error Responses

#### No Images Found

```json
{
  "success": false,
  "data": {
    "message": "No Images Found"
  }
}
```

#### Error Uploading File

```json
{
  "success": false,
  "data": {
    "error": ["Error uploading file"]
  }
}
```

#### No File Attached

```json
{
  "success": false,
  "data": {
    "message": "No File Attached"
  }
}
```

## Notes

- Only image files are supported for uploads
- Uploaded files are processed through WordPress media handling
- Attachments endpoint returns all images from the media library
- The init endpoint provides essential configuration for frontend applications
- Asset URLs point to the plugin's asset directory

---

**Related Documentation:**
- [Files API](./files) - File management with storage drivers
- [Settings API](./settings) - Store settings management

