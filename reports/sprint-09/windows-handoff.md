# Sprint 09 Windows 交接记录

2026-11-24，Windows 本机从 ToDesk 传入的 ZIP 解压四个交接文件。压缩包内的 SHA256 清单与单独收到的清单逐字节一致。两个 bundle 均通过 SHA256 与 `git bundle verify` 校验。

| 仓库 | 基线 | 首次发布并从远端回读的云端原始提交 | 原始提交数 |
|---|---|---|---|
| [Spacer](https://github.com/Timer009/Spacer/tree/sprint-09-mobile-quality) | `264194f6b1a40a2990c0d544d60c2b61e8b8bee1` | `a10a4634dd75dca6a3e78f9eed7e63c9ea5b5950` | 4 |
| [Bridge](https://github.com/Timer009/spacer-gai-bridge/tree/sprint-09-mobile-quality) | `982bad7d944f248a7ce89be69f37afa8afe42484` | `e94dbeb576a5891082792df86c030ac5c629dcaf` | 3 |

通过独立克隆导入，检查了完整历史、基线祖先关系、`git diff --check` 与 `git fsck`。直连下载发生连接重置，克隆改用本机已验证的基线库。推送使用本机 GitHub 授权和现有本机代理。两个 `main` 在首次推送前后回读一致。本记录作为 Bridge Sprint 分支上的后续文档提交，原始云端提交保留在同一分支历史中。

手机预览从已公开的 Spacer 提交加载固定版本，首次访问可点击第三方确认页上的 **Open the page**。预览服务返回 HTTP 200 与 HTML，内容 SHA-1 为 `4cb14d64d2b1e141c3c47614ef4acecf664415f0`，和 Git 提交内的游戏文件一致。正式 Pages 游戏的实测 SHA-1 为 `226ae26e6e4c6c12b72cc632f30fb63916440eb4`，与 Sprint 08 记录一致。[打开 Sprint 09 独立预览](https://rawcdn.githack.com/Timer009/Spacer/a10a4634dd75dca6a3e78f9eed7e63c9ea5b5950/vector-lander/index.html)

通过 Chrome 的 390×844 触屏模拟点击确认页进入线上预览，并通过航线图、热区、多指、暂停和设置操作复测。[测试报告](../latest-test.md)保留云端 Chromium 和 WebKit 结果，并补充 Windows Chrome 复测。iPhone Safari 与 Android Chrome 待实测系统旋转、地址栏和刘海安全区、多指及长按菜单、首次手势音频、帧率，以及 D5 短横屏低燃料提示与天体标签的局部重叠。正式版发布待批准。
