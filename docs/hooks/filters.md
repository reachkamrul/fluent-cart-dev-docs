---
title: Filter Hooks
description: FluentCart filter hooks documentation with complete reference and usage examples.
---

# FluentCart Filter Hooks

Filter hooks allow you to modify data, settings, and behavior in FluentCart. They are perfect for customizing functionality, modifying output, and extending FluentCart's capabilities.

## Core Filter Hooks

### Email & Notifications

#### `fluent_cart/email_notifications`
**Description:** Filter email notification settings  
**Parameters:** `$settings` (array) - Email notification settings  
**Returns:** `array` - Modified settings  
**Use Case:** Customize email notification behavior

```php
add_filter('fluent_cart/email_notifications', function($settings) {
    // Modify email notification settings
    $settings['custom_setting'] = 'custom_value';
    return $settings;
}, 10, 1);
```

### Coupon System

#### `fluent_cart/coupon/will_skip_item`
**Description:** Filter whether a coupon should skip an item  
**Parameters:** `$willSkip` (bool), `$data` (array) - Skip status and item data  
**Returns:** `bool` - Whether to skip the item  
**Use Case:** Custom coupon logic

```php
add_filter('fluent_cart/coupon/will_skip_item', function($willSkip, $data) {
    $item = $data['item'];
    $coupon = $data['coupon'];
    
    // Custom logic to determine if coupon should skip item
    if ($item['product_id'] === 123) {
        return true; // Skip this specific product
    }
    
    return $willSkip;
}, 10, 2);
```

### Payment Methods

#### `fluent_cart_form_disable_stripe_connect`
**Description:** Filter whether to disable Stripe Connect  
**Parameters:** `$disable` (bool), `$data` (array) - Disable status and data  
**Returns:** `bool` - Whether to disable Stripe Connect  
**Use Case:** Control Stripe Connect behavior

```php
add_filter('fluent_cart_form_disable_stripe_connect', function($disable, $data) {
    // Custom logic to disable Stripe Connect
    if (is_admin() && current_user_can('manage_options')) {
        return false; // Allow Stripe Connect for admins
    }
    
    return $disable;
}, 10, 2);
```

#### `fluent_cart/paypal_plan_id`
**Description:** Filter PayPal plan ID  
**Parameters:** `$planId` (string), `$data` (array) - Plan ID and data  
**Returns:** `string` - Modified plan ID  
**Use Case:** Customize PayPal subscription plans

```php
add_filter('fluent_cart/paypal_plan_id', function($planId, $data) {
    $subscription = $data['subscription'];
    
    // Custom logic for plan ID
    if ($subscription['billing_cycle'] === 'yearly') {
        return 'P-1234567890'; // Custom yearly plan
    }
    
    return $planId;
}, 10, 2);
```

#### `fluent_cart/payments/paypal_sdk_src`
**Description:** Filter PayPal SDK source URL  
**Parameters:** `$sdkSrc` (string), `$data` (array) - SDK source and data  
**Returns:** `string` - Modified SDK source  
**Use Case:** Customize PayPal SDK loading

```php
add_filter('fluent_cart/payments/paypal_sdk_src', function($sdkSrc, $data) {
    // Use custom PayPal SDK source
    return 'https://www.paypal.com/sdk/js?client-id=YOUR_CLIENT_ID';
}, 10, 2);
```

### Subscription System

#### `fluent_cart/subscription/url_{payment_method}`
**Description:** Filter subscription URL for specific payment method  
**Parameters:** `$url` (string), `$data` (array) - URL and subscription data  
**Returns:** `string` - Modified URL  
**Use Case:** Customize subscription URLs

```php
add_filter('fluent_cart/subscription/url_stripe', function($url, $data) {
    $subscription = $data['subscription'];
    
    // Custom subscription URL for Stripe
    return 'https://custom-portal.example.com/subscription/' . $subscription->id;
}, 10, 2);
```

#### `fluent_cart/subscription/can_reactivate`
**Description:** Filter whether subscription can be reactivated  
**Parameters:** `$canReactivate` (bool), `$data` (array) - Reactivation status and data  
**Returns:** `bool` - Whether subscription can be reactivated  
**Use Case:** Control subscription reactivation

```php
add_filter('fluent_cart/subscription/can_reactivate', function($canReactivate, $data) {
    $subscription = $data['subscription'];
    
    // Custom logic for reactivation
    if ($subscription->status === 'cancelled' && $subscription->cancelled_at > strtotime('-30 days')) {
        return true; // Allow reactivation within 30 days
    }
    
    return $canReactivate;
}, 10, 2);
```

### Order System

#### `fluent_cart/create_receipt_number_on_order_create`
**Description:** Filter whether to create receipt number on order creation  
**Parameters:** `$create` (bool) - Whether to create receipt number  
**Returns:** `bool` - Whether to create receipt number  
**Use Case:** Control receipt number generation

```php
add_filter('fluent_cart/create_receipt_number_on_order_create', function($create) {
    // Always create receipt numbers for paid orders
    return true;
}, 10, 1);
```

#### `fluent_cart/single_order_downloads`
**Description:** Filter single order downloads data  
**Parameters:** `$downloadData` (array), `$data` (array) - Download data and order data  
**Returns:** `array` - Modified download data  
**Use Case:** Customize order downloads

```php
add_filter('fluent_cart/single_order_downloads', function($downloadData, $data) {
    $order = $data['order'];
    
    // Add custom download data
    $downloadData['custom_download'] = [
        'name' => 'Custom File',
        'url' => 'https://example.com/custom-file.pdf'
    ];
    
    return $downloadData;
}, 10, 2);
```

### Transaction System

#### `fluent_cart/transaction/url_{payment_method}`
**Description:** Filter transaction URL for specific payment method  
**Parameters:** `$url` (string), `$data` (array) - URL and transaction data  
**Returns:** `string` - Modified URL  
**Use Case:** Customize transaction URLs

```php
add_filter('fluent_cart/transaction/url_stripe', function($url, $data) {
    $transaction = $data['transaction'];
    
    // Custom transaction URL for Stripe
    return 'https://dashboard.stripe.com/payments/' . $transaction->transaction_id;
}, 10, 2);
```

#### `fluentcart/transaction/receipt_page_url`
**Description:** Filter transaction receipt page URL  
**Parameters:** `$url` (string), `$data` (array) - URL and transaction data  
**Returns:** `string` - Modified URL  
**Use Case:** Customize receipt page URLs

```php
add_filter('fluentcart/transaction/receipt_page_url', function($url, $data) {
    $transaction = $data['transaction'];
    
    // Custom receipt page URL
    return home_url('/receipt/' . $transaction->id);
}, 10, 2);
```

### Admin Interface

#### `fluent_cart/admin_menu_title`
**Description:** Filter admin menu title  
**Parameters:** `$title` (string), `$data` (array) - Title and data  
**Returns:** `string` - Modified title  
**Use Case:** Customize admin menu title

```php
add_filter('fluent_cart/admin_menu_title', function($title, $data) {
    // Custom admin menu title
    return 'My Custom Store';
}, 10, 2);
```

#### `fluent_cart/admin_base_url`
**Description:** Filter admin base URL  
**Parameters:** `$url` (string), `$data` (array) - URL and data  
**Returns:** `string` - Modified URL  
**Use Case:** Customize admin URLs

```php
add_filter('fluent_cart/admin_base_url', function($url, $data) {
    // Custom admin base URL
    return admin_url('admin.php?page=my-custom-store#/');
}, 10, 2);
```

#### `fluent_cart/admin_filter_options`
**Description:** Filter admin filter options  
**Parameters:** `$options` (array), `$data` (array) - Options and data  
**Returns:** `array` - Modified options  
**Use Case:** Customize admin filters

```php
add_filter('fluent_cart/admin_filter_options', function($options, $data) {
    // Add custom filter options
    $options['custom_filter'] = [
        'label' => 'Custom Filter',
        'options' => ['option1', 'option2']
    ];
    
    return $options;
}, 10, 2);
```

### Cart System

#### `fluent_cart/item_max_quantity`
**Description:** Filter maximum item quantity  
**Parameters:** `$quantity` (int), `$data` (array) - Quantity and item data  
**Returns:** `int` - Modified quantity  
**Use Case:** Control item quantities

```php
add_filter('fluent_cart/item_max_quantity', function($quantity, $data) {
    $variation = $data['variation'];
    $product = $data['product'];
    
    // Custom quantity limits
    if ($product['id'] === 123) {
        return 5; // Limit specific product to 5
    }
    
    return $quantity;
}, 10, 2);
```

#### `fluent_cart/cart_item_product_variation`
**Description:** Filter cart item product variation  
**Parameters:** `$variation` (object), `$itemId` (int), `$incrementBy` (int), `$existingItems` (array) - Variation and item data  
**Returns:** `object` - Modified variation  
**Use Case:** Customize cart item variations

```php
add_filter('fluent_cart/cart_item_product_variation', function($variation, $itemId, $incrementBy, $existingItems) {
    // Custom variation logic
    if ($variation->id === 456) {
        $variation->custom_field = 'custom_value';
    }
    
    return $variation;
}, 10, 4);
```

### Checkout System

#### `fluent_cart/checkout_validation_rules`
**Description:** Filter checkout validation rules  
**Parameters:** `$rules` (array), `$data` (array) - Rules and checkout data  
**Returns:** `array` - Modified rules  
**Use Case:** Customize checkout validation

```php
add_filter('fluent_cart/checkout_validation_rules', function($rules, $data) {
    // Add custom validation rules
    $rules['custom_field'] = 'required|string|max:255';
    
    return $rules;
}, 10, 2);
```

#### `fluent_cart/checkout_address_fields`
**Description:** Filter checkout address fields  
**Parameters:** `$fields` (array), `$data` (array) - Fields and data  
**Returns:** `array` - Modified fields  
**Use Case:** Customize address fields

```php
add_filter('fluent_cart/checkout_address_fields', function($fields, $data) {
    // Add custom address field
    $fields['custom_field'] = [
        'label' => 'Custom Field',
        'type' => 'text',
        'required' => false
    ];
    
    return $fields;
}, 10, 2);
```

#### `fluent_cart/checkout_billing_fields`
**Description:** Filter checkout billing fields  
**Parameters:** `$fields` (array), `$data` (array) - Fields and data  
**Returns:** `array` - Modified fields  
**Use Case:** Customize billing fields

```php
add_filter('fluent_cart/checkout_billing_fields', function($fields, $data) {
    // Add custom billing field
    $fields['company_name'] = [
        'label' => 'Company Name',
        'type' => 'text',
        'required' => false
    ];
    
    return $fields;
}, 10, 2);
```

#### `fluent_cart/checkout_shipping_fields`
**Description:** Filter checkout shipping fields  
**Parameters:** `$fields` (array), `$data` (array) - Fields and data  
**Returns:** `array` - Modified fields  
**Use Case:** Customize shipping fields

```php
add_filter('fluent_cart/checkout_shipping_fields', function($fields, $data) {
    // Add custom shipping field
    $fields['delivery_instructions'] = [
        'label' => 'Delivery Instructions',
        'type' => 'textarea',
        'required' => false
    ];
    
    return $fields;
}, 10, 2);
```

### Status Filters

#### `fluent-cart/order_statuses`
**Description:** Filter available order statuses  
**Parameters:** `$statuses` (array) - Order statuses  
**Returns:** `array` - Modified statuses  
**Use Case:** Add custom order statuses

```php
add_filter('fluent-cart/order_statuses', function($statuses) {
    // Add custom order status
    $statuses['custom_status'] = 'Custom Status';
    
    return $statuses;
}, 10, 1);
```

#### `fluent-cart/editable_order_statuses`
**Description:** Filter editable order statuses  
**Parameters:** `$statuses` (array) - Editable statuses  
**Returns:** `array` - Modified statuses  
**Use Case:** Control which statuses are editable

```php
add_filter('fluent-cart/editable_order_statuses', function($statuses) {
    // Remove status from editable list
    unset($statuses['completed']);
    
    return $statuses;
}, 10, 1);
```

#### `fluent-cart/editable_customer_statuses`
**Description:** Filter editable customer statuses  
**Parameters:** `$statuses` (array) - Editable statuses  
**Returns:** `array` - Modified statuses  
**Use Case:** Control which customer statuses are editable

```php
add_filter('fluent-cart/editable_customer_statuses', function($statuses) {
    // Add custom customer status
    $statuses['vip'] = 'VIP Customer';
    
    return $statuses;
}, 10, 1);
```

#### `fluent-cart/shipping_statuses`
**Description:** Filter available shipping statuses  
**Parameters:** `$statuses` (array) - Shipping statuses  
**Returns:** `array` - Modified statuses  
**Use Case:** Add custom shipping statuses

```php
add_filter('fluent-cart/shipping_statuses', function($statuses) {
    // Add custom shipping status
    $statuses['custom_shipping'] = 'Custom Shipping';
    
    return $statuses;
}, 10, 1);
```

#### `fluent-cart/transaction_statuses`
**Description:** Filter available transaction statuses  
**Parameters:** `$statuses` (array) - Transaction statuses  
**Returns:** `array` - Modified statuses  
**Use Case:** Add custom transaction statuses

```php
add_filter('fluent-cart/transaction_statuses', function($statuses) {
    // Add custom transaction status
    $statuses['custom_transaction'] = 'Custom Transaction';
    
    return $statuses;
}, 10, 1);
```

#### `fluent-cart/editable_transaction_statuses`
**Description:** Filter editable transaction statuses  
**Parameters:** `$statuses` (array) - Editable statuses  
**Returns:** `array` - Modified statuses  
**Use Case:** Control which transaction statuses are editable

```php
add_filter('fluent-cart/editable_transaction_statuses', function($statuses) {
    // Remove status from editable list
    unset($statuses['completed']);
    
    return $statuses;
}, 10, 1);
```

#### `fluent-cart/coupon_statuses`
**Description:** Filter available coupon statuses  
**Parameters:** `$statuses` (array) - Coupon statuses  
**Returns:** `array` - Modified statuses  
**Use Case:** Add custom coupon statuses

```php
add_filter('fluent-cart/coupon_statuses', function($statuses) {
    // Add custom coupon status
    $statuses['custom_coupon'] = 'Custom Coupon';
    
    return $statuses;
}, 10, 1);
```

### Currency & Localization

#### `fluent-cart/available_currencies`
**Description:** Filter available currencies  
**Parameters:** `$currencies` (array) - Available currencies  
**Returns:** `array` - Modified currencies  
**Use Case:** Add custom currencies

```php
add_filter('fluent-cart/available_currencies', function($currencies) {
    // Add custom currency
    $currencies['BTC'] = 'Bitcoin';
    
    return $currencies;
}, 10, 1);
```

#### `fluent-cart/util/countries`
**Description:** Filter available countries  
**Parameters:** `$countries` (array) - Available countries  
**Returns:** `array` - Modified countries  
**Use Case:** Customize country list

```php
add_filter('fluent-cart/util/countries', function($countries) {
    // Add custom country
    $countries['XX'] = 'Custom Country';
    
    return $countries;
}, 10, 1);
```

#### `fluent-cart/site_prefix`
**Description:** Filter site prefix  
**Parameters:** `$prefix` (string) - Site prefix  
**Returns:** `string` - Modified prefix  
**Use Case:** Customize site prefix

```php
add_filter('fluent-cart/site_prefix', function($prefix) {
    // Custom site prefix
    return 'MYSTORE_';
}, 10, 1);
```

### File System

#### `fluent_cart/download_expiration_minutes`
**Description:** Filter download expiration minutes  
**Parameters:** `$minutes` (int), `$data` (array) - Minutes and file data  
**Returns:** `int` - Modified minutes  
**Use Case:** Control download expiration

```php
add_filter('fluent_cart/download_expiration_minutes', function($minutes, $data) {
    $file = $data['file'];
    
    // Custom expiration logic
    if ($file['type'] === 'premium') {
        return 1440; // 24 hours for premium files
    }
    
    return $minutes;
}, 10, 2);
```

## Related Documentation

- [Action Hooks](./actions) - FluentCart action hooks
- [Event System](./events) - FluentCart event system
- [Database Models](/database/models) - Models used in filter data
- [REST API](/api/) - API endpoints that use filters

## Previous/Next Navigation

- **Previous**: [Action Hooks](./actions) - FluentCart action hooks
- **Next**: [Event System](./events) - FluentCart event system

---

