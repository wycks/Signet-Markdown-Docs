---
title: "Signed Orders"
source: "https://signet.sh/docs/sr-5c8b4a1f/signed-orders/"
---

# Source: https://signet.sh/docs/sr-5c8b4a1f/signed-orders/

# Signed Orders

## Constructing Token Transfers

**Assemble Data**

Create the `outputs` array specifying the tokens, amounts, recipients, and destination chain IDs. Construct the `permit` object listing permitted tokens and amounts, along with the `nonce` and `deadline`.

**Generate Witness Hash**

Hash the `outputs` array to create a witness hash, ensuring the integrity of the transaction details.

**Hash Permit Data**

Combine the `permit` data with the witness hash and hash the result. This step binds the permit to the specific transaction details.

**Sign Data and Encode Signature**

Sign the final hashed data using your private key.

### JSON Example

```
{
   "outputs": [
      {
          "token": "0xtokenaddress",
          "amount": 100000,
          "recipient": "0xrecipientaddress",
          "chainId": 17000
      },
      {
          "token": "0xtokenaddress",
          "amount": 100000,
          "recipient": "0xrecipientaddress",
          "chainId": 17001
      }
   ],
   "permit": {
      "permitted": [
         {
            "token": "0xtokenaddress",
            "amount": 100000
         },
         {
            "token": "0xtokenaddress",
            "amount": 100000
         }
      ],
      "nonce": 0,
      "deadline": 123456789
   },
   "owner": "0xsigneraddress",
   "signature": "0xpackedVRSsignature"
}
```

## Submitting a Signed Order

Use the `initiatePermit2` function to submit the signed order. Pass the `outputs` array and the `permit2` object containing the permit data, owner address, and signature.

### Solidity Function Interface: InitiatePermit2

```
function initiatePermit2(
    address tokenRecipient, // Filler-submitted
    Output[] memory outputs,  // signed
    OrdersPermit2.Permit2Batch calldata permit2 // signed
) external;
```

Ensure that the `outputs` and `permit2` structs are correctly formatted and signed and validate the `nonce` to prevent replay attacks and check the `deadline` for transaction validity.

## Filling Orders

Use the `fillPermit2` function to process the order and transfer the specified tokens.

### Solidity Function Interface: `fillPermit2`

```
function fillPermit2(
    Output[] memory outputs,
    OrdersPermit2.Permit2Batch calldata permit2
) external;
```

The `permit.permitted` array acts as the `outputs` and must match the order exactly for the transaction to proceed.

Ensure that the format and structures used for filling orders are consistent with those used for submitting orders.

## Solidity Structs

### Struct: `Output`

```
struct Output {
    address token; // ERC20 token address on the destination chain
    uint256 amount; // Amount of the token to be sent
    address recipient; // Address to receive the output tokens
    uint32 chainId; // Destination chain ID for the Output
}
```

### Struct: `Permit2Batch`

```
struct Permit2Batch {
    ISignatureTransfer.PermitBatchTransferFrom permit;
    address owner;
    bytes signature;
}
```

### Struct: `PermitBatchTransferFrom`

```
struct PermitBatchTransferFrom {
    TokenPermissions[] permitted;
    uint256 nonce;
    uint256 deadline;
}
```

### Struct: `TokenPermissions`

```
struct TokenPermissions {
    address token; // ERC20 token address
    uint256 amount; // Maximum amount that can be spent
}
```

Non-linear nonce: Each nonce is unique and does not have to follow a sequential order. This design prevents replay attacks and increases transaction security.