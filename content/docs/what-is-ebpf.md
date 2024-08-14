---
title: 什麼是eBPF
type: docs
prev: /docs
next: docs/structure/
---

## 起因 - SDN實作的困難

{{< youtube Wb_vD3XZYOA >}}

因為當時Kernel內的BPF只能實作SDN中的Bridging, Switching等功能，所以就有志願者出來進行BPF的擴充，就成了現在的eBPF。

現在的eBPF比起原本的BPF(Berkerley Packet Filter)，更像是一個可以彈性掛載到Kernel上的Kernel Module，但是有較多的限制。
(e.g. 所有使用者執行的BPF程式都需要通過 [verifier.c](https://github.com/torvalds/linux/blob/master/kernel/bpf/verifier.c) 的測試才能在Kernel內執行。)

## eBPF vs BPF
- Note: 原本的BPF依然存在，它們兩個是並存在Kernel裡的。

| 差異 | 原BPF | eBPF |
| :---: | :---: | :---: |
| 執行方式 | VM(Sandbox) | VM(Sandbox) |
| 功能 | 有限的功能，基本上你只能過濾封包 | 基本上什麼都能做 |
| 用途 | 主要是網路封包處理 | 基本上成了弱化版本的Kernel Module |
| 安全性 | 靠編譯器在編譯時檢查 | 靠verifier.c在執行時檢查，過了才能載入Kernel內執行 |
| 採用率 | 普通 | 從Android手機到企業Server幾乎都有 |
| 使用者 | 主要是網路工程師 | 所有想擴充Kernel功能的開發者  |
| 方便性 | 不容易實作，要對Kernel有很深的認識 | 更加容易使用，因為有更高階的Abstraction |
| 創新性 | 有限 | 只要使用者想得到，都可以寫入eBPF程式內 |
