---
title: Action Hooks
description: FluentCart action hooks documentation with complete reference and usage examples.
---

# FluentCart Action Hooks

Action hooks allow you to execute custom code at specific points in FluentCart's execution flow. They are perfect for triggering side effects, sending notifications, logging events, or performing custom business logic.


## Core Action Hooks

### Order Lifecycle Hooks


<details>
<summary><strong>fluent_cart/order_fully_refunded</strong></summary>

This action runs when an order is fully refunded.

**Parameters**

- <code>$data</code> (array): Order and refund information

**Usage:**

```php
add_action('fluent_cart/order_fully_refunded', function($data) {
    // Do whatever you want with here
}, 10, 1);
```
</details>


<details>
<summary><strong>fluent_cart/order_partially_refunded</strong></summary>

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
<summary><strong>fluent_cart/order_paid</strong></summary>

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
<summary><strong>fluent_cart/order_refunded</strong></summary>

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
<summary><strong>fluent_cart/order/upgraded</strong></summary>

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
<summary><strong>fluent_cart/cart_completed</strong></summary>

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
<summary><strong>fluent_cart/payment_success</strong></summary>

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
<summary><strong>fluent_cart/payment_failed</strong></summary>

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
<summary><strong>fluent_cart/payments/after_payment_{status}</strong></summary>

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
<summary><strong>fluent_cart/payment_{status}</strong></summary>

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
<summary><strong>fluent_cart/payment_{type}_{status}</strong></summary>

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
<summary><strong>fluent_cart/subscription/data_updated</strong></summary>

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
<summary><strong>fluent_cart/payments/subscription_status_changed</strong></summary>

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
<summary><strong>fluent_cart/payments/subscription_{status}</strong></summary>

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
<summary><strong>fluent_cart/cart/line_item/line_meta</strong></summary>

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
<summary><strong>fluent_cart/cart/line_item/before_total</strong></summary>

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
<summary><strong>fluent_cart/cart/line_item/after_total</strong></summary>

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
<summary><strong>fluent_cart/cart/line_item/before_main_title</strong></summary>

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
<summary><strong>fluent_cart/cart/line_item/after_main_title</strong></summary>

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
<summary><strong>fluent_cart/product/render_product_header</strong></summary>

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
<summary><strong>fluent_cart/register_payment_methods</strong></summary>

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
<summary><strong>fluent_cart/loading_app</strong></summary>

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
<summary><strong>fluent_cart/admin_js_loaded</strong></summary>

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
<summary><strong>fluent_cart/views/checkout_order_summary</strong></summary>

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
<summary><strong>fluent_cart/views/checkout_order_receipt</strong></summary>

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
<summary><strong>fluent_cart/views/order_downloads</strong></summary>

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
<summary><strong>fluent_cart/views/order_licenses</strong></summary>

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
<summary><strong>fluent_cart/views/order_subscriptions</strong></summary>

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
<summary><strong>fluent_cart/views/cart_list</strong></summary>

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
<summary><strong>fluent_cart/views/cart_empty_content</strong></summary>

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
<summary><strong>fluent_cart/views/checkout_order_confirmation_page</strong></summary>

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
<summary><strong>fluent_cart/views/checkout_order_confirmation_page_error</strong></summary>

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
<summary><strong>fluent_cart/init</strong></summary>

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
<summary><strong>fluent_cart/user/after_register</strong></summary>

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
<summary><strong>fluent_cart/user/before_registration</strong></summary>

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
<summary><strong>fluent_cart/views/shop_app_filter_dollar_icon</strong></summary>

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
<summary><strong>fluent_cart/views/shop_app_responsive_filter_wrapper</strong></summary>

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

