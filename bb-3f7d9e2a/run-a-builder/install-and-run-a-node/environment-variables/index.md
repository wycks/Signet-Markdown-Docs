---
title: "Environment Variables"
source: "https://signet.sh/docs/bb-3f7d9e2a/run-a-builder/install-and-run-a-node/environment-variables/"
---

# Source: https://signet.sh/docs/bb-3f7d9e2a/run-a-builder/install-and-run-a-node/environment-variables/

|  |  |  |
| --- | --- | --- |
| BLOB\_EXPLORER\_URL | Required | URL of a blob explorer |
| SIGNET\_STATIC\_PATH | Required | Filesystem path to where the static\_files directory should be located |
| SIGNET\_DATABASE\_PATH | Required | Filesystem path to where the node should store its database |
| IPC\_ENDPOINT | Optional | Filesystem path for the .ipc file |
| GENESIS\_JSON\_PATH | Required | Path on the filesystem for the genesis file |
| RPC\_PORT | Required | Port to be used for the rollup node http json-rpc requests |
| WS\_RPC\_PORT | Required | Port to be used for the rollup node’s WebSocket connections |
| TX\_FORWARD\_URL | Optional | URL for the transaction cache API |
| SIGNET\_CL\_URL | Optional | URL to the consensus layer for fetching blobs and other CL responsibilities |
| SIGNET\_PYLON\_URL | Optional | URL to the Pylon node for blob storage |
| HOST\_START\_TIMESTAMP | Required | The host chain’s start timestamp for slot calculation purposes |
| HOST\_SLOT\_OFFSET | Required | The host chain’s slot offset |
| HOST\_SLOT\_DURATION | Required | The host chain’s slot duration |
| RUST\_LOG | Optional | Standard rust environment variable for logging |