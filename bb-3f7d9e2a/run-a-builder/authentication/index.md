---
title: "Authentication"
source: "https://signet.sh/docs/bb-3f7d9e2a/run-a-builder/authentication/"
---

# Source: https://signet.sh/docs/bb-3f7d9e2a/run-a-builder/authentication/

# Authentication

## Overview

Authentication will be required for the following behaviors:

* Getting a sequencer co-signature on a built block.
* Retrieving bundles from the bundle relay.

Authentication will be performed using a standard OAuth2 client credential grant and then the access token you receive can be used to authorize all requests to the sequencer and bundle relay.

## OAuth Identity Provider Reference

### Havarti

## Authenticating Using `curl`

First off a basic example of getting an OAuth2 access token and using it to authenticate any of our secured API’s

### Obtain an Access Token

Make a POST request to the token endpoint with your client credentials.

```
curl --request POST \
  --data grant_type=client_credentials \
  --data client_id=${CLIENT_ID} \
  --data client_secret=${CLIENT_SECRET} \
  --data audience="https://transactions.pecorino.signet.sh"
  https://auth.havarti.signet.sh/realms/master/protocol/openid-connect/token
```

### Use the Access Token to Call Protected APIs

Once you receive the access token, include it in the `Authorization` header as a Bearer token.

The `access_token` that is returned should be base64 encoded, and should remain base64 encoded when passed via the `Authorization` header

```
ACCESS_TOKEN="your_access_token"

curl -H "Authorization: Bearer $ACCESS_TOKEN" \
  https://transactions.pecorino.signet.sh
```

**Parameters:**

* `-H "Authorization: Bearer $ACCESS_TOKEN"`: Sets the `Authorization` header with the access token stored in an environment variable

## Authenticating in Rust

### Prerequisites

Add the following dependencies to your `Cargo.toml` file:

```
[dependencies]
oauth2 = { version = "4" }
reqwest = { version = "0.11", features = ["json", "native-tls"] }
tokio = { version = "1", features = ["full", "macros", "rt-multi-thread"] }
```

### Example Code

```
use oauth2::basic::BasicClient;
use oauth2::{AuthUrl, ClientId, ClientSecret, TokenResponse, TokenUrl};
use oauth2::reqwest::async_http_client;
use reqwest::Client;
use std::env;
use tokio;

#[tokio::main]
async fn main() -> Result<(), Box<dyn std::error::Error>> {
    // Retrieve client ID and secret from environment variables
    let client_id = ClientId::new(
        env::var("CLIENT_ID").expect("Missing CLIENT_ID environment variable"),
    );
    let client_secret = ClientSecret::new(
        env::var("CLIENT_SECRET").expect("Missing CLIENT_SECRET environment variable"),
    );

    // OAuth2 provider URLs
    let auth_url = AuthUrl::new("https://auth.havarti.signet.sh/authorize".to_string())?;
    let token_url = TokenUrl::new("https://auth.havarti.signet.sh/oauth/token".to_string())?;

    // Set up the OAuth2 client
    let client = BasicClient::new(
        client_id,
        Some(client_secret),
        auth_url,
        Some(token_url),
    );

    // Perform the client credentials grant
    let token = client
        .exchange_client_credentials()
        // Add the required `audience` param
        .add_extra_param("audience", "https://transactions.pecorino.signet.sh")
        .request(async_http_client)?;

    let access_token = token.access_token().secret();

    // Use the access token to make an API call
    let api_client = Client::new();

    let response = api_client
        .get("https://transactions.pecorino.signet.sh/get-bundles")
        .bearer_auth(access_token)
        .send()
        .await?;

    Ok(())
}
```