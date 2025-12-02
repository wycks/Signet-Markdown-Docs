---
title: "EVM Behavior"
source: "https://signet.sh/docs/build-on-signet/evm-behavior/"
---

# Source: https://signet.sh/docs/build-on-signet/evm-behavior/

# EVM Behavior

Signet is the most EVM-compatible rollup. This page describes the (very few)
differences between Signet and Ethereum Mainnet EVM behavior.

## USD Native Asset

The native asset on Signet is USD. USD has 18 decimals, like ETH on Ethereum Mainnet. See the [Passage](../ethereum-to-signet/passage/) contract for more information on how USD is minted.

The following opcodes inherit the values of the Ethereum block:

* `PREVRANDAO` — `block.difficulty` and `block.prevrandao`
* `TIMESTAMP` — `block.timestamp`

## Disabled Opcodes

The following opcodes are disabled in Signet:

* `BLOBHASH` — EIP-4844 is not supported.
* `BLOBBASEFEE` — EIP-4844 is not supported.

## Precompiles

Signet supports the
[same precompiles as ethereum](https://www.evm.codes/precompiled), plus the
following additional precompile:

* secp256r1 signature verification as specified in [RIP-7212](https://github.com/ethereum/RIPs/blob/master/RIPS/rip-7212.md) at address `0x100`.

## Address Aliasing

To conform to common rollup conventions, Signet uses address aliasing for
L1-to-L2 messages. When a contract on L1 sends a message to Signet via the
[`Transactor`](../ethereum-to-signet/transactor/) contract,
the sender’s address is modified by adding a constant offset to it. This
ensures that contracts on Signet can distinguish between messages sent from L1
and those sent from the same address on the L2.

The address aliasing offset is `0x1111000000000000000000000000000000001111`.
Aliasing is performed by converting the address to a number, adding the offset,
and then converting back to an address.

Signet differs from other rollup behaviors in that the addresses of ephemeral
contracts are NOT aliased. Signet treats ephemeral L1 contracts equivalently to
EOAs.

| Account Type | Address Aliased? |
| --- | --- |
| EOA | No |
| EIP-7702 Delegation | No |
| Ephemeral Contract | **No** |
| Smart Contract | Yes |