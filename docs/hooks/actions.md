---
title: Action Hooks
description: FluentCart action hooks documentation with complete reference and usage examples.
---

# FluentCart Action Hooks

Action hooks allow you to execute custom code at specific points in FluentCart's execution flow. They are perfect for triggering side effects, sending notifications, logging events, or performing custom business logic.


## Core Action Hooks

### Order Lifecycle Hooks


<details>
<summary><code>fluent_cart/order_fully_refunded</code></summary>

This action runs when an order is fully refunded.

**Parameters**

- <code>$data</code> (array): Order and refund information

#### <code> $data </code> sample 
```json
{
  "order": {
    "id": 123,
    "status": "completed",
    "parent_id": null,
    "receipt_number": "RC-2024-001",
    "invoice_no": "INV-2024-001",
    "fulfillment_type": "digital",
    "type": "payment",
    "mode": "test",
    "shipping_status": "",
    "customer_id": "456",
    "payment_method": "stripe",
    "payment_status": "refunded",
    "payment_method_title": "Credit Card",
    "currency": "USD",
    "subtotal": 15000,
    "discount_tax": 0,
    "manual_discount_total": 0,
    "coupon_discount_total": 0,
    "shipping_tax": 0,
    "shipping_total": 0,
    "tax_total": 0,
    "total_amount": 15000,
    "total_paid": "15000",
    "total_refund": 15000,
    "rate": "1.0000",
    "tax_behavior": "1",
    "note": "Customer requested full refund",
    "ip_address": "192.168.1.100",
    "completed_at": "2024-01-15 10:30:00",
    "refunded_at": "2024-01-15 14:45:00",
    "uuid": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "config": {
      "user_tz": "America/New_York",
      "create_account_after_paid": "yes"
    },
    "created_at": "2024-01-15T10:25:00+00:00",
    "updated_at": "2024-01-15T14:45:00+00:00",
    "customer": {}, //Customer object
    "shipping_address": {
      "id": 789,
      "order_id": "123",
      "type": "shipping",
      "name": "John Doe",
      "address_1": "123 Main Street",
      "address_2": "Apt 4B",
      "city": "New York",
      "state": "NY",
      "postcode": "10001",
      "country": "US",
      "meta": {
        "other_data": {
          "email": "john.doe@example.com",
          "last_name": "Doe",
          "first_name": "John"
        }
      },
      "created_at": "2024-01-15T10:25:00+00:00",
      "updated_at": "2024-01-15T10:25:00+00:00",
      "email": "john.doe@example.com",
      "first_name": "John",
      "last_name": "Doe",
      "full_name": "John Doe",
      "formatted_address": {}, // User address formatted
      "order": {} //Order object
    }, 
    "billing_address": {
      "id": 790,
      "order_id": "123",
      "type": "billing",
      "name": "John Doe",
      "address_1": "123 Main Street",
      "address_2": "Apt 4B",
      "city": "New York",
      "state": "NY",
      "postcode": "10001",
      "country": "US",
      "meta": {
        "other_data": {
          "email": "john.doe@example.com",
          "last_name": "Doe",
          "first_name": "John"
        }
      },
      "created_at": "2024-01-15T10:25:00+00:00",
      "updated_at": "2024-01-15T10:25:00+00:00",
      "email": "john.doe@example.com",
      "first_name": "John",
      "last_name": "Doe",
      "full_name": "John Doe",
      "formatted_address": {}, // User address formatted
      "order": {} //Order Object
    },
    "order_items": [
      {
        "id": 101,
        "order_id": "123",
        "post_id": "500",
        "fulfillment_type": "digital",
        "payment_type": "onetime",
        "post_title": "Premium Digital Course",
        "title": "Premium Digital Course",
        "object_id": "75",
        "cart_index": "0",
        "quantity": "1",
        "unit_price": "15000",
        "cost": "0",
        "subtotal": "15000",
        "tax_amount": "0",
        "shipping_charge": "0",
        "discount_total": "0",
        "line_total": "15000",
        "refund_total": "15000",
        "rate": "1",
        "other_info": {
          "times": "",
          "signup_fee": 0,
          "trial_days": "",
          "description": "Complete digital marketing course",
          "installment": "no",
          "payment_type": "onetime",
          "billing_summary": "",
          "repeat_interval": "",
          "signup_fee_name": "",
          "manage_setup_fee": "no",
          "setup_fee_per_item": "no"
        },
        "line_meta": [],
        "fulfilled_quantity": "0",
        "referrer": null,
        "created_at": "2024-01-15T10:25:00+00:00",
        "updated_at": "2024-01-15T14:45:00+00:00",
        "payment_info": "",
        "setup_info": "",
        "formatted_total": "&#36;150.00"
      }
    ],
    "order_tax_rates": [
      {
        "id": 201,
        "order_id": "123",
        "tax_rate_id": "0",
        "shipping_tax": "0",
        "order_tax": "0",
        "total_tax": "0",
        "created_at": "2024-01-15T10:25:00+00:00",
        "updated_at": "2024-01-15T10:25:00+00:00",
        "meta": {
          "tax_country": "US",
          "store_vat_number": ""
        },
        "filed_at": null
      }
    ]
  },
  "refunded_items": [
    {
      "id": 101,
      "order_id": "123",
      "post_id": "500",
      "fulfillment_type": "digital",
      "payment_type": "onetime",
      "post_title": "Premium Digital Course",
      "title": "Premium Digital Course",
      "object_id": "75",
      "cart_index": "0",
      "quantity": "1",
      "unit_price": "15000",
      "cost": "0",
      "subtotal": "15000",
      "tax_amount": "0",
      "shipping_charge": "0",
      "discount_total": "0",
      "line_total": "15000",
      "refund_total": "15000",
      "rate": "1",
      "other_info": {
        "times": "",
        "signup_fee": 0,
        "trial_days": "",
        "description": "Complete digital marketing course",
        "installment": "no",
        "payment_type": "onetime",
        "billing_summary": "",
        "repeat_interval": "",
        "signup_fee_name": "",
        "manage_setup_fee": "no",
        "setup_fee_per_item": "no"
      },
      "line_meta": [],
      "fulfilled_quantity": "0",
      "referrer": null,
      "created_at": "2024-01-15T10:25:00+00:00",
      "updated_at": "2024-01-15T14:45:00+00:00",
      "payment_info": "",
      "setup_info": "",
      "formatted_total": "&#36;150.00"
    }
  ],
  "new_refunded_items": [],
  "refunded_amount": 15000,
  "manage_stock": false,
  "transaction": {
    "order_id": "123",
    "order_type": "payment",
    "payment_method": "stripe",
    "payment_mode": "test",
    "payment_method_type": "card",
    "transaction_type": "refund",
    "subscription_id": null,
    "status": "refunded",
    "currency": "usd",
    "total": 15000,
    "meta": {
      "parent_id": 301,
      "reason": "Customer requested refund"
    },
    "uuid": "b2c3d4e5-f6g7-8901-bcde-f23456789012",
    "updated_at": "2024-01-15T14:45:00+00:00",
    "created_at": "2024-01-15T14:44:30+00:00",
    "id": 302,
    "vendor_charge_id": "re_3ABC123DEF456GHI789JKL012MNO",
    "url": "https://dashboard.stripe.com/refunds/re_3ABC123DEF456GHI789JKL012MNO"
  },
  "customer": {
    "id": 456,
    "user_id": "789",
    "contact_id": "0",
    "email": "john.doe@example.com",
    "first_name": "John",
    "last_name": "Doe",
    "status": "active",
    "purchase_value": null,
    "purchase_count": "1",
    "ltv": "15000",
    "first_purchase_date": "2024-01-15 10:25:00",
    "last_purchase_date": "2024-01-15 10:25:00",
    "aov": "15000.00",
    "notes": "",
    "uuid": "c3d4e5f6-g7h8-9012-cdef-345678901234",
    "country": "US",
    "city": "New York",
    "state": "NY",
    "postcode": "10001",
    "created_at": "2024-01-15T10:25:00+00:00",
    "updated_at": "2024-01-15T14:45:00+00:00",
    "full_name": "John Doe",
    "photo": "",
    "country_name": "United States",
    "formatted_address": {}, // User address formatted
    "user_link": "https://example.com/wp-admin/user-edit.php?user_id=789"
  },
  "type": "full"
}
```

**Usage:**

```php
add_action('fluent_cart/order_fully_refunded', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


<details>
<summary><code>fluent_cart/order_partially_refunded</code></summary>

This action runs when an order is partially refunded.

**Parameters**

- <code>$data</code> (array): Order and refund information

**Usage:**

```php
add_action('fluent_cart/order_partially_refunded', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


<details>
<summary><code>fluent_cart/order_paid</code></summary>

This action runs when an order is paid.

**Parameters**

- <code>$data</code> (array): Order and payment information

**Usage:**

```php
add_action('fluent_cart/order_paid', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


<details>
<summary><code>fluent_cart/order_refunded</code></summary>

This action runs when an order is refunded (full or partial).

**Parameters**

- <code>$data</code> (array): Order and refund information

**Usage:**

```php
add_action('fluent_cart/order_refunded', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


<details>
<summary><code>fluent_cart/order/upgraded</code></summary>

This action runs when an order is upgraded.

**Parameters**

- <code>$data</code> (array): Order upgrade information

**Usage:**

```php
add_action('fluent_cart/order/upgraded', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


<details>
<summary><code>fluent_cart/cart_completed</code></summary>

This action runs when a cart is completed (order placed).

**Parameters**

- <code>$data</code> (array): Cart and order information

**Usage:**

```php
add_action('fluent_cart/cart_completed', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


### Payment Hooks


<details>
<summary><code>fluent_cart/payment_success</code></summary>

This action runs when a payment is successfully processed.

**Parameters**

- <code>$data</code> (array): Payment and order information

**Usage:**

```php
add_action('fluent_cart/payment_success', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


<details>
<summary><code>fluent_cart/payment_failed</code></summary>

This action runs when a payment fails.

**Parameters**

- <code>$data</code> (array): Payment failure information

**Usage:**

```php
add_action('fluent_cart/payment_failed', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


<details>
<summary><code>fluent_cart/payments/after_payment_{status}</code></summary>

This action runs after payment processing with a specific status.

**Parameters**

- <code>$data</code> (array): Payment information

**Usage:**

```php
add_action('fluent_cart/payments/after_payment_pending', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


<details>
<summary><code>fluent_cart/payment_{status}</code></summary>

This action runs for a specific payment status (e.g., payment_pending, payment_completed).

**Parameters**

- <code>$data</code> (array): Payment and order information

**Usage:**

```php
add_action('fluent_cart/payment_pending', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


<details>
<summary><code>fluent_cart/payment_{type}_{status}</code></summary>

This action runs for a specific payment type and status (e.g., payment_stripe_completed).

**Parameters**

- <code>$data</code> (array): Payment and order information

**Usage:**

```php
add_action('fluent_cart/payment_stripe_completed', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


### Subscription Hooks


<details>
<summary><code>fluent_cart/subscription/data_updated</code></summary>

This action runs when subscription data is updated.

**Parameters**

- <code>$data</code> (array): Subscription information

**Usage:**

```php
add_action('fluent_cart/subscription/data_updated', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


<details>
<summary><code>fluent_cart/payments/subscription_status_changed</code></summary>

This action runs when subscription status changes.

**Parameters**

- <code>$data</code> (array): Subscription and status information

**Usage:**

```php
add_action('fluent_cart/payments/subscription_status_changed', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


<details>
<summary><code>fluent_cart/payments/subscription_{status}</code></summary>

This action runs when subscription reaches a specific status.

**Parameters**

- <code>$data</code> (array): Subscription information

**Usage:**

```php
add_action('fluent_cart/payments/subscription_active', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


### Cart Hooks


<details>
<summary><code>fluent_cart/cart/line_item/line_meta</code></summary>

This action runs for cart line item metadata.

**Parameters**

- <code>$data</code> (array): Line item data

**Usage:**

```php
add_action('fluent_cart/cart/line_item/line_meta', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


<details>
<summary><code>fluent_cart/cart/line_item/before_total</code></summary>

This action runs before cart line item total.

**Parameters**

- <code>$data</code> (array): Line item data

**Usage:**

```php
add_action('fluent_cart/cart/line_item/before_total', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


<details>
<summary><code>fluent_cart/cart/line_item/after_total</code></summary>

This action runs after cart line item total.

**Parameters**

- <code>$data</code> (array): Line item data

**Usage:**

```php
add_action('fluent_cart/cart/line_item/after_total', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


<details>
<summary><code>fluent_cart/cart/line_item/before_main_title</code></summary>

This action runs before cart line item main title.

**Parameters**

- <code>$data</code> (array): Line item data

**Usage:**

```php
add_action('fluent_cart/cart/line_item/before_main_title', function($data) {
    // Do whatever you want with here
}, 10, 1);

```
</details>


<details>
<summary><code>fluent_cart/cart/line_item/after_main_title</code></summary>

This action runs after cart line item main title.

**Parameters**

- <code>$data</code> (array): Line item data

**Usage:**

```php
add_action('fluent_cart/cart/line_item/after_main_title', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


### Product Hooks

<details>
<summary><code>fluent_cart/product/render_product_header</code></summary>

This action runs when rendering a product header.

**Parameters**

- <code>$productId</code> (int): Product ID

**Usage:**

```php
add_action('fluent_cart/product/render_product_header', function($productId) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


### Module Hooks

<details>
<summary><code>fluent_cart/register_payment_methods</code></summary>

This action runs to register payment methods.

**Parameters**

- None

**Usage:**

```php
add_action('fluent_cart/register_payment_methods', function() {
    // Do whatever you want with here
}, 10);
```
</details>


### Admin Hooks

<details>
<summary><code>fluent_cart/loading_app</code></summary>

This action runs when FluentCart admin app is loading.

**Parameters**

- <code>$app</code> (object): Application instance

**Usage:**

```php
add_action('fluent_cart/loading_app', function($app) {
    // Do whatever you want with here
}, 10, 1);
```
</details>

<details>
<summary><code>fluent_cart/admin_js_loaded</code></summary>

This action runs when admin JavaScript is loaded.

**Parameters**

- <code>$app</code> (object): Application instance

**Usage:**

```php
add_action('fluent_cart/admin_js_loaded', function($app) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


### View/Template Hooks

<details>
<summary><code>fluent_cart/views/checkout_order_summary</code></summary>

This action runs when rendering checkout order summary.

**Parameters**

- <code>$data</code> (array): Order summary data

**Usage:**

```php
add_action('fluent_cart/views/checkout_order_summary', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>

<details>
<summary><code>fluent_cart/views/checkout_order_receipt</code></summary>

This action runs when rendering checkout order receipt.

**Parameters**

- <code>$data</code> (array): Order receipt data

**Usage:**

```php
add_action('fluent_cart/views/checkout_order_receipt', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>

<details>
<summary><code>fluent_cart/views/order_downloads</code></summary>

This action runs when rendering order downloads.

**Parameters**

- <code>$data</code> (array): Order downloads data

**Usage:**

```php
add_action('fluent_cart/views/order_downloads', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>

<details>
<summary><code>fluent_cart/views/order_licenses</code></summary>

This action runs when rendering order licenses.

**Parameters**

- <code>$data</code> (array): Order licenses data

**Usage:**

```php
add_action('fluent_cart/views/order_licenses', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>

<details>
<summary><code>fluent_cart/views/order_subscriptions</code></summary>

This action runs when rendering order subscriptions.

**Parameters**

- <code>$data</code> (array): Order subscriptions data

**Usage:**

```php
add_action('fluent_cart/views/order_subscriptions', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>

<details>
<summary><code>fluent_cart/views/cart_list</code></summary>

This action runs when rendering cart list.

**Parameters**

- <code>$data</code> (array): Cart list data

**Usage:**

```php
add_action('fluent_cart/views/cart_list', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>

<details>
<summary><code>fluent_cart/views/cart_empty_content</code></summary>

This action runs when rendering empty cart content.

**Parameters**

- <code>$data</code> (array): Cart data

**Usage:**

```php
add_action('fluent_cart/views/cart_empty_content', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>

<details>
<summary><code>fluent_cart/views/checkout_order_confirmation_page</code></summary>

This action runs when rendering checkout order confirmation page.

**Parameters**

- <code>$data</code> (array): Confirmation page data

**Usage:**

```php
add_action('fluent_cart/views/checkout_order_confirmation_page', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>

<details>
<summary><code>fluent_cart/views/checkout_order_confirmation_page_error</code></summary>

This action runs when rendering checkout order confirmation page error.

**Parameters**

- <code>$data</code> (array): Error data

**Usage:**

```php
add_action('fluent_cart/views/checkout_order_confirmation_page_error', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


### Other Notable Action Hooks

<details>
<summary><code>fluent_cart/init</code></summary>

This action runs when FluentCart initializes.

**Parameters**

- <code>$app</code> (object): Application instance

**Usage:**

```php
add_action('fluent_cart/init', function($app) {
    // Do whatever you want with here
}, 10, 1);
```
</details>

<details>
<summary><code>fluent_cart/user/after_register</code></summary>

This action runs after a user registers.

**Parameters**

- <code>$user_id</code> (int): User ID
- <code>$data</code> (array): Registration data

**Usage:**

```php
add_action('fluent_cart/user/after_register', function($user_id, $data) {
    // Do whatever you want with here
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/user/before_registration</code></summary>

This action runs before a user registers.

**Parameters**

- <code>$data</code> (array): Registration data

**Usage:**

```php
add_action('fluent_cart/user/before_registration', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>

<details>
<summary><code>fluent_cart/views/shop_app_filter_dollar_icon</code></summary>

This action runs to render the dollar icon in shop app filter.

**Parameters**

- None

**Usage:**

```php
add_action('fluent_cart/views/shop_app_filter_dollar_icon', function() {
    // Do whatever you want with here
}, 10);
```
</details>

<details>
<summary><code>fluent_cart/views/shop_app_responsive_filter_wrapper</code></summary>

This action runs to render the responsive filter wrapper in shop app.

**Parameters**

- None

**Usage:**

```php
add_action('fluent_cart/views/shop_app_responsive_filter_wrapper', function() {
    // Do whatever you want with here
}, 10);
```
</details>

## Related Documentation

- [Filter Hooks](./filters) - FluentCart filter hooks
- [Event System](./events) - FluentCart event system
- [Database Models](/database/models) - Models used in hook data
- [REST API](/api/) - API endpoints that trigger hooks

## Previous/Next Navigation

- **Previous**: [Developer Hooks Overview](./) - FluentCart hooks system
- **Next**: [Filter Hooks](./filters) - FluentCart filter hooks

---

