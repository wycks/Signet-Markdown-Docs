---
title: "Off-chain Orders in Rust"
source: "https://signet.sh/docs/build-on-signet/signet-to-ethereum/rust-orders/"
---

# Source: https://signet.sh/docs/build-on-signet/signet-to-ethereum/rust-orders/

# Off-chain Orders in Rust

This page will walk you through creating and submitting off-chain Orders using
Rust and the Signet SDK.

The [Orders](https://github.com/init4tech/zenith/blob/main/src/orders/) contract enables trustless, cross-chain asset swaps between
Signet and Ethereum. Signet nodes listen for Order and Filled events,
and ensure that all transactions that emit Orders have corresponding Fills
executed on the destination chain in the same block.

Order events are emitted on Signet, while Filled events may be emitted
on either Ethereum or Signet. Off-chain orders are pre-signed, using
[Permit2](https://docs.uniswap.org/contracts/permit2/overview), and may be executed by a third-party filler, allowing users to
perform gasless swaps.

Set competitive prices on your orders

Signet Orders guarantee that if their Outputs are not Filled, no transaction
will be executed on Signet. However, there is no guarantee that any searcher
will choose to Fill your Order. Make sure to set competitive prices on your
orders to ensure they are filled!

## Setup

Set up your Rust project

```
cargo new my_cool_app --bin
```

Install the required Signet crates

```
cargo add signet-zenith
cargo add signet-constants
cargo add signet-types
cargo add signet-tx-cache
```

Ensure your account has approved [Permit2](https://docs.uniswap.org/contracts/permit2/overview) to spend your input tokens.

Consult the [Pecorino Quickstart](../../pecorino/) guide for contract addresses and RPC endpoints.

## Creating an Order

The [signet-types](http://docs.rs/signet-types/latest/signet_types/) crate provides a simple order builder via the
[UnsignedOrder](https://docs.rs/signet-types/latest/signet_types/signing/order/struct.UnsignedOrder.html) struct, which can be used to build orders. We can
start by creating a simple order that swaps 1 WETH on Signet for 1 WETH on
Ethereum:

```
use signet_types::signing::order::{UnsignedOrder};
use signet_constants::pecorino as constants;

let mut order = UnsignedOrder::default()
    .with_input(
        constants::RU_WETH,
        U256::from(1e18), // 1 WETH
    ).with_output(
        constants::HOST_WETH,
        U256::from(1e18),
        your_address,
        1, // Ethereum mainnet
    );
```

The `UnsignedOrder` struct also provides methods to sign orders, using any
alloy signer. The signer requires that you provide the `constants` object, so
that the permit2 signer can correctly derive the domain separator.

```
use signet_types::signing::order::{UnsignedOrder};
use signet_constants::pecorino as constants;

let signed = UnsignedOrder::default()
    .with_input(token_address, amount)
    .with_output(token_address, amount, recipient, chain_id)
    .with_chain(constants)
    .with_nonce(permit2_nonce)
    .sign(&signer).await?;
```

## Submitting an Order

Once signed, the order can be submitted to the Signet network via the Signet tx
cache. The tx cache makes the Order available to Searchers, who will include it
in execution bundles.

```
use signet_tx_cache::TxCache;

let tx_cache = TxCache::pecorino();
tx_cache.forward_order(signed_order).await?;
```

For on-chain order creation, check out [Solidity Orders](../on-chain-orders/).