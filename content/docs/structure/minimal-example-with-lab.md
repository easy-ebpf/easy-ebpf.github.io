---
title: 簡單的eBPF程式
type: docs
prev: docs/structure/
---

## 範例
- https://eunomia.dev/tutorials/1-helloworld/#hello-world-minimal-ebpf-program
```c
/* SPDX-License-Identifier: (LGPL-2.1 OR BSD-2-Clause) */
#define BPF_NO_GLOBAL_DATA
#include <linux/bpf.h>
#include <bpf/bpf_helpers.h>
#include <bpf/bpf_tracing.h>

typedef unsigned int u32;
typedef int pid_t;
const pid_t pid_filter = 0;

char LICENSE[] SEC("license") = "Dual BSD/GPL";

SEC("tp/syscalls/sys_enter_write") // 見下圖
int handle_tp(void *ctx)
{
 pid_t pid = bpf_get_current_pid_tgid() >> 32;
 if (pid_filter && pid != pid_filter)
  return 0;
 bpf_printk("BPF triggered sys_enter_write from PID %d.\n", pid);
 return 0;
}
```

## 說明
這個程式的目的為追縱 syscall 中 `write` 的呼叫，並且在每次偵測到時，都印出呼叫該 syscall 的 PID (Process ID) 。
而因為我們這次需要的資訊不多，不需要資訊像是寫入檔案的位置，所以我們只需要使用 `tracepoint` 即可。
這個程式使用了 `tracepoint` 種類的eBPF程式去偵測了 `syscalls` 中的 `sys_enter_write` 的呼叫:
![image](https://github.com/user-attachments/assets/6e22759d-702e-4fb4-8d20-787a8275e3f4)


並且在被觸發時，如果觸發程序 PID 不為 0，就會使用 `bpf_printk` 這個 helper function 印出訊息。


## 實作
我們可以在下面的 LAB 進行測試這個偵測的結果(請先[注冊GitHub](https://github.com/join)):
(LAB LINK)

點進去之後，點擊 `Create Codespace` 即可開啟 LAB 環境:
(圖)

進入之後，可以依照顯示出來的 Visual Studio Code 裡的 `README.md` 進行操作。
