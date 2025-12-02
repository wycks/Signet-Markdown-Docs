---
title: "Getting a Sequencer Signature"
source: "https://signet.sh/docs/bb-3f7d9e2a/customizing-a-builder/getting-a-sequencer-signature/"
---

# Source: https://signet.sh/docs/bb-3f7d9e2a/customizing-a-builder/getting-a-sequencer-signature/

# Getting a Sequencer Signature

Blocks must be cosigned by the Sequencer. The Sequencer blindly signs any number of candidate blocks for the current Builder via a simple API.

The Sequencer API accepts a [`SignRequest`](https://docs.rs/zenith-types/latest/zenith_types/struct.SignRequest.html) via a `POST` call to the `/signBlock` endpoint, and returns a [`SignResponse`](https://docs.rs/zenith-types/latest/zenith_types/struct.SignResponse.html). For details on calculating the `contents` hash, see the [rust builder example](https://github.com/init4tech/builder/blob/main/src/quincey.rs).

The sequencer is allowed to modify the returned copy of the `SignRequest`. This is to allow the sequencer to set a specific `gas_limit`. It currently does not modify the request before returning it, but may do so in the future.

## API Endpoint

**Request Body**: SignRequest JSON object
**Response**: SignResponse JSON object containing the sequencer’s signature