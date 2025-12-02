---
title: "On-chain Orders in Solidity"
source: "https://signet.sh/docs/build-on-signet/signet-to-ethereum/on-chain-orders/"
---

# Source: https://signet.sh/docs/build-on-signet/signet-to-ethereum/on-chain-orders/

# On-chain Orders in Solidity

Build smart contracts that create, fill, or interact with Signet Orders. These examples demonstrate practical patterns for capturing MEV, automating exits, and creating novel cross-chain primitives.

## Setup

**Solidity (Source):** Install the Signet Orders contracts

```
forge install https://github.com/init4tech/zenith
```

**Solidity (ABI):** Download the Orders ABI

```
curl -O https://signet.sh/docs/abis/Orders.abi.json
```

**Examples:** View example contracts at [signet-sol](https://github.com/init4tech/signet-sol)

The example repository demonstrates practical patterns for:

* Flash loans
* Quick exits with fees
* Payment gating
* MEV capture

Study these examples to understand how to build with Signet Orders.

## Example Contracts

All examples use the Signet Orders system to enable cross-chain, instant, atomic, and composable operations.

SignetStd.sol - System Configuration

Auto-configure Signet system parameters based on chain ID. Use this as a base for contracts that need to interact with Signet.

**When to use:**

* You’re building a contract that creates or interacts with Orders
* You need to reference Signet system contracts
* You want chain-agnostic Signet integration

```
import {SignetStd} from "./SignetStd.sol";

contract YourContract is SignetStd {
    function createOrder() external {
        // Automatically has access to:
        // - rollupOrders: The Orders contract address
        // - permit2: The Permit2 contract address
        // - Other Signet system parameters
    }
}
```

Source: [SignetStd.sol](https://github.com/init4tech/signet-sol/blob/main/src/SignetStd.sol)

Flash.sol - Cross-Chain Flash Loans

Flash borrow any asset by using an Order where the Output becomes the Input to its own Order.

**When to use:**

* You need temporary liquidity for a transaction
* You want to perform cross-chain arbitrage
* You need to borrow assets without upfront collateral

**How it works:**

1. Request a flash loan of X tokens
2. Searchers provide the tokens (knowing they’ll be repaid)
3. Your contract executes logic with the borrowed assets
4. The Order output repays the input, completing the cycle

```
// Example: Flash borrow WETH for arbitrage
flashBorrow(wethAddress, amount, arbitrageCalldata);
```

Source: [Flash.sol](https://github.com/init4tech/signet-sol/blob/main/src/examples/Flash.sol)

GetOut.sol - Quick Exit with Fee

Exit Signet by offering searchers a 50 basis point fee. The simplest way to move assets from Signet to Ethereum.

**When to use:**

* You want a one-line function to exit Signet
* You’re willing to pay a small fee for immediate exit
* You’re building a UI that needs a simple exit mechanism

```
// Exit Signet with a 50bps fee
getOut(tokenAddress, amount, recipient);
```

**How it works:**

* Your contract locks tokens on Signet
* Creates an Order offering 99.5% of tokens on Ethereum
* Searchers fill the order for the 0.5% profit
* You receive tokens on Ethereum instantly

Source: [GetOut.sol](https://github.com/init4tech/signet-sol/blob/main/src/examples/GetOut.sol)

PayMe.sol - Payment Gating

Gate contract execution behind a payment using an Order with no inputs. The calling contract doesn’t need to manage cash flow–any third party can fill the payment order.

**When to use:**

* You want users to pay for contract execution
* You don’t want your contract to handle payment logic
* You want to allow third-party payment (gasless transactions)

**How it works:**

* Your contract creates an Order with only outputs (payment required)
* Contract execution is invalid unless someone fills the Order
* Unlike `msg.value` checks, the payer can be anyone
* Greatly simplifies payment logic

```
function executeWithPayment() external {
    // Create payment order
    payMe(usdcAddress, 10e6); // Require 10 USDC payment

    // Your contract logic here
    // Only executes if payment Order is filled
}
```

Source: [PayMe.sol](https://github.com/init4tech/signet-sol/blob/main/src/examples/PayMe.sol)

PayYou.sol - MEV Capture and Bounties

Generate MEV by offering an Order with no outputs. This creates a bounty for calling your contract, functioning as an incentivized scheduling system.

**When to use:**

* You want to incentivize someone to call your contract
* You’re creating an automated system that needs execution
* You want to capture MEV produced by your protocol

**How it works:**

* Your contract creates an Order with only inputs (no outputs required)
* Searchers compete to call your contract to claim the bounty
* Functions as an incentivized scheduling/execution system

```
function executeAndPay() external {
    // Your contract logic that generates value
    performArbitrage();

    // Pay searchers for executing
    payYou(wethAddress, 0.01 ether); // Offer 0.01 ETH bounty
}
```

**Use cases:**

* Liquidation systems
* Automated rebalancing
* Scheduled maintenance
* MEV extraction from your protocol

Source: [PayYou.sol](https://github.com/init4tech/signet-sol/blob/main/src/examples/PayYou.sol)