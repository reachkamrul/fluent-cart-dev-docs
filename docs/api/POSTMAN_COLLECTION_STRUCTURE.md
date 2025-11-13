# FluentCart Postman Collections - Organized Structure

This document outlines the complete structure of all Postman collections for FluentCart API, organized with folders and endpoints.

## Collection Organization Summary

**Total Collections:** 17  
**Organized with folders:** 6 collections (Products, Orders, Customers, Dashboard, Settings, Tax)  
**Standalone collections:** 11 collections

---

## 1. Products
**File:** `Products.postman_collection.json`

### Main Endpoints
- List Products
- Get Product Details
- Create Product
- Update Product Pricing
- Get Product Pricing
- Get Product Pricing Widgets
- Delete Product
- Bulk Actions

### Folders

#### Variations
- List Variations
- Create Variation
- Update Variation
- Delete Variation
- Set Variation Media
- Update Variation Pricing Table
- Get Variation Upgrade Paths

#### Search & Utilities
- Search Product by Name
- Search Variant by Name
- Search Product Variant Options
- Find Subscription Variants
- Fetch Products by IDs
- Fetch Variations by IDs
- Get Product Terms List
- Get Product Term List by Parent
- Get Max Excerpt Word Count

#### Product Management
- Set Product Image
- Update Variant Option
- Add Product Terms
- Update Long Description Editor Mode
- Update Tax Class
- Remove Tax Class
- Sync Taxonomy Terms
- Delete Taxonomy Terms
- Update Product Detail
- Create Dummy Products

#### Downloadable Files
- Sync Downloadable Files
- Update Downloadable File
- Delete Downloadable File
- Get Downloadable URL

#### Upgrade Paths
- Get Upgrade Settings
- Save Upgrade Setting
- Update Upgrade Path
- Delete Upgrade Path

#### Integrations
- Get Product Integrations
- Get Product Integration Settings
- Save Product Integration
- Delete Product Integration
- Change Product Integration Feed Status

#### Variants
- List Variants

---

## 2. Orders
**File:** `Orders.postman_collection.json`

### Main Endpoints
- List Orders
- Create Order
- Get Order Details
- Update Order
- Delete Order
- Mark Order as Paid
- Refund Order
- Update Order Statuses
- Change Order Customer
- Create and Change Customer
- Bulk Actions
- Calculate Shipping
- Get Shipping Methods
- Generate Missing Licenses
- Update Order Address ID
- Update Order Address
- Create Custom Order
- Get Order Transactions
- Get Transaction Details
- Update Transaction Status
- Accept Dispute

### Folders

#### Notes
- Attach Note to Order

#### Activity
- List Activities
- Delete Activity
- Mark Activity as Read/Unread

#### Templates
- Get Print Templates
- Save Print Templates

---

## 3. Customers
**File:** `Customers.postman_collection.json`

### Main Endpoints
- List Customers
- Create Customer
- Get Customer Details
- Update Customer
- Update Customer Additional Info
- Get Customer Stats
- Get Customer Orders (Simple)
- Get Customer Orders (Paginated)
- Get Customer Addresses
- Create Customer Address
- Update Customer Address
- Delete Customer Address
- Set Primary Address
- Get Attachable Users
- Attach User to Customer
- Detach User from Customer
- Bulk Actions

### Folders

#### Address Info
- Get Countries Options
- Get Country Info

#### Labels
- List Labels
- Create Label
- Update Label Selections

---

## 4. Dashboard
**File:** `Dashboard.postman_collection.json`

### Main Endpoints
- Get Dashboard Stats
- Get Onboarding Data

### Folders

#### Widgets
- Get Widgets

#### Welcome
- Get Welcome Message (public endpoint, no auth)

#### Onboarding
- Get Onboarding Data
- Save Onboarding Settings
- Create Pages
- Create Single Page

---

## 5. Settings
**File:** `Settings.postman_collection.json`

### Folders

#### Store Settings
- Get Store Settings
- Save Store Settings

#### Payment Methods
- Get Payment Method Settings
- Get All Payment Methods
- Save Payment Method Settings
- Reorder Payment Methods
- Get Payment Method Connect Info
- Disconnect Payment Method
- Save Payment Method Design

#### PayPal Webhooks
- Get PayPal Seller Auth Token
- Setup PayPal Webhook
- Check PayPal Webhook

#### Storage Drivers
- List Storage Drivers
- Get Active Storage Drivers
- Get Storage Driver Settings
- Save Storage Driver Settings
- Verify Storage Driver Connection

#### Module Settings
- Get Module Settings
- Save Module Settings

#### Confirmation Settings
- Save Confirmation Settings
- Get Confirmation Shortcodes

#### Checkout Fields
- Get Checkout Fields
- Save Checkout Fields

---

## 6. Tax
**File:** `Tax.postman_collection.json`

### Folders

#### Tax Classes
- List Tax Classes
- Create Tax Class
- Update Tax Class
- Delete Tax Class

#### Tax Rates
- List Tax Rates
- Get Country Tax Rates
- Create Tax Rate
- Update Tax Rate
- Delete Tax Rate
- Delete Country Tax Rates
- Save Shipping Override
- Delete Shipping Override
- Get Country Tax ID
- Save Country Tax ID

#### Tax Configuration
- Get Tax Rates from Configuration
- Save Configured Countries
- Get Tax Settings
- Save Tax Settings

#### EU VAT Settings
- Save EU VAT Settings
- Get EU Tax Rates
- Save OSS Tax Override
- Delete OSS Tax Override
- Save OSS Shipping Override
- Delete OSS Shipping Override

#### Tax Filing
- List Tax Records
- Mark Taxes as Filed

---

## 7. Subscriptions
**File:** `Subscriptions.postman_collection.json`

### Endpoints
- List Subscriptions (Admin)
- Get Subscription Details (Admin)
- Cancel Subscription (Admin)
- Fetch Subscription (Admin)
- Reactivate Subscription (Admin)
- Pause Subscription (Admin)
- Resume Subscription (Admin)
- Update Payment Method (Admin)
- List Subscriptions (Customer)
- Get Subscription Details (Customer)
- Cancel Subscription (Customer)
- Fetch Subscription (Customer)
- Reactivate Subscription (Customer)
- Pause Subscription (Customer)
- Resume Subscription (Customer)
- Update Payment Method (Customer)
- List Subscription Plans
- Get Subscription Plan Details
- Create Subscription Plan
- Update Subscription Plan
- Delete Subscription Plan

---

## 8. Coupons
**File:** `Coupons.postman_collection.json`

### Endpoints
- List Coupons
- Create Coupon
- Get Coupon Details
- Update Coupon
- Delete Coupon
- Apply Coupon
- Cancel Coupon
- Re-apply Coupon
- Check Product Eligibility
- Get Coupon Settings
- Save Coupon Settings

---

## 9. Shipping
**File:** `Shipping.postman_collection.json`

### Folders

#### Shipping Zones
- List Shipping Zones
- Get Shipping Zone Details
- Create Shipping Zone
- Update Shipping Zone
- Delete Shipping Zone

#### Shipping Methods
- List Shipping Methods
- Get Shipping Method Details
- Create Shipping Method
- Update Shipping Method
- Delete Shipping Method

#### Shipping Classes
- List Shipping Classes
- Get Shipping Class Details
- Create Shipping Class
- Update Shipping Class
- Delete Shipping Class

---

## 10. Files
**File:** `Files.postman_collection.json`

### Endpoints
- List Files
- Upload File
- Delete File
- Get Bucket List
- Sync Product Downloadable Files
- Update Product Downloadable File
- Delete Product Downloadable File
- Get Product Downloadable URL

---

## 11. Email Notification
**File:** `Email-Notification.postman_collection.json`

### Endpoints
- List Email Notifications
- Get Email Notification
- Update Email Notification
- Enable Email Notification
- Disable Email Notification
- Get Email Shortcodes
- Get Email Templates
- Get Email Settings
- Save Email Settings

---

## 12. Integration
**File:** `Integration.postman_collection.json`

### Folders

#### Global Integrations
- List Global Addons
- Get Global Integration Settings
- Save Global Integration Settings
- Get Global Integration Feeds
- Create Global Integration Feed
- Update Global Integration Feed
- Delete Global Integration Feed
- Change Global Integration Feed Status

#### Product Integrations
- Get Product Integration Settings
- Save Product Integration Settings
- Get Product Integration Feeds
- Create Product Integration Feed
- Update Product Integration Feed
- Delete Product Integration Feed
- Change Product Integration Feed Status

---

## 13. Options (Attributes)
**File:** `Options.postman_collection.json`

### Folders

#### Attribute Groups
- List Attribute Groups
- Get Attribute Group Details
- Create Attribute Group
- Update Attribute Group
- Delete Attribute Group

#### Attribute Terms
- List Attribute Terms
- Get Attribute Term Details
- Create Attribute Term
- Update Attribute Term
- Delete Attribute Term
- Update Attribute Term Serial Order

---

## 14. Reports
**File:** `Reports.postman_collection.json`

### Folders

#### Overview Reports
- Get Overview Report
- Get Revenue Overview
- Get Sales Overview

#### Sales Reports
- Get Sales Report
- Get Sales by Product
- Get Sales by Customer
- Get Sales by Date

#### Product Reports
- Get Product Performance
- Get Top Products
- Get Low Stock Products

#### Revenue Reports
- Get Revenue Report
- Get Revenue by Product
- Get Revenue by Customer
- Get Revenue by Date

#### Order Reports
- Get Order Report
- Get Orders by Status
- Get Orders by Date

#### Refund Reports
- Get Refund Report
- Get Refunds by Date

#### Subscription Reports
- Get Subscription Report
- Get Active Subscriptions
- Get Subscription Revenue

#### Other Reports
- Get Customer Lifetime Value
- Get Average Order Value
- Get Conversion Rate
- Get Cart Abandonment Rate

---

## 15. Licensing
**File:** `Licensing.postman_collection.json`

### Folders

#### License Management
- Get License
- Activate License
- Deactivate License

#### Product License Management
- Get All Product Licenses
- Get Customer Product Licenses
- Get Specific Product License
- Regenerate License Key
- Extend License Validity
- Update License Status
- Update License Limit
- Deactivate License Site
- Activate License Site
- Delete License

#### Product License Settings
- Get Product License Settings
- Save Product License Settings

#### Customer License Management
- Get Customer Licenses
- Get Customer License Details

---

## 16. Roles & Permissions
**File:** `Roles-Permissions.postman_collection.json`

### Folders

#### Role Management
- Get All Roles
- Get Managers
- Get User List by Role
- Create Role
- Get Role Details
- Update Role
- Delete Role
- Assign Role to User
- Remove Role from User

#### Permission Management
- Get All Permissions
- Get Permissions by Role

---

## 17. App
**File:** `App.postman_collection.json`

### Endpoints
- Initialize App
- Get Attachments
- Upload Attachments

---

## Structure Summary

### Collections with Folders (6)
1. **Products** - 7 folders (Variations, Search & Utilities, Product Management, Downloadable Files, Upgrade Paths, Integrations, Variants)
2. **Orders** - 3 folders (Notes, Activity, Templates)
3. **Customers** - 2 folders (Address Info, Labels)
4. **Dashboard** - 3 folders (Widgets, Welcome, Onboarding)
5. **Settings** - 7 folders (Store Settings, Payment Methods, PayPal Webhooks, Storage Drivers, Module Settings, Confirmation Settings, Checkout Fields)
6. **Tax** - 5 folders (Tax Classes, Tax Rates, Tax Configuration, EU VAT Settings, Tax Filing)

### Standalone Collections (11)
1. **Subscriptions** - 21 endpoints (no folders)
2. **Coupons** - 11 endpoints (no folders)
3. **Shipping** - 3 folders (Shipping Zones, Shipping Methods, Shipping Classes)
4. **Files** - 8 endpoints (no folders)
5. **Email Notification** - 9 endpoints (no folders)
6. **Integration** - 2 folders (Global Integrations, Product Integrations)
7. **Options** - 2 folders (Attribute Groups, Attribute Terms)
8. **Reports** - 8 folders (Overview Reports, Sales Reports, Product Reports, Revenue Reports, Order Reports, Refund Reports, Subscription Reports, Other Reports)
9. **Licensing** - 4 folders (License Management, Product License Management, Product License Settings, Customer License Management)
10. **Roles & Permissions** - 2 folders (Role Management, Permission Management)
11. **App** - 3 endpoints (no folders)

---

## Recommended API Documentation Structure

Based on this organization, your API documentation should follow the same structure:

1. **Main API sections** should match collection names
2. **Subsections** should match folder names
3. **Endpoints** should be listed under their respective subsections
4. **Related endpoints** should be grouped together (e.g., all order-related endpoints including notes, activity, templates)

This structure provides:
- **Logical grouping** of related functionality
- **Easy navigation** for developers
- **Clear hierarchy** from general to specific
- **Consistent organization** across all API sections

