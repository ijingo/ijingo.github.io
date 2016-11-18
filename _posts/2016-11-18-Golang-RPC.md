---
layout: post
title: Golang HTTP/TCP RPC 的简单实用
---

[远程过程调用](https://zh.wikipedia.org/zh-cn/%E9%81%A0%E7%A8%8B%E9%81%8E%E7%A8%8B%E8%AA%BF%E7%94%A8)(Remote Procedure Call, RPC)，
是在分布式系统中一个比较重要的概念，是一种进程间(inter-process)通信的实现方式。
对于客户端进程来说，调用服务端进程提供的 Remote Procedure 就好像在调用本地方法一样。RPC 提供了很好的透明性(transparency)，大大简化了分布式程序编程的复杂性。

Golang 的 [net/rpc package](https://golang.org/pkg/net/rpc/) 提供了一套 RPC 的方法，本篇博文提供两个简单的例子，分别使用 HTTP 和 TCP 建立连接。


# Data Structure Definition

本例中提供了两个远程方法，都是关于简单的数值运算，分别是整数乘法和整数除法。

首先定义所需要的数据结构。

<script src="https://gist.github.com/ijingo/8337553301f0de90b237d2a473c16886.js"></script>


# HTTP RPC Server & Client

## Server

<script src="https://gist.github.com/ijingo/6a4e052534b845e08bbe3f2d5dcaceee.js"></script>

在 Server 程序中实现上面定义的两个方法，经过注册(`server.Register()`)之后客户端可以根据方法名字来进行匹配。

## Client

<script src="https://gist.github.com/ijingo/1347c5abf314a8c3a725bafa86c79a4b.js"></script>


# TCP RPC Server & Client

## Server

<script src="https://gist.github.com/ijingo/1f2307181c1a6e8d43af2dd3c42f673b.js"></script>

## Client

<script src="https://gist.github.com/ijingo/e7e58a09361416112c43ce3197a5318d.js"></script>
