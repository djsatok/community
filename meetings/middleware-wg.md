# Middleware Work Group Agenda and Notes
This thread contains agenda and/or summary of the regular Middleware sync meeting. Please propose agenda items through the PRs and Issues.

## 25.03.2020

### Agenda
High-level focus is closing the Mainnet release.
Story points:

Max Z - 18. 2 story points a week.
Evgeny K - 31. 4 story points a week.
Vlad F - 6 + explorer + block production debug
Alexey F - 10

* Evgeny K: Refactoring of TrieKeys, not sure we can do accout hashing without iterators. Vesting contracts are blocked on staking contract (Illia P is working on it). Token standard is done and in review;
* Nikolay I: Onboarding, getting familiar with Rust&codebase, and looking into fee estimator. Alexey F can hehlp with runtime questions;
* Alexey F: Fixing panics in runtime storage, the other issues assigned in Zenhub;
* Vlad F: In nearcore, b58 decoding issue. Cleaning up RPCs. Misterwhite's request to have different error codes;
* Anton B: Spec, Ethprover fixes, light client;
* Max Z: Disabling transfers, blocked by staking delegation (Illia P). Genesis content. Other things from ZenHub.

## 18.03.2020

### Agenda
High-level focus:
* Evgeny K: Vesting contract (vesting and lockups are two contracts now. Lockups are missing tests), Borsh perf improvements (almost done), updated token standard, Hashing of account ids and columns changes (stuck on migration script. Need to sync up with Bowen W);
* Anton B: Spec, Ethprover fixes, light client;
* Max Z: Learning eth-bridge, debugging EVM;
* Vlad F: Finished P0 for misterwhite, working on P1 issues for RPC label (reviewed by Evgeny K). Adding regression tests for RPC (changes API is taking a lot of time). Illia P brought up seat price in RPC. Benchmarking of RPC;
* Alexey F: Finished early version of runtime documentation. Still working on 1131, 1804, 1795.

### Notes
* Please comment on https://github.com/nearprotocol/NEPs/issues/40 ;
* Evgeny K: we need to come up with the process on how we propose and argue about NEPs. Checkout bitcoin proposal guidelines. It should be referring to our core principles and goals;
* Vlad F noticed that queries that touch non-tracking shard are extremely slow;
* Alexey F suggests that the refund is using current gas price instead of gas price attached to the receipt. Alexey F needs to create an issue.

## 11.03.2020

### Agenda
High-level focus:
* Evgeny K: Vesting contract, Borsh perf improvements, Hashing of account ids (some forward compatibility changes), columns changes (since we have fixed size keys now);
* Anton B: Working on spec with Sherif https://github.com/nearprotocol/NEPs/pull/38, verifiers QA (Ethprover), light client;
* Max Z: Turning off iterators. Light client and chain stability;
* Vlad F: Documentation for changes API https://github.com/nearprotocol/docs/issues/173 ; P0 changes for misterwhite (expose touched accounts in the block); further improvements of changes API to allow batch request for list of accounts (less critical). Needs to test through Python integration tests;
* Alexey F: deduct used gas at the very end of contract execution (also double check that our promise fee remains correct). RPC issues;

### Notes
* Anton B, Evgeny K: Multicontract requires scope that's too large and runtime is currently frozen. Let's revisit after the launch;
* Anton B, Alexey F: Let's consider instantiation ids for the contract given upon deployment, similarly to create2 in Eth. Let's revisit if after the launch. This will enable us the "sharded" contract architecture. Create commonwealth thread or NEPs;
* Vlad F: Too many work items. Alexey F to help;
* Alexey F: An idea to have a global gas counter living through the entire transaction/receipt lifetime;
* Vlad F, Alexey F: We don't need to expose used gas, because error messages already expose them;
* Evgeny K: Created PoW faucet, see https://near-examples.github.io/pow-faucet/ ;


## 04.03.2020

### Agenda

High-level focus:
1. Evgeny K: Making sure state iterators are working correctly and hide them from the contracts (some changes needed for AS), vesting contract (requested by misterwhite);
2. Anton B: Working on Eth-bridge with Sherif, more testing for eth-proof after cross-contract calls change by Evgeny K, finishing token example, fixing CI (for now omitting MacOS because of the docker problem);
3. Vlad F: Finishing misterwhite P0s (had to bulk multiple issues in one fix, which delayed P0s), wants to implement test suite in Rust (Python test suite is not flexible enough for changes API), maintenance of explorer;
4. Alexey F: working on 1131, 1804, 1795, also re-examining every error in the runtime, compiling list of scenarios for each error;
5. Max Z: Addressing Evgeny K' comments on metadata and Borsh schema, and ramping up on the chain stability issues;



### Notes

We have de-prioritized everything non-critical in runtime, including:
* Safes: https://github.com/nearprotocol/NEPs/pull/26
* The following storage rewrite: https://github.com/nearprotocol/nearcore/pull/2050



Explorer:
* We want to create business opportunities for people to build explorer-like backends on us;
* Ideally, we should not be running publicly available explorer backend because people will start building dependencies on it, and which would require from us guaranteeing the uptime. However for now it is fine to make it publicly available, and we will decide later what to do once backend is starts getting spammed.

## 26.02.2020

### Agenda

High-level focus:
1. Anton B: Eth bridge, adding token examples, fixing verifiers, contracts calls, documentation;
2. Evgeny K: Improving contract development experience: contract examples, gas profiling, safes (Alexey F), adding more features to near-bindgen (e.g. no std);
3. Evgeny K, Alexey F: Revisit runtime label on Zenhub;
4. Max Z: Borsh schema needs to be adjusted according to Vlad G comments. Need help from Applayer;
5. Mikhail K: Rewriting and stabilizing state storage. Max Z and Vlad F to onboard;
6. Vlad F: RPC/API issues with documentation;
7. Vlad F: Explorer backend/Node indexing discussion (Note from Anton F. Might address data-availability issue).

## 19.02.2020

### Agenda

High-level team focus:
1. Improving safety, DevX, performance of the Eth<> Near bridge;
2. Improving contract development experience: safes, contract examples, gas profiling, adding more features to near-bindgen (e.g. no std);
3. Introducing Borsh everywhere, need help from Applayer;
4. Rewriting and stabilizing state storage;
5. RPC/API issues with documentation.

### Notes
* Evgeny K: Need some fixes for Applayer as part of (3);
* Alexey F: Users do not know what is happening to transaction after they have submitted it. Max Z: Look at https://github.com/nearprotocol/nearcore/issues/1880 and https://github.com/nearprotocol/NEPs/pull/1 ;