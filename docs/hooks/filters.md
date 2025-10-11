---
title: Filter Hooks
description: FluentCart filter hooks documentation with complete reference and usage examples.
---

# FluentCart Filter Hooks

Filter hooks allow you to modify data, settings, and behavior in FluentCart. They are perfect for customizing functionality, modifying output, and extending FluentCart's capabilities.

## Core Filter Hooks

### Email & Notifications


<details>
<summary><code>`fluent_cart/email_notifications`</code> &mdash; Filter email notification settings</summary>

**When it runs:**
This filter is applied whenever FluentCart retrieves or prepares the email notification settings, allowing you to customize or override the default notification configuration.


**Parameters:**

- `$settings` (array): The current email notification settings
    ```php
    $settings = [
        'enabled'        => true,
        'recipients'     => ['admin@example.com'],
        'templates'      => [],
        'custom_setting' => 'any value',
    ];
    ```

**Returns:**
- $settings (array): The modified email notification settings array

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
<summary><code>`fluent_cart/coupon/will_skip_item`</code> &mdash; Filter whether a coupon should skip an item</summary>

**When it runs:**
This filter is applied during coupon validation for each cart item, allowing you to programmatically skip applying a coupon to specific items based on custom logic.

**Parameters:**

- `$willSkip` (bool): Whether the item should be skipped (default logic result)
- `$data` (array): Contextual data for the item and coupon
    ```php
    $data = [
        'item' => [
            'object_id',
            'product_id',
            'variation_id',
            'name',
            'quantity',
            'price',
            'subtotal',
            'total',
            'tax',
            'discount',
            'meta',
            'type',
            'sku',
            'image',
            'options',
            'cart_item_id',
        'coupon' => [
            'id',
            'parent',
            'title',
            'code',
            'status',
            'type',
            'conditions',
            'amount',
            'stackable',
            'priority',
            'use_count',
            'notes',
            'show_on_checkout',
            'start_date',
            'end_date',
            'max_uses',
        ],
        'cart' => [ /* Cart object, see Cart model for keys */ ]
    ];
    ```

**Returns:**
- `$willSkip` (bool): Whether to skip applying the coupon to this item

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
<summary><code>`fluent_cart_form_disable_stripe_connect`</code> &mdash; Filter whether to disable Stripe Connect</summary>

**When it runs:**

**Parameters:**

- `$disable` (bool): Whether Stripe Connect is disabled (default logic result)
- `$data` (array): Contextual data. Example structure:
    ```php
    $data = [
        'user' => [
            'ID',
            'user_login',
            'user_pass',
            'user_nicename',
            'user_email',
            'user_url',
            'user_registered',
            'user_activation_key',
            'user_status',
            'display_name',
            'roles',
            'allcaps',
            'filter',
        ],
        'cart' => [
            'id',
            'items',
            'total',
            'subtotal',
            'tax',
            'discount',
            'fees',
            'shipping_total',
            'currency',
            'customer_id',
            'created_at',
            'updated_at',
            'meta',
        ],
        'environment' => [
            'is_admin',
            'is_ajax',
            'site_url',
            'home_url',
            'current_user_id',
            'request_ip',
            'user_agent',
        ]
    ];
    ```

**Returns:**
- `$disable` (bool): Whether to disable Stripe Connect

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
<summary><code>`fluent_cart/paypal_plan_id`</code> &mdash; Filter PayPal plan ID</summary>

**When it runs:**
This filter is applied when FluentCart determines the PayPal plan ID to use for a subscription, allowing you to override the default plan ID based on subscription data.

**Parameters:**

- `$planId` (string): The current PayPal plan ID
- `$data` (array): Contextual data:
    ```php
    $data = [
        'subscription' => [
            'id',
            'status',
            'user_id',
            'product_id',
            'billing_cycle',
            'interval',
            'interval_count',
            'trial_days',
            'start_date',
            'total_cycles',
            'completed_cycles',
            'amount',
            'currency',
            'payment_method',
            'meta',
            'created_at',
            'updated_at',
        ]
    ];
    ```

**Returns:**
- `$planId` (string): The modified PayPal plan ID

**Usage:**
```php
add_filter('fluent_cart/paypal_plan_id', function($planId, $data) {
    $subscription = $data['subscription'];
    if ($subscription['billing_cycle'] === 'yearly') {
        return 'YEARLY_PLAN_ID';
    }
    return $planId;
}, 10, 2);
```
</details>


<details>
<summary><code>`fluent_cart/payments/paypal_sdk_src`</code> &mdash; Filter PayPal SDK source URL</summary>

**When it runs:**
This filter is applied when FluentCart enqueues the PayPal SDK script, allowing you to override the default SDK source URL.


**Parameters:**

- `$sdkSrc` (string): The current PayPal SDK source URL
- `$data` (array): Contextual data. Example structure:
    ```php
    $data = [
        'payment_method' => 'paypal',
        'environment' => [
            'is_admin',
            'is_ajax',
            'site_url',
            'home_url',
            'current_user_id',
            'request_ip',
            'user_agent',
        ],
        'cart' => [
            'id',
            'items',
            'total',
            'subtotal',
            'tax',
            'discount',
            'fees',
            'shipping_total',
            'currency',
            'customer_id',
            'created_at',
            'updated_at',
            'meta',
        ]
    ];
    ```

**Returns:**
- `$sdkSrc` (string): The modified SDK source URL

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
<summary><code>`fluent_cart/subscription/url_{payment_method}`</code> &mdash; Filter subscription URL for a specific payment method</summary>

**When it runs:**
This filter is applied when generating the management or view URL for a subscription, allowing you to customize the URL for each payment method (e.g., Stripe, PayPal).


**Parameters:**

- `$url` (string): The current subscription URL
- `$data` (array): Contextual data:
    ```php
    $data = [
            'status',
            'user_id',
            'product_id',
            'billing_cycle',
            'interval',
            'interval_count',
            'trial_days',
            'start_date',
            'end_date',
            'total_cycles',
            'completed_cycles',
            'amount',
            'currency',
            'payment_method',
            'meta',
            'created_at',
            'updated_at',
        ]
    ];
    ```

**Returns:**
- `$url` (string): The modified subscription URL

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
<summary><code>`fluent_cart/subscription/can_reactivate`</code> &mdash; Filter whether a subscription can be reactivated</summary>

**When it runs:**
This filter is applied when checking if a cancelled subscription is eligible for reactivation, allowing you to override the default logic.


**Parameters:**

- `$canReactivate` (bool): Whether the subscription can be reactivated (default logic result)
- `$data` (array): Contextual data:
    ```php
    $data = [
        'subscription' => [
            'id',
            'status',
            'user_id',
            'product_id',
            'billing_cycle',
            'interval',
            'interval_count',
            'trial_days',
            'start_date',
            'total_cycles',
            'completed_cycles',
            'amount',
            'currency',
            'payment_method',
            'cancelled_at',
            'meta',
            'updated_at',
        ]
    ];
    ```

**Returns:**
- `$canReactivate` (bool): Whether to allow reactivation

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
<summary><code>`fluent_cart/create_receipt_number_on_order_create`</code> &mdash; Filter whether to create a receipt number on order creation</summary>

**When it runs:**
This filter is applied when a new order is created, allowing you to control whether a receipt number should be generated for the order.


**Parameters:**

- `$create` (bool): Whether to create a receipt number (default logic result)

**Returns:**
- `$create` (bool): Whether to create a receipt number for the order

**Usage:**
```php
add_filter('fluent_cart/create_receipt_number_on_order_create', function($create) {
    // Always create receipt numbers for paid orders
    return true;
}, 10, 1);
```
</details>


<details>
<summary><code>`fluent_cart/single_order_downloads`</code> &mdash; Filter single order downloads data</summary>

**When it runs:**
This filter is applied when preparing the downloadable files for a specific order, allowing you to add, remove, or modify download data for the order.



**Parameters:**

- `$downloadData` (array): The current download data for the order
    ```php
    $downloadData = [
        'file_id' => [
            'name',
            'url',
            'size',
            'type',
            'expires_at',
            'download_count',
            'max_downloads',
        ]
    ];
    ```
- `$data` (array): Contextual data
    ```php
    $data = [
        'order' => [
            'id',
            'customer_id',
            'status',
            'total',
            'tax',
            'discount',
            'shipping_total',
            'currency',
            'created_at',
            'updated_at',
            'items',
            'meta',
        ]
    ];
    ```

**Returns:**
- `$downloadData` (array): The modified download data array

**Usage:**
```php
add_filter('fluent_cart/single_order_downloads', function($downloadData, $data) {
        $order = $data['order'];
        // Add a custom downloadable file
                'name' => 'Custom File',
                'url' => 'https://example.com/custom-file.pdf'
        ];
        return $downloadData;
}, 10, 2);
```
</details>



<details>
<summary><code>`fluent_cart/transaction/url_{payment_method}`</code> &mdash; Filter transaction URL for a specific payment method</summary>

**When it runs:**
This filter is applied when generating the management or view URL for a transaction, allowing you to customize the URL for each payment method (e.g., Stripe, PayPal).



**Parameters:**

- `$url` (string): The current transaction URL
- `$data` (array): Contextual data:
    ```php
    $data = [
        'transaction' => [
            'id',
            'transaction_id',
            'order_id',
            'payment_method',
            'status',
            'amount',
            'currency',
            'created_at',
            'updated_at',
            'meta',
        ]
    ];
    ```

**Returns:**
- `$url` (string): The modified transaction URL

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
<summary><code>`fluentcart/transaction/receipt_page_url`</code> &mdash; Filter transaction receipt page URL</summary>

**When it runs:**
This filter is applied when generating the URL for the transaction receipt page, allowing you to customize the receipt page URL for a transaction.




**Parameters:**

- `$url` (string): The current receipt page URL
- `$data` (array): Contextual data:
    ```php
    $data = [
        'transaction' => [
            'id',
            'transaction_id',
            'order_id',
            'payment_method',
            'status',
            'amount',
            'currency',
            'created_at',
            'updated_at',
            'meta',
        ],
        'order' => [
            'status',
            'parent_id',
            'invoice_no',
            'receipt_number',
            'fulfillment_type',
            'type',
            'customer_id',
            'payment_method',
            'payment_method_title',
            'payment_status',
            'currency',
            'subtotal',
            'discount_tax',
            'manual_discount_total',
            'coupon_discount_total',
            'shipping_tax',
            'shipping_total',
            'tax_total',
            'tax_behavior',
            'total_amount',
            'rate',
            'note',
            'ip_address',
            'completed_at',
            'refunded_at',
            'total_refund',
            'uuid',
            'created_at',
            'refunded_at',
            'total_paid',
            'mode',
            'shipping_status',
            'config',
        ]
    ];
    ```

**Returns:**
- `$url` (string): The modified receipt page URL

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
<summary><code>`fluent_cart/admin_menu_title`</code> &mdash; Filter admin menu title</summary>

**When it runs:**
This filter is applied when generating the FluentCart admin menu title, allowing you to customize the menu label in the WordPress dashboard.


**Parameters:**

- `$title` (string): The current admin menu title
- `$data` (array): Contextual data. Example structure:
    ```php
    $data = [
        'user' => [
            'ID',
            'user_login',
            'user_pass',
            'user_nicename',
            'user_email',
            'user_url',
            'user_registered',
            'user_activation_key',
            'user_status',
            'display_name',
            'roles',
            'allcaps',
            'filter',
        ],
        'settings' => [
            'currency',
            'tax_enabled',
            'shipping_enabled',
            'store_name',
            'store_email',
            'store_address',
            'meta',
        ]
    ];
    ```

**Returns:**
- `$title` (string): The modified admin menu title

**Usage:**
```php
add_filter('fluent_cart/admin_menu_title', function($title, $data) {
    // Custom admin menu title
    return 'My Custom Store';
}, 10, 2);
```
</details>


<details>
<summary><code>`fluent_cart/admin_base_url`</code> &mdash; Filter admin base URL</summary>

**When it runs:**
This filter is applied when generating the base URL for FluentCart admin pages, allowing you to customize the admin URL structure.


**Parameters:**

- `$url` (string): The current admin base URL. Default: Result of `admin_url('admin.php?page=fluent-cart#/')`
- `$data` (array): Empty array for future extensibility. Currently unused.

**Returns:**
- `$url` (string): The modified admin base URL

**Usage:**
```php
add_filter('fluent_cart/admin_base_url', function($url, $data) {
    // Customize the admin base URL
    return admin_url('admin.php?page=my-custom-fluent-cart#/');
}, 10, 2);
```
            'allcaps',
            'filter',
        ],
        'settings' => [
            'currency',
            'tax_enabled',
            'shipping_enabled',
            'store_name',
            'store_email',
            'store_address',
            'meta',
        ]
    ];
    ```

**Returns:**
- `$url` (string): The modified admin base URL

**Usage:**
```php
add_filter('fluent_cart/admin_base_url', function($url, $data) {
    // Custom admin base URL
    return admin_url('admin.php?page=my-custom-store#/');
}, 10, 2);
```
</details>


<details>
<summary><code>`fluent_cart/admin_filter_options`</code> &mdash; Filter admin filter options</summary>

**When it runs:**
This filter is applied when generating the available filter options in the FluentCart admin interface, allowing you to add, remove, or modify filter options.


**Parameters:**

- `$options` (array): The current filter options
    ```php
    $options = [
        'order_filter_options' => [
            'advance' => [
                'id' => [
                    'column' => 'id',
                    'description' => 'Order Id',
                    'type' => 'numeric',
                    'examples' => ['id = 1', 'id > 5', 'id :: 1-10']
                ],
                'status' => [
                    'column' => 'status',
                    'description' => 'Search by order status',
                    'type' => 'string',
                    'examples' => ['status = completed']
                ],
                'invoice' => [
                    'column' => 'status',
                    'description' => 'Invoice Number',
                    'type' => 'string'
                ],
                'payment' => [
                    'column' => 'payment_status',
                    'description' => 'Search by payment status',
                    'type' => 'string',
                    'examples' => ['payment = paid', 'payment = partially_paid']
                ],
                'payment_by' => [
                    'column' => 'payment_method',
                    'description' => 'Search by payment method',
                    'type' => 'string',
                    'examples' => ['payment_by = stripe', 'payment_by = paypal']
                ]
            ],
            'guide' => [] // Searchable fields guide
        ],
        'customer_filter_options' => [
            'advance' => [], // Customer-specific filter options
            'guide' => []
        ],
        'product_filter_options' => [
            'advance' => [], // Product-specific filter options
            'guide' => []
        ],
        'license_filter_options' => [
            'advance' => [], // License-specific filter options
            'guide' => []
        ],
        'tax_filter_options' => [
            'advance' => [], // Tax-specific filter options
            'guide' => []
        ]
    ];
    ```
- `$data` (array): Empty array for future extensibility. Currently unused.

**Returns:**
- `$options` (array): The modified filter options array

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
<summary><code>`fluent_cart/item_max_quantity`</code> &mdash; Filter maximum item quantity</summary>

**When it runs:**
This filter is applied when determining the maximum quantity allowed for a cart item, allowing you to set custom quantity limits per product or variation.



**Parameters:**

- `$quantity` (int): The current maximum quantity allowed
- `$data` (array): Contextual data
    ```php
    $data = [
        'variation' => [
            'id',
            'sku',
            'price',
            'stock',
            'attributes',
            'image',
            'meta',
        ],
        'product' => [
            'id',
            'name',
            'sku',
            'price',
            'stock',
            'type',
            'categories',
            'image',
            'meta',
        ]
    ];
    ```

**Returns:**
- `$quantity` (int): The modified maximum quantity

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
<summary><code>`fluent_cart/cart_item_product_variation`</code> &mdash; Filter cart item product variation</summary>

**When it runs:**
This filter is applied when retrieving or updating the product variation for a cart item, allowing you to modify the variation object before it is used in the cart.


**Parameters:**

- `$variation` (object): The current product variation object
- `$itemId` (int): The cart item ID
- `$incrementBy` (int): The quantity increment value
- `$existingItems` (array): The current cart items array

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


<details>
<summary><code>`fluent_cart/checkout_validation_rules`</code> &mdash; Filter checkout validation rules</summary>

**When it runs:**
This filter is applied when building the validation rules for the checkout form, allowing you to add, remove, or modify validation requirements for checkout fields.

**Parameters:**

- `$rules` (array): The current validation rules array. Example:
    ```php
    $rules = [
        'field_name' => 'required|string',
        'custom_field' => 'required|string|max:255',
        // ...
    ];
    ```
- `$data` (array): Contextual data for the checkout (may include cart, user, etc.)

**Returns:**
- `$rules` (array): The modified validation rules array

**Usage:**
```php
add_filter('fluent_cart/checkout_validation_rules', function($rules, $data) {
    // Add custom validation rules
    $rules['custom_field'] = 'required|string|max:255';
    return $rules;
}, 10, 2);
```
</details>


<details>
<summary><code>`fluent_cart/checkout_address_fields`</code> &mdash; Filter checkout address fields</summary>

**When it runs:**
This filter is applied when building the address fields for the checkout form, allowing you to add, remove, or modify address fields.


**Parameters:**

- `$fields` (array): The current address fields array
    ```php
    $fields = [
        'custom_field' => [
            'label'    => 'Custom Field',
            'type'     => 'text',
            'required' => false
        ]
    ];
    ```
- `$data` (array): Contextual data for the checkout (may include cart, user, etc.)

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
<summary><code>`fluent_cart/checkout_billing_fields`</code> &mdash; Filter checkout billing fields</summary>

**When it runs:**
This filter is applied when building the billing fields for the checkout form, allowing you to add, remove, or modify billing fields.


**Parameters:**

- `$fields` (array): The current billing fields array
    ```php
    $fields = [
        'company_name' => [
            'label'    => 'Company Name',
            'type'     => 'text',
            'required' => false
        ]
    ];
    ```
- `$data` (array): Contextual data for the checkout (may include cart, user, etc.)

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
<summary><code>`fluent_cart/checkout_shipping_fields`</code> &mdash; Filter checkout shipping fields</summary>

**When it runs:**
This filter is applied when building the shipping fields for the checkout form, allowing you to add, remove, or modify shipping fields.


**Parameters:**

- `$fields` (array): The current shipping fields array
    ```php
    $fields = [
        'delivery_instructions' => [
            'label'    => 'Delivery Instructions',
            'type'     => 'textarea',
            'required' => false
        ]
    ];
    ```
- `$data` (array): Contextual data for the checkout (may include cart, user, etc.)

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
<summary><code>`fluent-cart/order_statuses`</code> &mdash; Filter available order statuses</summary>

**When it runs:**
This filter is applied when retrieving the list of available order statuses, allowing you to add, remove, or modify order statuses.


**Parameters:**

- `$statuses` (array): The current order statuses array. Example structure:
    ```php
    $statuses = [
        'processing' => 'Processing',
        'completed'  => 'Completed',
        'on-hold'    => 'On Hold',
        'canceled'   => 'Canceled',
        'failed'     => 'Failed',
    ];
    ```

**Returns:**
- `$statuses` (array): The modified order statuses array

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
<summary><code>`fluent-cart/editable_order_statuses`</code> &mdash; Filter editable order statuses</summary>

**When it runs:**
This filter is applied when retrieving the list of order statuses that can be edited, allowing you to control which statuses are editable in the admin UI.


**Parameters:**

- `$statuses` (array): The current editable order statuses array. Example structure:
    ```php
    $statuses = [
        'on-hold'    => 'On Hold',
        'processing' => 'Processing',
        'completed'  => 'Completed',
        'canceled'   => 'Canceled',
    ];
    ```

**Returns:**
- `$statuses` (array): The modified editable order statuses array

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
<summary><code>`fluent-cart/editable_customer_statuses`</code> &mdash; Filter editable customer statuses</summary>

**When it runs:**
This filter is applied when retrieving the list of customer statuses that can be edited, allowing you to control which statuses are editable in the admin UI.


**Parameters:**

- `$statuses` (array): The current editable customer statuses array. Example structure:
    ```php
    $statuses = [
        'active'   => 'Active',
        'inactive' => 'Inactive',
    ];
    ```

**Returns:**
- `$statuses` (array): The modified editable customer statuses array

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
<summary><code>`fluent-cart/shipping_statuses`</code> &mdash; Filter available shipping statuses</summary>

**When it runs:**
This filter is applied when retrieving the list of available shipping statuses, allowing you to add, remove, or modify shipping statuses.


**Parameters:**

- `$statuses` (array): The current shipping statuses array. Example structure:
    ```php
    $statuses = [
        'unshipped'   => 'Unhipped',
        'shipped'     => 'Shipped',
        'delivered'   => 'Delivered',
        'unshippable' => 'Unshippable',
    ];
    ```

**Returns:**
- `$statuses` (array): The modified shipping statuses array

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
<summary><code>`fluent-cart/transaction_statuses`</code> &mdash; Filter available transaction statuses</summary>

**When it runs:**
This filter is applied when retrieving the list of available transaction statuses, allowing you to add, remove, or modify transaction statuses.


**Parameters:**

- `$statuses` (array): The current transaction statuses array. Example structure:
    ```php
    $statuses = [
        'pending'         => 'Pending',
        'paid'            => 'Paid',
        'require_capture' => 'Authorized (Require Capture)',
        'failed'          => 'Failed',
        'refunded'        => 'Refunded',
        'active'          => 'Active',
    ];
    ```

**Returns:**
- `$statuses` (array): The modified transaction statuses array

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
<summary><code>`fluent-cart/editable_transaction_statuses`</code> &mdash; Filter editable transaction statuses</summary>

**When it runs:**
This filter is applied when retrieving the list of transaction statuses that can be edited, allowing you to control which statuses are editable in the admin UI.


**Parameters:**

- `$statuses` (array): The current editable transaction statuses array. Example structure:
    ```php
    $statuses = [
        'pending'   => 'Pending',
        'succeeded' => 'Succeeded',
        'failed'    => 'Failed',
        'refunded'  => 'Refunded',
    ];
    ```

**Returns:**
- `$statuses` (array): The modified editable transaction statuses array

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
<summary><code>`fluent-cart/coupon_statuses`</code> &mdash; Filter available coupon statuses</summary>

**When it runs:**
This filter is applied when retrieving the list of available coupon statuses, allowing you to add, remove, or modify coupon statuses.


**Parameters:**

- `$statuses` (array): The current coupon statuses array. Example structure:
    ```php
    $statuses = [
        'active'   => 'Active',
        'expired'  => 'Expired',
        'disabled' => 'Disabled',
    ];
    ```

**Returns:**
- `$statuses` (array): The modified coupon statuses array

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
<summary><code>`fluent-cart/available_currencies`</code> &mdash; Filter available currencies</summary>

**When it runs:**
This filter is applied when retrieving the list of available currencies, allowing you to add, remove, or modify currencies.


**Parameters:**

- `$currencies` (array): The current available currencies array. Example structure:
    ```php
    $currencies = [
        'BDT' => [
            'label'  => 'Bangladeshi Taka',
            'value'  => 'BDT',
            'symbol' => '৳',
        ],
        'USD' => [
            'label'  => 'United State Dollar',
            'value'  => 'USD',
            'symbol' => '$',
        ],
        'GBP' => [
            'label'  => 'United Kingdom',
            'value'  => 'GBP',
            'symbol' => '£',
        ],
    ];
    ```

**Returns:**
- `$currencies` (array): The modified available currencies array

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
<summary><code>`fluent-cart/util/countries`</code> &mdash; Filter available countries</summary>

**When it runs:**
This filter is applied when retrieving the list of available countries, allowing you to add, remove, or modify countries.


**Parameters:**

- `$countries` (array): The current available countries array. Example structure:
    ```php
    $countries = [
        'AF' => 'Afghanistan',
        'AX' => 'Åland Islands',
        'AL' => 'Albania',
        'DZ' => 'Algeria',
        // ...
    ];
    ```

**Returns:**
- `$countries` (array): The modified available countries array

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
<summary><code>`fluent-cart/site_prefix`</code> &mdash; Filter site prefix</summary>

**When it runs:**
This filter is applied when retrieving the site prefix used for FluentCart data, allowing you to customize the prefix for multi-site or branding purposes.


**Parameters:**

- `$prefix` (string): The current site prefix

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
<summary><code>`fluent_cart/download_expiration_minutes`</code> &mdash; Filter download expiration minutes</summary>

**When it runs:**
This filter is applied when determining the expiration time (in minutes) for downloadable files, allowing you to set custom expiration times based on file type or other logic.


**Parameters:**

- `$minutes` (int): The current expiration time in minutes
- `$data` (array): Contextual data
    ```php
    $data = [
        'file' => [
            'type' => 'premium',
            'name' => 'file.pdf',
            // ...
        ]
    ];
    ```

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

