---
id: overall_architecture
title: PlatON Overall Architecture
sidebar_label: PlatON Overall Architecture
---

## PlatON Overall Architecture

### Overall Logical Structure

<img src="https://platonnetwork.github.io/Docs/en-us/Introduction/PlatON_overall_solution.assets/overall_logical_architecture.png" alt="overall_logical_architecture"/>

In addition to providing the underlying chain, PlatON also provides open source implementations of a wallet, a block browser, and a node management tool:

- ATON Wallet - A mobile wallet that supports hot and cold wallet, transaction and delegation. The private key is managed on the client, and Keyshared (a key management system based on threshold signature) is subsequently supported.
- PlatScan Block Browser - The official block browser provided by PlatON
- Node Tool

### Logical Structure

<img src="https://platonnetwork.github.io/Docs/en-us/Introduction/PlatON_overall_solution.assets/logical_architecture.png" alt="logical_architecture"/>

PlatON's Layer1 consensus network layer is based on the Ethereum skeleton. The core components have been completely rewritten, and some new components have been extended:

- Cryptographic algorithm: In addition to the SHA256Hash algorithm and ECDSA signature algorithm that have been used since Bitcoin, PlatON also adds BLS as aggregate signature for consensus, VRF for random election of validators, and ZKP and HE for privacy preserving.
- P2P network: Instead of using the popular libp2p and devp2p libraries, PlatON implements RELOAD (REsource LOcation And Discovery) protocol defined by RFC6940  and ReDiR(Recursive Distributed Rendezvous) service discovery mechanism defined by RFC7374.
- Account model and data storage: Following Ethereum's account model, state data is stored in the Patricia tree. Due to the large amount of data, PPoS-related data is stored in the Patricia tree with poor performance. It is not stored in the Patricia tree, but is stored separately in another SNAPDB that does not store historical status.
- Consensus mechanism: use BFT-style PoS consensus mechanism. PPoS is a DPoS mechanism with VRF. The randomness introduced by VRF can endogenously curb the expansion of staking pools and ensure the decentralization and security. PlatON's CBFT consensus mechanism is a three-phase pipelining consensus protocol that and produce and verifies batch blocks in parallel, thereby improves the consensus efficiency. 
- Smart contract: Support EVM and WASM virtual machine at the same time,  and support mainstream programming languages such as Solidity, C ++, Java, Python. A modified version of Truffle is provided to support the development of Solidity and C ++ contracts.
- DAPP SDK: Based on Ethereum's WEB3 (supports Javascript, Java, Python, Swift languages) and JSON RPC, it is modified according to the function of PlatON. In addition, a more efficient GRPC-based interface has been added.

Layer2 extends complex computing to off-chain and implements Privacy-Preserving Computing protocols through off-chain Secure Multi-Party Computation.

- Cryptographic algorithm: Verifiable Computation (VC) algorithm can implement the non-interactive proof of off-chain computing scale solution. The privacy computing protocol is implemented by combining Secure Multi-Party Computation (MPC), secret sharing (SS), and homomorphic encryption (HE).
- MPC virtual machine: The privacy contract is compiled into the LLVM IR and executed in the MPC VM implemented through the LLVM JIT. The privacy calculation protocols including MPC, SS, and HE have been built into the MPC VM to reduce the size of the LLVM IR compiled from the privacy contract.
-  Computing specific hardware: Computing specific hardware based on FPGA/ASIC can greatly improve computing performance and reduce computing power.
- Privacy computing and data exchange protocol: A computing protocol that enables collaborative computing and results verification without revealing the original data.
- Privacy-Preserving Computing Framework: A development framework that encapsulates Privacy-Preserving Computing and data exchange protocols, including a privacy AI development framework based on a Privacy-Preserving Computing protocol.

### Network Structure

<img src="https://platonnetwork.github.io/Docs/en-us/Introduction/PlatON_overall_solution.assets/network_structure.png" alt="network_structure"/>

#### Basic Network

PlatON's basic blockchain network is mainly composed of the following types of nodes, which are connected by P2P:

In general, we can divide node into two types: full nodes and light(weight) nodes. Full nodes verify block that is broadcast onto the network. Full nodes that preserve the entire history of transactions are known as full archiving nodes.Light nodes, in contrast, do not verify every block or transaction and may not have a copy of the current blockchain state. They rely on full nodes to provide them with missing details.

- Light Nodes
Light nodes do not verify every block or transaction and may not have a copy of the current blockchain state. They rely on full nodes to provide them with missing details.

- Full Nodes
Full nodes verify block that is broadcast onto the network. That is, they ensure that the transactions contained in the blocks (and the blocks themselves) follow the rules defined in the PlatON specifications.  All full nodes will have to replay all the transactions to ensure that they arrive at the correct, agreed-upon next state of the blockchain.

- Archive Nodes
Full nodes that preserve the entire history of transactions are known as full archiving nodes.

- Bootstrap Nodes
The new node joins the PlatON network and first connects to the bootstrap node and discovers other nodes.

- Validator Nodes
Responsible for production and verify blocks, validator nodes are randomly selected through PPoS + VRF, and run the CBFT protocol for consensus.

#### Decentralized Application

To deploy DAPP applications (including blockchain), the following servers need to be deployed in the intranet environment:

- Full node
This node must connect to mainnet or testnet of PlatON. The P2P port of the node can be exposed to the internet, but the RPC port is not recommended to be exposed to the internet. 

- DAPP server
The DAPP server is connected to the local full-node RPC port, monitor transactions, events, and blocks on the chain. At the same time, the DAPP server is also connected to the original business system of the enterprise.

#### Validator pool

The validator pool deploys multiple validator nodes, and it is recommended to connect to the internet through a public front-end full node. For specific security deployment solution, see [validator deployment](#validator-deployment).

#### Operations platform

The Operations platform synchronizes all blocks, transactions, and events through a full node and perform monitoring.

#### PlatScan Block Browser

The PlatScan block browser synchronizes all blocks, transactions, and events through a full node, and displays data such as blocks and transactions. The PlatScan block browser requires the following servers to be deployed:

- Full node: RPC port allows only data processing server access
- Data processing server
- Database server
- WEB server
- Push server

#### ATON wallet server

ATON is a mobile wallet which implements key management, signing transactions forwarded to the chain through the ATON server. The data including transaction, block, validator on the chain are synchronized by the ATON server through the full node and pushed to the mobile client. ATON wallet server needs to deploy the following servers:

- Full node: RPC port allows only data processing server access
- Data processing server
- Database server
- WEB server
- Push server

### Validator Deployment

<img src="https://platonnetwork.github.io/Docs/en-us/Introduction/PlatON_overall_solution.assets/node_deployment.png" alt="node_deployment"/>

Appropriate measures should be taken to ensure the security of validator for running stably: 
- RPC ports of full node and validator node are closed.
- The validator node is not exposed on the Internet and communicates through non-validator full nodes.
- Each validtor node should have at least 2 public full nodes and 2 non-public full nodes. The IPs of the public full nodes can be exposed on the Internet. The IPs of the non-public full nodes are only exposed  to other reliable validator nodes and are not exposed on the Internet to avoid DDoS attacks.
- Prevent network-wide scanning to locate highly-defensive servers. Modify the port 9876 (the same as RPC 8888) to ports 80, 443, or 22. This can effectively increase the cost of attacker positioning.

