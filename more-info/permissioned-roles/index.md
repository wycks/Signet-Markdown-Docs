---
title: "Permissioned Roles"
source: "https://signet.sh/docs/more-info/permissioned-roles/"
---

# Source: https://signet.sh/docs/more-info/permissioned-roles/

# Permissioned Roles

Signet’s smart contracts use a system of permissioned roles to manage access control. Each contract has specific roles that can perform certain administrative functions.

## Core Roles

### Sequencer Admin

The `sequencerAdmin` role manages the list of authorized sequencers in the Zenith contract. This role can:

* Add or remove sequencers
* Update sequencer configuration
* Pause sequencing if needed

### Sequencer

The `sequencer` role is responsible for validating and co-signing blocks before they are submitted to the Zenith contract. Sequencers:

* Validate blocks from builders
* Co-sign valid blocks
* Ensure blocks follow the protocol rules

### Gas Admin

The `gasAdmin` role in the Transactor contract manages gas-related parameters for force-included transactions. This role can:

* Update gas price limits
* Adjust gas estimation parameters
* Configure gas subsidies

### Token Admin

The `tokenAdmin` role in the Passage contract manages which tokens can be bridged between chains. This role can:

* Add new supported tokens
* Update token configuration
* Set bridge limits for specific tokens

## Role Management

All permissioned roles are managed through a secure access control system. Role transitions are transparent and logged on-chain through events. This provides auditability while allowing the protocol to evolve over time.