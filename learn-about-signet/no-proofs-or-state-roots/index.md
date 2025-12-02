---
title: "No Proofs or State Roots"
source: "https://signet.sh/docs/learn-about-signet/no-proofs-or-state-roots/"
---

# Source: https://signet.sh/docs/learn-about-signet/no-proofs-or-state-roots/

# No Proofs or State Roots

Why this matters

* No proving systems or state roots drastically reduces computational overhead
* Conditional transactions provide secure, atomic cross-chain operations
* Cross-chain transfers are market-based

Rollups extend Ethereum by allowing nodes to track additional data. Traditional rollups face significant complexity when communicating this data back to Ethereum, typically relying on proving systems. Signet takes a different approach.

## No proving system

Most rollups use complex proving systems like optimistic or zero-knowledge proofs to communicate with Ethereum. These systems introduce significant overhead and complexity and are not necessary for most users. Instead of a proving system, Signet facilitates cross-chain transfers through markets. Assets are bought and sold between Signet and Ethereum, rather than being “proven” back onto Ethereum.

This approach:

* Reduces computational overhead, lowering transaction costs
* Increases capacity for processing transactions
* Simplifies the overall architecture, making it easier to maintain and upgrade

## No state roots

[State roots](../../more-info/glossary/#state-roots) were designed for a world where everyone runs a full node. However, most users today interact with blockchains through intermediaries like wallet providers or node services, relying on these for state information rather than verifying the entire chain themselves. In this new paradigm, state roots are much less critical for day-to-day operations and consume significant computational resources.

Signet removes state roots as part of our broader strategy to streamline rollup architecture. By eliminating the proving system, we’ve created an environment where state roots become redundant. This allows us to focus on what matters most to users: fast, cheap transactions and a simple, robust system.

By removing state roots, Signet:

* Drastically reduces computational overhead
* Significantly increases transaction throughput
* Lowers transaction costs for users

Tradeoffs of this Approach

Signet prioritizes the happy path and the average user. While removing proving systems and state roots offers significant benefits to most people, it does not support the following:

* Light clients
* Cryptographic proofs of state