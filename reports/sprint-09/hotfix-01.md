# SPACER-SPRINT-09-HOTFIX-01

2026-11-24 · P1-3 · 等待 iPhone 真机复验。原始 Sprint 09 未通过正式验收。

## 缺陷和根因证据

用户报告 iPhone 已关闭系统方向锁定，但浏览器中的 Sprint 09 预览旋转后仍为竖屏。尚未取得这台 iPhone 的方向事件和尺寸日志。

检查基线 `a10a4634dd75dca6a3e78f9eed7e63c9ea5b5950`。原预览 HTML 的字节与 Git 一致，浏览器回读游戏为顶层文档，页面中没有 iframe。没有 manifest 方向设置、锁屏 API 或旋转 Canvas 的 CSS。viewport 使用设备宽度、初始缩放 1 和 `viewport-fit=cover`。基线的 Canvas 计算和逐帧兜底只读取 `window.innerWidth/innerHeight`，旋转提示另外由 CSS 媒体查询控制，且没有监听 `visualViewport`。

| 对照场景 | Sprint 09 基线 | Hotfix 01 |
|---|---|---|
| Playwright 改变窗口视口，390×844 → 844×390 | 正常横屏 | 正常横屏 |
| 注入可见视口改变，窗口仍是 390×844 | Canvas 留在 390px 宽，等待原延迟回调后仍相同 | Canvas 与控件切到 844×390，竖屏提示退出 |
| 模拟窗口先变，可见视口仍是旧值 | 采用新窗口尺寸 | 采用新窗口尺寸，后续对齐到可见视口 |
| 地址栏模拟，可见高度 390 → 352，偏移 18px | 基线不消费相应事件 | Canvas 和控件跟随高度和位置 |
| 缺少两个方向相关 API，或只有方向事件但尺寸不变 | 依赖窗口几何 | 尺寸实变则重排，尺寸未变则保留可用的竖屏 |

两个 Windows 浏览器引擎都复现了可见视口单独改变时的基线缺陷。这个故障能够解释所报现象，仍需用 iPhone 日志确认。有些应用内浏览器作为顶层 WebView 运行，网页的顶层检测无法判断其宿主是否限制旋转。如果独立 Safari 标签页内两个视口都没有改变，先用最小检查页核对浏览器提供的方向与尺寸。Apple 的视口说明及 WebKit 公开问题记录可供交叉参考。[Safari 视口说明](https://developer.apple.com/library/archive/documentation/AppleApplications/Reference/SafariWebContent/UsingtheViewport/UsingtheViewport.html) · [WebKit 可见视口更新时序记录](https://bugs.webkit.org/show_bug.cgi?id=265578)

## 修改

- `vector-lander/index.html` 使用同一个视口容器布局 Canvas、HUD、触控、设置和横屏提示。支持窗口、可见视口、媒体查询、旧方向事件及 Screen Orientation 变化，按 DPR 更新像素并延后复读安全区。只有原本的一个游戏 RAF 循环。
- 屏幕方向改变清除键盘、指针捕获、转向和推力，以及未完成的地图点按。手动暂停、设置与旋转提示分别管理。横竖屏布局切换不重载关卡。
- 保留 22px 描边图标和至少 44×44 CSS px 热区。飞行控件降低底色遮挡。D5 及其他关卡在 HUD 占用区避让天体小标签，重要警告闪动的两个颜色都可辨识。
- `debug=1` 默认关闭，打开后可查看浏览器、窗口/可见视口/屏幕方向、Canvas、布局、安全区、最近事件与版本。复制失败可手动选择。诊断信息留在本机，页面无上传逻辑。
- `vector-lander/orientation-check.html` 是独立、无 Canvas 或游戏逻辑的检查页。`tests/mobile-hotfix.cjs` 保存双引擎回归，可在有 Playwright、Chromium 和 WebKit 的环境运行 `node tests/mobile-hotfix.cjs`。

## 测试

Windows Chrome 158.0.8127.36 与 Playwright WebKit 26.5 分别执行七组动态尺寸。手机覆盖 320×568、375×667、390×844、393×852、430×932 及对应横屏。另跑 768×1024 平板与 900×1440 桌面尺寸及其反向布局。两引擎均验证竖屏和横屏启动、连续旋转、菜单和航线图、飞行、暂停、设置、成功与坠毁画面。390×844 和 844×390 注入安全区。Chromium 通过 CDP 产生多指事件，WebKit 使用合成 Pointer Events。两者均确认旋转清键与旋转后恢复触控。脚本验证网页禁止游戏区长按菜单事件，系统手势仍待真机检查。

每引擎完成十关合法启动、十组推力/燃料和预测、十次硬碰撞及重生、十次辅助三星着陆，以及存档和解锁。采用相同随机种子与输入，对照 `a10a463`，记录的飞行状态、预测和落地存档一致。D5 568×320 两种闪烁颜色均可绘制，背景「地球」标签不再叠放。所有通过案例中无页面 JS 异常。D10 采样的 120 帧用于比较桌面模拟趋势，两个引擎都只有一个待执行的游戏 RAF。

| D10 桌面 RAF 间隔 | 基线中位 / P95 | 修复版中位 / P95 |
|---|---|---|
| Chromium | 16.6 / 17.1 ms | 16.6 / 16.8 ms |
| WebKit | 28 / 47 ms | 24 / 32 ms |

模拟尺寸、注入安全区、辅助着陆和截图目查没有覆盖 iPhone 系统级方向限制、真实地址栏、系统手势、音频解锁、或持续移动性能。真机测试仍待用户完成。

截图：[Chrome 短横屏 D5](hotfix-01/chromium-d5-568x320.png) · [WebKit 短横屏 D5](hotfix-01/webkit-d5-568x320.png) · [横屏标题](hotfix-01/chromium-title-landscape.png) · [竖屏航线图](hotfix-01/chromium-map-portrait.png) · [横屏统计](hotfix-01/chromium-stats-landscape.png) · [竖屏设置](hotfix-01/webkit-settings-portrait.png) · [着陆](hotfix-01/webkit-landed-portrait.png) · [坠毁](hotfix-01/webkit-crash-portrait.png) · [诊断面板](hotfix-01/webkit-debug-portrait.png)

## iPhone 验收

1. 把固定提交的预览链接复制到 Safari 独立标签页，首次出现 CDN 确认页时点 **Open the page**。在标题页竖转横，再横转竖。
2. 进入关卡，检查旋转时画面比例、刘海、底部手势区和地址栏。试双指转向加推力、旋转后松手、暂停时旋转和继续。检查游戏状态没有重置。
3. 若仍停在竖屏，打开诊断版并展开「屏幕诊断」，分别在竖屏和横放 1 秒后复制结果。再打开最小检查页，重复竖转横并复制结果，便于比较宿主方向事件和实际视口。

[正常游戏](https://rawcdn.githack.com/Timer009/Spacer/b97c0c5710837251a396b0db9416fa229cf85049/vector-lander/index.html) · [诊断模式](https://rawcdn.githack.com/Timer009/Spacer/b97c0c5710837251a396b0db9416fa229cf85049/vector-lander/index.html?debug=1) · [最小方向检查](https://rawcdn.githack.com/Timer009/Spacer/b97c0c5710837251a396b0db9416fa229cf85049/vector-lander/orientation-check.html)

使用本机 Chrome 通过确认页访问了三个链接。三者均为 HTTP 200、顶层无 iframe，响应字节的 SHA256 与固定 Git 提交一致。确认了正常预览关闭诊断、诊断预览正确显示完整提交，及最小检查页响应模拟横屏。正式 Pages 实际响应字节仍与 Sprint 08 的 `264194f` 一致。

发布范围为 `sprint-09-mobile-quality`。正式版沿用 Sprint 08。Sprint 10–16 沿用原路线图，等待相应批准。
