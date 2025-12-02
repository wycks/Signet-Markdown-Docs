---
title: "Submitting a Block to Ethereum"
source: "https://signet.sh/docs/bb-3f7d9e2a/customizing-a-builder/submitting-a-block-to-ethereum/"
---

# Source: https://signet.sh/docs/bb-3f7d9e2a/customizing-a-builder/submitting-a-block-to-ethereum/

```
let header = Zenith::BlockHeader {
    hostBlockNumber: resp.req.host_block_number,
    rollupChainId: U256::from(self.config.ru_chain_id),
    gasLimit: resp.req.gas_limit,
    rewardAddress: resp.req.ru_reward_address,
    blockDataHash: in_progress.contents_hash(),
};
```