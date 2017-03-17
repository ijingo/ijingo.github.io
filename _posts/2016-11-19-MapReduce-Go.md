---
layout: post
title: 用 Go 实现 MapReduce
---

[MapReduce](https://zh.wikipedia.org/wiki/MapReduce) 是 Google 十年前提出的一个并行计算框架，将很多分布式计算任务抽象成为 Map 和 Reduce 两个算子，由系统自动处理任务调度、容错，简化了并行计算任务编程的复杂度。本篇文章介绍一个 MapReduce 计算框架的 Go 语言简单实现。本文中涉及的源代码保存在 [此 Github Repo](https://github.com/ijingo/mapreduce_go) 中。

## 系统概要
系统由 `Master` 和 `Worker` 两个主要模块构。`Worker` 向 `Master` 注册 (Register) 之后， `Master` 可以将任务 (tasks) 分配给 `Worker`，并且 `Master` 可以在某一个 `Worker` 失效后自动分配一个新的 `Worker` 重新进行刚刚失败的任务。

实现了 `Sequential` 和 `Distributed` 两种计算方式。`Sequential` 模式下 `Master` 将所有的 Mapper 和 Reducer 在本地顺序执行，可以用于 Debug。`Distributed` 模式下 `Master` 会把任务分配给远程的 `Worker`。

和原论文不太一致的地方是，本系统依赖于 `Master` 和 `Worker` 共享文件系统 (类似于 NFS、AFS、HDFS 之类的文件系统)，用以共享各个阶段的输入输出文件。比如 Mapper 产生的中间文件，在原论文中 Mapper 产生的中间文件保存在执行 Map 函数的 Worker 上，再由下一阶段的 Reduce Worker 拉取到本地，而本系统需要一个共享的文件路径。

本例中实现了 word count 和 inverted index 两个经典的计算任务。

## 实现细节

### 数据结构设计

#### Master

<script src="https://gist.github.com/ijingo/159e200af937f60b975b7dbb060902bf.js"></script>

`address` 保存 `Master` 自身的地址； `registerChannel` 里面保存着现在可以使用的 `Worker` 的地址； `doneChannel` 在所有子 task 完成后会被设置； `workers` 保存着所有注册过的 `Worker` 的地址，用于最后广播关闭所有 `Worker` 时使用。

`jobName`、`files`、`nReduce` 是每个任务的配置， Mapper 个数与输入文件个数相同（即 `len(files)`)。

#### Worker

<script src="https://gist.github.com/ijingo/e6c66a25de6e4e272e13c6b7e3ed0a75.js"></script>

`Worker` 启动时会设置本数据结构，`nRPC` 记录了本 `Worker` 接收到了多少 RPC 调用。

### RPC 接口设计

#### Master

`Master` 有 `Register()` 和 `Shutdown()` 两个 RPC API。`Worker` 通过 `Register()` 将自己的地址注册给 `Master`，`Master` 还提供一个 `Shutdown()` API 用于关闭 `Master` 的 RPC Server。

<script src="https://gist.github.com/ijingo/d563e6e523eabe543c25ae77cd780deb.js"></script>

#### Worker

`Worker` 同样有两个 RPC API，分别是 `DoTask()` 和 `Shutdown()`。`Master` 通过调用 `DoTask()` 给 `Worker` 安排计算任务，使用 `Shutdown()` 来关闭 `Worker`

<script src="https://gist.github.com/ijingo/dc74f99c9ebfbf3760f53d6041a4c4cf.js"></script>

### Scheduler 设计

`Master` 端进程还会负责分配、调度子任务，当 `DoTask()` 这个 RPC 失效时 `Master` 自动选择另一个闲置的 `Worker` 来重新尝试计算此子任务。当 `Worker` 成功完成了一个子任务之后，会被重新加入 `regsiterChannel` 中等待下一个任务。

<script src="https://gist.github.com/ijingo/8bf4ba05b8264f77c7b4a48d6835a724.js"></script>

### doMap() 与 doReduce()
在 `Distributed`　模式下，由　`Worker` 运行着两个函数来完成计算；在 `Sequential`　模式下，　`Master` 自身依次调用这两个函数来完成计算。

`doMap()` 和　`doReduce()` 实际都是读取（解析）输入文件并保存在内存中，调用用户自定义的 `MapF` 或　`ReduceF` 变换读取后的文件内容，然后将变换结果转存为输出文件，因此这两个函数的主要工作是文件操作。`doMap()` 会把每一个　Mapper 对应的输入文件处理后存为 nReduce 份，相当于做了一个 Shuffle，本实现中使用的是 hash partition，而 `doReduce()` 会把所有对应的中间文件组合起来输出最终的结果。

<script src="https://gist.github.com/ijingo/85989514557cfd0cdbff9ed8d9ba6b41.js"></script>

## 实例

实际使用时接口非常简便，只需要根据任务要求自定义相应的 `MapF` 和 `ReduceF`。

### word count

<script src="https://gist.github.com/ijingo/ed8e281d952f5d9f812fed2ea718bc31.js"></script>

### inverted index

<script src="https://gist.github.com/ijingo/d1ba42507fab820aff30a61507e51447.js"></script>

## References
* Dean, Jeffrey & Ghemawat, Sanjay (2004). MapReduce: Simplified Data Processing on Large  Clusters
* MIT 6.824 Lab 1 MapReduce, https://pdos.csail.mit.edu/6.824/labs/lab-1.html
