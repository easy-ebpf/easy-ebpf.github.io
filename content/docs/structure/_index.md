---
title: eBPF程式架構
weight: 2
type: docs
prev: docs/what-is-ebpf
next: docs/structure/leaf
sidebar:
  open: true
---

eBPF的運作方式如下:
![](https://imgur-backup.hackmd.io/i7b3DkP.png)

簡單來說，eBPF程式的bytecode被注入到Kernel內之後，就是靠map在跟userspace裡的程式進行溝通，以達成更好的功能整合。
而eBPF有四種主要的形式(不包含xdp, cgroup之類的)

接下來我們會講到四種不同的eBPF程式。
