---
title: "Docker"
source: "https://signet.sh/docs/bb-3f7d9e2a/run-a-builder/install-and-run-a-node/docker/"
---

# Source: https://signet.sh/docs/bb-3f7d9e2a/run-a-builder/install-and-run-a-node/docker/

```
docker run -d \
    -e BLOB_EXPLORER_URL=value \
    -e SIGNET_STATIC_PATH=value \
    -e SIGNET_DATABASE_PATH=value \
    -e IPC_ENDPOINT=value \
    -e RPC_PORT=value \
    -e WS_RPC_PORT=value \
    -e IPC_ENDPOINT=value \
    -e TX_FORWARD_URL=value \
    -e GENESIS_JSON_PATH=value \
    -e BASE_FEE_RECIPIENT=value \
    -e SIGNET_CL_URL=value \
    -e SIGNET_PYLON_URL=value \
    -e HOST_START_TIMESTAMP=value \
    -e HOST_SLOT_OFFSET=value \
    -e HOST_SLOT_DURATION=value

    ghcr.io/init4tech/signet:latest
```