---
title: eBPF程式架構
weight: 2
type: docs
prev: docs/what-is-ebpf
next: docs/structure/minimal-example-with-lab
sidebar:
  open: true
---

eBPF的運作方式如下:
![](https://imgur-backup.hackmd.io/i7b3DkP.png)

簡單來說，eBPF程式的bytecode被注入到Kernel內之後，就是靠map在跟userspace裡的程式進行溝通，以達成更好的功能整合。
而eBPF有四種主要的形式(不包含xdp, cgroup之類的):
1. `kprobes`: 綁定eBPF程式至指定的Kernel-space函式上。 
2. `uprobes`: 綁定eBPF程式至指定的User-space函式上。 
3. `tracepoints`: 綁定eBPF程式至特定某些Kernel Event上，並取得該Event的詳細資料。 
4. `perf_events`: 綁定eBPF程式至指定的Kernel Event上，並快速的取得統計數據。 

接下來我們會使用一個簡單的例子介紹一個完整的eBPF程式架構。
