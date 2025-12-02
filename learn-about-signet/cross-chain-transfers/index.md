---
title: "Cross-chain transfers"
source: "https://signet.sh/docs/learn-about-signet/cross-chain-transfers/"
---

# Source: https://signet.sh/docs/learn-about-signet/cross-chain-transfers/

# Cross-chain transfers

Why this matters

* Moving assets into and out of Signet is simple and instant
* Conditional transactions require cross-chain transfers to be fully executed in the same block on both chains

## Moving from Ethereum to Signet

Because Signet produces blocks at the same time as Ethereum, assets and data can move freely from Ethereum to Signet in the same block. If you send Ether to Signet, entering Signet has **no time delay**. Signet does not require a multi-minute wait like centrally sequenced rollups.

Users can also send transactions from Ethereum to Signet. These transactions correspond to the “forced inclusion” mechanisms on other rollups but have **no time delay.** They always execute immediately on Signet, at the end of the current block.

Moving from Ethereum to Signet always occurs in the same block, and cannot be censored or delayed by anyone.

At present, Signet supports **ETH**, **USDC**, **USDT**, and **WBTC**. Custom assets may be created within Signet, but not bridged from Ethereum. If you would like your asset to be bridged to Signet from Ethereum, please reach out.

Example: Moving assets from Ethereum to Signet

The [Passage](https://github.com/init4tech/zenith/blob/main/src/passage/Passage.sol) contract facilitates asset transfers from Ethereum to Signet.

A user wants to move 10 ETH from Ethereum to Signet:

1. User sends 10 ETH to the Signet/Passage contract on Ethereum.
2. The contract emits an `Enter` event.
3. Signet Rollup Node observes the event.
4. Rollup Node mints 10 ETH to the user’s address on Signet.

This process is permissionless and requires no action on Signet from the user.

## Moving from Signet to Ethereum

Signet introduces [Conditional Transactions](../../more-info/glossary/#conditional-transactions) to enable both local trades, and cross-chain transfers.

Conditional transactions succeed *if and only if* some condition is met at the end of execution. This condition can look at state within the rollup, or in limited cases on Ethereum. This allows same-block interaction and trading with Ethereum.

Transfers and trades are conditional on full execution. I.e. if the trade does not complete, it never occurs at all. The rollup erases failed trades and failed transfers from its history. Signet requires cross-chain transfers to be fully executed in the same block on both chains. Otherwise, the transaction is invalid and has no effect on Signet’s state; it’s as if the transaction never existed.

This allows for secure, instant transfers between Ethereum and Signet, so long as there is a Filler willing to accept the user’s order.

Example: Moving assets from Signet to Ethereum

A user wants to move 5 ETH from Signet to Ethereum. They create a conditional transaction to transfer 5 ETH. This transaction is only valid if the user receives 5 ETH on Ethereum in the same block.

1. Some Filler accepts this order by sending 5 ETH to the user on Ethereum.
2. The conditional transaction is now valid.
3. The Filler receives 5 ETH on Signet.

The user’s ETH on Signet moves *if and only if* the ETH on Ethereum goes to the user. The user cannot lose their ETH, unless they also get ETH.

Tradeoffs of this approach

Signet prioritizes the happy path and the average user. Conditional transactions provide same-block trades and interactions with Ethereum, however, they cannot provide the following:

* Synchronous composability
* Arbitrary message passing between smart contracts