---
title: Order Details Meta Model
description: FluentCart OrderDetailsMeta model documentation with attributes, scopes, relationships, and methods.
---

# Order Details Meta Model

| DB Table Name | {wp_db_prefix}_fct_order_details_meta               |
| ------------- | --------------------------------------------------- |
| Schema        | [Check Schema](/database/schema#fct-order-details-meta-table) |
| Source File   | fluent-cart/app/Models/OrderDetailsMeta.php        |
| Name Space    | FluentCart\App\Models                              |
| Class         | FluentCart\App\Models\OrderDetailsMeta             |

## Attributes

| Attribute          | Data Type | Comment |
| ------------------ | --------- | ------- |
| id                 | Integer   | Primary Key |
| object_type        | String    | Type of object (order, order_item, etc.) |
| object_id          | Integer   | ID of the associated object |
| meta_key           | String    | Meta key name |
| meta_value         | Text      | Meta value (JSON encoded for arrays/objects) |
| created_at         | Date Time | Creation timestamp |
| updated_at         | Date Time | Last update timestamp |

## Usage

Please check [Model Basic](/database/models) for Common methods.

### Accessing Attributes

```php
$orderDetailsMeta = FluentCart\App\Models\OrderDetailsMeta::find(1);

$orderDetailsMeta->id; // returns id
$orderDetailsMeta->object_type; // returns object type
$orderDetailsMeta->object_id; // returns object ID
$orderDetailsMeta->meta_key; // returns meta key
```

## Methods

Along with Global Model methods, this model has few helper methods.

### setMetaValueAttribute($value)

Set meta value with automatic JSON encoding (mutator)

* Parameters  
   * $value - mixed (array, object, or string)
* Returns `void`

#### Usage

```php
$orderDetailsMeta->meta_value = ['custom_data' => 'value', 'settings' => ['key' => 'value']];
// Automatically JSON encodes arrays and objects
```

### getMetaValueAttribute($value)

Get meta value with automatic JSON decoding (accessor)

* Parameters  
   * $value - mixed
* Returns `mixed`

#### Usage

```php
$metaValue = $orderDetailsMeta->meta_value; // Returns decoded value (array, object, or string)
```

## Usage Examples

### Get Order Details Meta

```php
$orderDetailsMeta = FluentCart\App\Models\OrderDetailsMeta::where('object_type', 'order')
    ->where('object_id', 123)
    ->get();

foreach ($orderDetailsMeta as $meta) {
    echo "Key: " . $meta->meta_key;
    echo "Value: " . print_r($meta->meta_value, true);
}
```

### Create Order Details Meta

```php
$orderDetailsMeta = FluentCart\App\Models\OrderDetailsMeta::create([
    'object_type' => 'order',
    'object_id' => 123,
    'meta_key' => 'custom_field',
    'meta_value' => 'custom_value'
]);
```

### Store Complex Data

```php
$orderDetailsMeta = FluentCart\App\Models\OrderDetailsMeta::create([
    'object_type' => 'order_item',
    'object_id' => 456,
    'meta_key' => 'product_options',
    'meta_value' => [
        'color' => 'red',
        'size' => 'large',
        'customizations' => ['engraving' => 'Happy Birthday']
    ]
]);
```

### Get Meta by Key

```php
$meta = FluentCart\App\Models\OrderDetailsMeta::where('object_type', 'order')
    ->where('object_id', 123)
    ->where('meta_key', 'shipping_notes')
    ->first();

if ($meta) {
    echo "Shipping Notes: " . $meta->meta_value;
}
```

### Update Meta Value

```php
$meta = FluentCart\App\Models\OrderDetailsMeta::find(1);
$meta->meta_value = ['updated' => true, 'timestamp' => now()];
$meta->save();
```

---

