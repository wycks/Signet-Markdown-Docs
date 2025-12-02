---
title: "FAQ"
source: "https://signet.sh/docs/more-info/faq/"
---

# Source: https://signet.sh/docs/more-info/faq/

# FAQ

What is Signet?

Signet is a pragmatic Ethereum rollup designed to offer sustainable economic incentives. It aims to modernize and streamline rollups by simplifying their architecture and focusing on efficiency.

How does Signet differ from traditional rollups?

Signet differs in several key ways:

* It doesn’t use proving systems or state roots, which reduces computational overhead.
* It uses market-based cross-chain transfers instead of complex bridging mechanisms.
* It replaces block auctions and centralized rollup sequencing with a controlled block inclusion mechanism.
* It introduces conditional transactions for secure, atomic cross-chain operations.

How does Signet handle cross-chain transfers?

Signet uses market-based mechanisms and conditional transactions for cross-chain transfers. This allows for secure, instant transfers between Ethereum and Signet without the need for lockup periods.

See [Cross-chain Transfers](../../learn-about-signet/cross-chain-transfers/).

Is Signet suitable for all use cases?

While Signet offers significant benefits for most users, it may not be suitable for all situations. For example, it’s not ideal for users who require light client functionality or certain types of cross-chain interactions that rely on cryptographic proofs.

How does Signet ensure fair block production?

Instead of using auctions, Signet uses a central sequencer that assigns block production rights in a round-robin style to block builders. This prevents domination by a small number of wealthy builders and promotes fair participation.

What tokens are supported for bridging?

Signet supports **ETH**, **USDC**, **USDT**, and **WBTC** for bridging between Ethereum and Signet. Custom assets may be created within Signet but cannot be bridged from Ethereum without coordination with the Signet team.

See [Moving Assets to Signet](../../build-on-signet/ethereum-to-signet/passage/) for details.

What is Pecorino?

Pecorino is a private Ethereum testnet for rollup and application experimentation, available to the public for testing and validation. It includes RPC endpoints, faucet, explorer, and transaction cache infrastructure for development.

See [Pecorino Quickstart](../../build-on-signet/pecorino/) for network configuration and contract addresses.

How does Signet guarantee atomic cross-chain execution?

Signet requires cross-chain transfers to be fully executed in the same block on both chains. If the transfer is not fully executed, the transaction is invalid and has no effect on Signet’s state—as if the transaction never existed.

See [Cross-chain Transfers](../../learn-about-signet/cross-chain-transfers/) for more details.

Do I need to run my own Ethereum or Signet node?

No. You can use public RPC endpoints. For Pecorino testnet, see the [Pecorino Quickstart](../../build-on-signet/pecorino/) for endpoints. For block builders, RPC access can be configured via environment variables—running your own nodes is optional infrastructure.

See [Environment Variables](../../bb-3f7d9e2a/run-a-builder/environment-variables/) for builder configuration.

What do block builders do in the Signet ecosystem?

Block Builders collect user transactions, build blocks, and post those blocks to Ethereum. Some user transactions create swap orders. These orders may trade between Signet and Ethereum, or within Signet. Block builders can chose to fill any number of orders as part of constructing the block.