---
title: "Glossary"
source: "https://signet.sh/docs/more-info/glossary/"
---

# Source: https://signet.sh/docs/more-info/glossary/

Atomic, instant, cross-chain swaps between Signet and Ethereum. Orders specify inputs (what you’re providing on Signet) and outputs (the assets you want to receive, the chain, and address for delivery). Orders can be created on-chain via the [Orders Contract](https://github.com/init4tech/zenith/blob/main/src/orders/OrderOrigin.sol) or off-chain via SignedOrder objects. Cross-chain transfers must be fully executed in the same block on both chains; otherwise, the transaction is invalid and has no effect on Signet’s state.

See [Working with Orders](../../build-on-signet/signet-to-ethereum/orders/) for implementation details.