**English** | [中文](https://p3terx.com/archives/cloudflare-warp-configuration-script.html)

# Cloudflare WARP Installer

A Bash script that automatically installs and configures CloudFlare WARP in Linux, connects to WARP networks with WARP official client or WireGuard.

## Features

- Automatically install CloudFlare WARP Official Linux Client
- Quickly enable WARP Proxy Mode, access WARP network with SOCKS5
- Automatically install WireGuard related components
- Configuration WARP IPv4 Network interface (with WireGuard)
- Configuration WARP IPv6 Network interface (with WireGuard)
- Configuration WARP Dual Stack Network interface (with WireGuard)
- ...

## Requirements

*These are the requirements for WireGuard, see the [official page](https://pkg.cloudflareclient.com/packages/cloudflare-warp) for the CloudFlare WARP client requirements.*

Supported distributions:

- Debian >= 10
- Ubuntu >= 16.04
- Fedora
- CentOS
- Oracle Linux
- Arch Linux
- Other similar distributions

Supported platform architecture:

- x86(i386)
- x86_64(amd64)
- ARMv8(aarch64)
- ARMv7(armhf)

## Usage

```bash
bash <(curl -fsSL git.io/warp.sh) [SUBCOMMAND]
# or
wget git.io/warp.sh
bash warp.sh [SUBCOMMAND]
```

### Subcommands

```
install         Install Cloudflare WARP Official Linux Client
uninstall       uninstall Cloudflare WARP Official Linux Client
restart         Restart Cloudflare WARP Official Linux Client
proxy           Enable WARP Client Proxy Mode (default SOCKS5 port: 40000)
unproxy         Disable WARP Client Proxy Mode
wg              Install WireGuard and related components
wg4             Configuration WARP IPv4 Global Network (with WireGuard), all IPv4 outbound data over the WARP network
wg6             Configuration WARP IPv6 Global Network (with WireGuard), all IPv6 outbound data over the WARP network
wgd             Configuration WARP Dual Stack Global Network (with WireGuard), all outbound data over the WARP network
wgx             Configuration WARP Non-Global Network (with WireGuard), set fwmark or interface IP Address to use the WARP network
rwg             Restart WARP WireGuard service
dwg             Disable WARP WireGuard service
status          Prints status information
version         Prints version information
help            Prints this message or the help of the given subcommand(s)
menu            Chinese special features menu
```

### Example

- Install and automatically configure the Proxy Mode feature of the WARP client, enable the local loopback port 40000, and use an application that supports SOCKS5 to connect to this port.
    ```
    bash <(curl -fsSL git.io/warp.sh) proxy
    ```

- Install and automatically configure WARP IPv6 Network (with WireGuard)，Giving your Linux server access to IPv6 networks.
    ```
    bash <(curl -fsSL git.io/warp.sh) wg6
    ```

- This Bash script is also a good WireGuard installer.
    ```
    bash <(curl -fsSL git.io/warp.sh) wg
    ```

## Credits

- [Cloudflare WARP](https://1.1.1.1/)
- [WireGuard](https://www.wireguard.com/)
- [ViRb3/wgcf](https://github.com/ViRb3/wgcf)

## License

[MIT](https://github.com/P3TERX/warp.sh/blob/main/LICENSE) © **[P3TERX](https://p3terx.com/)**

## Notice of Non-Affiliation and Disclaimer

We are not affiliated, associated, authorized, endorsed by, or in any way officially connected with Cloudflare, or any of its subsidiaries or its affiliates. The official Cloudflare website can be found at https://www.cloudflare.com/.

The names Cloudflare Warp and Cloudflare as well as related names, marks, emblems and images are registered trademarks of their respective owners.


前言
Cloudflare WARP 一键安装脚本（简称： WARP 脚本，英文名：Cloud­flare WARP In­staller）是一个简化在 Linux VPS 云服务器上安装和配置 Cloud­flare WARP 的脚本，支持 Cloud­flare WARP 官方 Linux 客户端 SOCKS5 代理和 WARP Wire­Guard 网络接口等多种 WARP 使用方式的一键部署，适用于 IPv4/​IPv6 单双栈各类的网络环境，操作系统、 CPU 架构和虚拟化平台支持全面。本篇是介绍说明及简单使用教程。

Cloud­flare WARP 是什么？能干什么？以及这个脚本的实现原理知识和其它周边配套设置参见《Cloudflare WARP 给 Linux VPS 云服务器添加原生 IPv4/IPv6 双栈网络》。

项目地址
https://github.com/P3TERX/warp.sh

支持本项目欢迎随手点个 star，可以让更多的人发现、使用并受益。你的支持是持续开发维护的动力。

脚本特点
系统支持：Debian、Ubuntu、Fedora、CentOS、Rocky Linux、Oracle Linux、Arch Linux 等大部分现代主流 Linux 发行版
CPU 架构支持：x86(i386)、x86_64(amd64)、ARMv8(aarch64)、ARMv7(armhf) 等
虚拟化平台支持：KVM、Xen、OpenVZ、LXC 等
无需更换 Linux 内核，更稳定、更安全、更自由
智能识别网络方案并自动匹配最佳配置方案进行部署
内置独家配置方案和优化算法，能获得更快、更好的 WARP 网络体验
直观的进程状态、网络状态和 WARP 状态显示功能
Cloudflare WARP 官方 Linux 客户端支持
“一把梭”式极致体验

基础使用
首先使用 SSH 工具连上 VPS 。AD: 还没有 VPS ？赶紧点这里去选一个吧！

以下两种模式按照自己的需求二选一，二者功能是独立的。

WARP WireGuard 网络接口模式
WARP Wire­Guard 网络接口模式，是指通过第三方 WARP 工具 (ViRb3/wgcf) 所生成的通用 Wire­Guard 配置文件创建名称为 wgcf 的 Wire­Guard 网络接口的方式去连接 WARP 网络。按照自己的需求执行以下命令即可，整个过程将自动进行，几种网络状态可自由切换。

无论 VPS 是 IPv4 还是 IPv6 又或都有，添加 WARP Wire­Guard 双栈全局网络，直接使用以下 WARP 脚本命令一把梭：

# 自动配置 WARP WireGuard 双栈全局网络
bash <(curl -fsSL git.io/warp.sh) d
添加或更改 IPv4/​IPv6 网络中的一个出口走 WARP Wire­Guard 网络，使用以下 WARP 脚本命令一把梭：

# 自动配置 WARP WireGuard IPv4 网络
bash <(curl -fsSL git.io/warp.sh) 4

# 自动配置 WARP WireGuard IPv6 网络
bash <(curl -fsSL git.io/warp.sh) 6
其它相关命令：

# 查看 WARP 脚本子命令列表
bash <(curl -fsSL git.io/warp.sh) help

# 重启 WARP WireGuard 网络接口
systemctl restart wg-quick@wgcf

# 禁用 WARP WireGuard 网络接口
systemctl disable wg-quick@wgcf --now
WARP 官方 Linux 客户端 SOCKS5 代理模式
Cloud­flare WARP 官方 Linux 客户端的 Proxy Mode 功能可以让应用通过本地的 SOCKS5 代理端口去直接使用 WARP 网络。

TIPS: WARP 官方 Linux 客户端目前只支持在 x86_64(amd64) CPU 架构的 De­bian 10/​11、Ubuntu 18~22、Cen­tOS 8 (及其它 RHEL 8 系) 系统中使用。其它发行版也许能正常安装，但可能存在无法正常启动的问题。官方客户端由于受疫情影响开发进度缓慢，还有很多小问题待解决，目前只建议作为备用方案。
使用以下命令一把梭后将自动安装 WARP 官方客户端并开启 SOCKS5 代理端口 (127.0.0.1:40000)：

# 自动配置 WARP 官方客户端 SOCKS5 代理
bash <(curl -fsSL git.io/warp.sh) s5
如果觉得官方客户端不好用，那么一把梭干掉它：

# 卸载 WARP 官方 Linux 客户端
bash <(curl -fsSL git.io/warp.sh) uninstall
WARP 脚本功能菜单
给喜欢功能菜单的小伙伴特别准备的功能，执行以下命令显示功能菜单和贴心的状态显示：

# Cloudflare WARP 一键配置脚本 功能菜单
bash <(curl -fsSL git.io/warp.sh) menu
TIPS: 随着 WARP 脚本的更新，此菜单可能会随时有变动。

进阶使用
WARP 脚本的一些彩蛋及高级进阶功能的使用方法。还没写完，咕咕咕...

备份重要配置文件（WireGuard 模式）
接触 WARP 比较早的小伙伴可能还记得当年 Cloud­flare 通过更新算法直接导致了所有第三方工具失效，所以记得备份。

目前 WARP 脚本通过调用 ViRb3/wgcf 自动申请 WARP 账户信息 (wgcf-account.toml) 并生成通用 Wire­Guard 配置文件 (wgcf-profile.conf)，脚本自动配置完成后会原样保存至 /etc/warp 目录 (注意备份)，以便下次脚本自动调用，同时也避免了重复申请 WARP 账号导致 IP 被 Cloud­flare 拉黑 (429 Too Many Requests)。

使用已有配置文件（WireGuard 模式）
若之前有生成过带有 WARP+ 流量的配置文件，又或者之前使用过其它古早第三方 WARP 工具或脚本生成过 Wire­Guard 配置文件，只要符合 Wire­Guard 配置文件标准即可。

方法一：恢复之前的备份/etc/warp目录后执行 WARP 脚本。
方法二：将配置文件命名为wgcf-profile.conf并上传至 VPS ，并在此配置文件所在目录执行 WARP 脚本。
脚本会截取关键信息生成符合所选网络方案的新配置文件 (/etc/wireguard/wgcf.conf) 以便 Wire­Guard 调用。

注意事项和其它说明
WARP 脚本允许 WARP 官方 Linux 客户端与 WARP WireGuard 网络同时开启，但在 WG IPv4 或 WG 双栈全局模式下，因官方客户端默认走 IPv4 出口，WARP 客户端的网络数据可能会走在 WARP WireGuard 隧道中，这属于套娃行为，不仅减速效果非常明显，而且官方会限制这种行为并导致网络不稳定，所以并不建议这样使用。
OpenVZ 或 LXC 的 VPS 需要先启用 TUN/TAP 功能，一般在网页管理面板开启，不明白请自行咕鸽搜索开启方法，否则 WARP WireGuard 模式会启动失败。不要再问为什么不能用了，都什么年代了还不整一个全功能带内核级加速的 KVM VPS ？相同的价格，更好的体验：高性价比便宜 VPS 传送门点此
遇到问题如何处理
部分已知问题由于篇幅过长已经转移至《Cloudflare WARP 一键安装脚本已知问题和解决方法》这篇文章中，遇到问题可以先看看。
遇到问题请在 WARP 脚本的 GitHub issues 页面进行反馈(顺便点个星)，提供虚拟化平台、系统版本、内核版本以及从脚本运行到末尾的详细日志或其它有用的信息，以便分析问题原因改进脚本。若未提供有用信息一律当做垃圾信息删除
重启、重装、重买是解决问题的三大法宝。
写在最后
Cloudflare WARP 一键安装脚本从方案设计到代码编写全部都是由博主原创，花费了大量时间和精力打磨而成，最初只是自己使用，觉得达到了近乎完美的状态也就开源分享了出来。如果觉得这个脚本对你有帮助，可以去 WARP 脚本的 Github 项目页面 随手点下 Star 点亮小星星支持一下，Star 越多，更新越快，你的支持就是我维护的更新维护动力。希望小伙伴们多多分享，让更多的人看到。

相关推荐
Cloudflare WARP 给 VPS 服务器额外添加 IPv4 或 IPv6 网络获得“原生”IP
使用 HE Tunnel Broker 给 IPv4 VPS 免费添加公网 IPv6 支持
国外便宜高性价比和免费白嫖 VPS 推荐
本博客已开设 Telegram 频道，欢迎小伙伴们订阅关注。

本文作者：P3TERX

本文链接：https://p3terx.com/archives/cloudflare-warp-configuration-script.html
