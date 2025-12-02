---
title: "Getting Transactions and Bundles"
source: "https://signet.sh/docs/bb-3f7d9e2a/customizing-a-builder/getting-transactions-and-bundles-for-a-block/"
---

# Source: https://signet.sh/docs/bb-3f7d9e2a/customizing-a-builder/getting-transactions-and-bundles-for-a-block/

# Getting Transactions and Bundles

The transaction cache offers endpoints for getting simple transactions and Flashbots-style transaction bundles.

Fetching bundles requires authentication. This is because Builders are only allowed to build blocks for their assigned slots. See [Authentication](../../run-a-builder/authentication/) for details.

## Transaction cache basics:

* **API Endpoint**: `transactions.api.signet.sh`
* **Cache Duration**: 10 minutes
* **Authentication:** Authentication is required to retrieve bundles, but not to retrieve transactions.

## API Endpoints

### Get Transactions

Returns a list of transactions available for inclusion in a block.

### Get Bundles

Returns a list of bundles available for inclusion in a block. Requires authentication.