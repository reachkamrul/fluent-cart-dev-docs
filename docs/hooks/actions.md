---
title: Action Hooks
description: FluentCart action hooks documentation with complete reference and usage examples.
---

# FluentCart Action Hooks

Action hooks allow you to execute custom code at specific points in FluentCart's execution flow. They are perfect for triggering side effects, sending notifications, logging events, or performing custom business logic.

## Core Action Hooks

### Order Lifecycle Hooks

#### `fluent_cart/order/invoice_number_added`
**Description:** Fired when an invoice number is added to an order  
**Parameters:** `$data` (array) - Contains order information  
**Priority:** 10  
**Use Case:** Track invoice generation, send notifications

```php
add_action('fluent_cart/order/invoice_number_added', function($data) {
    $order = $data['order'];
    // Send invoice notification
    wp_mail($order->customer->email, 'Invoice Generated', 'Your invoice #' . $order->invoice_no . ' has been generated');
}, 10, 1);
```

### Payment Hooks

#### `fluent_cart/payment_success`
**Description:** Fired when a payment is successfully processed  
**Parameters:** `$data` (array) - Payment and order information  
**Priority:** 10  
**Use Case:** Send confirmation emails, update external systems

```php
add_action('fluent_cart/payment_success', function($data) {
    $order = $data['order'];
    $transaction = $data['transaction'];
    
    // Send payment confirmation
    wp_mail($order->customer->email, 'Payment Confirmed', 'Your payment has been processed successfully');
}, 10, 1);
```

#### `fluent_cart/payment_failed`
**Description:** Fired when a payment fails  
**Parameters:** `$data` (array) - Payment failure information  
**Priority:** 10  
**Use Case:** Log failures, send failure notifications

```php
add_action('fluent_cart/payment_failed', function($data) {
    $order = $data['order'];
    $error = $data['error'];
    
    // Log payment failure
    error_log('Payment failed for order #' . $order->id . ': ' . $error);
}, 10, 1);
```

#### `fluent_cart/payments/after_payment_{status}`
**Description:** Fired after payment processing with specific status  
**Parameters:** `$data` (array) - Payment information  
**Priority:** 10  
**Use Case:** Handle specific payment statuses

```php
add_action('fluent_cart/payments/after_payment_pending', function($data) {
    // Handle pending payment
    $order = $data['order'];
    // Send pending payment notification
}, 10, 1);
```

### Subscription Hooks

#### `fluent_cart/subscription/data_updated`
**Description:** Fired when subscription data is updated  
**Parameters:** `$data` (array) - Subscription information  
**Priority:** 10  
**Use Case:** Sync subscription data with external systems

```php
add_action('fluent_cart/subscription/data_updated', function($data) {
    $subscription = $data['subscription'];
    // Update external CRM
    update_crm_subscription($subscription);
}, 10, 1);
```

#### `fluent_cart/payments/subscription_status_changed`
**Description:** Fired when subscription status changes  
**Parameters:** `$data` (array) - Subscription and status information  
**Priority:** 10  
**Use Case:** Handle subscription status changes

```php
add_action('fluent_cart/payments/subscription_status_changed', function($data) {
    $subscription = $data['subscription'];
    $oldStatus = $data['old_status'];
    $newStatus = $data['new_status'];
    
    // Handle status change
    if ($newStatus === 'cancelled') {
        // Cancel external services
        cancel_external_subscription($subscription);
    }
}, 10, 1);
```

#### `fluent_cart/payments/subscription_{status}`
**Description:** Fired when subscription reaches specific status  
**Parameters:** `$data` (array) - Subscription information  
**Priority:** 10  
**Use Case:** Handle specific subscription statuses

```php
add_action('fluent_cart/payments/subscription_active', function($data) {
    $subscription = $data['subscription'];
    // Activate external services
    activate_external_subscription($subscription);
}, 10, 1);
```

### Cart Hooks

#### `fluent_cart/cart/item_added`
**Description:** Fired when an item is added to the cart  
**Parameters:** `$data` (array) - Cart and item information  
**Priority:** 10  
**Use Case:** Track cart additions, update inventory

```php
add_action('fluent_cart/cart/item_added', function($data) {
    $cart = $data['cart'];
    $item = $data['item'];
    
    // Track cart addition
    track_cart_addition($cart, $item);
}, 10, 1);
```

#### `fluent_cart/cart/item_removed`
**Description:** Fired when an item is removed from the cart  
**Parameters:** `$data` (array) - Cart and item information  
**Priority:** 10  
**Use Case:** Track cart removals, update inventory

```php
add_action('fluent_cart/cart/item_removed', function($data) {
    $cart = $data['cart'];
    $item = $data['item'];
    
    // Track cart removal
    track_cart_removal($cart, $item);
}, 10, 1);
```

### Product Hooks

#### `fluent_cart/product_updated`
**Description:** Fired when a product is updated  
**Parameters:** `$data` (array) - Product information  
**Priority:** 10  
**Use Case:** Sync product data, update external catalogs

```php
add_action('fluent_cart/product_updated', function($data) {
    $product = $data['product'];
    // Sync with external catalog
    sync_external_catalog($product);
}, 10, 1);
```

### Module Hooks

#### `fluent_cart/module/activated/{module_key}`
**Description:** Fired when a module is activated  
**Parameters:** `$moduleData` (array), `$prevSettings` (array) - Module information  
**Priority:** 10  
**Use Case:** Initialize module-specific functionality

```php
add_action('fluent_cart/module/activated/payment_methods', function($moduleData, $prevSettings) {
    // Initialize payment method module
    initialize_payment_methods();
}, 10, 2);
```

#### `fluent_cart/module/deactivated/{module_key}`
**Description:** Fired when a module is deactivated  
**Parameters:** `$moduleData` (array), `$prevSettings` (array) - Module information  
**Priority:** 10  
**Use Case:** Clean up module-specific functionality

```php
add_action('fluent_cart/module/deactivated/payment_methods', function($moduleData, $prevSettings) {
    // Clean up payment method module
    cleanup_payment_methods();
}, 10, 2);
```

### Admin Hooks

#### `fluent_cart/loading_app`
**Description:** Fired when FluentCart admin app is loading  
**Parameters:** `$app` (object) - Application instance  
**Priority:** 10  
**Use Case:** Add custom admin functionality

```php
add_action('fluent_cart/loading_app', function($app) {
    // Add custom admin functionality
    add_custom_admin_features($app);
}, 10, 1);
```

#### `fluent_cart/admin_js_loaded`
**Description:** Fired when admin JavaScript is loaded  
**Parameters:** `$app` (object) - Application instance  
**Priority:** 10  
**Use Case:** Add custom admin JavaScript

```php
add_action('fluent_cart/admin_js_loaded', function($app) {
    // Add custom admin JavaScript
    enqueue_custom_admin_scripts();
}, 10, 1);
```

### View/Template Hooks

#### `fluent_cart/views/single_product_page`
**Description:** Fired on single product page  
**Parameters:** `$data` (array) - Product and page data  
**Priority:** 10  
**Use Case:** Add custom content to product pages

```php
add_action('fluent_cart/views/single_product_page', function($data) {
    $product = $data['product'];
    // Add custom product page content
    echo '<div class="custom-product-info">Custom content here</div>';
}, 10, 1);
```

#### `fluent_cart/views/shop_app_wrapper`
**Description:** Fired in shop app wrapper  
**Parameters:** `$data` (array) - Shop data  
**Priority:** 10  
**Use Case:** Add custom shop functionality

```php
add_action('fluent_cart/views/shop_app_wrapper', function($data) {
    // Add custom shop functionality
    add_custom_shop_features($data);
}, 10, 1);
```

#### `fluent_cart/views/checkout_page`
**Description:** Fired on checkout page  
**Parameters:** `$data` (array) - Checkout data  
**Priority:** 10  
**Use Case:** Add custom checkout functionality

```php
add_action('fluent_cart/views/checkout_page', function($data) {
    $checkout = $data['checkout'];
    $cart = $data['cart'];
    // Add custom checkout functionality
    add_custom_checkout_features($checkout, $cart);
}, 10, 1);
```

#### `fluent_cart/views/checkout_page_empty_cart`
**Description:** Fired when checkout page has empty cart  
**Parameters:** `$data` (array) - Checkout data  
**Priority:** 10  
**Use Case:** Handle empty cart scenarios

```php
add_action('fluent_cart/views/checkout_page_empty_cart', function($data) {
    // Handle empty cart
    redirect_to_shop();
}, 10, 1);
```

### Cart Line Item Hooks

#### `fluent_cart/cart/line_item/line_meta`
**Description:** Fired for cart line item metadata  
**Parameters:** `$data` (array) - Line item data  
**Priority:** 10  
**Use Case:** Add custom line item metadata

```php
add_action('fluent_cart/cart/line_item/line_meta', function($data) {
    $item = $data['item'];
    // Add custom line item metadata
    echo '<div class="custom-line-meta">Custom metadata</div>';
}, 10, 1);
```

#### `fluent_cart/cart/line_item/before_total`
**Description:** Fired before cart line item total  
**Parameters:** `$data` (array) - Line item data  
**Priority:** 10  
**Use Case:** Add content before line item total

```php
add_action('fluent_cart/cart/line_item/before_total', function($data) {
    // Add content before total
    echo '<div class="before-total">Before total content</div>';
}, 10, 1);
```

#### `fluent_cart/cart/line_item/after_total`
**Description:** Fired after cart line item total  
**Parameters:** `$data` (array) - Line item data  
**Priority:** 10  
**Use Case:** Add content after line item total

```php
add_action('fluent_cart/cart/line_item/after_total', function($data) {
    // Add content after total
    echo '<div class="after-total">After total content</div>';
}, 10, 1);
```

#### `fluent_cart/cart/line_item/before_main_title`
**Description:** Fired before cart line item main title  
**Parameters:** `$data` (array) - Line item data  
**Priority:** 10  
**Use Case:** Add content before line item title

```php
add_action('fluent_cart/cart/line_item/before_main_title', function($data) {
    // Add content before title
    echo '<div class="before-title">Before title content</div>';
}, 10, 1);
```

#### `fluent_cart/cart/line_item/after_main_title`
**Description:** Fired after cart line item main title  
**Parameters:** `$data` (array) - Line item data  
**Priority:** 10  
**Use Case:** Add content after line item title

```php
add_action('fluent_cart/cart/line_item/after_main_title', function($data) {
    // Add content after title
    echo '<div class="after-title">After title content</div>';
}, 10, 1);
```

## Related Documentation

- [Filter Hooks](./filters) - FluentCart filter hooks
- [Event System](./events) - FluentCart event system
- [Database Models](/database/models) - Models used in hook data
- [REST API](/api/) - API endpoints that trigger hooks

## Previous/Next Navigation

- **Previous**: [Developer Hooks Overview](./) - FluentCart hooks system
- **Next**: [Filter Hooks](./filters) - FluentCart filter hooks

---

