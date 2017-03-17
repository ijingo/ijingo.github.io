---
layout: post
title: BlockBench - A Framework for Analyzing Private Blockchains
---

## TL;DR

We published Blockbench, the first evaluation framework for analyzing private blockchains. It serves as a fair means of comparison for different platforms and enables deeper understanding of different system design choices.

## What is Private Blockchain, Really?

A typical blockchain system consists of multiple nodes which do not fully trust each other. Some nodes exhibit Byzantine behavior, but the majority is honest. Together, the nodes maintain a set of shared, global states and perform transactions modifying the states. Blockchain is a special data structure which maintains the states and the historical transactions. All nodes in the system agree on the transactions and their order as stored on the blockchain. Because of this, blockchain is often referred to as a distributed ledger. Recent blockchain systems, e.g., Hyperledger, consider restricted settings wherein nodes are authenticated. Although Poof-of-Work is still useful in such permissioned environments, there are more efficient and deterministic solutions where node identities are known. Recent permissioned blockchains either use existing PBFT, as in Hyperledger, or develop their own variants, as in Parity, Ripple and ErisDB. Most of these systems support smart contracts, though in different languages, with different APIs and execution engines (see a more comprehensive comparison in the Paper). As a result, permissioned blockchains can execute complex application more efficiently than PoW-based blockchains, while being Byzantine fault tolerant. These properties and the commercial interests from major banking and financial institutions have bestowed on private blockchains the potentials to disrupt the current practice in data management.

## BlockBench Design & Implementation

We identify four abstraction layers found in all of these systems and design our workloads to target these layers. The consensus layer contains protocols via which a block is considered appended to the blockchain. The data layer contains the structure, content and operations on the blockchain data. The execution layer includes details of the runtime environment support blockchain operations. Finally, the application layer includes classes of blockchain applications.

![layers](http://vivaladb.com/images/blockchain_layer.png "Layers in a typical blockchain software stack.")

The following figure illustrates our Blockbench's implementation. To evaluate a blockchain system, the first step is to integrate the blockchain into the framework's backend by implementing IBlockchainConnector interface. The interface contains operations for deploying application, invoking it by sending a transaction, and for querying the blockchain's states. Ethereum, Parity and Hyperledger are current backends supported by Blockbench. A user can use one of the existing workloads to evaluate the blockchain, or implement a new workload using the IWorkloadConnector interface (we assume that the smart contract handling the workload's logic is already implemented and deployed on the blockchain). This interface essentially wraps the workload's operations into transactions to be sent to the blockchain. Specifically, it has a getNextTransaction method which returns a new blockchain transaction. Blockbench's core component is the Driver which takes as input a workload, user-defined configuration (number of operations, number of clients, threads, etc.), executes it on the blockchain and outputs running statistics.

![layers](http://vivaladb.com/images/blockbench.png "BlockBench software stack.")

Our benchmark is open sourced for public use, this [link](https://github.com/ooibc88/blockbench) is the GitHub repository. Our academic paper is accepted by SIGMOD 2017.

## Performance Benchmark

We selected Ethereum, Parity and Hyperledger for our study currently, as they occupy different positions in the blockchain design space, and also for their codebase maturity. We evaluate the three systems using both macro and micro benchmark workloads. Our main findings are

* Hyperledger performs consistently better than Ethereum and Parity across the benchmarks. But it fails to scale up to more than 16 nodes.

* Ethereum and Parity are more resilient to node failures, but they are vulnerable to security attacks that forks the blockchain.

* The main bottlenecks in Hyperledger and Ethereum are the consensus protocols, but for Parity the bottleneck is caused by transaction signing.

* Ethereum and Parity incur large overhead in terms of memory and disk usage. Their execution engine is also less efficient than that of Hyperledger.

* Hyperledger's data model is low level, but its flexibility enables customized optimization for analytical queries of the blockchain data.


