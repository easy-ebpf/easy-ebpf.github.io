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
{{< cards >}}
  {{< card link="https://codespaces.new/easy-ebpf/tutorial-minimal-example?quickstart=1" title="在GitHub Codespace中開啟LAB" icon="github" >}}
{{< /cards >}}

點進去之後，點擊 `Create new codespace` 即可開啟 LAB 環境:
![](https://github.com/user-attachments/assets/7742f70d-2cac-43ea-b364-0306ece1c9ea)

進入之後，可能要先等他跑一下，等左邊的檔案都有正常顯示出來之後:
![](https://github.com/user-attachments/assets/5f62db35-c9e4-4684-a5a8-8db6d68abf4b)

就可以打開 `README.md` ，並依照上面的指示，進行實驗的操作。

Note: 在 LAB 的環境裡，`README.md` 裡的指令是可以直接點左邊的播放鍵執行的:
![](https://github.com/user-attachments/assets/f43dc45c-53be-40eb-9fe6-a8cd75bbf6ae)

如果沒有看到的話，可能是外掛還沒有裝完，等一下再開一次 `README.md` 這個檔案就會出現了。
