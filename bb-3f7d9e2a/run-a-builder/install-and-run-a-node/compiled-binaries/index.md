---
title: "Compiled Binaries"
source: "https://signet.sh/docs/bb-3f7d9e2a/run-a-builder/install-and-run-a-node/compiled-binaries/"
---

# Source: https://signet.sh/docs/bb-3f7d9e2a/run-a-builder/install-and-run-a-node/compiled-binaries/

```
signet node \
    --chain pecorino \
    --authrpc.jwtsecret /path/to/your/jwt.secret \
    --http \
    --http.addr 127.0.0.1 \
    --http.api eth,net,trace,txpool,web3,rpc,debug,ots
```