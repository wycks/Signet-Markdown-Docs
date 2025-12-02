---
title: "Working with Orders"
source: "https://signet.sh/docs/build-on-signet/signet-to-ethereum/orders/"
---

# Source: https://signet.sh/docs/build-on-signet/signet-to-ethereum/orders/

# Working with Orders

Signet Orders enable atomic, instant, cross-chain swaps between Signet and
Ethereum. Orders specify assets in, assets out, and on what chain the assets
out should be delivered. Orders can be created by smart contract execution via
the [Orders Contract](https://github.com/init4tech/zenith/blob/main/src/orders/OrderOrigin.sol), or via an off-chain `SignedOrder` object.

## How Orders Work

MEV Searchers (called Fillers) compete to fulfill each Order by providing the
output tokens. Your input tokens are locked on Signet until a Filler completes
the swap.

**Orders are a form of direct interaction with the MEV ecosystem.** You can
think of them as a way to express your intent to move assets across chains,
while allowing the MEV market to find the best execution strategy.

An Order has two main components:

* **Inputs**: What you’re providing on Signet
* **Outputs**: The assets you want to receive, as well as the chain and address
  to which to deliver them.

`Input` and `Output` structs are specified in the [`IOrders.sol`](https://github.com/init4tech/zenith/blob/main/src/orders/IOrders.sol) interface.

## Implementation Paths

Choose your implementation based on your stack:

### On-chain Orders in Solidity

Build smart contracts that create, fill, or interact with Signet Orders on-chain. Perfect for:

* Automated MEV capture
* Flash loans across chains
* Payment gating
* Smart contract exits from Signet

[Learn how to work with Solidity Orders](../on-chain-orders/)

### Off-chain Orders in Rust

Build applications that create and fill Signet Orders programmatically. Perfect for:

* Market making bots
* Order monitoring services
* Cross-chain arbitrage
* Custom filler strategies

[Learn how to work with Rust Orders](../rust-orders/)

## Next Steps

Start with the implementation path that matches your stack, or explore both to understand the full capabilities of Signet Orders.