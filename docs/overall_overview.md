---
id: overall_overview
title: Overview
sidebar_label: Overview
---

## Overview

### WEB3 Computing Infrastructure
With the rapid growth of the Internet, the Internet giants represented by FAANG and BAT, by virtue of their technological monopoly status, have collected and stored enormous user data. And with the use of big data and AI, they are enjoying data monopoly and acquiring huge business benefits. Users not only fail to obtain data dividends, but also bear the risk of personal privacy being violated and personal data being abused.

WEB3 is a serverless Internet and a decentralized network. In this Internet, users have full ownership of their own data, and no one or any organization can use their data without permission. But it also brings the following problems:

- Any individual can only get hold of a small subset of the massive amount of data. It is impossible for any entity to stream the whole set of data valuable to them, handicapping their full grasp of the landscape. Every participant of the digitalized world is partially blind, blocked in a certain angle towards the full picture. 
- Participants are weakly trusted or even untrusted, and they cannot use "trusted third parties" for data collection and validity verification, as well as the sharing of value, information and assets. Emerging cloud computing platforms are now typical "trusted third party".

PlatON is committed to building the next generation of Privacy-Preserving Computing and data exchange networks in the WEB3 era. Based on modern cryptography and blockchain technology, PlatON creates a new computing paradigm to maintain privacy of the client’s data without the need to rely on third parties for collaborative computing and Verify the integrity of the results.

<img src="https://platonnetwork.github.io/Docs/en-us/Introduction/PlatON_overall_solution.assets/overall_architecture.png" alt="overall_architecture"/>

### Scalable Privacy-Preserving Computing

#### Blockchain: Consensus-based Strategy

<img src="https://platonnetwork.github.io/Docs/en-us/Introduction/PlatON_overall_solution.assets/consensus_based_computing.png" alt="consensus_based_computing"/>

In a broad sense, the existing blockchain architecture is a consensus-based schemes, which also implements a simple computation protocol based on smart contract. To assure correctness the computation must be replicated by all the nodes, manifesting the intrinsic contradiction between efficiency and trustlessness.

Driven by practicality, the blockchain industry focuses on two issues: scalability and privacy.

**Scalability** is still a huge challenge for the blockchain. The mainstream blockchain is not highly-effective in processing transactions per second, which is several orders of magnitude different from the processing power required to run mainstream financial markets. Although there are hundreds of projects addressing scalability issues through various solutions which are limited to the "impossible triangle" at the expense of decentralization or security. In consensus-based schemes, smart contract is limited to support simple computing logic.

**Privacy** is another major issue of blockchain. Although the blockchain's advantages such as immutability, decentralization, and no trust are tempting, it also faces the same dilemma of obtaining data as big data and AI technologies. Neither companies nor individuals have the willingness to share private information, or post to public ledges that will be freely read by governments, family, colleagues and business competitors without restriction.

#### PlatON: Non-interactive Proof Privacy-Preserving Computation

PlatON uses modern cryptographic algorithms including but not limited Zero-Knowledge Proof (ZKP), Verifiable Computation (VC), Homomorphic Encryption (HE), Secure Multi-Party Computation (MPC), Secret Sharing (SS), etc. to implement non-interactive proof computation scale solution.

##### Scalability

The scalability problem of the existing blockchain architecture is mainly due to the tight coupling of consensus and computing. PlatON's scheme based on verifiable computing uses cryptographic algorithms to weaken their endogenous binding relationship, thereby fundamentally decoupling consensus and computing.

<img src="https://platonnetwork.github.io/Docs/en-us/Introduction/PlatON_overall_solution.assets/laye2_computing_network.png" alt="laye2_computing_network"/>



To avoid the trade off in efficiency, people in the industry have increasingly come to an agreement: the proper use of blockchain is for verification only; the computing tasks must be separated from the consensus layer and migrated off-chain, but the untrusted off-chain is new problem.  PlatON's Verifiable Computation (VC) cryptographic algorithm passes trust off-chain. Through verifiable computation, the contract only needs to be processed off-chain once, and all nodes can quickly verify the correctness, on the one hand, it improves the transaction processing performance, and on the other hand, it makes PlatON support complex contracts.

##### Privacy

On PlatON, MPC and HE are combined to achieve complete privacy-preserving computing, ensuring the privacy of input data and the computation logic. Compared to trusted computing that relies on the trusted hardware or TEE (such as SGX) provided by a third-party manufacturer for computational integrity, trustless computing on PlatON relies only on falsifiable cryptographic assumptions, and thus during its life, it provides unprecedented private data security without trust boundaries.

