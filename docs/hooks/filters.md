---
title: Filter Hooks
description: FluentCart filter hooks documentation with complete reference and usage examples.
---

# FluentCart Filter Hooks

Filter hooks allow you to modify data, settings, and behavior in FluentCart. They are perfect for customizing functionality, modifying output, and extending FluentCart's capabilities.

## Core Filter Hooks

### Email & Notifications


<details>
<summary><strong>`fluent_cart/email_notifications`</strong> &mdash; Filter email notification settings</summary>

**When it runs:**
This filter is applied whenever FluentCart retrieves or prepares the email notification settings, allowing you to customize or override the default notification configuration.

**Parameters:**
- <code>$settings</code> (array): The current email notification settings. Example keys:
    - <code>enabled</code> (bool): Whether notifications are enabled
    - <code>recipients</code> (array): List of recipient emails
    - <code>templates</code> (array): Email template settings
    - <code>custom_setting</code> (mixed): Any custom settings you add

**Returns:**
- (array): The modified email notification settings array

**Usage:**
```php
add_filter('fluent_cart/email_notifications', function($settings) {
        // Example: Add a custom setting
        $settings['custom_setting'] = 'custom_value';
        return $settings;
}, 10, 1);
```
</details>

### Coupon System


<details>
<summary><strong>`fluent_cart/coupon/will_skip_item`</strong> &mdash; Filter whether a coupon should skip an item</summary>

**When it runs:**
This filter is applied during coupon validation for each cart item, allowing you to programmatically skip applying a coupon to specific items based on custom logic.

**Parameters:**
- <code>$willSkip</code> (bool): Whether the item should be skipped (default logic result)
- <code>$data</code> (array): Contextual data for the item and coupon:
  - <code>item</code> (array): The cart item data (e.g., <code>product_id</code>, <code>quantity</code>, etc.)
  - <code>coupon</code> (array): The coupon data (e.g., <code>code</code>, <code>discount_type</code>, etc.)

**Returns:**
- (bool): Whether to skip applying the coupon to this item

**Usage:**
```php
add_filter('fluent_cart/coupon/will_skip_item', function($willSkip, $data) {
    $item = $data['item'];
    $coupon = $data['coupon'];
    // Custom logic: skip coupon for a specific product
    if ($item['product_id'] === 123) {
        return true;
    }
    return $willSkip;
}, 10, 2);
```
</details>

### Payment Methods


<details>
<summary><strong>`fluent_cart_form_disable_stripe_connect`</strong> &mdash; Filter whether to disable Stripe Connect</summary>

**When it runs:**
This filter is applied when determining whether to enable or disable Stripe Connect as a payment method in the checkout or settings UI.

**Parameters:**
- <code>$disable</code> (bool): Whether Stripe Connect is disabled (default logic result)
- <code>$data</code> (array): Contextual data (may include user, cart, or environment info)

**Returns:**
- (bool): Whether to disable Stripe Connect

**Usage:**
```php
add_filter('fluent_cart_form_disable_stripe_connect', function($disable, $data) {
    // Example: Only allow Stripe Connect for admins
    if (is_admin() && current_user_can('manage_options')) {
        return false;
    }
    return $disable;
}, 10, 2);
```
</details>


<details>
<summary><strong>`fluent_cart/paypal_plan_id`</strong> &mdash; Filter PayPal plan ID</summary>

**When it runs:**
This filter is applied when FluentCart determines the PayPal plan ID to use for a subscription, allowing you to override the default plan ID based on subscription data.

**Parameters:**
- <code>$planId</code> (string): The current PayPal plan ID
- <code>$data</code> (array): Contextual data, including:
  - <code>subscription</code> (array): Subscription details (e.g., <code>billing_cycle</code>, <code>product_id</code>, etc.)

**Returns:**

        <details>
        <summary><strong>`fluent_cart/checkout_validation_rules`</strong> &mdash; Filter checkout validation rules</summary>

        **When it runs:**
        This filter is applied when building the validation rules for the checkout form, allowing you to add, remove, or modify validation requirements for checkout fields.

        **Parameters:**
        - <code>$rules</code> (array): The current validation rules array (e.g., <code>['field_name' => 'required|string']</code>)
        - <code>$data</code> (array): Contextual data for the checkout (may include cart, user, etc.)

        **Returns:**
        - (array): The modified validation rules array

        **Usage:**
        ```php
        add_filter('fluent_cart/checkout_validation_rules', function($rules, $data) {
            // Add custom validation rules
            $rules['custom_field'] = 'required|string|max:255';
            return $rules;
        }, 10, 2);
        ```
        </details>
</details>


<details>
<summary><strong>`fluent_cart/payments/paypal_sdk_src`</strong> &mdash; Filter PayPal SDK source URL</summary>

**When it runs:**
This filter is applied when FluentCart enqueues the PayPal SDK script, allowing you to override the default SDK source URL.

**Parameters:**
- <code>$sdkSrc</code> (string): The current PayPal SDK source URL
- <code>$data</code> (array): Contextual data (may include environment, payment method, etc.)

**Returns:**
- (string): The modified SDK source URL

**Usage:**
```php
add_filter('fluent_cart/payments/paypal_sdk_src', function($sdkSrc, $data) {
    // Use a custom PayPal SDK source
    return 'https://www.paypal.com/sdk/js?client-id=YOUR_CLIENT_ID';
}, 10, 2);
```
</details>

### Subscription System


<details>
<summary><strong>`fluent_cart/subscription/url_{payment_method}`</strong> &mdash; Filter subscription URL for a specific payment method</summary>

**When it runs:**
This filter is applied when generating the management or view URL for a subscription, allowing you to customize the URL for each payment method (e.g., Stripe, PayPal).

**Parameters:**
- <code>$url</code> (string): The current subscription URL
- <code>$data</code> (array): Contextual data, including:
    - <code>subscription</code> (object|array): The subscription object or array (e.g., <code>id</code>, <code>status</code>, <code>payment_method</code>, etc.)

**Returns:**
- (string): The modified subscription URL

**Usage:**
```php
add_filter('fluent_cart/subscription/url_stripe', function($url, $data) {
        $subscription = $data['subscription'];
        // Custom subscription URL for Stripe
        return 'https://custom-portal.example.com/subscription/' . $subscription->id;
}, 10, 2);
```
</details>


<details>
<summary><strong>`fluent_cart/subscription/can_reactivate`</strong> &mdash; Filter whether a subscription can be reactivated</summary>

**When it runs:**
This filter is applied when checking if a cancelled subscription is eligible for reactivation, allowing you to override the default logic.

**Parameters:**
- <code>$canReactivate</code> (bool): Whether the subscription can be reactivated (default logic result)
- <code>$data</code> (array): Contextual data, including:
  - <code>subscription</code> (object|array): The subscription object or array (e.g., <code>status</code>, <code>cancelled_at</code>, etc.)

**Returns:**
- (bool): Whether to allow reactivation

**Usage:**
```php
add_filter('fluent_cart/subscription/can_reactivate', function($canReactivate, $data) {
    $subscription = $data['subscription'];
    // Allow reactivation within 30 days of cancellation
    if ($subscription->status === 'cancelled' && $subscription->cancelled_at > strtotime('-30 days')) {
        return true;
    }
    return $canReactivate;
}, 10, 2);
```
</details>

### Order System


<details>
<summary><strong>`fluent_cart/create_receipt_number_on_order_create`</strong> &mdash; Filter whether to create a receipt number on order creation</summary>

**When it runs:**
This filter is applied when a new order is created, allowing you to control whether a receipt number should be generated for the order.

**Parameters:**
- <code>$create</code> (bool): Whether to create a receipt number (default logic result)

**Returns:**
- (bool): Whether to create a receipt number for the order

**Usage:**
```php
add_filter('fluent_cart/create_receipt_number_on_order_create', function($create) {
    // Always create receipt numbers for paid orders
    return true;
}, 10, 1);
```
</details>


<details>
<summary><strong>`fluent_cart/single_order_downloads`</strong> &mdash; Filter single order downloads data</summary>

**When it runs:**
This filter is applied when preparing the downloadable files for a specific order, allowing you to add, remove, or modify download data for the order.

**Parameters:**
- <code>$downloadData</code> (array): The current download data for the order. Example structure:
    - <code>[ 'file_id' => [ 'name' => 'File Name', 'url' => 'https://...' ] ]</code>
- <code>$data</code> (array): Contextual data, including:
    - <code>order</code> (object|array): The order object or array

**Returns:**
- (array): The modified download data array

**Usage:**
```php
add_filter('fluent_cart/single_order_downloads', function($downloadData, $data) {
        $order = $data['order'];
        // Add a custom downloadable file
        $downloadData['custom_download'] = [
                'name' => 'Custom File',
                'url' => 'https://example.com/custom-file.pdf'
        ];
        return $downloadData;
}, 10, 2);
```
</details>

### Transaction System


<details>
<summary><strong>`fluent_cart/transaction/url_{payment_method}`</strong> &mdash; Filter transaction URL for a specific payment method</summary>

**When it runs:**
This filter is applied when generating the management or view URL for a transaction, allowing you to customize the URL for each payment method (e.g., Stripe, PayPal).

**Parameters:**
- <code>$url</code> (string): The current transaction URL
- <code>$data</code> (array): Contextual data, including:
    - <code>transaction</code> (object|array): The transaction object or array (e.g., <code>transaction_id</code>, <code>payment_method</code>, etc.)

**Returns:**
- (string): The modified transaction URL

**Usage:**
```php
add_filter('fluent_cart/transaction/url_stripe', function($url, $data) {
        $transaction = $data['transaction'];
        // Custom transaction URL for Stripe
        return 'https://dashboard.stripe.com/payments/' . $transaction->transaction_id;
}, 10, 2);
```
</details>


<details>
<summary><strong>`fluentcart/transaction/receipt_page_url`</strong> &mdash; Filter transaction receipt page URL</summary>

**When it runs:**
This filter is applied when generating the URL for the transaction receipt page, allowing you to customize the receipt page URL for a transaction.

**Parameters:**
- <code>$url</code> (string): The current receipt page URL
- <code>$data</code> (array): Contextual data, including:
    - <code>transaction</code> (object|array): The transaction object or array (e.g., <code>id</code>, <code>order_id</code>, etc.)

**Returns:**
- (string): The modified receipt page URL

**Usage:**
```php
add_filter('fluentcart/transaction/receipt_page_url', function($url, $data) {
        $transaction = $data['transaction'];
        // Custom receipt page URL
        return home_url('/receipt/' . $transaction->id);
}, 10, 2);
```
</details>

### Admin Interface


<details>
<summary><strong>`fluent_cart/admin_menu_title`</strong> &mdash; Filter admin menu title</summary>

**When it runs:**
This filter is applied when generating the FluentCart admin menu title, allowing you to customize the menu label in the WordPress dashboard.

**Parameters:**
- <code>$title</code> (string): The current admin menu title
- <code>$data</code> (array): Contextual data (may include user, settings, etc.)

**Returns:**
- (string): The modified admin menu title

**Usage:**
```php
add_filter('fluent_cart/admin_menu_title', function($title, $data) {
    // Custom admin menu title
    return 'My Custom Store';
}, 10, 2);
```
</details>


<details>
<summary><strong>`fluent_cart/admin_base_url`</strong> &mdash; Filter admin base URL</summary>

**When it runs:**
This filter is applied when generating the base URL for FluentCart admin pages, allowing you to customize the admin URL structure.

**Parameters:**
- <code>$url</code> (string): The current admin base URL
- <code>$data</code> (array): Contextual data (may include user, settings, etc.)

**Returns:**
- (string): The modified admin base URL

**Usage:**
```php
add_filter('fluent_cart/admin_base_url', function($url, $data) {
    // Custom admin base URL
    return admin_url('admin.php?page=my-custom-store#/');
}, 10, 2);
```
</details>


<details>
<summary><strong>`fluent_cart/admin_filter_options`</strong> &mdash; Filter admin filter options</summary>

**When it runs:**
This filter is applied when generating the available filter options in the FluentCart admin interface, allowing you to add, remove, or modify filter options.

**Parameters:**
- <code>$options</code> (array): The current filter options. Example structure:
  - <code>[ 'filter_key' => [ 'label' => 'Label', 'options' => [ ... ] ] ]</code>
- <code>$data</code> (array): Contextual data (may include user, context, etc.)

**Returns:**
- (array): The modified filter options array

**Usage:**
```php
add_filter('fluent_cart/admin_filter_options', function($options, $data) {
    // Add a custom filter option
    $options['custom_filter'] = [
        'label' => 'Custom Filter',
        'options' => ['option1', 'option2']
    ];
    return $options;
}, 10, 2);
```
</details>

### Cart System


<details>
<summary><strong>`fluent_cart/item_max_quantity`</strong> &mdash; Filter maximum item quantity</summary>

**When it runs:**
This filter is applied when determining the maximum quantity allowed for a cart item, allowing you to set custom quantity limits per product or variation.

**Parameters:**
- <code>$quantity</code> (int): The current maximum quantity allowed
- <code>$data</code> (array): Contextual data, including:
  - <code>variation</code> (array|object): The product variation data
  - <code>product</code> (array|object): The product data (e.g., <code>id</code>, <code>name</code>, etc.)

**Returns:**
- (int): The modified maximum quantity

**Usage:**
```php
add_filter('fluent_cart/item_max_quantity', function($quantity, $data) {
    $variation = $data['variation'];
    $product = $data['product'];
    // Custom quantity limit for a specific product
    if ($product['id'] === 123) {
        return 5;
    }
    return $quantity;
}, 10, 2);
```
</details>


<details>
<summary><strong>`fluent_cart/cart_item_product_variation`</strong> &mdash; Filter cart item product variation</summary>

**When it runs:**
This filter is applied when retrieving or updating the product variation for a cart item, allowing you to modify the variation object before it is used in the cart.

**Parameters:**
- <code>$variation</code> (object): The current product variation object
- <code>$itemId</code> (int): The cart item ID
- <code>$incrementBy</code> (int): The quantity increment value
- <code>$existingItems</code> (array): The current cart items array

**Returns:**
- (object): The modified product variation object

**Usage:**
```php
add_filter('fluent_cart/cart_item_product_variation', function($variation, $itemId, $incrementBy, $existingItems) {
    // Custom variation logic
    if ($variation->id === 456) {
        $variation->custom_field = 'custom_value';
    }
    return $variation;
}, 10, 4);
```
</details>

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


<details>
<summary><strong>`fluent_cart/checkout_address_fields`</strong> &mdash; Filter checkout address fields</summary>

**When it runs:**
This filter is applied when building the address fields for the checkout form, allowing you to add, remove, or modify address fields.

**Parameters:**
- <code>$fields</code> (array): The current address fields array. Example structure:
  - <code>[ 'field_key' => [ 'label' => 'Label', 'type' => 'text', 'required' => true ] ]</code>
- <code>$data</code> (array): Contextual data for the checkout (may include cart, user, etc.)

**Returns:**
- (array): The modified address fields array

**Usage:**
```php
add_filter('fluent_cart/checkout_address_fields', function($fields, $data) {
    // Add a custom address field
    $fields['custom_field'] = [
        'label' => 'Custom Field',
        'type' => 'text',
        'required' => false
    ];
    return $fields;
}, 10, 2);
```
</details>


<details>
<summary><strong>`fluent_cart/checkout_billing_fields`</strong> &mdash; Filter checkout billing fields</summary>

**When it runs:**
This filter is applied when building the billing fields for the checkout form, allowing you to add, remove, or modify billing fields.

**Parameters:**
- <code>$fields</code> (array): The current billing fields array. Example structure:
  - <code>[ 'field_key' => [ 'label' => 'Label', 'type' => 'text', 'required' => true ] ]</code>
- <code>$data</code> (array): Contextual data for the checkout (may include cart, user, etc.)

**Returns:**
- (array): The modified billing fields array

**Usage:**
```php
add_filter('fluent_cart/checkout_billing_fields', function($fields, $data) {
    // Add a custom billing field
    $fields['company_name'] = [
        'label' => 'Company Name',
        'type' => 'text',
        'required' => false
    ];
    return $fields;
}, 10, 2);
```
</details>


<details>
<summary><strong>`fluent_cart/checkout_shipping_fields`</strong> &mdash; Filter checkout shipping fields</summary>

**When it runs:**
This filter is applied when building the shipping fields for the checkout form, allowing you to add, remove, or modify shipping fields.

**Parameters:**
- <code>$fields</code> (array): The current shipping fields array. Example structure:
  - <code>[ 'field_key' => [ 'label' => 'Label', 'type' => 'text', 'required' => true ] ]</code>
- <code>$data</code> (array): Contextual data for the checkout (may include cart, user, etc.)

**Returns:**
- (array): The modified shipping fields array

**Usage:**
```php
add_filter('fluent_cart/checkout_shipping_fields', function($fields, $data) {
    // Add a custom shipping field
    $fields['delivery_instructions'] = [
        'label' => 'Delivery Instructions',
        'type' => 'textarea',
        'required' => false
    ];
    return $fields;
}, 10, 2);
```
</details>

### Status Filters


<details>
<summary><strong>`fluent-cart/order_statuses`</strong> &mdash; Filter available order statuses</summary>

**When it runs:**
This filter is applied when retrieving the list of available order statuses, allowing you to add, remove, or modify order statuses.

**Parameters:**
- <code>$statuses</code> (array): The current order statuses array (e.g., <code>['pending' => 'Pending', ...]</code>)

**Returns:**
- (array): The modified order statuses array

**Usage:**
```php
add_filter('fluent-cart/order_statuses', function($statuses) {
    // Add a custom order status
    $statuses['custom_status'] = 'Custom Status';
    return $statuses;
}, 10, 1);
```
</details>


<details>
<summary><strong>`fluent-cart/editable_order_statuses`</strong> &mdash; Filter editable order statuses</summary>

**When it runs:**
This filter is applied when retrieving the list of order statuses that can be edited, allowing you to control which statuses are editable in the admin UI.

**Parameters:**
- <code>$statuses</code> (array): The current editable order statuses array

**Returns:**
- (array): The modified editable order statuses array

**Usage:**
```php
add_filter('fluent-cart/editable_order_statuses', function($statuses) {
    // Remove a status from the editable list
    unset($statuses['completed']);
    return $statuses;
}, 10, 1);
```
</details>


<details>
<summary><strong>`fluent-cart/editable_customer_statuses`</strong> &mdash; Filter editable customer statuses</summary>

**When it runs:**
This filter is applied when retrieving the list of customer statuses that can be edited, allowing you to control which statuses are editable in the admin UI.

**Parameters:**
- <code>$statuses</code> (array): The current editable customer statuses array

**Returns:**
- (array): The modified editable customer statuses array

**Usage:**
```php
add_filter('fluent-cart/editable_customer_statuses', function($statuses) {
    // Add a custom customer status
    $statuses['vip'] = 'VIP Customer';
    return $statuses;
}, 10, 1);
```
</details>


<details>
<summary><strong>`fluent-cart/shipping_statuses`</strong> &mdash; Filter available shipping statuses</summary>

**When it runs:**
This filter is applied when retrieving the list of available shipping statuses, allowing you to add, remove, or modify shipping statuses.

**Parameters:**
- <code>$statuses</code> (array): The current shipping statuses array

**Returns:**
- (array): The modified shipping statuses array

**Usage:**
```php
add_filter('fluent-cart/shipping_statuses', function($statuses) {
    // Add a custom shipping status
    $statuses['custom_shipping'] = 'Custom Shipping';
    return $statuses;
}, 10, 1);
```
</details>


<details>
<summary><strong>`fluent-cart/transaction_statuses`</strong> &mdash; Filter available transaction statuses</summary>

**When it runs:**
This filter is applied when retrieving the list of available transaction statuses, allowing you to add, remove, or modify transaction statuses.

**Parameters:**
- <code>$statuses</code> (array): The current transaction statuses array

**Returns:**
- (array): The modified transaction statuses array

**Usage:**
```php
add_filter('fluent-cart/transaction_statuses', function($statuses) {
    // Add a custom transaction status
    $statuses['custom_transaction'] = 'Custom Transaction';
    return $statuses;
}, 10, 1);
```
</details>


<details>
<summary><strong>`fluent-cart/editable_transaction_statuses`</strong> &mdash; Filter editable transaction statuses</summary>

**When it runs:**
This filter is applied when retrieving the list of transaction statuses that can be edited, allowing you to control which statuses are editable in the admin UI.

**Parameters:**
- <code>$statuses</code> (array): The current editable transaction statuses array

**Returns:**
- (array): The modified editable transaction statuses array

**Usage:**
```php
add_filter('fluent-cart/editable_transaction_statuses', function($statuses) {
    // Remove a status from the editable list
    unset($statuses['completed']);
    return $statuses;
}, 10, 1);
```
</details>


<details>
<summary><strong>`fluent-cart/coupon_statuses`</strong> &mdash; Filter available coupon statuses</summary>

**When it runs:**
This filter is applied when retrieving the list of available coupon statuses, allowing you to add, remove, or modify coupon statuses.

**Parameters:**
- <code>$statuses</code> (array): The current coupon statuses array

**Returns:**
- (array): The modified coupon statuses array

**Usage:**
```php
add_filter('fluent-cart/coupon_statuses', function($statuses) {
    // Add a custom coupon status
    $statuses['custom_coupon'] = 'Custom Coupon';
    return $statuses;
}, 10, 1);
```
</details>

### Currency & Localization


<details>
<summary><strong>`fluent-cart/available_currencies`</strong> &mdash; Filter available currencies</summary>

**When it runs:**
This filter is applied when retrieving the list of available currencies, allowing you to add, remove, or modify currencies.

**Parameters:**
- <code>$currencies</code> (array): The current available currencies array (e.g., <code>['USD' => 'US Dollar', ...]</code>)

**Returns:**
- (array): The modified available currencies array

**Usage:**
```php
add_filter('fluent-cart/available_currencies', function($currencies) {
    // Add a custom currency
    $currencies['BTC'] = 'Bitcoin';
    return $currencies;
}, 10, 1);
```
</details>


<details>
<summary><strong>`fluent-cart/util/countries`</strong> &mdash; Filter available countries</summary>

**When it runs:**
This filter is applied when retrieving the list of available countries, allowing you to add, remove, or modify countries.

**Parameters:**
- <code>$countries</code> (array): The current available countries array (e.g., <code>['US' => 'United States', ...]</code>)

**Returns:**
- (array): The modified available countries array

**Usage:**
```php
add_filter('fluent-cart/util/countries', function($countries) {
    // Add a custom country
    $countries['XX'] = 'Custom Country';
    return $countries;
}, 10, 1);
```
</details>


<details>
<summary><strong>`fluent-cart/site_prefix`</strong> &mdash; Filter site prefix</summary>

**When it runs:**
This filter is applied when retrieving the site prefix used for FluentCart data, allowing you to customize the prefix for multi-site or branding purposes.

**Parameters:**
- <code>$prefix</code> (string): The current site prefix

**Returns:**
- (string): The modified site prefix

**Usage:**
```php
add_filter('fluent-cart/site_prefix', function($prefix) {
    // Custom site prefix
    return 'MYSTORE_';
}, 10, 1);
```
</details>

### File System


<details>
<summary><strong>`fluent_cart/download_expiration_minutes`</strong> &mdash; Filter download expiration minutes</summary>

**When it runs:**
This filter is applied when determining the expiration time (in minutes) for downloadable files, allowing you to set custom expiration times based on file type or other logic.

**Parameters:**
- <code>$minutes</code> (int): The current expiration time in minutes
- <code>$data</code> (array): Contextual data, including:
  - <code>file</code> (array|object): The file data (e.g., <code>type</code>, <code>name</code>, etc.)

**Returns:**
- (int): The modified expiration time in minutes

**Usage:**
```php
add_filter('fluent_cart/download_expiration_minutes', function($minutes, $data) {
    $file = $data['file'];
    // Custom expiration logic for premium files
    if ($file['type'] === 'premium') {
        return 1440; // 24 hours
    }
    return $minutes;
}, 10, 2);
```
</details>

## Related Documentation

- [Action Hooks](./actions) - FluentCart action hooks
- [Event System](./events) - FluentCart event system
- [Database Models](/database/models) - Models used in filter data
- [REST API](/api/) - API endpoints that use filters

## Previous/Next Navigation

- **Previous**: [Action Hooks](./actions) - FluentCart action hooks
- **Next**: [Event System](./events) - FluentCart event system

---

