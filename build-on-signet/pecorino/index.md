---
title: "Pecorino Quickstart"
source: "https://signet.sh/docs/build-on-signet/pecorino/"
---

# Source: https://signet.sh/docs/build-on-signet/pecorino/

# Pecorino Quickstart

Pecorino is a private Ethereum testnet for rollup and application experimentation, available to the public for testing and validation. This page contains key contract addresses and RPC endpoints for developers looking to quickly set up and interact with the Pecorino network.

These constants are also available to rust code via the [`signet-constants`](https://docs.rs/signet-constants/latest/signet_constants/) crate. If you need to test applications or software that interacts with both host and rollup chains, [please reach out](mailto:hello@init4.technology)!

## Network Configuration

## Host System Contracts

| Contract | Address |
| --- | --- |
| [Zenith](https://github.com/init4tech/zenith/blob/main/src/Zenith.sol) | `0xf17E98baF73F7C78a42D73DF4064de5B7A20EcA6` |
| [HostOrders](https://github.com/init4tech/zenith/blob/main/src/orders/HostOrders.sol) | `0x0A4f505364De0Aa46c66b15aBae44eBa12ab0380` |
| [Passage](https://github.com/init4tech/zenith/blob/main/src/passage/Passage.sol) | `0x12585352AA1057443D6163B539EfD4487f023182` |
| [Transactor](https://github.com/init4tech/zenith/blob/main/src/Transactor.sol) | `0x3903279B59D3F5194053dA8d1f0C7081C8892Ce4` |

## Rollup System Contracts

| Contract | Address |
| --- | --- |
| [RollupOrders](https://github.com/init4tech/zenith/blob/main/src/orders/RollupOrders.sol) | `0x000000000000007369676e65742d6f7264657273` |
| [RollupPassage](https://github.com/init4tech/zenith/blob/main/src/passage/RollupPassage.sol) | `0x0000000000007369676e65742d70617373616765` |
| WETH | `0x0000000000000000007369676e65742d77657468` |
| WBTC | `0x0000000000000000007369676e65742d77627463` |

## Rollup Utility Contracts