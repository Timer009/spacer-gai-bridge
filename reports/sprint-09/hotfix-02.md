# SPACER-SPRINT-09-HOTFIX-02

P1-4 · 跨浏览器横屏兼容性 · 等待 iOS 和 Android 夸克真机复验。

Spacer 测试分支提交为 `319d54ac4256d50cc1fa931fe133c265c89f5315`，父提交为 Hotfix 01 的 `b97c0c5710837251a396b0db9416fa229cf85049`。

## 反馈和证据

用户报告 Hotfix 01 后 iOS Safari 已可横屏，iOS 与 Android 夸克仍无法正常横屏。两端夸克的版本、浏览器方向设置、是否通过应用内窗口打开，以及旋转前后的诊断尚未取得。夸克官方帮助说明可从独立标签页打开网页和进入设置，未确认这两个手机版本的方向开关路径。真机检查时，先打开系统自动旋转，若夸克自身提供屏幕旋转开关，再核对其状态。 [夸克官方帮助](https://www.quark.cn/documents/help/know-the-ui)

Hotfix 01 会跟随窗口或 visualViewport 尺寸。若外层容器持续给出竖屏尺寸，或只改了容器尺寸而没有窗口事件，旧实现没有独立容器观测和可操作的横屏后备。HOTFIX-02 本地验证了只改变容器的 ResizeObserver 路径、禁全屏 iframe、API 缺失与拒绝，以及容器始终为 390×844 时的 844×390 逻辑画面。这些是可复现的兼容场景，夸克两端分别触发哪一种仍需真机日志。

| 真机诊断结果 | 下一步判断 |
|---|---|
| 版本 SHA 与本报告不同 | 重新复制固定提交链接，在新标签页打开，并对比最小检查页，排除旧页面或缓存 |
| 游戏和最小检查页都收到横屏尺寸 | 自动模式应切横屏。若 Canvas 仍竖屏，记录容器、逻辑尺寸与 Canvas 尺寸，继续排查游戏 |
| 最小检查页和游戏的实际视口均保持竖屏 | 优先排查浏览器方向开关、应用内宿主和系统。兼容横屏可以在竖屏物理容器内独立运行 |
| Context 为 embedded 或全屏/锁定返回拒绝 | 尝试在浏览器独立标签页打开。网页 API 取决于当前宿主的权限和支持能力 |

浏览器的全屏和方向锁定有激活、嵌入策略及平台约束。[Fullscreen 标准](https://fullscreen.spec.whatwg.org/) · [Screen Orientation 标准](https://w3c.github.io/screen-orientation/)

## 三级兼容

1. **自动**为默认模式。优先按当前可用容器布局，窗口、可见视口和方向信号用于更新尺寸，并用 ResizeObserver 重新读取宿主。不会在自动模式调用全屏或方向锁定。
2. **尝试原生全屏横屏**由玩家点击。按能力请求 Fullscreen 和 Screen Orientation，记录缺失、拒绝与请求后仍无横屏尺寸的情形。启动页或设置可继续选择兼容模式。退出只释放游戏自己请求的全屏或方向锁定。
3. **兼容横屏**由玩家从启动提示或设置开启。容器仍竖屏时，将游戏逻辑画面设为横屏并旋转完整交互区域，Canvas 使用逆坐标变换命中地图，HTML 按钮使用浏览器的变换后命中。四边刘海及手势区映射到逻辑方向。若容器本身变宽，自动去掉 90° 变换。退出可选设置中的「自动」或「竖屏」。在原生横屏时选「竖屏」，画面居中显示竖屏比例。

切换时清理按住的转向、主引擎、指针捕获和待确认的地图点按。保留手动暂停、飞船、关卡、燃料、生命及存档。方向偏好只在当前页面有效。`debug=1` 增加真实容器、逻辑尺寸、全屏策略、API 能力及最近失败原因，结果可以手动复制，无上传逻辑。

## 自动化结果

| Windows 环境 | 动态横竖屏预设 | 容器观测、受限 iframe、原生 API 成功/拒绝桩、兼容模式 | 十关回归 |
|---|---:|---|---|
| Chrome 158.0.8127.36 | 7 组 | 通过，CDP 双指 | 通过 |
| Playwright WebKit 26.5 | 7 组 | 通过，合成 Pointer Events | 通过 |
| Firefox 153.0 | 专项模拟 | 通过，合成 Pointer Events 和鼠标命中 | 通过 |
| Microsoft Edge 131.0.2903.99 | 2 组 | 通过，CDP 双指 | 通过 |

Chromium 和 WebKit 各跑 320×568、375×667、390×844、393×852、430×932、768×1024、900×1440 及各自反向尺寸。Edge 跑 320×568 和 390×844 两对。专项目标包括 390×844 竖屏容器、844×390 虚拟布局、DPR 2、四边安全区非对称、容器缩放 0.9、旋转地图命中、虚拟飞行中的双指转向加推力、转入原生横屏时清键、显式竖屏与退出、暂停状态不变。受限 iframe 测试验证尺寸及嵌入诊断。用能力桩验证原生 API 成功、缺失和拒绝，真实系统权限仍待移动设备测试。

四个浏览器各通过十关启动、推力/燃料、预测、硬碰撞、重生、辅助三星着陆、存档和解锁。固定随机种子及输入与 Hotfix 01 的飞行、预测和落地记录一致。通过用例无页面 JS 异常。Chrome 和 WebKit 的 D10 采样仍只有一个游戏 RAF 循环。 [测试脚本](https://github.com/Timer009/Spacer/blob/319d54ac4256d50cc1fa931fe133c265c89f5315/tests/mobile-hotfix.cjs)

截图中的设备容器仍然竖屏，因此兼容模式是侧向画面。 [Chrome 兼容飞行](hotfix-02/chromium-virtual-flight.png) · [WebKit 兼容航线图](hotfix-02/webkit-virtual-map.png) · [Firefox 兼容飞行](hotfix-02/firefox-virtual-flight.png) · [Edge 兼容飞行](hotfix-02/edge-virtual-flight.png) · [诊断](hotfix-02/webkit-direction-debug.png)

## 手机真机矩阵

| 平台与浏览器 | 已知结果 | Hotfix 02 |
|---|---|---|
| iOS Safari | 用户反馈 Hotfix 01 横屏正常 | 待回归 |
| iOS Chrome | 未验收 | 待验证 |
| iOS 夸克 | 用户反馈 Hotfix 01 仍异常 | 待验证自动、原生 API、兼容三条路径 |
| Android Chrome | 未验收 | 待验证 |
| Android 夸克 | 用户反馈 Hotfix 01 仍异常 | 待验证自动、原生 API、兼容三条路径 |
| Android Edge | 未验收 | 待验证 |
| Android Firefox | 未验收 | 待验证 |

## 手机预览与复验

独立预览固定到 Spacer 提交。首次出现 CDN 确认页时点 **Open the page**。用夸克的网页标签打开，先在自动模式转动手机；仍竖屏时点「尝试原生全屏横屏」。若高度和宽度仍未交换，开「兼容横屏」并把手机顶部转向左侧。进入关卡试转向加推力、暂停、设置和退出兼容模式。

在 Windows Chrome 中打开以下三个独立页面，均返回 HTTP 200，页面字节 SHA256 与固定提交一致，且游戏和检查页均为顶层文档，未嵌入 iframe。正常页复测竖屏容器内开启兼容横屏及容器变宽后去掉变换。诊断页显示正确 SHA 和容器尺寸。正式 Pages 的响应字节仍与 Sprint 08 的 `264194f` 一致。

若自动横屏仍失败，在游戏诊断和最小检查页里各记录竖屏与旋转后的输出，附上系统、夸克版本及自身方向设置状态。若诊断模式中仍显示旧提交，先用新标签页重开最新固定链接。

[正常预览](https://rawcdn.githack.com/Timer009/Spacer/319d54ac4256d50cc1fa931fe133c265c89f5315/vector-lander/index.html) · [诊断预览](https://rawcdn.githack.com/Timer009/Spacer/319d54ac4256d50cc1fa931fe133c265c89f5315/vector-lander/index.html?debug=1) · [最小方向检查](https://rawcdn.githack.com/Timer009/Spacer/319d54ac4256d50cc1fa931fe133c265c89f5315/vector-lander/orientation-check.html)
