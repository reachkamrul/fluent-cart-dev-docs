# API Documentation Update Instructions

## Overview
This file contains instructions for updating all FluentCart API documentation with real server response data. All current API docs contain assumed/fake data and need to be replaced with actual server responses.

## Priority Order
1. **Products API** (Partially done - only list endpoint updated)
2. **Orders API** 
3. **Customers API**
4. **Subscriptions API**
5. **Coupons API**
6. **Files API**
7. **Licensing API** (Pro)
8. **Roles & Permissions API** (Pro)

---

## 1. PRODUCTS API

### Current Status: ⚠️ PARTIALLY DONE
- ✅ List Products (`GET /wp-json/fluent-cart/v2/products`) - Updated with real data
- ❌ Create Product (`POST /wp-json/fluent-cart/v2/products`) - Still has fake data
- ❌ Update Product (`PUT /wp-json/fluent-cart/v2/products/{id}`) - Still has fake data
- ❌ Delete Product (`DELETE /wp-json/fluent-cart/v2/products/{id}`) - Still has fake data
- ✅ Get Product (`GET /wp-json/fluent-cart/v2/products/{id}`) - Updated with real data

### Required Data for Products API:

#### 1.1 Create Product
```json
{
  "endpoint": "POST /wp-json/fluent-cart/v2/products",
  "request_body": {
    "post_title": "Sample Product Title",
    "post_content": "Product description",
    "post_excerpt": "Product short description",
    "post_status": "publish",
    "meta": {
      "price": "29.99",
      "sale_price": "19.99",
      "sku": "PROD-001",
      "stock_quantity": 100,
      "manage_stock": true,
      "stock_status": "instock"
    }
  },
  "success_response": {
    // Actual success response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 1.2 Update Product
```json
{
  "endpoint": "PUT /wp-json/fluent-cart/v2/products/{id}",
  "request_body": {
    "post_title": "Updated Product Title",
    "post_content": "Updated product description",
    "meta": {
      "price": "39.99",
      "sale_price": "29.99"
    }
  },
  "success_response": {
    // Actual success response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 1.3 Get Single Product
```json
{
  "endpoint": "GET /wp-json/fluent-cart/v2/products/{id}",
  "success_response": {
    // Actual single product response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 1.4 Delete Product
```json
{
  "endpoint": "DELETE /wp-json/fluent-cart/v2/products/{id}",
  "success_response": {
    // Actual delete success response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

---

## 2. ORDERS API

### Current Status: ❌ ALL FAKE DATA

#### 2.1 List Orders
```json
{
  "endpoint": "GET /wp-json/fluent-cart/v2/orders",
  "success_response": {
    // Actual list orders response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 2.2 Get Single Order
```json
{
  "endpoint": "GET /wp-json/fluent-cart/v2/orders/{id}",
  "success_response": {
    // Actual single order response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 2.3 Create Order
```json
{
  "endpoint": "POST /wp-json/fluent-cart/v2/orders",
  "request_body": {
    "customer_id": 123,
    "items": [
      {
        "product_id": 456,
        "quantity": 2,
        "price": "29.99"
      }
    ],
    "billing_address": {
      "first_name": "John",
      "last_name": "Doe",
      "email": "john@example.com"
    }
  },
  "success_response": {
    // Actual create order response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 2.4 Update Order
```json
{
  "endpoint": "PUT /wp-json/fluent-cart/v2/orders/{id}",
  "request_body": {
    "status": "processing",
    "notes": "Order updated"
  },
  "success_response": {
    // Actual update order response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 2.5 Delete Order
```json
{
  "endpoint": "DELETE /wp-json/fluent-cart/v2/orders/{id}",
  "success_response": {
    // Actual delete order response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

---

## 3. CUSTOMERS API

### Current Status: ❌ ALL FAKE DATA

#### 3.1 List Customers
```json
{
  "endpoint": "GET /wp-json/fluent-cart/v2/customers",
  "success_response": {
    // Actual list customers response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 3.2 Get Single Customer
```json
{
  "endpoint": "GET /wp-json/fluent-cart/v2/customers/{id}",
  "success_response": {
    // Actual single customer response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 3.3 Create Customer
```json
{
  "endpoint": "POST /wp-json/fluent-cart/v2/customers",
  "request_body": {
    "first_name": "John",
    "last_name": "Doe",
    "email": "john@example.com",
    "phone": "+1234567890"
  },
  "success_response": {
    // Actual create customer response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 3.4 Update Customer
```json
{
  "endpoint": "PUT /wp-json/fluent-cart/v2/customers/{id}",
  "request_body": {
    "first_name": "Jane",
    "last_name": "Smith",
    "email": "jane@example.com"
  },
  "success_response": {
    // Actual update customer response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 3.5 Delete Customer
```json
{
  "endpoint": "DELETE /wp-json/fluent-cart/v2/customers/{id}",
  "success_response": {
    // Actual delete customer response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

---

## 4. SUBSCRIPTIONS API

### Current Status: ❌ ALL FAKE DATA

#### 4.1 List Subscriptions
```json
{
  "endpoint": "GET /wp-json/fluent-cart/v2/subscriptions",
  "success_response": {
    // Actual list subscriptions response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 4.2 Get Single Subscription
```json
{
  "endpoint": "GET /wp-json/fluent-cart/v2/subscriptions/{id}",
  "success_response": {
    // Actual single subscription response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 4.3 Create Subscription
```json
{
  "endpoint": "POST /wp-json/fluent-cart/v2/subscriptions",
  "request_body": {
    "customer_id": 123,
    "product_id": 456,
    "billing_cycle": "monthly",
    "amount": "29.99"
  },
  "success_response": {
    // Actual create subscription response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 4.4 Update Subscription
```json
{
  "endpoint": "PUT /wp-json/fluent-cart/v2/subscriptions/{id}",
  "request_body": {
    "status": "active",
    "next_billing_date": "2024-02-01"
  },
  "success_response": {
    // Actual update subscription response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 4.5 Cancel Subscription
```json
{
  "endpoint": "POST /wp-json/fluent-cart/v2/subscriptions/{id}/cancel",
  "success_response": {
    // Actual cancel subscription response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

---

## 5. COUPONS API

### Current Status: ❌ ALL FAKE DATA

#### 5.1 List Coupons
```json
{
  "endpoint": "GET /wp-json/fluent-cart/v2/coupons",
  "success_response": {
    // Actual list coupons response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 5.2 Get Single Coupon
```json
{
  "endpoint": "GET /wp-json/fluent-cart/v2/coupons/{id}",
  "success_response": {
    // Actual single coupon response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 5.3 Create Coupon
```json
{
  "endpoint": "POST /wp-json/fluent-cart/v2/coupons",
  "request_body": {
    "code": "SAVE20",
    "discount_type": "percentage",
    "discount_value": "20",
    "usage_limit": 100,
    "expiry_date": "2024-12-31"
  },
  "success_response": {
    // Actual create coupon response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 5.4 Update Coupon
```json
{
  "endpoint": "PUT /wp-json/fluent-cart/v2/coupons/{id}",
  "request_body": {
    "discount_value": "25",
    "usage_limit": 150
  },
  "success_response": {
    // Actual update coupon response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 5.5 Delete Coupon
```json
{
  "endpoint": "DELETE /wp-json/fluent-cart/v2/coupons/{id}",
  "success_response": {
    // Actual delete coupon response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

---

## 6. FILES API

### Current Status: ❌ ALL FAKE DATA

#### 6.1 List Files
```json
{
  "endpoint": "GET /wp-json/fluent-cart/v2/files",
  "success_response": {
    // Actual list files response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 6.2 Upload File
```json
{
  "endpoint": "POST /wp-json/fluent-cart/v2/files",
  "request_body": {
    "file": "base64_encoded_file_data",
    "filename": "document.pdf",
    "product_id": 123
  },
  "success_response": {
    // Actual upload file response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 6.3 Get Single File
```json
{
  "endpoint": "GET /wp-json/fluent-cart/v2/files/{id}",
  "success_response": {
    // Actual single file response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 6.4 Delete File
```json
{
  "endpoint": "DELETE /wp-json/fluent-cart/v2/files/{id}",
  "success_response": {
    // Actual delete file response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

---

## 7. LICENSING API (PRO)

### Current Status: ❌ ALL FAKE DATA

#### 7.1 List Licenses
```json
{
  "endpoint": "GET /wp-json/fluent-cart/v2/licensing/licenses",
  "success_response": {
    // Actual list licenses response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 7.2 Get Single License
```json
{
  "endpoint": "GET /wp-json/fluent-cart/v2/licensing/licenses/{id}",
  "success_response": {
    // Actual single license response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 7.3 Create License
```json
{
  "endpoint": "POST /wp-json/fluent-cart/v2/licensing/licenses",
  "request_body": {
    "license_key": "LIC-123456789",
    "product_id": 456,
    "customer_id": 123,
    "expiry_date": "2024-12-31"
  },
  "success_response": {
    // Actual create license response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 7.4 Update License
```json
{
  "endpoint": "PUT /wp-json/fluent-cart/v2/licensing/licenses/{id}",
  "request_body": {
    "status": "active",
    "expiry_date": "2025-12-31"
  },
  "success_response": {
    // Actual update license response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 7.5 Delete License
```json
{
  "endpoint": "DELETE /wp-json/fluent-cart/v2/licensing/licenses/{id}",
  "success_response": {
    // Actual delete license response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

---

## 8. ROLES & PERMISSIONS API (PRO)

### Current Status: ❌ ALL FAKE DATA

#### 8.1 List Roles
```json
{
  "endpoint": "GET /wp-json/fluent-cart/v2/roles",
  "success_response": {
    // Actual list roles response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 8.2 Get Single Role
```json
{
  "endpoint": "GET /wp-json/fluent-cart/v2/roles/{key}",
  "success_response": {
    // Actual single role response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 8.3 Create Role
```json
{
  "endpoint": "POST /wp-json/fluent-cart/v2/roles",
  "request_body": {
    "name": "Custom Role",
    "key": "custom_role",
    "permissions": ["read_orders", "create_products"]
  },
  "success_response": {
    // Actual create role response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 8.4 Update Role
```json
{
  "endpoint": "PUT /wp-json/fluent-cart/v2/roles/{key}",
  "request_body": {
    "name": "Updated Custom Role",
    "permissions": ["read_orders", "create_products", "update_orders"]
  },
  "success_response": {
    // Actual update role response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

#### 8.5 Delete Role
```json
{
  "endpoint": "DELETE /wp-json/fluent-cart/v2/roles/{key}",
  "success_response": {
    // Actual delete role response from server
  },
  "error_response": {
    // Actual error response from server
  }
}
```

---

## Instructions for User

### How to Provide Data:
1. **Copy the JSON structure** for the endpoint you want to update
2. **Replace the placeholder comments** with actual server response data
3. **Send one endpoint at a time** or multiple endpoints together
4. **Include both success and error responses** when possible

### Example:
```json
{
  "endpoint": "POST /wp-json/fluent-cart/v2/products",
  "request_body": {
    "post_title": "Test Product",
    "post_content": "Test description",
    "meta": {
      "price": "29.99"
    }
  },
  "success_response": {
    "success": true,
    "data": {
      "ID": 123,
      "post_title": "Test Product",
      "post_status": "publish"
    }
  },
  "error_response": {
    "success": false,
    "message": "Validation failed",
    "errors": {
      "post_title": ["Title is required"]
    }
  }
}
```

### Priority:
1. **Start with Products API** (complete the missing endpoints)
2. **Then Orders API** (most important for e-commerce)
3. **Continue with other APIs** in order

### Notes:
- All endpoints use `/wp-json/fluent-cart/v2/` base URL
- Include actual field names and data types from your server
- Include pagination data for list endpoints
- Include validation error messages for error responses
- Include any additional fields that your API returns
