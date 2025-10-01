# FluentCart Database Tables - Comprehensive Analysis

## Migration Files Analysis (38 tables)

Based on migration files found in the codebase:

### Core Tables (30 tables)
1. fct_activity
2. fct_applied_coupons
3. fct_atts_groups
4. fct_atts_relations
5. fct_atts_terms
6. fct_carts
7. fct_coupons
8. fct_customer_addresses
9. fct_customer_meta
10. fct_customers
11. fct_label
12. fct_label_relationships
13. fct_meta
14. fct_order_addresses
15. fct_order_details_meta
16. fct_order_download_permissions
17. fct_order_items
18. fct_order_meta
19. fct_order_operations
20. fct_order_tax_rate
21. fct_order_transactions
22. fct_orders
23. fct_product_details
24. fct_product_downloads
25. fct_product_meta
26. fct_product_variations
27. fct_scheduled_actions
28. fct_shipping_classes
29. fct_shipping_methods
30. fct_shipping_zones
31. fct_subscription_meta
32. fct_subscriptions
33. fct_tax_classes
34. fct_tax_rates

### Pro Plugin Tables (4 tables)
35. fct_license_activations
36. fct_license_meta
37. fct_license_sites
38. fct_licenses

## Schema Documentation Analysis

### Tables Documented in Schema (with duplicates removed)
1. fct_activity
2. fct_applied_coupons
3. fct_atts_groups
4. fct_atts_relations
5. fct_atts_terms
6. fct_carts
7. fct_coupons
8. fct_customer_addresses
9. fct_customer_meta
10. fct_customers
11. fct_email_notifications
12. fct_label
13. fct_label_relationships
14. fct_license_activations
15. fct_license_meta
16. fct_license_sites
17. fct_licenses
18. fct_meta
19. fct_order_addresses
20. fct_order_details_meta
21. fct_order_download_permissions
22. fct_order_items
23. fct_order_meta
24. fct_order_operations
25. fct_order_promotions
26. fct_order_promotion_stats
27. fct_order_tax_rate
28. fct_order_transactions
29. fct_orders
30. fct_product_details
31. fct_product_downloads
32. fct_product_meta
33. fct_product_variations
34. fct_scheduled_actions
35. fct_shipping_classes
36. fct_shipping_methods
37. fct_shipping_zones
38. fct_subscription_meta
39. fct_subscriptions
40. fct_tax_classes
41. fct_tax_rates
42. fct_webhook_logger

## Model Documentation Analysis (46 model files)

### Core Models (39 models)
1. activity
2. applied-coupon
3. attribute-group
4. attribute-relation
5. attribute-term
6. cart
7. coupon
8. customer
9. customer-addresses
10. customer-meta
11. dynamic-model
12. label
13. label-relationship
14. meta
15. order
16. order-address
17. order-details-meta
18. order-download-permission
19. order-item
20. order-meta
21. order-operation
22. order-tax-rate
23. order-transaction
24. product
25. product-detail
26. product-download
27. product-meta
28. product-variation
29. scheduled-action
30. shipping-class
31. shipping-method
32. shipping-zone
33. subscription
34. subscription-meta
35. tax-class
36. tax-rate
37. user
38. user-meta
39. relationships (special file)

### Pro Plugin Models (7 models)
40. license
41. license-activation
42. license-meta
43. license-site
44. order-promotion
45. order-promotion-stat
46. user-meta

## Issues Found

### 1. Missing Migration Files
- fct_order_promotions (exists as model, no migration)
- fct_order_promotion_stats (exists as model, no migration)
- fct_email_notifications (in schema docs, no migration found)
- fct_webhook_logger (in schema docs, no migration found)

### 2. Extra Tables in Schema Docs
- fct_email_notifications (not in migrations)
- fct_webhook_logger (not in migrations)

### 3. Missing Model Documentation
- email-notifications (if table exists)
- webhook-logger (if table exists)

### 4. Duplicates in Schema Documentation
- Multiple entries for same tables (shipping, activity, etc.)

## Recommendations

1. **Clean up schema documentation** - Remove duplicates
2. **Verify missing tables** - Check if fct_email_notifications and fct_webhook_logger actually exist
3. **Create migration files** for promotion tables or document why they don't exist
4. **Standardize naming** - Ensure all three sources use consistent table names
5. **Update total count** - Schema shows 42 tables but should be 38 based on migrations

## Final Count Should Be
- **Migration Files**: 38 tables (34 Core + 4 Pro)
- **Schema Documentation**: 38 tables (34 Core + 4 Pro) 
- **Model Documentation**: 38 models (34 Core + 4 Pro)

**Total**: 38 tables across all three sources
