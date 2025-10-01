---
title: Developer Hooks
description: FluentCart developer hooks documentation including action hooks, filter hooks, and event system.
---

# FluentCart Developer Hooks

FluentCart provides a comprehensive hook system that allows developers to extend and customize the plugin's functionality. The hook system is built on WordPress's native action and filter system with FluentCart-specific prefixes.

## Hook System Overview

FluentCart uses WordPress's native hook system with custom prefixes to ensure uniqueness and avoid conflicts with other plugins. All FluentCart hooks are prefixed with `fluent_cart/` to maintain namespace separation.

### Hook Types

FluentCart provides three main types of hooks:

1. **Action Hooks** - Execute code at specific points in the plugin lifecycle
2. **Filter Hooks** - Modify data before it's used or displayed
3. **Event System** - Custom event dispatching for complex workflows

## Hook Naming Convention

All FluentCart hooks follow a consistent naming pattern:

```
fluent_cart/{category}/{specific_action}
```

### Examples:
- `fluent_cart/payment_success` - Payment completed successfully
- `fluent_cart/subscription/data_updated` - Subscription data was updated
- `fluent_cart/cart/line_item/before_total` - Before displaying cart item total
- `fluent_cart/email_notifications` - Modify email notification settings

## Hook Categories

### 1. Order Lifecycle Hooks
Hooks related to order processing and management:
- Order creation and updates
- Order status changes
- Order completion and fulfillment

### 2. Payment Hooks
Hooks for payment processing:
- Payment success/failure
- Payment method selection
- Payment gateway integration

### 3. Subscription Hooks
Hooks for subscription management:
- Subscription creation and updates
- Subscription status changes
- Subscription renewals and cancellations

### 4. Cart Hooks
Hooks for shopping cart operations:
- Item addition/removal
- Cart updates and modifications
- Cart line item rendering

### 5. Product Hooks
Hooks for product management:
- Product creation and updates
- Product display and rendering
- Product variation handling

### 6. Admin Hooks
Hooks for admin interface:
- Admin app loading
- Admin menu customization
- Admin JavaScript loading

### 7. View/Template Hooks
Hooks for frontend rendering:
- Single product page rendering
- Checkout page rendering
- Shop app rendering

## Action Hooks

Action hooks allow you to execute custom code at specific points in FluentCart's execution flow. These hooks are perfect for:

- **Triggering side effects** - Send notifications, log events, update external systems
- **Custom business logic** - Implement custom workflows and processes
- **Integration points** - Connect with third-party services and APIs
- **Event handling** - Respond to order, payment, and customer events

### Key Action Hook Categories

- **Order Lifecycle** - `fluent_cart/order/invoice_number_added`
- **Payment Processing** - `fluent_cart/payment_success`, `fluent_cart/payment_failed`, `fluent_cart/payments/after_payment_{status}`
- **Subscription Management** - `fluent_cart/subscription/data_updated`, `fluent_cart/payments/subscription_status_changed`
- **Cart Operations** - `fluent_cart/cart/item_added`, `fluent_cart/cart/item_removed`
- **Product Operations** - `fluent_cart/product_updated`
- **Module Management** - `fluent_cart/module/activated/{module_key}`, `fluent_cart/module/deactivated/{module_key}`
- **Admin Interface** - `fluent_cart/loading_app`, `fluent_cart/admin_js_loaded`
- **View/Template** - `fluent_cart/views/single_product_page`, `fluent_cart/views/checkout_page`

[View Complete Action Hooks Reference →](./actions)

## Filter Hooks

Filter hooks allow you to modify data, settings, and behavior in FluentCart. These hooks are perfect for:

- **Data modification** - Change values before they're used or displayed
- **Customization** - Modify default behavior and settings
- **Integration** - Adapt data for third-party services
- **Localization** - Customize text and formatting

### Key Filter Hook Categories

- **Email & Notifications** - `fluent_cart/email_notifications`
- **Payment Methods** - `fluent_cart_form_disable_stripe_connect`, `fluent_cart/paypal_plan_id`
- **Subscription System** - `fluent_cart/subscription/url_{payment_method}`, `fluent_cart/subscription/can_reactivate`
- **Order System** - `fluent_cart/create_receipt_number_on_order_create`, `fluent_cart/single_order_downloads`
- **Transaction System** - `fluent_cart/transaction/url_{payment_method}`, `fluentcart/transaction/receipt_page_url`
- **Admin Interface** - `fluent_cart/admin_menu_title`, `fluent_cart/admin_base_url`
- **Cart System** - `fluent_cart/item_max_quantity`, `fluent_cart/cart_item_product_variation`
- **Checkout System** - `fluent_cart/checkout_validation_rules`, `fluent_cart/checkout_address_fields`
- **Status Filters** - `fluent-cart/order_statuses`, `fluent-cart/editable_order_statuses`
- **Currency & Localization** - `fluent-cart/available_currencies`, `fluent-cart/util/countries`

[View Complete Filter Hooks Reference →](./filters)

## Event System

FluentCart includes a custom event system built on top of WordPress hooks. The event system provides:

- **Structured event dispatching** - Organized event handling with proper data structures
- **Event listeners** - Automatic event handling through listener classes
- **Activity tracking** - Built-in activity logging for events
- **Hook integration** - Events automatically fire WordPress hooks

### Key Event Classes

- **Order Events** - `OrderCreated`, `OrderStatusUpdated`, `OrderPaid`, `OrderCanceled`, `OrderRefund`
- **Subscription Events** - `SubscriptionActivated`, `SubscriptionRenewed`, `SubscriptionCanceled`
- **User Events** - `UserCreated`
- **Stock Events** - `StockChanged`
- **Plan Events** - `PlanChanged`

### Event System Features

- **EventDispatcher Base Class** - All events extend this base class
- **Automatic Activity Logging** - Events can automatically create activity logs
- **Listener System** - Events can have multiple listeners
- **Hook Integration** - Events automatically fire corresponding WordPress hooks

[View Complete Event System Reference →](./events)

## Hook Usage Examples

### Basic Action Hook Usage

```php
// Listen for payment success
add_action('fluent_cart/payment_success', function($data) {
    $order = $data['order'];
    $transaction = $data['transaction'];
    
    // Send confirmation email
    wp_mail(
        $order->customer->email,
        'Payment Confirmed',
        'Your payment has been processed successfully'
    );
}, 10, 1);
```

### Basic Filter Hook Usage

```php
// Modify email notification settings
add_filter('fluent_cart/email_notifications', function($settings) {
    // Add custom email setting
    $settings['custom_notification'] = true;
    
    return $settings;
}, 10, 1);
```

### Event System Usage

```php
// Listen for order created event
add_action('fluent_cart/order_created', function($data) {
    $order = $data['order'];
    $customer = $data['customer'];
    
    // Custom order processing
    process_custom_order($order, $customer);
}, 10, 1);
```

## Best Practices

### 1. Hook Priority
Use appropriate priority values to ensure hooks execute in the correct order:

```php
// High priority for critical operations
add_action('fluent_cart/payment_success', 'my_critical_function', 5, 1);

// Low priority for cleanup operations
add_action('fluent_cart/payment_success', 'my_cleanup_function', 100, 1);
```

### 2. Parameter Validation
Always validate hook parameters:

```php
add_action('fluent_cart/payment_success', function($data) {
    if (!isset($data['order']) || !isset($data['transaction'])) {
        return; // Invalid data, exit early
    }
    
    $order = $data['order'];
    $transaction = $data['transaction'];
    
    // Process payment success
}, 10, 1);
```

### 3. Error Handling
Implement proper error handling in hooks:

```php
add_action('fluent_cart/payment_success', function($data) {
    try {
        // Process payment success
        process_payment_success($data);
    } catch (Exception $e) {
        // Log error but don't break the flow
        error_log('Payment success hook error: ' . $e->getMessage());
    }
}, 10, 1);
```

### 4. Performance Considerations
Keep hook functions lightweight and efficient:

```php
add_action('fluent_cart/payment_success', function($data) {
    // Use background processing for heavy operations
    wp_schedule_single_event(time(), 'my_background_processing', [$data]);
}, 10, 1);
```

## Hook Development Tips

### 1. Use Descriptive Names
Choose clear, descriptive hook names:

```php
// Good
add_action('fluent_cart/payment_success', 'handle_payment_success');

// Avoid
add_action('fluent_cart/ps', 'hps');
```

### 2. Document Your Hooks
Always document custom hooks:

```php
/**
 * Custom hook for payment processing
 * 
 * @param array $data Payment data
 * @param object $order Order object
 * @param object $transaction Transaction object
 */
add_action('fluent_cart/payment_success', 'my_custom_payment_handler', 10, 1);
```

### 3. Test Hook Functionality
Always test hooks in a development environment:

```php
// Add debugging to hooks during development
add_action('fluent_cart/payment_success', function($data) {
    if (WP_DEBUG) {
        error_log('Payment success hook called with data: ' . print_r($data, true));
    }
    
    // Process payment success
}, 10, 1);
```

## Related Documentation

- [Database Models](/database/models) - Models used in hook data
- [REST API](/api/) - API endpoints that trigger hooks
- [Module System](/modules/) - Modules that extend hook functionality
- [Frontend Development](/guides/frontend) - Frontend hook integration

## Next Steps

Continue with hook development:

1. **[Action Hooks](./actions)** - Learn about available action hooks
2. **[Filter Hooks](./filters)** - Learn about available filter hooks
3. **[Event System](./events)** - Learn about the custom event system
4. **[Database Models](/database/models)** - Understand data models used in hooks

## Previous/Next Navigation

- **Previous**: [Database Models](/database/models) - FluentCart data models
- **Next**: [REST API](/api/) - FluentCart REST API

---

