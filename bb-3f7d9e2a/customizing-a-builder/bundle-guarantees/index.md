---
title: "Bundle Guarantees"
source: "https://signet.sh/docs/bb-3f7d9e2a/customizing-a-builder/bundle-guarantees/"
---

# Source: https://signet.sh/docs/bb-3f7d9e2a/customizing-a-builder/bundle-guarantees/

# Bundle Guarantees

Signet bundles are [Flashbots-style](https://docs.flashbots.net/flashbots-protect/additional-documentation/bundle-cache) bundles of transactions wrapped with a `host_fills` field.

When building blocks containing Signet orders, the atomicity constraints apply to `host_fills` as well, meaning that if a `host_fill` is included and no corresponding rollup transaction is included, it would be considered invalid.

## Bundle Guarantees

Block Builders should respect the following guarantees around bundles when building blocks.

* **Ordering**: The transaction ordering in a bundle must be preserved.
* **Atomicity**: Bundles won’t be split up and will be applied as a contiguous block of transactions or won’t be applied at all.
* **Revertibility**: Transactions in a bundle won’t revert unless explicitly marked as revertible.