# 红果短剧 for macOS

> **非官方、独立实现**的开源 macOS 短剧客户端，仅供学习交流。

原生 SwiftUI 实现，无 WebView。通过本地 Hummingbird 网关解析公开网页数据并统一代理播放流量（剥离 Referer 以适配 CDN），AVPlayer 播放，SwiftData 持久化收藏与观看进度。

## 功能

- **浏览**：发现 / 排行榜 / 探索三分区，分类芯片 + 无限分页，⌘F 搜索
- **详情页**：真实渲染封面、标签、选集、相关推荐
- **个人库**：收藏、观看历史、秒级断点续播
- **播放器**：倍速（0.5–3.0x）、自动连播、画中画、老板键（⌘⇧H 一键隐藏+暂停）、系统媒体控制、选集面板、查找其他季
- **Mac 原生**：Dark Mode、原生菜单与快捷键（Space 播放暂停 / ⌘↩ 全屏 / ⌘←→ 切集）、网关健康检查

## 系统要求

- macOS 14.0 或更高版本
- 当前发行包为 **Intel（x86_64）** 构建；Apple Silicon 可自行编译（见下文）

## 下载安装

前往 [Releases](https://github.com/g-star1024/hongguo-mac/releases/latest) 下载 `.dmg` 或 `.zip`。

当前包为 **ad-hoc 签名、未公证**，首次打开会被 Gatekeeper 拦截，任选其一：

1. 在 `访达` 中**右键点击 App → 打开**，再点「打开」；
2. 或在终端执行（按实际安装路径调整）：

```bash
xattr -cr "/Applications/红果短剧.app"
```

各版本文件 SHA-256 见对应 Release 说明，下载后建议核对。

## 从源码构建

```bash
git clone https://github.com/g-star1024/hongguo-mac.git
cd hongguo-mac
swift build                      # 开发构建
./Scripts/build-app-bundle.sh    # 组装 .app + zip + dmg（ad-hoc 签名）
```

Apple Silicon 上可出 arm64 或 universal 包：

```bash
ARCH=arm64 ./Scripts/build-app-bundle.sh
# ARCH=universal 需在 Apple Silicon 上执行
```

依赖：Swift 6 工具链（Xcode 16+）、macOS 14 SDK。纯 SPM 项目，无 .xcodeproj。

## 架构一览

```
HongguoCore        数据模型 / 网页解析（SwiftSoup）/ HTTP 客户端 / 配置
HongguoGatewayCore Hummingbird 2 本地网关（127.0.0.1:8787，播放流量收口）
HongguoGateway     网关独立可执行入口
HongguoDesktopMac  SwiftUI 界面 / SwiftData 持久化 / 播放器 / 系统集成
HongguoMacApp      App 可执行入口（打包脚本装入 .app）
```

## 声明

- 本项目不存储、不分发任何影视内容，所有数据来自公开网页的实时解析，内容的版权归各自权利方所有。
- 本项目仅供学习交流使用，请勿用于商业用途。
- 环境要求：本地网关仅监听 `127.0.0.1`，不对外提供服务。
- 使用本软件产生的一切后果由使用者自行承担。

## 反馈

问题或建议请[提交 Issue](https://github.com/g-star1024/hongguo-mac/issues/new)。
