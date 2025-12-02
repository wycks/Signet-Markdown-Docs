---
title: "Environment Variables"
source: "https://signet.sh/docs/bb-3f7d9e2a/run-a-builder/environment-variables/"
---

# Source: https://signet.sh/docs/bb-3f7d9e2a/run-a-builder/environment-variables/

|  |  |  |
| --- | --- | --- |
| HOST\_CHAIN\_ID | Required | Host-chain ID (e.g. 3151908) |
| RU\_CHAIN\_ID | Required | Rollup-chain ID (e.g. 14174) |
| HOST\_RPC\_URL | Required | RPC endpoint for the host chain |
| ROLLUP\_RPC\_URL | Required | RPC endpoint for the rollup chain |
| TX\_POOL\_URL | Required | Transaction pool URL (must end with /) |
| FLASHBOTS\_ENDPOINT | Optional | When configured, the Builder will send Signet blocks to this URL as transaction bundles |
| TX\_BROADCAST\_URLS | Optional | Additional endpoints for blob txs (comma-separated, slash required) |
| ZENITH\_ADDRESS | Required | Zenith contract address |
| BUILDER\_HELPER\_ADDRESS | Required | Builder helper contract address |
| QUINCEY\_URL | Required | Remote sequencer signing endpoint |
| BUILDER\_PORT | Required | HTTP port for the Builder (default: 8080) |
| SEQUENCER\_KEY | Required | AWS KMS key ID *or* local private key for sequencer signing |
| BUILDER\*KEY | Required | AWS KMS key ID *or* local private key for builder signing |
| BUILDER\_REWARDS\_ADDRESS | Required | Address receiving builder rewards |
| ROLLUP\_BLOCK\_GAS\_LIMIT | Optional | Override for block gas limit |
| CONCURRENCY\_LIMIT | Optional | Max concurrent tasks the simulator uses |
| OAUTH\_CLIENT\_ID | Required | Oauth client ID for the builder |
| OAUTH\_CLIENT\_SECRET | Required | Oauth client secret for the builder |
| OAUTH\_AUTHENTICATE\_URL | Required | Oauth authenticate URL for the builder for performing OAuth logins |
| OAUTH\_TOKEN\_URL | Required | Oauth token URL for the builder to get an Oauth2 access token |
| AUTH\_TOKEN\_REFRESH\_INTERVAL | Required | The OAuth token refresh interval in seconds. |
| CHAIN\_NAME | Required | The name of the chain (e.g. `pecorino`) |