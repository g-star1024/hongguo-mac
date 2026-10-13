# DramaCube macOS (Swift) CI 打包发布仓
#
# 本仓用于承载 Swift 原生 macOS 版的 GitHub Actions 构建与 Release 发布。
# 源码在私有仓 [hongguo-desktop](https://github.com/g-star1024/hongguo-desktop)，
# 本仓 workflow 用 PAT checkout 后构建，Actions 免费（公开仓）。
#
# 发版：
#   gh workflow run build.yml -R g-star1024/hongguo-mac -f ref=main -f version=2.3.6
#
# 参数：ref=源码 ref（main / mac-vX.Y.Z / commit）、version=版本号、arch=universal|arm64|x86_64
name: hongguo-mac
