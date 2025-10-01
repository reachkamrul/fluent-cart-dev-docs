---
title: Event System
description: FluentCart event system documentation for custom event dispatching and handling.
---

# FluentCart Event System

FluentCart includes a custom event system that allows for more sophisticated event handling beyond WordPress's native action and filter system. This system provides better organization, type safety, and more powerful event dispatching capabilities.

## Event System Overview

The FluentCart event system is built on top of WordPress's hook system but provides additional features:

- **Event Classes** - Structured event objects with typed data
- **Event Listeners** - Dedicated listener classes for handling events
- **Event Dispatching** - Centralized event dispatching with error handling
- **Event Queuing** - Asynchronous event processing capabilities

## Event Classes

### Creating Custom Events

```php
<?php

namespace MyPlugin\Events;

use FluentCart\Framework\Events\Event;

class OrderCreatedEvent extends Event
{
    public $order;
    public $customer;
    public $timestamp;

    public function __construct($order, $customer)
    {
        $this->order = $order;
        $this->customer = $customer;
        $this->timestamp = time();
    }

    public function getEventName()
    {
        return 'order.created';
    }
}
```

### Built-in FluentCart Events

FluentCart provides several built-in event classes:

#### Order Events
- `OrderCreatedEvent` - Fired when a new order is created
- `OrderUpdatedEvent` - Fired when an order is updated
- `OrderStatusChangedEvent` - Fired when order status changes
- `OrderCompletedEvent` - Fired when an order is completed

#### Payment Events
- `PaymentProcessedEvent` - Fired when payment is processed
- `PaymentFailedEvent` - Fired when payment fails
- `PaymentRefundedEvent` - Fired when payment is refunded

#### Subscription Events
- `SubscriptionCreatedEvent` - Fired when subscription is created
- `SubscriptionUpdatedEvent` - Fired when subscription is updated
- `SubscriptionCancelledEvent` - Fired when subscription is cancelled

## Event Listeners

### Creating Event Listeners

```php
<?php

namespace MyPlugin\Listeners;

use FluentCart\Framework\Events\Listener;
use MyPlugin\Events\OrderCreatedEvent;

class OrderCreatedListener extends Listener
{
    public function handle(OrderCreatedEvent $event)
    {
        $order = $event->order;
        $customer = $event->customer;

        // Send order confirmation email
        $this->sendOrderConfirmation($order, $customer);

        // Update inventory
        $this->updateInventory($order);

        // Notify fulfillment team
        $this->notifyFulfillmentTeam($order);
    }

    private function sendOrderConfirmation($order, $customer)
    {
        // Email logic here
        wp_mail(
            $customer->email,
            'Order Confirmation',
            "Your order #{$order->id} has been created successfully."
        );
    }

    private function updateInventory($order)
    {
        foreach ($order->items as $item) {
            // Update inventory logic
            update_product_stock($item->product_id, -$item->quantity);
        }
    }

    private function notifyFulfillmentTeam($order)
    {
        // Notification logic here
        wp_mail(
            'fulfillment@example.com',
            'New Order for Fulfillment',
            "Order #{$order->id} is ready for fulfillment."
        );
    }
}
```

### Registering Event Listeners

```php
<?php

// In your plugin's main file or service provider
use FluentCart\App\App;
use MyPlugin\Events\OrderCreatedEvent;
use MyPlugin\Listeners\OrderCreatedListener;

$app = App::getInstance();

// Register event listener
$app->addEventListener(OrderCreatedEvent::class, OrderCreatedListener::class);

// Or register multiple listeners for the same event
$app->addEventListener(OrderCreatedEvent::class, [
    OrderCreatedListener::class,
    InventoryUpdateListener::class,
    NotificationListener::class
]);
```

## Event Dispatching

### Dispatching Events

```php
<?php

use FluentCart\Framework\Events\EventDispatcher;
use MyPlugin\Events\OrderCreatedEvent;

// Get event dispatcher
$dispatcher = EventDispatcher::getInstance();

// Dispatch event
$event = new OrderCreatedEvent($order, $customer);
$dispatcher->dispatch($event);
```

### Dispatching Events in FluentCart

FluentCart automatically dispatches events at key points:

```php
// In OrderService.php
public function createOrder($orderData)
{
    // Create order logic
    $order = Order::create($orderData);
    
    // Dispatch event
    $event = new OrderCreatedEvent($order, $customer);
    EventDispatcher::getInstance()->dispatch($event);
    
    return $order;
}
```

## Event Queuing

### Asynchronous Event Processing

For events that might take time to process, you can queue them:

```php
<?php

use FluentCart\Framework\Events\QueuedEvent;

class HeavyProcessingEvent extends QueuedEvent
{
    public $orderId;
    public $data;

    public function __construct($orderId, $data)
    {
        $this->orderId = $orderId;
        $this->data = $data;
    }

    public function getEventName()
    {
        return 'order.heavy_processing';
    }
}

// Queue the event
$event = new HeavyProcessingEvent($orderId, $data);
EventDispatcher::getInstance()->queue($event);
```

### Processing Queued Events

```php
<?php

namespace MyPlugin\Listeners;

use FluentCart\Framework\Events\Listener;
use MyPlugin\Events\HeavyProcessingEvent;

class HeavyProcessingListener extends Listener
{
    public function handle(HeavyProcessingEvent $event)
    {
        // This will be processed asynchronously
        $this->processLargeData($event->orderId, $event->data);
        $this->generateReports($event->orderId);
        $this->syncWithExternalSystems($event->orderId);
    }

    private function processLargeData($orderId, $data)
    {
        // Heavy processing logic
        sleep(10); // Simulate heavy processing
    }
}
```

## Event Middleware

### Creating Event Middleware

```php
<?php

namespace MyPlugin\Middleware;

use FluentCart\Framework\Events\Middleware;

class LoggingMiddleware extends Middleware
{
    public function handle($event, $next)
    {
        // Log before processing
        error_log('Event dispatched: ' . $event->getEventName());
        
        // Process event
        $result = $next($event);
        
        // Log after processing
        error_log('Event processed: ' . $event->getEventName());
        
        return $result;
    }
}
```

### Registering Middleware

```php
<?php

use FluentCart\Framework\Events\EventDispatcher;
use MyPlugin\Middleware\LoggingMiddleware;

$dispatcher = EventDispatcher::getInstance();
$dispatcher->addMiddleware(LoggingMiddleware::class);
```

## Event Subscribers

### Creating Event Subscribers

Event subscribers can listen to multiple events:

```php
<?php

namespace MyPlugin\Subscribers;

use FluentCart\Framework\Events\Subscriber;
use MyPlugin\Events\OrderCreatedEvent;
use MyPlugin\Events\OrderUpdatedEvent;
use MyPlugin\Events\OrderCompletedEvent;

class OrderSubscriber extends Subscriber
{
    public function subscribe($events)
    {
        $events->listen(OrderCreatedEvent::class, 'onOrderCreated');
        $events->listen(OrderUpdatedEvent::class, 'onOrderUpdated');
        $events->listen(OrderCompletedEvent::class, 'onOrderCompleted');
    }

    public function onOrderCreated(OrderCreatedEvent $event)
    {
        // Handle order created
        $this->sendWelcomeEmail($event->customer);
    }

    public function onOrderUpdated(OrderUpdatedEvent $event)
    {
        // Handle order updated
        $this->logOrderChange($event->order);
    }

    public function onOrderCompleted(OrderCompletedEvent $event)
    {
        // Handle order completed
        $this->triggerFulfillment($event->order);
    }
}
```

### Registering Subscribers

```php
<?php

use FluentCart\Framework\Events\EventDispatcher;
use MyPlugin\Subscribers\OrderSubscriber;

$dispatcher = EventDispatcher::getInstance();
$dispatcher->addSubscriber(OrderSubscriber::class);
```

## Built-in FluentCart Events

### Order Events

#### OrderCreatedEvent
```php
use FluentCart\App\Events\OrderCreatedEvent;

add_action('fluent_cart/events/order_created', function(OrderCreatedEvent $event) {
    $order = $event->order;
    $customer = $event->customer;
    
    // Handle order creation
    sendOrderConfirmation($order, $customer);
});
```

#### OrderStatusChangedEvent
```php
use FluentCart\App\Events\OrderStatusChangedEvent;

add_action('fluent_cart/events/order_status_changed', function(OrderStatusChangedEvent $event) {
    $order = $event->order;
    $oldStatus = $event->oldStatus;
    $newStatus = $event->newStatus;
    
    // Handle status change
    if ($newStatus === 'completed') {
        triggerFulfillment($order);
    }
});
```

### Payment Events

#### PaymentProcessedEvent
```php
use FluentCart\App\Events\PaymentProcessedEvent;

add_action('fluent_cart/events/payment_processed', function(PaymentProcessedEvent $event) {
    $payment = $event->payment;
    $order = $event->order;
    
    // Handle successful payment
    sendPaymentConfirmation($order, $payment);
    updateOrderStatus($order, 'processing');
});
```

### Subscription Events

#### SubscriptionCreatedEvent
```php
use FluentCart\App\Events\SubscriptionCreatedEvent;

add_action('fluent_cart/events/subscription_created', function(SubscriptionCreatedEvent $event) {
    $subscription = $event->subscription;
    $customer = $event->customer;
    
    // Handle subscription creation
    grantAccess($customer, $subscription);
    sendWelcomeEmail($customer);
});
```

## Event Testing

### Testing Events

```php
<?php

use PHPUnit\Framework\TestCase;
use FluentCart\Framework\Events\EventDispatcher;
use MyPlugin\Events\OrderCreatedEvent;
use MyPlugin\Listeners\OrderCreatedListener;

class EventTest extends TestCase
{
    public function testOrderCreatedEvent()
    {
        $dispatcher = EventDispatcher::getInstance();
        $dispatcher->addEventListener(OrderCreatedEvent::class, OrderCreatedListener::class);
        
        $order = $this->createMockOrder();
        $customer = $this->createMockCustomer();
        
        $event = new OrderCreatedEvent($order, $customer);
        $dispatcher->dispatch($event);
        
        // Assert that listener was called
        $this->assertTrue($event->wasHandled());
    }
}
```

## Best Practices

### 1. Use Specific Event Classes
```php
// Good - specific event
class OrderCreatedEvent extends Event
{
    public $order;
    public $customer;
}

// Avoid - generic event
class GenericEvent extends Event
{
    public $data;
}
```

### 2. Keep Listeners Focused
```php
// Good - focused listener
class OrderCreatedListener extends Listener
{
    public function handle(OrderCreatedEvent $event)
    {
        $this->sendConfirmationEmail($event->order);
    }
}

// Avoid - doing too much
class OrderCreatedListener extends Listener
{
    public function handle(OrderCreatedEvent $event)
    {
        $this->sendEmail($event->order);
        $this->updateInventory($event->order);
        $this->syncWithCRM($event->order);
        $this->generateReports($event->order);
        // Too many responsibilities
    }
}
```

### 3. Handle Errors Gracefully
```php
class OrderCreatedListener extends Listener
{
    public function handle(OrderCreatedEvent $event)
    {
        try {
            $this->sendConfirmationEmail($event->order);
        } catch (Exception $e) {
            // Log error but don't break the flow
            error_log('Failed to send confirmation email: ' . $e->getMessage());
        }
    }
}
```

### 4. Use Queued Events for Heavy Operations
```php
// For heavy operations, use queued events
class HeavyProcessingEvent extends QueuedEvent
{
    public $orderId;
    public $data;
}

// Queue the event instead of processing immediately
$event = new HeavyProcessingEvent($orderId, $data);
EventDispatcher::getInstance()->queue($event);
```

## Common Use Cases

### 1. Order Processing Workflow
```php
class OrderProcessingWorkflow
{
    public function handleOrderCreated(OrderCreatedEvent $event)
    {
        $order = $event->order;
        
        // Step 1: Validate order
        $this->validateOrder($order);
        
        // Step 2: Reserve inventory
        $this->reserveInventory($order);
        
        // Step 3: Send confirmation
        $this->sendConfirmation($order);
        
        // Step 4: Notify fulfillment
        $this->notifyFulfillment($order);
    }
}
```

### 2. Subscription Management
```php
class SubscriptionManager
{
    public function handleSubscriptionCreated(SubscriptionCreatedEvent $event)
    {
        $subscription = $event->subscription;
        $customer = $event->customer;
        
        // Grant access to premium features
        $this->grantPremiumAccess($customer, $subscription);
        
        // Send welcome email
        $this->sendWelcomeEmail($customer, $subscription);
        
        // Setup recurring billing
        $this->setupRecurringBilling($subscription);
    }
}
```

### 3. Integration with External Systems
```php
class ExternalSystemIntegration
{
    public function handleOrderCompleted(OrderCompletedEvent $event)
    {
        $order = $event->order;
        
        // Sync with CRM
        $this->syncWithCRM($order);
        
        // Update accounting system
        $this->updateAccounting($order);
        
        // Notify shipping provider
        $this->notifyShippingProvider($order);
    }
}
```

---

**Next Steps:**
- [Action Hooks Reference](./actions) - Complete action hooks documentation
- [Filter Hooks Reference](./filters) - Complete filter hooks documentation
- [Hooks Overview](../hooks) - Back to hooks overview
