---
hip: \${XYZ}
title: Extend isAuthorized to process current transaction in HAS System Contract
author: Brendan Graetz <@bguiz>
working-group: Nana Essilfie-Conduah <@nana-ec>, Luke Lee  <@lukelee-sl>
type: Standards Track
category: Service
needs-council-approval: Yes
status: Draft
last-call-date-time: 2023-\${MM}-\${DD}T16:00:00Z
created: 2023-08-21
discussions-to: https://github.com/hashgraph/hedera-improvement-proposal/discussions/\${XYZ}
updated: 2023-08-21
requires: 632
---

## Abstract

<!-- a short (~200 word) description of the technical issue being addressed. -->

HIP-632 adds a new system contract, `hederaAccountService` that exposes a method `isAuthorized(address, messageHash, signatureBlob)`. This HIP proposes a similar version of that which implements the same functionality, but restricted for use *only* on the current (in flight) transaction. This would expose a method `isAuthorizedCurrentTransaction()`.

## Motivation

<!-- The motivation is critical for HIPs that want to change the Hedera codebase or ecosystem. It should clearly explain why the existing specification is inadequate to address the problem that the HIP solves. HIP submissions without sufficient motivation may be rejected outright. -->

`hederaAccountService.isAuthorized(address, messageHash, signatureBlob)` works for the following scenarios:

- When an account's admin key is "simple", and is comprised of either a single EdDSA key, or a single ECDSA key
- When an account's admin key is "complex", and is comprised of multiple EdDSA keys and/or  ECDSA keys, combined using one or more `KeyList`s or `ThresholdKey`s.

`hederaAccountService.isAuthorized(address, messageHash, signatureBlob)` does **not** work for the following scenarios:

- When an account's admin key is "complex", and is comprised of multiple EdDSA keys and/or  ECDSA keys and/or smart contract IDs, combined using one or more `KeyList`s or `ThresholdKey`s.

The proposed `hederaAccountService.isAuthorizedCurrentTransaction()` method aims to fulfil the above scenario, and specific use cases pertaining to this scenario will be elaborated upon in the [use cases section](#use-cases) below.

Furthermore, Hedera Token Service exposes an authorization mechanism already,
which is capable of handling this scenario that is presently unfulfilled by Hedera Account Service.
<!-- TODO links/ references that demonstrate this in HTS -->

> NOTE:
> "EdDSA" refers to **EdDSA ED25519**, and
> "ECDSA" refers to **ECDSA secp256k1** throughout this HIP, unless otherwise stated.
> These are the only types of cryptographic keys currently supported by Hedera's account system.

## Rationale

<!-- The rationale fleshes out the specification by describing why particular design decisions were made. It should describe alternate designs that were considered and related work, e.g., how the feature is supported in other languages. The rationale should provide evidence of consensus within the community and discuss important objections or concerns raised during the discussion. -->

## User stories

<!-- Provide a list of “user stories” to express how this feature, functionality, improvement, or tool will be used by the end user. Template for user story: “As (user persona), I want (to perform this action) so that (I can accomplish this goal).” -->

## Specification

<!-- The technical specification should describe the syntax and semantics of any new features. The specification should be detailed enough to allow competing, interoperable implementations for at least the current Hedera ecosystem. -->

## Backwards compatibility

<!-- All HIPs that introduce backward incompatibilities must include a section describing these incompatibilities and their severity. The HIP must explain how the author proposes to deal with these incompatibilities. HIP submissions without a sufficient backward compatibility treatise may be rejected outright. -->

## Security implications

<!-- If there are security concerns in relation to the HIP, those concerns should be explicitly addressed to make sure reviewers of the HIP are aware of them. -->

## How to teach this

<!-- For a HIP that adds new functionality or changes interface behaviors, it is helpful to include a section on how to teach users, new and experienced, how to apply the HIP to their work. -->

## Reference Implementations

<!-- The reference implementation must be complete before any HIP is given the status of “Final”. The final implementation must include test code and documentation. -->

## Rejected Ideas

<!-- Throughout the discussion of a HIP, various ideas will be proposed which are not accepted. Those rejected ideas should be recorded along with the reasoning as to why they were rejected. This both helps record the thought process behind the final version of the HIP as well as preventing people from bringing up the same rejected idea again in subsequent discussions. In a way, this section can be thought of as a breakout section of the Rationale section that focuses specifically on why certain ideas were not ultimately pursued. -->

## Open Issues

<!-- While a HIP is in draft, ideas can come up which warrant further discussion. Those ideas should be recorded so people know that they are being thought about but do not have a concrete resolution. This helps make sure all issues required for the HIP to be ready for consideration are complete and reduces people duplicating prior discussions. -->

Nil

## References

<!-- A collection of URLs used as references through the HIP. -->

- [HIP-632 - Hedera Account Service (HAS) System Contract](../hip-632)
- [`ecrecover` Precompiled Contract](https://ethereum.github.io/execution-specs/autoapi/ethereum/frontier/vm/precompiled_contracts/ecrecover/index.html)

## Copyright/license

This document is licensed under the Apache License, Version 2.0 -- see [LICENSE](../LICENSE) or [`https://www.apache.org/licenses/LICENSE-2.0`](https://www.apache.org/licenses/LICENSE-2.0)