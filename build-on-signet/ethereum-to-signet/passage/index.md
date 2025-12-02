---
title: "Moving Assets to Signet"
source: "https://signet.sh/docs/build-on-signet/ethereum-to-signet/passage/"
---

# Source: https://signet.sh/docs/build-on-signet/ethereum-to-signet/passage/

# Moving Assets to Signet

The [Passage](https://github.com/init4tech/zenith/blob/main/src/passage/Passage.sol) contract helps move assets from Ethereum to Signet instantly.
Signet nodes listen for `Passage` events, and mint tokens on Signet in the
**same block**.

Consult the [Pecorino Quickstart](../../pecorino/) guide for contract addresses and RPC
endpoints.

## Setup

**Solidity (ABI):** Download the Passage ABI from [Passage ABI](../../../../abis/Passage-abi-json/)

```
curl -O https://signet.sh/docs/abis/Passage.abi.json
```

**Solidity (Source):** The Passage contract is open source

```
forge install https://github.com/init4tech/zenith
```

**Rust:** Alloy bindings are available via the [signet-bindings](https://docs.rs/signet-bindings/latest/signet_bindings/) crate

```
cargo add signet-bindings
```

## Overview

`Passage.sol` exposes a simple interface:

**Move ETH to Signet:**

```
enter(address rollupRecipient)
```

The `fallback` and `receive` functions also move ETH to Signet, with `msg.sender` as recipient.

**Move ERC-20 tokens to Signet:**

```
enterToken(address rollupRecipient, address token, uint256 amount)
```

Requires prior `approve` of Passage to spend tokens.

Passage can be observed using the `Enter` and `EnterToken` events. The `Enter`
event is fired whenever ETH is bridging to Signet, and `EnterToken` is fired
when ERC-20 tokens are bridged. The Signet node listens for these events directly, so if the event fired, the tokens were bridged.

## Code Examples

Solidity

Passage is available as a Solidity contract or ABI. See the [Setup](#setup) section above.

```
contract YourContract {
    Passage public passage;
    IERC20 public token;

    constructor(address _passage, IERC20 _token) {
        passage = Passage(_passage);
        token = _token;
        token.approve(_passage, type(uint256).max);
    }

    // Enter on behalf of a user
    function bridgeETH() external payable {
        passage.enter{value: msg.value}(msg.sender);
    }

    // Move ERC-20 tokens to Signet
    function bridgeToken(uint256 amount) external {
        token.transferFrom(msg.sender, address(this), amount);
        passage.enterToken(address(token), msg.sender);
    }
}
```

Cast

To enter the rollup, Send ETH directly to the Passage contract:

```
# Using cast
cast send $PASSAGE_ADDRESS \
  --value 1ether \
  --rpc-url $HOST_CHAIN_RPC \
  --private-key $PRIVATE_KEY
```

Entering with tokens requires multiple transactions:

```
# 1. Approve Passage
cast send $TOKEN_ADDRESS \
  "approve(address,uint256)" \
  $PASSAGE_ADDRESS, $AMOUNT \
  --rpc-url $HOST_CHAIN_RPC \
  --private-key $PRIVATE_KEY

# 2. Call Passage to bridge tokens
# See Passage.sol for the exact function name and parameters
cast send $PASSAGE_ADDRESS \
  "enterTokens(address,address,uint256)" \
  $SIGNET_RECIPIENT, $TOKEN_ADDRESS, $AMOUNT \
  --rpc-url $HOST_CHAIN_RPC \
  --private-key $PRIVATE_KEY
```

Typescript

```
// Using ethers.js
const tx = await signer.sendTransaction({
  to: PASSAGE_ADDRESS,
  value: ethers.parseEther("1.0"),
});

await tx.wait();
```

Listen for events:

```
import { ethers } from "ethers";

const provider = new ethers.JsonRpcProvider("https://eth.llamarpc.com");
const passage = new ethers.Contract(
  PASSAGE_ADDRESS,
  PASSAGE_ABI, // Get ABI from contract source
  provider
);

// Listen for events
// Event names and signatures from Passage.sol
passage.on("Enter", (...args) => {
  console.log("ETH bridged:", args);
});

passage.on("EnterToken", (...args) => {
  console.log("Token bridged:", args);
});
```

Rust

```
let passage = PassageContract::new(
    signet_constants::pecorino::HOST_PASSAGE,
    provider.clone(),
);

// Enter the rollup from your EOA
passage.enter().value(eth_in_wei).send(rollup_recipient).await?;
```

## Next Steps

Send a rollup transaction using the [Transactor](../transactor/) contract.