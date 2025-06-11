# cfworker-vless-nat64

在 CF Workers 部署 VLESS 代理脚本最新 NAT64 版

### 对比其它传统脚本有巨大优势：

### 1. 此版本无需 ProxyIP 无需 SOCKS 无需 VPS 可直接访问 CF 网站！

### 2. 此版本永远固定 IP 不跳 IP！不管是访问 CF 网站还是非 CF 网站，落地 IP 均相同且固定不变！下载/直播不会中断！

### 3. 此版本长期可用不失效！部署一次长期可用！无需频繁更新 IP / ProxyIP！

---

## 快速部署

1. 在 CF Worker 控制台中创建一个新的 Worker

2. 把 [worker.js](https://github.com/77889977/cfworker-vless-nat64/blob/main/_worker.js) 的全部内容粘贴到 Worker 代码编辑器中

3. 将第 2 行 `userID` 修改成你自己的 UUID（或通过环境变量配置）

4. 访问 `https://你的项目域名/你设置的UUID` 即可获取 VLESS 链接（默认优选 10 个 CFIP/域名）

5. V2ray 客户端开启分片(Fragment)使用，或绑定自定义域使用

不会的话可参考其它类似项目，部署和使用的方式都是差不多的。

## 环境变量配置

| 变量作用 | 变量名称| 变量值要求| 变量默认值| 变量要求|
| :--- | :--- | :--- | :--- | :--- |
| UUID (可以看作是密码) | `uuid` |符合 uuid 规定格式 |uuid 格式：`12345678-1234-1234-1234-123456789012`|**建议立即修改!**|
| NAT64 前缀 (可以看作是落地IP) | `nat64prefix` |公共 NAT64 地址的前缀(不带"/96")|Ztvi 公共 NAT64：`2602:fc59:11:64::`|**保持默认即可**|

### 原理说明：

**客户端** ---*优选IP/域名*--> **Worker** ---*IPv6*--> **Public NAT64** ---*IPv4*--> **目标网站(CF/非CF网站)**

所以落地 IP 为 **公共 NAT64 的 IPv4**，从而实现固定 IP 不跳。

### 缺点以及注意事项：

公共 NAT64 地址没多少个，所以能选的落地 IP 不多，寻找更多公共 NAT64 地址在 [nat64.xyz](https://nat64.xyz) 上有，更多的请自行网上搜索，懒人小白用默认就行

## 鸣谢/开源代码引用

- [zizifn edgetunnel](https://github.com/zizifn/edgetunnel)
- [3Kmfi6HP EDtunnel](https://github.com/6Kmfi6HP/EDtunnel)

免责声明：所有代码来源于Github社区。本项目仅供测试目的。在下载和使用本项目代码时，必须遵守使用者所适用的法律和规定。使用者有责任确保其行为符合所在地区的法律规章制度及其他相关规定。
