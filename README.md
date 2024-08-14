# Easy eBPF教學網頁

[![Deploy Hugo site to Pages](https://github.com/easy-ebpf/easy-ebpf.github.io/actions/workflows/pages.yaml/badge.svg)](https://github.com/easy-ebpf/easy-ebpf.github.io/actions/workflows/pages.yaml)

- 如果要修改內容，請先Fork，改完Push上去之後再提交PR。

## 線上修改文件內容

- [GitHub Codespaces](https://github.com/codespaces) 
    
    建立一個新的codespace並按照 [本地開發](#本地開發) 的指示開啟預覽。 

## 本地開發

Pre-requisites: [Hugo](https://gohugo.io/getting-started/installing/), [Go](https://golang.org/doc/install) and [Git](https://git-scm.com)

```shell
# Clone the repo
git clone git@github.com:easy-ebpf/easy-ebpf.github.io.git easy-ebpf

# Change directory
cd easy-ebpf

# Start the server
hugo mod tidy
hugo server --logLevel debug --disableFastRender -p 1313
```

## 參考資料:
- https://eunomia.dev/tutorials/1-helloworld/
- https://docs.cilium.io/en/latest/bpf/toolchain/#development-environment
- https://blog.cloudflare.com/live-patch-security-vulnerabilities-with-ebpf-lsm
- https://ebpf-go.dev/concepts/loader/#collectionspec
