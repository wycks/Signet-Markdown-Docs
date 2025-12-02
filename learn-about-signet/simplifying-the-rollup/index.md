---
title: "Simplifying the Rollup"
source: "https://signet.sh/docs/learn-about-signet/simplifying-the-rollup/"
---

# Source: https://signet.sh/docs/learn-about-signet/simplifying-the-rollup/

# Simplifying the Rollup

Signet is a pragmatic Ethereum rollup with sustainable economic incentives. It offers a new set of ideas, aiming to radically modernize and streamline rollups.

* No proving systems or state roots, drastically reducing computational overhead
* Market-based cross-chain transfers for instant asset movement
* Removes block auctions in favor of a controlled block inclusion mechanism
* Introduces conditional transactions for secure, atomic cross-chain operations

Signet is built by [Init4](https://x.com/init4tech), a research collective building next-generation Ethereum.

## A Brief History of the Rollup

Ethereum rollups are the intellectual descendants of a project called [Plasma](https://ethereum.org/en/developers/docs/scaling/plasma/). Plasmas were complex multi-layered chain systems that used intricate proofs to connect to Ethereum. The research community gradually abandoned Plasmas because their proving trade-offs turned out to be unsuitable to real applications.

Around the time Plasma was falling out of favor, a transaction batching service for simple payments called [roll\_up](https://github.com/barryWhiteHat/roll_up) was being developed. Plasma researchers co-opted the name *rollup* and shifted their focus to the development of early rollups, while still focusing on the proving systems.

Today, many more rollups have been created. All of these projects have carried forward the original Plasma architecture, placing a proving system at the center of the tech stack. Today rollups are mostly categorized by their proving system — zk or optimistic — but that doesn’t have to be the case.

## Back to basics

Ethereum rollups have always been complex. They have never had an era where they *weren’t* complex. They didn’t start simple and evolve; they were born complex and stayed that way. Their core ideas have never been fundamentally challenged.

**Signet’s thesis is that the complexity isn’t necessary.**

> A rollup is an opt-in subset of another consensus, keeping a superset of state, via a custom state-transition function. — [Defining “rollup”](https://prestwich.substack.com/p/defining-rollup)

## Rollups are sandwiches

Think of rollups as sandwiches. Current-generation rollups all have the same set of “mandatory ingredients” inherited from their common ancestry. To differentiate, they add more and more “toppings”, resulting in increasingly massive sandwich-systems.

Signet is the classic grilled cheese of rollups. Bread, butter, and cheese: simple, effective, and satisfying for most users. We’re not saying complex rollups aren’t for anyone, just that they’re not for everyone.

## Signet is just a rollup

We built Signet to be straightforward, fast, and affordable.

* **Full EVM compatibility**: Deploy smart contracts, connect wallets, farm $YAMs.
* **Simple deployment and ops**: Signet is a drop-in update to your existing Ethereum node. No more 4-node `docker-compose` setups to run a rollup.
* **Massively higher gas limits**: Eliminating protocol and proving overhead frees up resources for users.