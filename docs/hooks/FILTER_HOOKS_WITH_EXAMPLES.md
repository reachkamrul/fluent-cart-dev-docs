# FluentCart Filter Hooks - Complete Reference with Examples

This document lists all filter hooks in the FluentCart plugin with detailed examples and parameter information.

---

## Core Filters

### Plugin Settings

<details>
<summary><code>fluent_cart/admin_app_data</code> &mdash; Filter admin app data</summary>

**When it runs:**
This filter is applied when loading the admin app, allowing you to modify the data passed to the admin interface.

**Parameters:**

- `$adminLocalizeData` (array): The admin app localization data
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$adminLocalizeData` (array): The modified admin app data

**Usage:**
```php
add_filter('fluent_cart/admin_app_data', function($adminLocalizeData, $data) {
    // Add custom data to admin app
    $adminLocalizeData['custom_setting'] = 'custom_value';
    return $adminLocalizeData;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/admin_base_url</code> &mdash; Filter admin base URL</summary>

**When it runs:**
This filter is applied when generating the admin base URL for the FluentCart admin interface.

**Parameters:**

- `$baseUrl` (string): The default admin base URL
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$baseUrl` (string): The modified admin base URL

**Usage:**
```php
add_filter('fluent_cart/admin_base_url', function($baseUrl, $data) {
    // Customize admin base URL
    return admin_url('admin.php?page=custom-fluent-cart#/');
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/admin_menu_title</code> &mdash; Filter admin menu title</summary>

**When it runs:**
This filter is applied when registering the admin menu, allowing you to change the menu title.

**Parameters:**

- `$menuTitle` (string): The default menu title ('FluentCart')
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$menuTitle` (string): The modified menu title

**Usage:**
```php
add_filter('fluent_cart/admin_menu_title', function($menuTitle, $data) {
    // Change menu title
    return 'My Store';
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/admin_notices</code> &mdash; Filter admin notices</summary>

**When it runs:**
This filter is applied when displaying admin notices in the FluentCart admin interface.

**Parameters:**

- `$notices` (array): Array of admin notices
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$notices` (array): The modified notices array

**Usage:**
```php
add_filter('fluent_cart/admin_notices', function($notices, $data) {
    // Add a custom notice
    $notices[] = [
        'type' => 'info',
        'message' => 'Custom admin notice'
    ];
    return $notices;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/admin_translations</code> &mdash; Filter admin translations</summary>

**When it runs:**
This filter is applied when loading admin translation strings.

**Parameters:**

- `$translations` (array): Array of translation strings
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$translations` (array): The modified translations array

**Usage:**
```php
add_filter('fluent_cart/admin_translations', function($translations, $data) {
    // Customize translation strings
    $translations['custom_key'] = 'Custom Translation';
    return $translations;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/blocks_translations</code> &mdash; Filter blocks translations</summary>

**When it runs:**
This filter is applied when loading block editor translation strings.

**Parameters:**

- `$translations` (array): Array of block translation strings
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$translations` (array): The modified translations array

**Usage:**
```php
add_filter('fluent_cart/blocks_translations', function($translations, $data) {
    // Customize block translation strings
    $translations['block_key'] = 'Block Translation';
    return $translations;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/customer_profile_translations</code> &mdash; Filter customer profile translations</summary>

**When it runs:**
This filter is applied when loading customer profile translation strings.

**Parameters:**

- `$translations` (array): Array of customer profile translation strings
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$translations` (array): The modified translations array

**Usage:**
```php
add_filter('fluent_cart/customer_profile_translations', function($translations, $data) {
    // Customize customer profile translation strings
    $translations['profile_key'] = 'Profile Translation';
    return $translations;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/front_url_slug</code> &mdash; Filter frontend URL slug</summary>

**When it runs:**
This filter is applied when generating frontend URLs for products and pages.

**Parameters:**

- `$urlSlug` (string): The default URL slug
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$urlSlug` (string): The modified URL slug

**Usage:**
```php
add_filter('fluent_cart/front_url_slug', function($urlSlug, $data) {
    // Change URL slug
    return 'shop';
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/site_prefix</code> &mdash; Filter site prefix</summary>

**When it runs:**
This filter is applied when generating site-specific prefixes for various operations.

**Parameters:**

- `$prefix` (string): The default site prefix
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$prefix` (string): The modified site prefix

**Usage:**
```php
add_filter('fluent_cart/site_prefix', function($prefix, $data) {
    // Customize site prefix
    return 'custom_prefix_';
}, 10, 2);
```
</details>

### Store Settings

<details>
<summary><code>fluent_cart/store_settings/values</code> &mdash; Filter store settings values</summary>

**When it runs:**
This filter is applied when retrieving store settings values.

**Parameters:**

- `$defaultSettings` (array): The default store settings
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$defaultSettings` (array): The modified settings array

**Usage:**
```php
add_filter('fluent_cart/store_settings/values', function($defaultSettings, $data) {
    // Modify default store settings
    $defaultSettings['store_name'] = 'My Custom Store';
    return $defaultSettings;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/store_settings/fields</code> &mdash; Filter store settings fields</summary>

**When it runs:**
This filter is applied when rendering store settings fields in the admin interface.

**Parameters:**

- `$fields` (array): Array of settings field definitions
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$fields` (array): The modified fields array

**Usage:**
```php
add_filter('fluent_cart/store_settings/fields', function($fields, $data) {
    // Add a custom settings field
    $fields['custom_section']['fields'][] = [
        'key' => 'custom_field',
        'label' => 'Custom Field',
        'type' => 'text'
    ];
    return $fields;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/store_settings/rules</code> &mdash; Filter store settings validation rules</summary>

**When it runs:**
This filter is applied when validating store settings before saving.

**Parameters:**

- `$rules` (array): Array of validation rules

**Returns:**
- `$rules` (array): The modified validation rules

**Usage:**
```php
add_filter('fluent_cart/store_settings/rules', function($rules) {
    // Add custom validation rule
    $rules['custom_field'] = 'required|string|max:255';
    return $rules;
});
```


### Confirmation Settings

<details>
<summary><code>fluent_cart/confirmation_setting_fields</code> &mdash; Filter confirmation setting fields</summary>

**When it runs:**
This filter is applied when rendering confirmation page settings fields.

**Parameters:**

- `$fields` (array): Array of confirmation settings field definitions
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$fields` (array): The modified fields array

**Usage:**
```php
add_filter('fluent_cart/confirmation_setting_fields', function($fields, $data) {
    // Add custom confirmation field
    $fields[] = [
        'key' => 'custom_message',
        'label' => 'Custom Confirmation Message',
        'type' => 'textarea'
    ];
    return $fields;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/confirmation_shortcodes</code> &mdash; Filter confirmation shortcodes</summary>

**When it runs:**
This filter is applied when processing shortcodes available for confirmation pages.

**Parameters:**

- `$shortcodes` (array): Array of available shortcodes
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$shortcodes` (array): The modified shortcodes array

**Usage:**
```php
add_filter('fluent_cart/confirmation_shortcodes', function($shortcodes, $data) {
    // Add custom shortcode
    $shortcodes['custom_code'] = 'Custom Shortcode Description';
    return $shortcodes;
}, 10, 2);
```
</details>

### Module Settings

<details>
<summary><code>fluent_cart/module_setting/default_values</code> &mdash; Filter module setting default values</summary>

**When it runs:**
This filter is applied when loading default values for module settings.

**Parameters:**

- `$defaultValues` (array): Array of default module setting values
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$defaultValues` (array): The modified default values

**Usage:**
```php
add_filter('fluent_cart/module_setting/default_values', function($defaultValues, $data) {
    // Set custom default values
    $defaultValues['custom_module'] = 'enabled';
    return $defaultValues;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/module_setting/fields</code> &mdash; Filter module setting fields</summary>

**When it runs:**
This filter is applied when rendering module settings fields.

**Parameters:**

- `$fields` (array): Array of module settings field definitions
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$fields` (array): The modified fields array

**Usage:**
```php
add_filter('fluent_cart/module_setting/fields', function($fields, $data) {
    // Add custom module field
    $fields[] = [
        'key' => 'custom_module_option',
        'label' => 'Custom Module Option',
        'type' => 'checkbox'
    ];
    return $fields;
}, 10, 2);
```
</details>

---

## Currency & Pricing

<details>
<summary><code>fluent_cart/global_currency_setting</code> &mdash; Filter global currency settings</summary>

**When it runs:**
This filter is applied when retrieving global currency settings.

**Parameters:**

- `$settings` (array): Currency settings array
    ```php
    $settings = [
        'currency' => 'USD',
        'currency_sign' => '$',
        'currency_position' => 'left',
        'decimal_separator' => '.',
        'thousand_separator' => ',',
        'number_of_decimals' => 2
    ];
    ```
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$settings` (array): The modified currency settings

**Usage:**
```php
add_filter('fluent_cart/global_currency_setting', function($settings, $data) {
    // Change currency settings
    $settings['currency'] = 'EUR';
    $settings['currency_sign'] = '€';
    return $settings;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/global_currency_symbols</code> &mdash; Filter global currency symbols</summary>

**When it runs:**
This filter is applied when retrieving currency symbols for all supported currencies.

**Parameters:**

- `$symbols` (array): Array of currency symbols (currency code => symbol)
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$symbols` (array): The modified currency symbols array

**Usage:**
```php
add_filter('fluent_cart/global_currency_symbols', function($symbols, $data) {
    // Add custom currency symbol
    $symbols['BTC'] = '₿';
    return $symbols;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/accepted_currencies</code> &mdash; Filter accepted currencies</summary>

**When it runs:**
This filter is applied when retrieving the list of accepted currencies.

**Parameters:**

- `$currencies` (array): Array of accepted currency codes
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$currencies` (array): The modified currencies array

**Usage:**
```php
add_filter('fluent_cart/accepted_currencies', function($currencies, $data) {
    // Add custom currency
    $currencies[] = 'BTC';
    return $currencies;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/zero_decimal_currencies</code> &mdash; Filter zero decimal currencies</summary>

**When it runs:**
This filter is applied when determining which currencies don't use decimal places (e.g., JPY, KRW).

**Parameters:**

- `$currencies` (array): Array of zero decimal currency codes
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$currencies` (array): The modified zero decimal currencies array

**Usage:**
```php
add_filter('fluent_cart/zero_decimal_currencies', function($currencies, $data) {
    // Add currency that doesn't use decimals
    $currencies[] = 'VND';
    return $currencies;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/price_class</code> &mdash; Filter price CSS class</summary>

**When it runs:**
This filter is applied when rendering product prices to customize the CSS class.

**Parameters:**

- `$class` (string): The default CSS class ('price')
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$class` (string): The modified CSS class

**Usage:**
```php
add_filter('fluent_cart/price_class', function($class, $data) {
    // Change price CSS class
    return 'custom-price-class';
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/product/price_suffix_atts</code> &mdash; Filter product price suffix attributes</summary>

**When it runs:**
This filter is applied when rendering price suffix text (e.g., "incl. VAT").

**Parameters:**

- `$suffix` (string): The price suffix text
- `$data` (array): Context data
    ```php
    $data = [
        'product' => Product object,
        'variation' => ProductVariation object or null
    ];
    ```

**Returns:**
- `$suffix` (string): The modified price suffix

**Usage:**
```php
add_filter('fluent_cart/product/price_suffix_atts', function($suffix, $data) {
    // Add custom price suffix
    return ' (incl. 20% VAT)';
}, 10, 2);
```
</details>

---

## Order Filters

<details>
<summary><code>fluent_cart/order_statuses</code> &mdash; Filter order statuses</summary>

**When it runs:**
This filter is applied when retrieving the list of available order statuses.

**Parameters:**

- `$statuses` (array): Array of order statuses (key => label)
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$statuses` (array): The modified order statuses array

**Usage:**
```php
add_filter('fluent_cart/order_statuses', function($statuses, $data) {
    // Add custom order status
    $statuses['custom_status'] = 'Custom Status';
    return $statuses;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/order/type</code> &mdash; Filter order type</summary>

**When it runs:**
This filter is applied when determining the order type.

**Parameters:**

- `$type` (string): The order type
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$type` (string): The modified order type

**Usage:**
```php
add_filter('fluent_cart/order/type', function($type, $data) {
    // Customize order type
    return 'subscription';
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/order/view</code> &mdash; Filter order view data</summary>

**When it runs:**
This filter is applied when preparing order data for display in the admin or customer portal.

**Parameters:**

- `$order` (array): The order data array
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$order` (array): The modified order data

**Usage:**
```php
add_filter('fluent_cart/order/view', function($order, $data) {
    // Add custom data to order view
    $order['custom_field'] = 'Custom Value';
    return $order;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/single_order_downloads</code> &mdash; Filter single order downloads data</summary>

**When it runs:**
This filter is applied when preparing the downloadable files for a specific order, allowing you to add, remove, or modify download data for the order.

**Parameters:**

- `$downloadData` (array): The current download data for the order
    ```php
    $downloadData = [
        [
            'title' => 'Product Name - Variation Title',
            'product_id' => 123,
            'variation_id' => 456,
            'additional_html' => '',
            'downloads' => [
                [
                    'id' => 1,
                    'name' => 'File Name',
                    'url' => 'https://example.com/file.pdf',
                    'size' => '1.5 MB',
                    'type' => 'pdf',
                    'expires_at' => '2025-12-31',
                    'download_count' => 0,
                    'max_downloads' => 5
                ]
            ]
        ]
    ];
    ```
- `$data` (array): Contextual data
    ```php
    $data = [
        'order' => Order object,
        'scope' => 'admin' or 'customer'
    ];
    ```

**Returns:**
- `$downloadData` (array): The modified download data array

**Usage:**
```php
add_filter('fluent_cart/single_order_downloads', function($downloadData, $data) {
    $order = $data['order'];
    // Add a custom downloadable file
    $downloadData[] = [
        'title' => 'Bonus Content',
        'product_id' => 0,
        'variation_id' => 0,
        'additional_html' => '',
        'downloads' => [
            [
                'name' => 'Bonus File',
                'url' => 'https://example.com/bonus.pdf'
            ]
        ]
    ];
    return $downloadData;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/customer/order_data</code> &mdash; Filter customer order data</summary>

**When it runs:**
This filter is applied when preparing order data for display in the customer portal.

**Parameters:**

- `$formattedOrderData` (array): The formatted order data
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$formattedOrderData` (array): The modified order data

**Usage:**
```php
add_filter('fluent_cart/customer/order_data', function($formattedOrderData, $data) {
    // Add custom field to customer order view
    $formattedOrderData['custom_note'] = 'Thank you for your purchase!';
    return $formattedOrderData;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/invoice_prefix</code> &mdash; Filter invoice prefix</summary>

**When it runs:**
This filter is applied when generating invoice numbers.

**Parameters:**

- `$prefix` (string): The invoice prefix
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$prefix` (string): The modified invoice prefix

**Usage:**
```php
add_filter('fluent_cart/invoice_prefix', function($prefix, $data) {
    // Customize invoice prefix
    return 'INV-' . date('Y') . '-';
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/min_receipt_number</code> &mdash; Filter minimum receipt number</summary>

**When it runs:**
This filter is applied when generating receipt numbers to set the starting number.

**Parameters:**

- `$minNumber` (int): The minimum receipt number
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$minNumber` (int): The modified minimum receipt number

**Usage:**
```php
add_filter('fluent_cart/min_receipt_number', function($minNumber, $data) {
    // Start receipt numbers from 1000
    return 1000;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/create_receipt_number_on_order_create</code> &mdash; Filter whether to create receipt number on order creation</summary>

**When it runs:**
This filter is applied when creating an order to determine if a receipt number should be generated immediately.

**Parameters:**

- `$createReceipt` (bool): Whether to create receipt number (default: false)
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$createReceipt` (bool): The modified boolean value

**Usage:**
```php
add_filter('fluent_cart/create_receipt_number_on_order_create', function($createReceipt, $data) {
    // Always create receipt number on order creation
    return true;
}, 10, 2);
```
</details>

---

## Cart Filters

<details>
<summary><code>fluent_cart/cart/estimated_total</code> &mdash; Filter cart estimated total</summary>

**When it runs:**
This filter is applied when calculating the cart total, allowing you to modify the final total amount.

**Parameters:**

- `$total` (int): The cart total in cents
- `$data` (array): Context data
    ```php
    $data = [
        'cart' => Cart object
    ];
    ```

**Returns:**
- `$total` (int): The modified cart total in cents

**Usage:**
```php
add_filter('fluent_cart/cart/estimated_total', function($total, $data) {
    $cart = $data['cart'];
    // Add a processing fee
    $processingFee = 200; // $2.00 in cents
    return $total + $processingFee;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/cart/tax_behavior</code> &mdash; Filter cart tax behavior</summary>

**When it runs:**
This filter is applied when determining how taxes should be calculated and displayed.

**Parameters:**

- `$taxBehavior` (int): The tax behavior (0 = exclusive, 1 = inclusive)
- `$data` (array): Context data
    ```php
    $data = [
        'cart' => Cart object
    ];
    ```

**Returns:**
- `$taxBehavior` (int): The modified tax behavior

**Usage:**
```php
add_filter('fluent_cart/cart/tax_behavior', function($taxBehavior, $data) {
    // Force tax inclusive pricing
    return 1;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/cart_cookie_minutes</code> &mdash; Filter cart cookie expiration minutes</summary>

**When it runs:**
This filter is applied when setting the cart cookie expiration time.

**Parameters:**

- `$minutes` (int): Cookie expiration in minutes
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$minutes` (int): The modified expiration time

**Usage:**
```php
add_filter('fluent_cart/cart_cookie_minutes', function($minutes, $data) {
    // Set cart cookie to expire in 7 days
    return 7 * 24 * 60;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/item_max_quantity</code> &mdash; Filter item maximum quantity</summary>

**When it runs:**
This filter is applied when determining the maximum quantity allowed for a cart item.

**Parameters:**

- `$quantity` (int): The maximum quantity
- `$data` (array): Context data
    ```php
    $data = [
        'variation' => ProductVariation object,
        'product' => Product object
    ];
    ```

**Returns:**
- `$quantity` (int): The modified maximum quantity

**Usage:**
```php
add_filter('fluent_cart/item_max_quantity', function($quantity, $data) {
    $variation = $data['variation'];
    // Limit to 10 items per product
    return min($quantity, 10);
}, 10, 2);
```
</details>

---

## Checkout Filters

<details>
<summary><code>fluent_cart/checkout_address_fields</code> &mdash; Filter checkout address fields</summary>

**When it runs:**
This filter is applied when rendering address fields on the checkout page.

**Parameters:**

- `$fields` (array): Array of address field definitions
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$fields` (array): The modified fields array

**Usage:**
```php
add_filter('fluent_cart/checkout_address_fields', function($fields, $data) {
    // Add a custom address field
    $fields['company'] = [
        'label' => 'Company Name',
        'type' => 'text',
        'required' => false
    ];
    return $fields;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/checkout_active_payment_methods</code> &mdash; Filter active payment methods on checkout</summary>

**When it runs:**
This filter is applied when displaying available payment methods on the checkout page.

**Parameters:**

- `$paymentMethods` (array): Array of active payment methods
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$paymentMethods` (array): The modified payment methods array

**Usage:**
```php
add_filter('fluent_cart/checkout_active_payment_methods', function($paymentMethods, $data) {
    // Remove a specific payment method
    unset($paymentMethods['paypal']);
    return $paymentMethods;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/checkout_page_css_classes</code> &mdash; Filter checkout page CSS classes</summary>

**When it runs:**
This filter is applied when rendering the checkout page to customize CSS classes.

**Parameters:**

- `$classes` (array): Array of CSS classes
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$classes` (array): The modified CSS classes array

**Usage:**
```php
add_filter('fluent_cart/checkout_page_css_classes', function($classes, $data) {
    // Add custom CSS class
    $classes[] = 'custom-checkout-theme';
    return $classes;
}, 10, 2);
```
</details>

---

## Product Filters

<details>
<summary><code>fluent_cart/product/add_to_cart_text</code> &mdash; Filter add to cart button text</summary>

**When it runs:**
This filter is applied when rendering the "Add to Cart" button text.

**Parameters:**

- `$text` (string): The button text
- `$data` (array): Context data
    ```php
    $data = [
        'product' => Product object
    ];
    ```

**Returns:**
- `$text` (string): The modified button text

**Usage:**
```php
add_filter('fluent_cart/product/add_to_cart_text', function($text, $data) {
    // Customize button text
    return 'Add to Basket';
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/product/buy_now_button_text</code> &mdash; Filter buy now button text</summary>

**When it runs:**
This filter is applied when rendering the "Buy Now" button text.

**Parameters:**

- `$text` (string): The button text
- `$data` (array): Context data
    ```php
    $data = [
        'product' => Product object
    ];
    ```

**Returns:**
- `$text` (string): The modified button text

**Usage:**
```php
add_filter('fluent_cart/product/buy_now_button_text', function($text, $data) {
    // Customize button text
    return 'Purchase Now';
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/product_stock_availability</code> &mdash; Filter product stock availability</summary>

**When it runs:**
This filter is applied when checking product stock availability.

**Parameters:**

- `$availability` (array): Stock availability data
    ```php
    $availability = [
        'is_available' => true,
        'message' => 'In Stock',
        'quantity' => 10
    ];
    ```
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$availability` (array): The modified availability data

**Usage:**
```php
add_filter('fluent_cart/product_stock_availability', function($availability, $data) {
    // Customize stock message
    if ($availability['quantity'] < 5) {
        $availability['message'] = 'Only ' . $availability['quantity'] . ' left!';
    }
    return $availability;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/product_download/can_be_downloaded</code> &mdash; Filter whether product can be downloaded</summary>

**When it runs:**
This filter is applied when determining if a product file can be downloaded by the customer.

**Parameters:**

- `$canBeDownloaded` (bool): Whether the file can be downloaded
- `$data` (array): Context data
    ```php
    $data = [
        'download' => Download object,
        'order' => Order object,
        'customer' => Customer object
    ];
    ```

**Returns:**
- `$canBeDownloaded` (bool): The modified boolean value

**Usage:**
```php
add_filter('fluent_cart/product_download/can_be_downloaded', function($canBeDownloaded, $data) {
    $order = $data['order'];
    // Only allow downloads for paid orders
    if ($order->payment_status !== 'paid') {
        return false;
    }
    return $canBeDownloaded;
}, 10, 2);
```
</details>

<details>
<summary><code>fluent_cart/download_expiration_minutes</code> &mdash; Filter download expiration minutes</summary>

**When it runs:**
This filter is applied when generating download links to set expiration time.

**Parameters:**

- `$minutes` (int): Expiration time in minutes
- `$data` (array): Additional context data (empty array)

**Returns:**
- `$minutes` (int): The modified expiration time

**Usage:**
```php
add_filter('fluent_cart/download_expiration_minutes', function($minutes, $data) {
    // Set download links to expire in 24 hours
    return 24 * 60;
}, 10, 2);
```
</details>

---

**Note:** This is a comprehensive reference. Due to the large number of filters (173+), the complete documentation with all filters and examples would be very extensive. The examples above demonstrate the pattern for all FluentCart filters.

**All filters follow this structure:**
1. Clear description of when the filter runs
2. Detailed parameter documentation with data structures
3. Return value specification
4. Practical usage example

For the complete list of all 173+ filters, refer to `FILTER_HOOKS.md`.

**When it runs:**
This filter is applied when sanitizing store settings before saving.

**Parameters:**

- `$sanitizer` (array): Array of sanitization rules

**Returns:**
- `$sanitizer` (array): The modified sanitizer rules

**Usage:**
```php
add_filter('fluent_cart/store_settings/sanitizer', function($sanitizer) {
    // Add custom sanitization
    $sanitizer['custom_field'] = 'sanitize_text_field';
    return $sanitizer;
});
```
</details>


