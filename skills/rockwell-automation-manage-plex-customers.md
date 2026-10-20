---
name: manage-plex-customers
description: Look up, create and maintain customer master records and their addresses in Plex through the Plex Connect MDM API.
api: rockwell-automation:plex-erp-api
operations:
- listCustomers
- getCustomer
- createCustomer
- updateCustomer
- listCustomerAddresses
- createCustomerAddress
- deactivateCustomer
generated: '2026-10-20'
method: generated
source: openapi/rockwell-automation-plex-openapi.yml
---
# Manage Plex customers

1. Send every request to `https://connect.plex.com` (or `https://test.connect.plex.com` with a separate test key) with the `X-Plex-Connect-Api-Key` header; add `X-Plex-Connect-Tenant-Id` to act on a non-default tenant.
2. Search before creating: `listCustomers` (GET /mdm/v1/customers), then `getCustomer` by id.
3. Create with `createCustomer` only when no match exists. No idempotency key is documented, so a retried POST can create a duplicate: re-list before retrying.
4. Update with `updateCustomer`; manage ship-to/bill-to with `listCustomerAddresses` and `createCustomerAddress`.
5. Prefer `deactivateCustomer` over deletion; no reversal window is documented.
6. Most APIs are limited to 200 calls per minute; 401 `REQUEST_NOT_AUTHENTICATED` means a missing, invalid or expired key.
