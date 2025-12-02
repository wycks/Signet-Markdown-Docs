---
title: "Clone and Build"
source: "https://signet.sh/docs/bb-3f7d9e2a/run-a-builder/clone-and-build/"
---

# Source: https://signet.sh/docs/bb-3f7d9e2a/run-a-builder/clone-and-build/

# Clone and Build the Signet Builder

The Builder simulates bundles and transactions to create valid rollup blocks and submits them to Ethereum.

## Prerequisites

## Recommended System Specs

* CPU: 0.5 vCPU (minimum 0.1 vCPU)
* Memory: 512MB (minimum 256MB)
* Clock speed: 2.8GHz+ (builder prefers clock speed over core count)

## Clone the Repository

```
git clone https://github.com/init4tech/builder
cd builder
```

## Build Options

### Local Build

The compiled binary will be available at `target/release/builder`.

### Docker Build

```
docker build -t builder:latest .
```

## Deployment

After building the Docker image:

1. Push to your container registry:

   ```
   docker push <registry>/builder:latest
   ```
2. Update your deployment manifests with the new image
3. Verify expected behavior in your target network

## Next Steps