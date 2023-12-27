---
hip: <HIP number (this is determined by the HIP editor)>
title: Add EVM Support for new non-blob Cancun opcodes
author: Danno Ferrin (@shemnon)
working-group: // TBD
type: Standards Track 
category: Core 
needs-council-approval: Yes
status: Draft 
created: // TBD
discussions-to: // TBD
updated: <comma separated list of dates>
requires: <HIP number(s)>
replaces: <HIP number(s)>
superseded-by: <HIP number(s)>
---

## Abstract

Update the Hedera EVM to add support for new Opcodes found in the Cancun fork of Ethereum Mainnet, namely TSTORE, TLOAD, and MCOPY 

## Motivation

Hedera's goal of Ethereum Equivalence also includes the requirement to stay up-to-date with the current state of Ethereum Mainnet.  This HIP addresses new opcodes added to the EVM that do not address any features relating to Blobs, or the Consensus Layer, or changes to existing opcodes.

## Rationale

The opcodes discussed in this HIP only exist within the EVM and do not interact with any novel features of ethereum mainnet.  It is expected that future versions of solidity will support both implicit and explicit use of these opcodes.  Because of that we need to support them as specified.  

## User stories

* As a smart contract author, I want to be able to use transient storage features of solidity in my hedera smart contracts.
* As a smart contract author, I want to be able to use future versions of solidity that may use memory copying implicitly, like what happened with the `PUSH0` operation.
* As a smart contract author, I want to be able to explicitly use the memory copy features solidity may expose in future releases.
  
## Specification

### EVM Implementation

Two EIPs define the operational semantics of the added opcodes.  For the transient storage opcodes `TSTORE` and `TLOAD` they are defined in [EIP-1153](https://eips.ethereum.org/EIPS/eip-1153).  For the `MCOPY` operation they are defined in [EIP-5656](https://eips.ethereum.org/EIPS/eip-5656).

The specified opcodes are to be implemented identically to Ethereum Mainnet and as specified in their respective EIPs.  This includes opcode numbers, gas schedules, stack semantics, and new facilities such as transient storage added to the execution frame.

### Hedera Activation

The operations will be added into a new EVM version of Hedera (notionally version 0.50, but subject to change), like the versions added for Shanghai support (v 0.38) and Paris support (v 0.34).  There will be multiple HIPs rolled into this EVM version.

## Backwards Compatibility

The core EVM library shipping with Hedera as of version 0.46 already contains the needed EVM support.  The activation will add a new Hedera EVM version that will activate all the Cancun support in one release. 

## Security Implications

Because the operations are being brought in with identical semantics there are no security risks above those already present from existing Ethereum Equivalence changes.

## How to Teach This

Any smart contract tutorials will want to examine the possibility of adding sample contracts showcasing the use of transient storage and easy memory copying.  Ideally these could be sourced from existing Ethereum Tutorials as the features are fairly well anticipated in the Ethereum community.  

## Reference Implementation

// TBD

## Rejected Ideas

No ideas were rejected around these three opcodes, aside from not supporting Cancun features.

The idea of supporting [EIP-4788](https://eips.ethereum.org/EIPS/eip-4788): Beacon block root in the EVM was rejected because there is no EL/CL separation in Hedera.  If we wanted to support similar hash storage ideas we would want to mine a different address.

## Open Issues

While a HIP is in draft, ideas can come up which warrant further discussion. Those ideas should be recorded so people know that they are being thought about but do not have a concrete resolution. This helps make sure all issues required for the HIP to be ready for consideration are complete and reduces people duplicating prior discussions.

## References

* [EIP-1153](https://eips.ethereum.org/EIPS/eip-1153): Transient storage opcodes
* [EIP-5656](https://eips.ethereum.org/EIPS/eip-5656): MCOPY - Memory copying instruction

## Copyright/license

This document is licensed under the Apache License, Version 2.0 -- see [LICENSE](../LICENSE) or (https://www.apache.org/licenses/LICENSE-2.0)