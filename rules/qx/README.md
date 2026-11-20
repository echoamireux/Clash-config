# Quantumult X 规则

`echo_personal.list` 是 Echo 配置个人分流规则与当前 Clash `my_direct.yaml`、`my_proxy.yaml` 的并集版本。
它不包含墨鱼配置自带的基础规则，也不重复包含 Apple Intelligence 和 YSP 这两个已有远程资源。

在 Echo 配置的 `[filter_remote]` 下添加：

```text
https://raw.githubusercontent.com/echoamireux/Clash-config/refs/heads/main/rules/qx/echo_personal.list, tag=Echo个人分流, update-interval=86400, opt-parser=false, inserted-resource=true, enabled=true
```

这个 list 使用 QX 原生格式，例如 `host-suffix`、`host`、`ip-cidr` 和 `host-keyword`。文件里包含多个策略，因此不要添加 `force-policy`，否则所有规则都会被强制改成同一个策略。

Clash 侧只维护两个 provider：`my_direct.yaml` 和 `my_proxy.yaml`。Clash 的 `MyProxy` 统一绑定到 `国际媒体`，所以 QX 中的 `proxy`、美国节点、国际媒体、自动选择和香港节点规则，在 Clash 中都会通过 `MyProxy` 走国际媒体；这是两种客户端策略模型不同造成的结果。

修改 list 后提交到 GitHub，QX 到达 `update-interval` 后会刷新；也可以在 QX 中手动更新远程资源。确认远程资源正常后，再从 Echo 的 `[filter_local]` 删除已经迁移到这个 list 的个人规则。
