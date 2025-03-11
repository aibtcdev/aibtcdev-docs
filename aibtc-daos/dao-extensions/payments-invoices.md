---
description: Handles payment processing for DAO services
---

# Payments/Invoices Extension

The Payments/Invoices extension (`aibtc-payments-invoices`) provides a payment processing system for DAO services. It allows the DAO to define resources with prices, track user payments, and manage access to services.

## Contract Overview

- **Title**: aibtc-payments-invoices
- **Version**: 1.0.0
- **Implements**: 
  - `extension` trait
  - `invoices` trait
  - `resources` trait

## Print Events

| Event | Description | Data |
|-------|-------------|------|
| `set-payment-address` | Emitted when payment address is updated | Old address, new address, caller |
| `add-resource` | Emitted when a new resource is added | Resource data, resource index, caller |
| `toggle-resource` | Emitted when a resource is enabled/disabled | Resource index, resource data, caller |
| `pay-invoice` | Emitted when an invoice is paid | Invoice data, resource data, user data, payment details |

## Public Functions

| Function | Description | Parameters |
|----------|-------------|------------|
| `callback` | Standard extension callback | `sender`: principal, `memo`: buff 34 |
| `set-payment-address` | Set the payment recipient address | `newAddress`: principal |
| `add-resource` | Add a new resource with pricing | `name`: string-utf8 50, `description`: string-utf8 255, `price`: uint, `url`: optional string-utf8 255 |
| `toggle-resource` | Enable or disable a resource | `resourceIndex`: uint |
| `toggle-resource-by-name` | Enable or disable a resource by name | `name`: string-utf8 50 |
| `pay-invoice` | Pay for a resource | `resourceIndex`: uint, `memo`: optional buff 34 |
| `pay-invoice-by-resource-name` | Pay for a resource by name | `name`: string-utf8 50, `memo`: optional buff 34 |

## Read-Only Functions

| Function | Description | Parameters |
|----------|-------------|------------|
| `get-total-users` | Get total number of users | None |
| `get-user-index` | Get user index for an address | `user`: principal |
| `get-user-data` | Get user data by index | `index`: uint |
| `get-user-data-by-address` | Get user data by address | `user`: principal |
| `get-total-resources` | Get total number of resources | None |
| `get-resource-index` | Get resource index by name | `name`: string-utf8 50 |
| `get-resource` | Get resource data by index | `index`: uint |
| `get-resource-by-name` | Get resource data by name | `name`: string-utf8 50 |
| `get-total-invoices` | Get total number of invoices | None |
| `get-invoice` | Get invoice data by index | `index`: uint |
| `get-recent-payment` | Get recent payment index | `resourceIndex`: uint, `userIndex`: uint |
| `get-recent-payment-data` | Get recent payment data | `resourceIndex`: uint, `userIndex`: uint |
| `get-recent-payment-data-by-address` | Get recent payment by name and address | `name`: string-utf8 50, `user`: principal |
| `get-payment-address` | Get current payment address | None |
| `get-total-revenue` | Get total revenue collected | None |
| `get-contract-data` | Get aggregate contract data | None |

## Error Codes

| Code | Constant | Description |
|------|----------|-------------|
| u5000 | ERR_UNAUTHORIZED | Caller is not authorized |
| u5001 | ERR_INVALID_PARAMS | Invalid parameters provided |
| u5002 | ERR_NAME_ALREADY_USED | Resource name already exists |
| u5003 | ERR_SAVING_RESOURCE_DATA | Error saving resource data |
| u5004 | ERR_DELETING_RESOURCE_DATA | Error deleting resource data |
| u5005 | ERR_RESOURCE_NOT_FOUND | Resource not found |
| u5006 | ERR_RESOURCE_DISABLED | Resource is disabled |
| u5007 | ERR_USER_ALREADY_EXISTS | User already exists |
| u5008 | ERR_SAVING_USER_DATA | Error saving user data |
| u5009 | ERR_USER_NOT_FOUND | User not found |
| u5010 | ERR_INVOICE_ALREADY_PAID | Invoice already paid |
| u5011 | ERR_SAVING_INVOICE_DATA | Error saving invoice data |
| u5012 | ERR_INVOICE_NOT_FOUND | Invoice not found |
| u5013 | ERR_RECENT_PAYMENT_NOT_FOUND | Recent payment not found |

## Resource Management

Resources are defined with:
- Name (unique identifier)
- Description
- Price (in STX)
- Optional URL
- Enabled/disabled status

When users pay for a resource:
1. An invoice is created
2. Payment is transferred to the payment address
3. Usage statistics are updated for both user and resource
4. The payment is recorded for future reference
