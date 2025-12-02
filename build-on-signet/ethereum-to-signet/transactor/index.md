---
title: "Ethereum-driven Transactions"
source: "https://signet.sh/docs/build-on-signet/ethereum-to-signet/transactor/"
---

# Source: https://signet.sh/docs/build-on-signet/ethereum-to-signet/transactor/

# Ethereum-driven Transactions

The [`Transactor`](https://github.com/init4tech/zenith/blob/main/src/Transactor.sol) contract creates transactions on Signet from Ethereum.
Transactions made via the `Transactor` always execute on Signet at the end of
the current block, bypassing any possibility of builder censorship.

Consult the [Pecorino Quickstart](../../pecorino/) guide for contract addresses and RPC
endpoints.

## Setup

**Solidity (ABI):** Download the Transactor ABI from [Transactor ABI](../../../../abis/Transactor-abi-json/)

```
curl -O https://signet.sh/docs/abis/Transactor.abi.json
```

**Solidity (Source):** The Transactor contract is open source

```
forge install https://github.com/init4tech/zenith
```

**Rust:** Alloy bindings are available via the [`signet-zenith`](https://docs.rs/signet-zenith/latest/signet_zenith/) crate

## Overview

`Transactor.sol` exposes a basic EVM transaction as a single function:

```
function transact(
    address to,
    bytes calldata data,
    uint256 value,
    uint256 gas,
    uint256 maxFeePerGas
) external payable
```

Calling the `transact` function results in a system transaction being issued on
Signet **from the address of the caller**. This allows Ethereum contracts to
own assets on Signet, and to trigger contract execution on Signet from
Ethereum with native authentication.

The `value` argument is the amount of USD in wei to send **on the rollup**.
USD is the native asset of Signet. This amount will be attached to the Signet
transaction. The balance of originating address on Signet must be sufficient to
cover this value.

Transact events are executed at the **end** of the Signet block. Contract
creation via `Transactor` is not currently supported.

The Transactor emits a `Transact` event that can be monitored. The Signet node
listens for these events directly, so if the event fired, the transaction
**was** included in Signet (although it may revert or be dropped by the
[Signet Orders](../../signet-to-ethereum/orders/) system).

Use Transactor when...

* You need guaranteed transaction inclusion
* You want to trigger Signet actions from Ethereum
* You’re building cross-chain workflows
* You need censorship resistance

## Code Examples

Solidity

```
contract YourContract {
    Transactor public transactor;

    constructor(Transactor _transactor) {
        transactor = _transactor;
    }

    // Execute a function on Signet from Ethereum
    function executeOnSignet(
        address signetTarget,
        bytes calldata functionData
    ) external {
        transactor.transact(
            signetTarget,
            functionData,
            0, // USD value on Signet
            1_000_000, // gas limit on Signet
            100 gwei // max fee per gas (in USD) on Signet
        );
    }

    // Emergency action on Signet
    function emergencyAction(address signetContract) external onlyOwner {
        // Encode the emergency function call
        bytes memory data = abi.encodeWithSignature("emergencyPause()");
        executeOnSignet(signetContract, data);
    }
}
```

Monitoring Transactor activity in JavaScript/TypeScript

Listen for Transactor events to track Host-driven transactions:

```
import { ethers } from "ethers";

const provider = new ethers.JsonRpcProvider("https://eth.llamarpc.com");
const transactor = new ethers.Contract(
  TRANSACTOR_ADDRESS,
  TRANSACTOR_ABI, // Get ABI from contract source
  provider
);

// Listen for Host-driven transactions
// Event name and signature from Transactor.sol
transactor.on("Transact", (...args) => {
  console.log("Host-driven execution:", args);

  // Decode the calldata if needed
  const [from, to, data] = args; // Adjust based on actual event
  console.log(`${from} Host-driven execution on ${to}`);
});
```