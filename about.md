---
layout: page
title: about
permalink: /about/
---

Hi there! This is WANG Ji (王冀), a second year M.Sc. candidate from [Database System Research Group](http://www.comp.nus.edu.sg/~dbsystem/) at [School of Computing (SoC)](http://www.comp.nus.edu.sg), [National University of Singapore](http://www.nus.edu.sg/). I am supervised under [Prof. Beng Chin Ooi](http://www.comp.nus.edu.sg/~ooibc/). My resume [here.](http://www.vivaladb.com/uploads/resume-wangji.pdf) My Chinese version resume [here.](http://www.vivaladb.com/uploads/resume-wangji-zh.pdf)

-------

### Projects
#### [BlockBench: A Framework for Analyzing Private Blockchains](http://www.comp.nus.edu.sg/~dbsystem/blockbench/index.html)
*C++, Golang, Shell, Node.js, Python*

BlockBench is the first general benchmarking test suite for private or permissioned
blockchain platforms. BlockBench includes a set of macro-benchmark to give a overview
of performance of private blockchains, as well as a set of micro-benchmark to test each
layer of blockchain platform independently, i.e. consensus layer, data model layer
and smart-contract execution layer. This benchmark suite is open sourced for public
use. Now it can support Hyperledger fabric, Ethereum and Parity. I designed and
implemented the workload driver and blockchain connector. Its academic paper is
accepted by SIGMOD 2017.

#### [UStore: Distributed, Scalable, Universal Datastore](http://www.comp.nus.edu.sg/~dbsystem/ustore/)
*C++, ZeroMQ, Protobuf*

UStore is a distributed storage system ultilizing data branching functionality, providing
immutability, data sharing and security properties to the upper-layer applications. It
supports flexible built-in data structures (e.g., List, Map, Set, Blob, String and Int).
The features of this system is sourced from Git and Blockchain. It supports versioning
control, branching and collaborative operation like Git, also supports immutable and
tamper-proof data structure like Blockchain. We creatively combine characters from
B-tree and Merkle-tree as our indexing structure. The system also embraces modern
hardware trends such as RDMA to gain high performance. This project is closed-
sourced and under construction for the present. Its related paper is submitted to
USENIX ATC 2017 under peer review.

#### COHANA: Cohort Analysis Query Processing Engine
*Java, Python/Django, Javascript*

COHANA is a data analytics engine built for Cohort Analysis query processing. It
supports both traditional cohort analysis and generalized cohort analysis query. Different from traditional relational databases such as MySQL, COHANA utilizes column-
oriented data storage. It is able to process queries directly on compressed data. It can
leverage multiple encoding schemes such as Run-Length Encoding and Dictionary-
based Encoding. Its related paper is accpted by VLDB 2017. I mainly take part in the
front-end visualization module for this system.

#### [SINGA: A Distributed Deep Learning Platform](http://singa.incubator.apache.org/)
*C++, Cuda, CuDNN, SWIG, CMake, Protobuf, Python*

SINGA is an Apache Incubator open source, distributed training platform for deep learning models, and is designed based on three principles: usability, scalability and extensiblity. SINGA supports a variety of popular deep learning models e.g. Convolutional Neural Network (CNN), Recurrent Neural Network (RNN) and Restricted Boltzmann Machine (RBM). SINGA architecture is sufficiently flexible to run synchronous, asynchronous and hybrid training frameworks both on CPU cluster and GPU cluster. I join the project since August 2015.

-------

### Personal Projects

#### [MapReduce in Go](https://github.com/ijingo/mapreduce_go)

*Golang, Parallel & Distribtued Computing*

A prototype of MapReduce framework implemented using Go RPC. This framework
supports two modes, i.e., Sequential and Distributed. Under Sequential mode, all sub
tasks run on Master process sequentially which is easy to debug. Under Distributed
mode, Master process schedules all sub-tasks on Worker processes that are registered on
the Master. To achieve fault-tolerance, When a Worker fails, the Master can re-assign
the sub-task to other available Workers.

-------

### Publications

* Anh Dinh, **Ji Wang**, Gang Chen, Rui Liu, Beng Chin Ooi and Kian-Lee Tan. **BLOCKBENCH: A Framework for Analyzing Private Blockchains.** Accepted by **SIGMOD 2017**.

* Anh Dinh, **Ji Wang**, Sheng Wang, Gang Chen, Chin Wei Ngan, Qian Lin, Beng
Chin Ooi, Kian-Lee Tan, Pingcheng Ruan, Zhongle Xie, Hao Zhang and Meihui Zhang.
**UStore: A Distributed Storage With Rich Semantics.** Submitted to USENIX ATC 2017,
under peer review.

### Contact

Mail: [jiwang.cs@gmail.com](mailto:jiwang.cs@gmail.com)

Witter: [@ijingobravo](https://twitter.com/jingobravo)

Weibo: [@一头乱码的Jingo](http://weibo.com/ijingo)

Blog: [Viva La Data Bases!](http://vivaladb.com)

GitHub: [@ijingo](https://github.com/ijingo)
