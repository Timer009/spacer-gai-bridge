# Sprint 09 跨浏览器兼容性收尾

测试分支收尾版本 `fbc8e0f2f6d37beabb5a4545c46e54a54e1c7d42`，基线 Hotfix 02 为 `319d54ac4256d50cc1fa931fe133c265c89f5315`。

## 真机反馈与待查原因

用户报告 iOS Safari、iOS Chrome、iOS Edge、Android Chrome 和 Android Edge 均可正常横屏。iOS 与 Android 夸克仍无法横屏，尚未收到这两端旋转前后的尺寸、方向、运行环境或全屏返回值。Android Firefox 暂无新的真机反馈。P1-4 开放，等待夸克验收。

夸克公开帮助说明可在标签页打开网址和进入浏览器设置，未提供本案涉及的手机版本方向配置说明。先确认系统自动旋转和当前夸克版本自身的方向设置（如提供），从夸克独立网页标签打开固定提交的诊断页，避免阅读器、内置预览或其他嵌入入口。 [夸克官方帮助](https://www.quark.cn/documents/help/know-the-ui)

| 记录结果 | 可得结论 |
|---|---|
| 两个页面报告的提交 SHA 与本页不同 | 当前加载旧地址或旧缓存，需用固定提交链接重测 |
| 最小检查页旋转后窗口和可见视口仍竖屏 | 该宿主未向页面提供横屏尺寸。即使设备角度改变，网页无法自行解除宿主或系统的方向限制 |
| 最小检查页与游戏都收到宽屏尺寸，自动模式下 Canvas 未随之变化 | 核对 `Container`、逻辑尺寸、`Canvas` 和事件顺序，继续排查游戏 |
| 原生全屏或方向请求为不可用、被拒绝 | 记下 API 返回值及页面上下文。可改用兼容模式，兼容模式不依赖这些 API |

## 本轮改动

- `vector-lander/index.html` 的 `?compat=1` 链接明确进入 HOTFIX-02 的既有虚拟横屏，与浏览器品牌、粗略指针能力、方向事件及全屏权限无关。设置中的「退出兼容」恢复自动模式，并从当前 URL 移除兼容参数，保留其他参数。正常链接沿用原有自动路径。
- `vector-lander/orientation-check.html` 增加「记录竖放时」与「记录横放后」，两次读数和事件历史可一并复制。保留宽高、角度、嵌入上下文、API 能力以及版本号，便于区分未发生视口变化与未处理事件。
- 其余 Canvas 布局、指针逆变换、安全区映射、多指输入和飞行参数沿用 Hotfix 02。未修改 Sprint 10–16 路线图。

## 回归结果

Windows Chrome、Playwright WebKit、Firefox 和 Edge 均通过专项与十关回归。已覆盖容器尺寸固定、指针检测为 fine、没有全屏请求、旋转后 Canvas 像素及 CSS 尺寸、缩放后地图点击、非对称安全区、双指转向加推力、暂停中退出兼容和刷新回到自动模式。Chrome、WebKit、Edge 的标准动态视口矩阵合计 16 组。Chrome 和 Edge 多指用 CDP 驱动，WebKit 和 Firefox 用合成指针事件。四个浏览器各完成十次辅助三星着陆，固定随机种子下的飞行、预测及落地记录匹配 Hotfix 02。两个诊断快照可同时保留；所有通过用例无页面脚本错误。这些结果属于桌面自动化，夸克两端待真机复验。 [回归脚本](https://github.com/Timer009/Spacer/blob/fbc8e0f2f6d37beabb5a4545c46e54a54e1c7d42/tests/mobile-hotfix.cjs)

## 复验入口

Windows Chrome 对以下四个固定地址均收到 HTTP 200，响应 SHA256 与 Git 提交一致。确认游戏和检查页为顶层页面，兼容链接可进入和退出，最小检查页可复制两次记录。正式 GitHub Pages 游戏响应仍对应 Sprint 08 的 `264194f`。

- [正常预览](https://rawcdn.githack.com/Timer009/Spacer/fbc8e0f2f6d37beabb5a4545c46e54a54e1c7d42/vector-lander/index.html) · [兼容横屏直达](https://rawcdn.githack.com/Timer009/Spacer/fbc8e0f2f6d37beabb5a4545c46e54a54e1c7d42/vector-lander/index.html?compat=1)
- [游戏诊断](https://rawcdn.githack.com/Timer009/Spacer/fbc8e0f2f6d37beabb5a4545c46e54a54e1c7d42/vector-lander/index.html?debug=1) · [最小方向检查与成对采样](https://rawcdn.githack.com/Timer009/Spacer/fbc8e0f2f6d37beabb5a4545c46e54a54e1c7d42/vector-lander/orientation-check.html)

请在 iOS 和 Android 夸克各验证一次兼容入口。进入后把手机顶部朝左，试双指转向加推力、暂停，再从齿轮进入设置选择「退出兼容」。如果正常预览仍无法原生横屏，在最小检查页先点「记录竖放时」，转动手机等一秒，再点「记录横放后」和「复制结果」。如试过原生全屏，再补一份游戏诊断及夸克版本、入口和方向设置状态。
