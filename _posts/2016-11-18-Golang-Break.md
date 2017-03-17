---
layout: post
title: Golang 的 break
---

Golang 提供了一种方便的 break 语义，可以允许在嵌套的循环里面从内层循环直接 break 出所有循环。

下面有三段代码的例子：

<script src="https://gist.github.com/ijingo/4ccb931a8fba341ed545602ea91ba4df.js"></script>

例子1是一段死循环。

<script src="https://gist.github.com/ijingo/71474a6d90371c4d165c5ebaeab3f10b.js"></script>

例子2中， break 只对内层的 switch 起了作用，但没有跳出外层的 for 循环。

<script src="https://gist.github.com/ijingo/1db19a8938c455be5f0949b8ecd2fb1f.js"></script>

例子3中的 break 将对标记了 LOOP 的 for 循环起作用，于是此段程序不再是一个死循环。
[Play it Online](https://play.golang.org/p/_b7jva0PjG).

