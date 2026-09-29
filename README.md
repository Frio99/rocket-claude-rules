# Shadowrocket Claude DNS 配置

复制下面的地址，在 Shadowrocket 的「配置」页点击右上角 `+`，粘贴地址并下载：

```text
https://raw.githubusercontent.com/Frio99/rocket-claude-rules/main/shadowrocket-claude-dns.conf
```

下载后添加自己的代理节点或订阅，选中可用节点，再把 `shadowrocket-claude-dns.conf` 设为使用中的配置并重新连接。配置文件**不包含节点、订阅地址或账号凭据**。

这份配置保留了原有的国内直连、国外代理分流，并把 Claude 相关域名优先交给代理。主 DNS 使用 Google DoH，备用使用 Cloudflare DoH，均经当前代理节点转发；关闭系统 DNS 回退和 IPv6，劫持常见的硬编码 53 端口 DNS，并拦截已知 HTTPDNS。微信的两个解析端点仍直连。

局域网、部分 Apple 域名和配置中明确直连的流量有例外，因此一次 DNS 检测结果不能代表所有 App 的行为。HTTPDNS 拦截也可能影响个别 App 的加载；出现问题时可切回原配置或为该服务单独添加例外。此配置不能保证第三方服务账号的可用性。

## 打开网站明显变慢时

严格版会让 DNS 查询经过代理，可能增加网页首次打开的等待时间。可试用[速度优先版](https://raw.githubusercontent.com/Frio99/rocket-claude-rules/main/shadowrocket-claude-dns-balanced.conf)，它只将明确走 `DIRECT` 的域名改用系统 DNS，其他 DNS 设置和 Claude 代理规则保持一致。请在**同一个节点、同一个网络**下分别测试两版。速度优先版可能让本地运营商 DNS 出现在检测结果中；如果目标是不出现本地 DNS，请继续使用上面的严格版。

若两版都慢，检查 Shadowrocket 是否处于「配置」路由模式，并换一个延迟较低的节点测试。下载速度慢通常不是 DNS 设置造成的。

## 来源与授权

本配置基于 [Johnshall 的 `lazy.conf`](https://github.com/Johnshall/Shadowrocket-ADBlock-Rules-Forever/blob/release/lazy.conf) 修改。新增了 Claude 专属规则，并参考 [LingJingMaster 的 Shadowrocket 配置](https://github.com/LingJingMaster/Shadowrocket-Rules/blob/main/Shadowrocket.conf)调整 DNS、IPv6、53 端口劫持及 HTTPDNS 处理。HTTPDNS 规则集链接指向 [blackmatrix7 的规则](https://github.com/blackmatrix7/ios_rule_script/blob/master/rule/Shadowrocket/BlockHttpDNS/BlockHttpDNS.list)，规则集本身不存放在本仓库。

本仓库中的衍生配置按 [Creative Commons Attribution-ShareAlike 4.0 International](https://creativecommons.org/licenses/by-sa/4.0/) 共享，保留原作者署名，并注明了修改内容。本仓库不会自动同步上游配置的更新。
