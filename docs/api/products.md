---
title: Products API
description: FluentCart Products API documentation with complete endpoint reference and usage examples.
---

# Products API

The Products API provides comprehensive endpoints for managing products in FluentCart. This includes creating, reading, updating, and deleting products, as well as managing product variations, attributes, and integrations.

## Base URL

```
https://yoursite.com/wp-json/fluent-cart/v2/products
```

## Authentication

All endpoints require authentication and appropriate permissions:

- **Authentication**: WordPress Application Password or Cookie
- **Policy**: `ProductPolicy`
- **Permissions**: Various product-related permissions

## Endpoints

### List Products

**GET** `/products`

Retrieve a paginated list of products with optional filtering and searching.

#### Parameters

| Parameter | Type | Description | Default |
|-----------|------|-------------|---------|
| `page` | integer | Page number | 1 |
| `per_page` | integer | Items per page (max 100) | 10 |
| `search` | string | Search query | - |
| `filters` | object | Filter options | - |
| `order_by` | string | Sort field | id |
| `order_type` | string | Sort direction (ASC/DESC) | DESC |

#### Filter Options

```json
{
  "status": "publish",
  "type": "simple",
  "category": "electronics",
  "price_min": 1000,
  "price_max": 5000
}
```

#### Response

```json
{
  "products": {
    "current_page": 1,
    "data": [
      {
        "ID": 74,
        "post_author": "1",
        "post_date": "2025-09-24 05:12:35",
        "post_date_gmt": "2025-09-24 05:12:35",
        "post_content": "This stylish zipper hoodie is designed for versatility and comfort. Featuring a full-length zipper, it is easy to layer over t-shirts or under coats during cooler months. The hood offers added warmth, while the lightweight yet durable material ensures long-lasting wear. Ideal for casual outings, gym sessions, or simply lounging around, this hoodie provides a modern twist to the classic design.",
        "post_title": "Zipper Hoodie",
        "post_excerpt": "A stylish zipper hoodie with modern detailing, perfect for casual wear and layering during cooler months.",
        "post_status": "publish",
        "comment_status": "open",
        "ping_status": "closed",
        "post_password": "",
        "post_name": "zipper-hoodie-24-09-2025-05:12:35",
        "to_ping": "",
        "pinged": "",
        "post_modified": "2025-09-24 05:12:35",
        "post_modified_gmt": "2025-09-24 05:12:35",
        "post_content_filtered": "",
        "post_parent": "0",
        "guid": "https://yoursite.com/?items=zipper-hoodie-24-09-2025-05:12:35",
        "menu_order": "0",
        "post_type": "fluent-products",
        "post_mime_type": "",
        "comment_count": "0",
        "view_url": "https://yoursite.com/item/zipper-hoodie-24-09-2025-05:12:35/",
        "edit_url": "https://yoursite.com/wp-admin/post.php?post=74&action=edit"
      }
    ],
    "first_page_url": "https://yoursite.com/wp-json/fluent-cart/v2/products/?page=1",
    "from": 1,
    "last_page": 10,
    "last_page_url": "https://yoursite.com/wp-json/fluent-cart/v2/products/?page=10",
    "links": [
      {
        "url": null,
        "label": "pagination.previous",
        "active": false
      },
      {
        "url": "https://yoursite.com/wp-json/fluent-cart/v2/products/?page=1",
        "label": "1",
        "active": true
      },
      {
        "url": "https://yoursite.com/wp-json/fluent-cart/v2/products/?page=2",
        "label": "2",
        "active": false
      }
    ],
    "next_page_url": "https://yoursite.com/wp-json/fluent-cart/v2/products/?page=2",
    "path": "https://yoursite.com/wp-json/fluent-cart/v2/products",
    "per_page": 1,
    "prev_page_url": null,
    "to": 1,
    "total": 10
  }
}
```

#### Response Structure

The Products API returns a paginated response with the following structure:

**Product Object Fields:**
- `ID` - WordPress post ID
- `post_title` - Product title
- `post_content` - Product description
- `post_excerpt` - Product short description
- `post_status` - Product status (publish, draft, etc.)
- `post_name` - Product slug
- `post_type` - Always "fluent-products"
- `post_date` - Creation date
- `post_modified` - Last modification date
- `view_url` - Public product URL
- `edit_url` - Admin edit URL

**Pagination Fields:**
- `current_page` - Current page number
- `per_page` - Items per page
- `total` - Total number of products
- `last_page` - Last page number
- `from` - Starting item number
- `to` - Ending item number
- `first_page_url` - URL to first page
- `last_page_url` - URL to last page
- `next_page_url` - URL to next page
- `prev_page_url` - URL to previous page
- `links` - Array of pagination links

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v2/products?page=1&per_page=20&search=sample" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Create Product

**POST** `/products`

Create a new product.

#### Request Body

```json
{
  "post_title": "Dynamic Product",
  "post_content": "",
  "post_excerpt": "",
  "post_date": "Wed Sep 24 2025 15:44:07 GMT+0600 (Bangladesh Standard Time)",
  "post_status": "draft",
  "detail": {
    "fulfillment_type": "digital",
    "variation_type": "simple",
    "manage_stock": "0",
    "manage_downloadable": "0",
    "other_info": {
      "use_pricing_table": "yes",
      "group_pricing_by": "repeat_interval",
      "active_editor": "wp-editor",
      "sold_individually": "no"
    }
  }
}
```

#### Response

```json
{
    "data": {
        "ID": 7529320,
        "product_details": null
    },
    "message": "Product has been created successfully"
}
```

#### Example Request

```bash
curl --location 'https://yoursite.com/wp-json/fluent-cart/v2/products/' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic ZgdgeZXZwIHk5TEogV2pPNSBIbWpyIGd4dlUgYnlENQ==' \
--data '{
  "post_title": "Dynamic Product 2",
  "post_content": "",
  "post_excerpt": "",
  "post_date": "Wed Sep 24 2025 15:44:07 GMT+0600 (Bangladesh Standard Time)",
  "post_status": "draft",
  "detail": {
    "fulfillment_type": "digital",
    "variation_type": "simple",
    "manage_stock": "0",
    "manage_downloadable": "0",
    "other_info": {
      "use_pricing_table": "yes",
      "group_pricing_by": "repeat_interval",
      "active_editor": "wp-editor",
      "sold_individually": "no"
    }
  }
}'
```

### Create Product Pricing (need update)
<!-- 
**POST** `/products`

Create pricing for the created product.

#### Request Body

```json
{
  "ID": 7529320,
  "post_author": 5,
  "post_date": "2025-09-24T15:48:31+06:00",
  "post_date_gmt": "0000-00-00 00:00:00",
  "post_content": "",
  "post_title": "Dynamic Product 2",
  "post_excerpt": "",
  "post_status": "draft",
  "comment_status": "closed",
  "ping_status": "closed",
  "post_password": "",
  "post_name": "",
  "to_ping": "",
  "pinged": "",
  "post_modified": "2025-09-24 09:48:31",
  "post_modified_gmt": "0000-00-00 00:00:00",
  "post_content_filtered": "",
  "post_parent": 0,
  "guid": "https://cart.junior.ninja/?post_type=fluent-products&p=7529320",
  "menu_order": 0,
  "post_type": "fluent-products",
  "post_mime_type": "",
  "comment_count": 0,
  "view_url": "https://cart.junior.ninja/?post_type=fluent-products&p=7529320",
  "edit_url": "https://cart.junior.ninja/wp-admin/post.php?post=7529320&action=edit",
  "detail": {
    "id": 42,
    "post_id": 7529320,
    "fulfillment_type": "digital",
    "min_price": "0",
    "max_price": "0",
    "default_variation_id": 0,
    "default_media": "",
    "manage_stock": "0",
    "stock_availability": "in-stock",
    "variation_type": "simple",
    "manage_downloadable": "0",
    "other_info": {
      "active_editor": "wp-editor",
      "group_pricing_by": "repeat_interval",
      "sold_individually": "no",
      "use_pricing_table": "yes"
    },
    "created_at": "2025-09-24T09:48:31+00:00",
    "updated_at": "2025-09-24T09:48:31+00:00",
    "featured_media": "",
    "gallery_image": ""
  },
  "variants": [
    {
      "id": 177,
      "post_id": 7529320,
      "media_id": "",
      "serial_index": 1,
      "sold_individually": "0",
      "variation_title": "Dynamic Product 2",
      "variation_identifier": "",
      "manage_stock": "0",
      "payment_type": "",
      "stock_status": "in-stock",
      "backorders": "0",
      "total_stock": 1,
      "on_hold": 0,
      "committed": 0,
      "available": 1,
      "fulfillment_type": "digital",
      "item_status": "active",
      "manage_cost": false,
      "item_price": "20",
      "item_cost": "0",
      "compare_price": "",
      "shipping_class": "",
      "other_info": {
        "description": "",
        "payment_type": "onetime",
        "times": "",
        "repeat_interval": "",
        "trial_days": "",
        "billing_summary": "",
        "manage_setup_fee": "no",
        "signup_fee_name": "",
        "signup_fee": "0",
        "setup_fee_per_item": "no"
      },
      "downloadable": false,
      "created_at": "2025-09-24T09:48:31+00:00",
      "updated_at": "2025-09-24T09:48:31+00:00",
      "thumbnail": "",
      "formatted_total": "$0.00",
      "media": "",
      "rowId": 0,
      "new_stock": 1,
      "adjusted_quantity": 0
    }
  ]
}
```

#### Response

```json
{
    "data": {
        "ID": 7529320,
        "product_details": null
    },
    "message": "Product has been created successfully"
}
```

#### Example Request

```bash
curl --location 'https://cart.junior.ninja/wp-json/fluent-cart/v2/products/7529320/pricing' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic Zmx1ZW50Y2FydDpqbXZwIHk5TEogV2pPNSBIbWpyIGd4dlUgYnlENQ==' \
--data '{
  "post_title": "Dynamic Product 2",
  "post_status": "publish",
  "detail": {
    "fulfillment_type": "digital",
    "min_price": "0",
    "max_price": "0",
    "default_variation_id": 0,
    "default_media": "",
    "manage_stock": "0",
    "stock_availability": "in-stock",
    "variation_type": "simple",
    "manage_downloadable": "0",
    "other_info": {
      "active_editor": "wp-editor",
      "group_pricing_by": "repeat_interval",
      "sold_individually": "no",
      "use_pricing_table": "yes"
    },
    "created_at": "2025-09-24T09:48:31+00:00",
    "updated_at": "2025-09-24T09:48:31+00:00",
    "featured_media": "",
    "gallery_image": ""
  },
  "variants": [
    {
      "id": 177,
      "post_id": 7529320,
      "media_id": "",
      "serial_index": 1,
      "sold_individually": "0",
      "variation_title": "Dynamic Product 2",
      "variation_identifier": "",
      "manage_stock": "0",
      "payment_type": "",
      "stock_status": "in-stock",
      "backorders": "0",
      "total_stock": 1,
      "on_hold": 0,
      "committed": 0,
      "available": 1,
      "fulfillment_type": "digital",
      "item_status": "active",
      "manage_cost": false,
      "item_price": "50",
      "item_cost": "0",
      "compare_price": "",
      "shipping_class": "",
      "other_info": {
        "description": "",
        "payment_type": "onetime",
        "times": "",
        "repeat_interval": "",
        "trial_days": "",
        "billing_summary": "",
        "manage_setup_fee": "no",
        "signup_fee_name": "",
        "signup_fee": "0",
        "setup_fee_per_item": "no"
      },
      "downloadable": false,
      "created_at": "2025-09-24T09:48:31+00:00",
      "updated_at": "2025-09-24T09:48:31+00:00",
      "thumbnail": "",
      "formatted_total": "$0.00",
      "media": "",
      "rowId": 0,
      "new_stock": 1,
      "adjusted_quantity": 0
    }
  ]
}'
``` -->


### Get Product Details

**GET** `/products/{product}`

Retrieve detailed information about a specific product.

#### Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `product` | integer | Product ID |

#### Response

```json
{
  "success": true,
  "data": {
    "product": {
      "id": 33,
      "post_id": 7529108,
      "variations": [
        {
          "id": 145,
          "post_id": 7529108,
          "serial_index": 6,
          "sold_individually": 0,
          "variation_title": "Unlimited Sites Lifetime License",
          "variation_identifier": "6",
          "manage_stock": "0",
          "payment_type": "onetime",
          "stock_status": "in-stock",
          "backorders": 0,
          "total_stock": 0,
          "on_hold": 0,
          "committed": 0,
          "available": 0,
          "fulfillment_type": "digital",
          "item_status": "active",
          "manage_cost": "false",
          "item_price": 129900,
          "item_cost": 0,
          "compare_price": 0,
          "shipping_class": "0",
          "other_info": {
            "payment_type": "onetime"
          },
          "downloadable": "1",
          "created_at": "2021-09-22T07:09:20+00:00",
          "updated_at": "2025-06-06T14:36:34+00:00",
          "thumbnail": null,
          "formatted_total": "&#36;1,299.00",
          "media": null
        }
      ],
      "detail": {
        "id": 33,
        "post_id": 7529108,
        "fulfillment_type": "digital",
        "min_price": 8900,
        "max_price": 129900,
        "default_variation_id": "145",
        "default_media": null,
        "manage_stock": "0",
        "stock_availability": "in-stock",
        "variation_type": "simple_variations",
        "manage_downloadable": "1",
        "other_info": {
          "group_pricing_by": "repeat_interval",
          "use_pricing_table": "yes"
        },
        "created_at": "2021-09-22T07:09:20+00:00",
        "updated_at": "2025-09-24T09:09:50+00:00",
        "featured_media": null,
        "gallery_image": {
          "meta_id": "63",
          "post_id": 7529108,
          "meta_key": "fluent-products-gallery-image",
          "meta_value": []
        }
      }
    }
  }
}
```

#### Error Response

```json
{
  "message": "Product not found",
  "data": null
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v2/products/33" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Update Product

**PUT** `/products/{postId}/pricing`

Update product pricing information.

#### Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `postId` | integer | Product ID |

#### Request Body

```json
{
  "price": 3000,
  "sale_price": 2500,
  "sku": "SP-001-UPDATED"
}
```

#### Response

```json
{
  "success": true,
  "data": {
    "product": {
      "id": 1,
      "price": 3000,
      "sale_price": 2500,
      "sku": "SP-001-UPDATED",
      "updated_at": "2024-01-01T11:00:00Z"
    }
  }
}
```

#### Example Request

```bash
curl -X PUT "https://yoursite.com/wp-json/fluent-cart/v1/products/1/pricing" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ=" \
  -H "Content-Type: application/json" \
  -d '{
    "price": 3000,
    "sale_price": 2500
  }'
```

### Delete Product

**DELETE** `/products/{product}`

Delete a product (soft delete).

#### Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `product` | integer | Product ID |

#### Response

```json
{
  "success": true,
  "message": "Product deleted successfully"
}
```

#### Example Request

```bash
curl -X DELETE "https://yoursite.com/wp-json/fluent-cart/v1/products/1" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Search Products by Name

**GET** `/products/searchProductByName`

Search for products by name.

#### Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `search` | string | Search query |

#### Response

```json
{
  "success": true,
  "data": {
    "products": [
      {
        "id": 1,
        "title": "Sample Product",
        "sku": "SP-001",
        "price": 2500
      }
    ]
  }
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v1/products/searchProductByName?search=sample" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Search Variants by Name

**GET** `/products/searchVariantByName`

Search for product variants by name.

#### Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `search` | string | Search query |

#### Response

```json
{
  "success": true,
  "data": {
    "variants": [
      {
        "id": 1,
        "title": "Small",
        "product_id": 1,
        "price": 2000,
        "sku": "SP-001-S"
      }
    ]
  }
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v1/products/searchVariantByName?search=small" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Search Product Variant Options

**GET** `/products/search-product-variant-options`

Search for product variant options.

#### Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `search` | string | Search query |

#### Response

```json
{
  "success": true,
  "data": {
    "options": [
      {
        "id": 1,
        "name": "Size",
        "values": ["Small", "Medium", "Large"]
      }
    ]
  }
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v1/products/search-product-variant-options?search=size" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Find Subscription Variants

**GET** `/products/findSubscriptionVariants`

Find variants that support subscriptions.

#### Response

```json
{
  "success": true,
  "data": {
    "variants": [
      {
        "id": 1,
        "title": "Monthly Subscription",
        "product_id": 1,
        "price": 2000,
        "billing_cycle": "monthly"
      }
    ]
  }
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v1/products/findSubscriptionVariants" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Fetch Products by IDs

**GET** `/products/fetchProductsByIds`

Fetch multiple products by their IDs.

#### Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `ids` | string | Comma-separated product IDs |

#### Response

```json
{
  "success": true,
  "data": {
    "products": [
      {
        "id": 1,
        "title": "Product 1",
        "price": 2500
      },
      {
        "id": 2,
        "title": "Product 2",
        "price": 3000
      }
    ]
  }
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v1/products/fetchProductsByIds?ids=1,2,3" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Fetch Variations by IDs

**GET** `/products/fetchVariationsByIds`

Fetch multiple product variations by their IDs.

#### Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `ids` | string | Comma-separated variation IDs |

#### Response

```json
{
  "success": true,
  "data": {
    "variations": [
      {
        "id": 1,
        "title": "Small",
        "product_id": 1,
        "price": 2000
      },
      {
        "id": 2,
        "title": "Medium",
        "product_id": 1,
        "price": 2500
      }
    ]
  }
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v1/products/fetchVariationsByIds?ids=1,2,3" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Get Product Terms List

**GET** `/products/fetch-term`

Get product terms (categories, tags, etc.).

#### Response

```json
{
  "success": true,
  "data": {
    "terms": [
      {
        "id": 1,
        "name": "Electronics",
        "taxonomy": "product_category",
        "count": 25
      },
      {
        "id": 2,
        "name": "Clothing",
        "taxonomy": "product_category",
        "count": 15
      }
    ]
  }
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v1/products/fetch-term" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Get Product Terms by Parent

**POST** `/products/fetch-term-by-parent`

Get product terms by parent term.

#### Request Body

```json
{
  "parent_id": 1,
  "taxonomy": "product_category"
}
```

#### Response

```json
{
  "success": true,
  "data": {
    "terms": [
      {
        "id": 3,
        "name": "Smartphones",
        "parent_id": 1,
        "taxonomy": "product_category"
      }
    ]
  }
}
```

#### Example Request

```bash
curl -X POST "https://yoursite.com/wp-json/fluent-cart/v1/products/fetch-term-by-parent" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ=" \
  -H "Content-Type: application/json" \
  -d '{
    "parent_id": 1,
    "taxonomy": "product_category"
  }'
```

### Get Max Excerpt Word Count

**GET** `/products/get-max-excerpt-word-count`

Get the maximum word count for product excerpts.

#### Response

```json
{
  "success": true,
  "data": {
    "max_words": 55
  }
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v1/products/get-max-excerpt-word-count" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Get Product Pricing Widgets

**GET** `/products/{productId}/pricing-widgets`

Get pricing widgets for a product.

#### Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `productId` | integer | Product ID |

#### Response

```json
{
  "success": true,
  "data": {
    "widgets": [
      {
        "id": "price_display",
        "type": "price",
        "settings": {
          "show_sale_price": true,
          "show_regular_price": true
        }
      }
    ]
  }
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v1/products/1/pricing-widgets" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Set Product Image

**GET** `/products/{variantId}/thumbnail`

Set product image for a variant.

#### Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `variantId` | integer | Variant ID |

#### Response

```json
{
  "success": true,
  "data": {
    "image": {
      "id": 1,
      "url": "https://example.com/image.jpg",
      "alt": "Product image"
    }
  }
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v1/products/1/thumbnail" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Update Variant Option

**POST** `/products/{postId}/update-variant-option`

Update a product variant option.

#### Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `postId` | integer | Product ID |

#### Request Body

```json
{
  "variant_id": 1,
  "option_name": "Size",
  "option_value": "Large"
}
```

#### Response

```json
{
  "success": true,
  "data": {
    "variant": {
      "id": 1,
      "options": {
        "Size": "Large"
      },
      "updated_at": "2024-01-01T11:00:00Z"
    }
  }
}
```

#### Example Request

```bash
curl -X POST "https://yoursite.com/wp-json/fluent-cart/v1/products/1/update-variant-option" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ=" \
  -H "Content-Type: application/json" \
  -d '{
    "variant_id": 1,
    "option_name": "Size",
    "option_value": "Large"
  }'
```

### Add Product Terms

**POST** `/products/add-product-terms`

Add terms (categories, tags) to a product.

#### Request Body

```json
{
  "product_id": 1,
  "terms": [
    {
      "taxonomy": "product_category",
      "term_id": 1
    },
    {
      "taxonomy": "product_tag",
      "term_id": 2
    }
  ]
}
```

#### Response

```json
{
  "success": true,
  "data": {
    "product": {
      "id": 1,
      "terms": [
        {
          "taxonomy": "product_category",
          "term_id": 1
        },
        {
          "taxonomy": "product_tag",
          "term_id": 2
        }
      ]
    }
  }
}
```

#### Example Request

```bash
curl -X POST "https://yoursite.com/wp-json/fluent-cart/v1/products/add-product-terms" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ=" \
  -H "Content-Type: application/json" \
  -d '{
    "product_id": 1,
    "terms": [
      {
        "taxonomy": "product_category",
        "term_id": 1
      }
    ]
  }'
```

### Bulk Actions

**POST** `/products/do-bulk-action`

Perform bulk actions on multiple products.

#### Request Body

```json
{
  "action": "update_status",
  "product_ids": [1, 2, 3],
  "data": {
    "status": "draft"
  }
}
```

#### Available Actions

- `update_status` - Update status of multiple products
- `delete` - Delete multiple products
- `export` - Export multiple products

#### Response

```json
{
  "success": true,
  "data": {
    "processed": 3,
    "failed": 0,
    "results": [
      {
        "product_id": 1,
        "success": true
      },
      {
        "product_id": 2,
        "success": true
      },
      {
        "product_id": 3,
        "success": true
      }
    ]
  }
}
```

#### Example Request

```bash
curl -X POST "https://yoursite.com/wp-json/fluent-cart/v1/products/do-bulk-action" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ=" \
  -H "Content-Type: application/json" \
  -d '{
    "action": "update_status",
    "product_ids": [1, 2, 3],
    "data": {
      "status": "draft"
    }
  }'
```

### Create Dummy Products

**POST** `/products/create-dummy`

Create dummy products for testing.

#### Request Body

```json
{
  "count": 5,
  "type": "simple"
}
```

#### Response

```json
{
  "success": true,
  "data": {
    "created": 5,
    "products": [
      {
        "id": 1,
        "title": "Dummy Product 1",
        "sku": "DUMMY-001"
      }
    ]
  }
}
```

#### Example Request

```bash
curl -X POST "https://yoursite.com/wp-json/fluent-cart/v1/products/create-dummy" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ=" \
  -H "Content-Type: application/json" \
  -d '{
    "count": 5,
    "type": "simple"
  }'
```

## Product Variations

### List Variations

**GET** `/products/variants`

List all product variations.

#### Response

```json
{
  "success": true,
  "data": {
    "variations": [
      {
        "id": 1,
        "product_id": 1,
        "title": "Small",
        "price": 2000,
        "sku": "SP-001-S",
        "stock_quantity": 50
      }
    ]
  }
}
```

#### Example Request

```bash
curl -X GET "https://yoursite.com/wp-json/fluent-cart/v1/products/variants" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ="
```

### Create Variation

**POST** `/products/variants`

Create a new product variation.

#### Request Body

```json
{
  "product_id": 1,
  "title": "Large",
  "price": 3000,
  "sku": "SP-001-L",
  "stock_quantity": 25,
  "options": {
    "Size": "Large",
    "Color": "Red"
  }
}
```

#### Response

```json
{
  "success": true,
  "data": {
    "variation": {
      "id": 2,
      "product_id": 1,
      "title": "Large",
      "price": 3000,
      "sku": "SP-001-L",
      "stock_quantity": 25,
      "created_at": "2024-01-01T10:00:00Z"
    }
  }
}
```

#### Example Request

```bash
curl -X POST "https://yoursite.com/wp-json/fluent-cart/v1/products/variants" \
  -H "Authorization: Basic dXNlcm5hbWU6YXBwbGljYXRpb25fcGFzc3dvcmQ=" \
  -H "Content-Type: application/json" \
  -d '{
    "product_id": 1,
    "title": "Large",
    "price": 3000,
    "sku": "SP-001-L"
  }'
```

## Error Handling

### Common Error Codes

| Code | Description |
|------|-------------|
| `product_not_found` | Product with specified ID not found |
| `invalid_sku` | SKU is invalid or already exists |
| `insufficient_permissions` | User lacks required permissions |
| `validation_error` | Request data validation failed |
| `variation_not_found` | Variation with specified ID not found |

### Error Response Example

```json
{
  "success": false,
  "error": {
    "code": "product_not_found",
    "message": "Product with ID 999 not found"
  }
}
```

## Rate Limiting

- **List operations**: 100 requests per hour
- **Create operations**: 50 requests per hour
- **Update operations**: 200 requests per hour
- **Delete operations**: 20 requests per hour

## Related Documentation

- [Orders API](./orders) - Order management endpoints
- [Customers API](./customers) - Customer management endpoints
- [Database Models](/database/models) - Product data models
- [Developer Hooks](/hooks/) - Product-related hooks

## Next Steps

Continue with product management:

1. **[Orders API](./orders)** - Manage product orders
2. **[Customers API](./customers)** - Manage customer data
3. **[Database Models](/database/models)** - Understand product data structure
4. **[Developer Hooks](/hooks/)** - Product-related hooks

## Previous/Next Navigation

- **Previous**: [Customers API](./customers) - Customer management endpoints
- **Next**: [Subscriptions API](./subscriptions) - Subscription management endpoints

---

