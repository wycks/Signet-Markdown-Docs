---
title: "Simple Sequencing"
source: "https://signet.sh/docs/learn-about-signet/simple-sequencing/"
---

# Source: https://signet.sh/docs/learn-about-signet/simple-sequencing/

# Simple Sequencing

Why this matters

* Ethereum block production is overwhelmingly centralized. Most blocks are built by just a few builders (see below)
* To address this centralization, Signet assigns block production rights in a round-robin style to block builders
* This round-robin model does away with proposer-builder auctions and therefore prevents the most wealthy block builders from dominating the market

## Centralization of Sequencing

Every blockchain needs a way to order transactions — that’s sequencing. Ethereum uses auctions to determine who gets to build blocks and sequence transactions. There are a few problems with this:

1. Auctions mainly benefit the Ethereum block proposer, even though they do no valuable work.
2. Auctions centralize block building by favoring a small number of hyper-specialized builders who can out-compete smaller players.

Ethereum's blocks are built by a small number of block builders

Block building is a very high-sophistication activity, leading to a very competitive market. Marginal improvements in MEV extraction lead to significantly increased probability of winning a block auction. This means that the most aggressive builders tend to squeeze out smaller builders. This leads to aggregation of control in the hands of a small number of builders.

![Block builder market share showing the majority of blocks built by two builders](mevboost_hu_873d7eb1db9cbb2f-png/)

Block builder market share statistics from [MEVboost.pics](https://mevboost.pics/) show that Ethereum’s blocks are built by just a handful of builders.

Even worse, rollup sequencing is centralized *by default.* The chain’s order is set by a single entity, with little-to-no recourse. No rollup has credible plans to decentralize the sequencer.

## An alternative approach to sequencing

Instead of auctions, Signet uses a central sequencer that ***assigns block production rights*** to block builders in a round-robin fashion. Each Ethereum block, a specific builder may create a Signet block. That builder is responsible for creating a Signet block and for submitting that block to Ethereum. The Signet sequencer co-signs the builder’s block *without seeing its contents*.

### Resistance to censorship by the Signet sequencer

Once the assigned builder has produced a block, the Signet sequencer co-signs the block header without seeing the block contents. This means the sequencer only sees the block’s hash and the builder’s identity, not the transactions. By signing blocks without knowing their contents, the Signet sequencer can’t selectively censor transactions, ensuring fair and unbiased block inclusion while maintaining its role in managing builder participation.

Tradeoffs of this approach

This model represents a trade-off between *theoretical* and *operational* decentralization. While Ethereum’s system is *theoretically* decentralized, in that there is no single authority or administrator, it is *operationally centralized* because a small number of block builders control sequencing. Signet’s approach prioritizes *operational* decentralization by increasing the number of builders, by introducing a centralized sequencer to permission and manage that builder set.

We believe that active management is the best solution to emergent centralization.