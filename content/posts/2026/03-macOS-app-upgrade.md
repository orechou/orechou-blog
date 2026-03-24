---
title: 如何管理 macOS 应用更新
date: 2026-03-24 20:00:00 +0800
tags:
  - macOS
categories:
  - macOS
---

我目前的主力生产电脑是 2023 年的 MacBook Pro，配置是 M2 Max，64GB 内存版本。我是一名 AI 软件工程师，所以平时折腾、安装各种软件也是高频的操作，并且我对数字产品有着更新洁癖：即总想要把所有的设备、以及设备中的软件都更新到最新的系统、版本。

## 安装渠道
对于 macOS 的软件安装我制定了以下的优先级：
1. 如果有网页版就使用网页版，不安装本地客户端；例如 ChatGPT、Google 日历等。
2. 如果 AppStore 支持下载，优先使用 AppStore 安装；例如 WeChat、Feishu 等；
3. 如果 homebrew 支持下载，其次使用 brew 安装；例如 Claude Code、Chrome 等；

除此之外的不考虑安装（除非是有调研需求，必须要尝试的除外）。按照这个规则，基本能够满足大部分的软件安装使用需求。

## 更新方式
我希望时刻保持软件最新。

对于 AppStore 安装的软件，因为 AppStore 的更新推送是"尽力而为"的后台机制，不是实时推送。因为你总要进到 AppStore 里面去主动刷新看是否有更新。这个操作路径实在是太复杂了。所以我安装了 mas (Mac App Store command-line interface)这个工具，它可以通过命令行指令的方式，来触发 AppStore 软件更新下载。

对于 homebrew 安装的软件就更好办了，直接通过 brew 指令完成更新。

最后，将所有的指令组合打包，实现一个命令完成所有软件的更新下载。在 zsh 或者 bash 的配置文件做这样一行设置：
```
alias appupgrade="mas list && mas upgrade && brew update && brew outdated && brew upgrade && brew cu -a -y && brew cleanup"
```

上面重命名了一个叫 appupgrade 的指令，它组合了 mas 和 brew 的软件更新。效果如下：
![](https://orechou.oss-cn-shenzhen.aliyuncs.com/images/appupgrade.png)

这样，我每天只要使用电脑的时候，在命令行中执行一下 appupgrade，就能保证所有的软件是最新的了。
