# CHANGELOG

本文件记录报告仓库的初始化/更新，以及 Spacer 源码变更摘要。源码的完整历史以 <https://github.com/Timer009/Spacer> 为准。

## 2026-11-24 — Spacer Sprint 08 竖屏 HUD 与 D5 避让（已上线）

### Changed

- `vector-lander/index.html`：2732 行；SHA1 `226ae26e6e4c6c12b72cc632f30fb63916440eb4`。

### Fixed

- 竖屏燃料条缩为 132×8，HUD 上移量降到 92px。
- `W<700` 时风标移到站名下方、ATM 移到右上，避免与站名重叠。
- 关卡开场名称/提示字号按屏宽自适应，修复 D5「水手谷」长名称贴边。

### Verification

- 390×844 下风标/ATM/站名不重叠；燃料条与按钮间距 20px。
- D5 开场名称左右留白充足；十关软着陆 10/10。
- 无 `window.error`；测试四键已清空。

详见 [reports/latest-test.md](../reports/latest-test.md)。

### Commit status

- 已推送到 Spacer `main`：`264194f6b1a40a2990c0d544d60c2b61e8b8bee1`。
- GitHub Pages 已更新，线上文件 SHA1 核对为 `226ae26e6e4c6c12b72cc632f30fb63916440eb4`。

## 2026-11-24 — Spacer Sprint 07 安卓横屏画布与网格修复（已上线）

### Changed

- `vector-lander/index.html`：2709 行；SHA1 `51b734839acc87045190c0614df52cac67d20877`。

### Fixed

- Canvas CSS 尺寸与 `innerWidth/innerHeight` 精确同步，并在每帧自愈，修复安卓横屏圆变椭圆。
- 手机横屏航线图改为 5×2 网格，标题/站点/星级不再拥挤。
- HUD 上移条件加入 `navigator.maxTouchPoints`，避免安卓横屏按钮压住燃料条。
- 横屏标题右栏增加暗色底板，降低背景天体干扰。

### Verification

- 640×360 下 Canvas 横纵 CSS/像素比例均为 1；地图节点为圆。
- 5×2 网格地图截图核对，标题/站点/星级不重叠。
- HUD/按钮间距 13–28px；十关软着陆 10/10；测试四键已清空。

详见 [reports/latest-test.md](../reports/latest-test.md)。

### Commit status

- 已推送到 Spacer `main`：`69c959abcd8d9084f0bd53f78f745b63f9884d4e`。
- GitHub Pages 已更新，线上文件 SHA1 核对为 `51b734839acc87045190c0614df52cac67d20877`。

## 2026-11-24 — Spacer Sprint 06 iOS 旋转崩溃热修（已上线）

### Changed

- `vector-lander/index.html`：2628 行；SHA1 `7852b69f222129803ea364635d7a93649dd19855`。

### Fixed

- 移除 `requestFullscreen` / `screen.orientation.lock`，避免 iOS Safari 旋转时崩溃。
- 横屏提示按钮改为「如何横屏」，只显示关闭竖屏锁定说明。
- `resize` / `orientationchange` 改为防抖，减少旋转时重复重建画布。
- 移除触控按钮 `backdrop-filter`，降低 iOS 合成压力。

### Verification

- 源码无崩溃 API 与 `backdrop-filter`；「如何横屏」不调用全屏 API。
- 旋转后防抖 resize 到 844×390，横屏布局生效。
- 十关软着陆 10/10；无 `window.error`；测试四键已清空。
- 本地无法复现 iOS WebKit 崩溃；真机需重点确认。

详见 [reports/latest-test.md](../reports/latest-test.md)。

### Commit status

- 已推送到 Spacer `main`：`e56797efdd9c3c4ace9a8e4ce66ab15c28d07d95`。
- GitHub Pages 已更新，线上文件 SHA1 核对为 `7852b69f222129803ea364635d7a93649dd19855`。

## 2026-11-24 — Spacer Sprint 05 横屏入口与长按菜单修复（已上线）

### Changed

- `vector-lander/index.html`：2639 行；SHA1 `b9e23824ae73768ad84fb1d1162298edc81d4e61`。

### Added / Fixed

- 竖屏提示增加「尝试自动横屏」；设置面板增加「尝试横屏」入口。
- `orientationchange` 后强制 `resize`，修复旋转后仍使用竖屏布局。
- 触控方向/点火键改 CSS 三角形，齿轮/统计改 SVG，移除可选中文字。
- 全局 `user-select` / `touch-callout` / `contextmenu` / `selectstart` 抑制并清空选区。

### Verification

- 触控键无文本节点；CSS 三角形与 SVG 按钮点击正常。
- 自动横屏失败提示、旋转后 844×390 布局、触控推力、统计/齿轮均通过。
- 十关软着陆 10/10；无 `window.error`；测试四键已清空。

详见 [reports/latest-test.md](../reports/latest-test.md)。

### Commit status

- 已推送到 Spacer `main`：`eab719daf6f7360ca24eda82b3daa61695da5f07`。
- GitHub Pages 已更新，线上文件 SHA1 核对为 `b9e23824ae73768ad84fb1d1162298edc81d4e61`。

## 2026-11-24 — Spacer Sprint 04 手机横屏布局（已上线）

### Changed

- `vector-lander/index.html`：2582 行；SHA1 `9fab3e5ed88882a04a7b68b54465241ca9799c6a`。
- `README.md`：手机端说明补充「建议横屏、竖屏提示旋转」。

### Added / Fixed

- 手机竖屏显示「请横屏游玩」提示；旋转中暂停，可「继续竖屏」。
- 横屏标题改左右双栏，短屏文字不再重叠。
- 横屏航线图使用触屏提示与统计按钮；站点标签区域可点选。
- HUD 支持左右安全区，横屏触控按钮与燃料/ALT/VX/VY 保持间距。

### Verification

- 844×390 / 667×375 / 568×320 横屏标题截图核对，无文字互相覆盖。
- 竖屏旋转提示显示/暂停/继续竖屏恢复逻辑通过。
- 横屏地图标签点选、统计按钮、HUD 间距通过。
- 桌面地图与十关软着陆回归通过；测试四键已清空。

详见 [reports/latest-test.md](../reports/latest-test.md)。

### Commit status

- 已推送到 Spacer `main`：`0d99d8af86b88bef82ca270b0b1eb08a5211a385`。
- GitHub Pages 已更新，线上文件 SHA1 核对为 `9fab3e5ed88882a04a7b68b54465241ca9799c6a`。

## 2026-11-24 — Spacer Sprint 03 手机端界面与飞船皮肤（已上线）

### Changed

- `vector-lander/index.html`：最终 2501 行；SHA1 `cf002d2ba86f0c98503f35d5e0aed5abbdd8ce58`。
- `README.md`：设置面板说明补充飞船外观。
- 源码 commits：`7d3a5cf`（站点名）、`7e5cb67`（触控/HUD）、`92df820`（地图/UI）、`8cd40cd`（皮肤）。

### Added / Fixed

- D4 HUD 与开场改用站点名「小行星带」。
- 手机竖屏航线图改纵向列表；点站点选择、再点一次出发。
- 触控方向/点火键只在飞行状态显示；地图增加统计按钮。
- HUD 上移避开按钮与安全区；按钮对比度、按下反馈、pointer capture。
- 抑制长按系统菜单/选择提示（`contextmenu` / `selectstart` / `touch-callout`）。
- 三套飞船皮肤：经典矢量 / 猎鹰 9 / 星舰；设置面板切换并持久化 `vl_cfg.skin`。

### Verification

- 三套皮肤各十关软着陆 30/30，均 3★；碰撞包络 −14 / +9。
- 三套皮肤坠毁正常；合法/非法/旧档皮肤配置兼容。
- 390×844、320×568 地图/面板布局与触控推力测试通过。
- 桌面地图点击与十关回归通过。
- 测试四键已清空。

详见 [reports/latest-test.md](../reports/latest-test.md)。

### Commit status

- 已推送到 Spacer `main`：`8cd40cd501abba4c55bd5d000cc984a9b1e84c95`。
- GitHub Pages 已更新，线上文件 SHA1 核对为 `cf002d2ba86f0c98503f35d5e0aed5abbdd8ce58`。

## 2026-11-23 — 报告仓库初始化

### Added

- `README.md`：双仓库职责、读取顺序、更新协议、安全规则。
- `PROJECT-STATUS.md`：当前源码 commit、工作区状态、问题统计、测试摘要、人工测试项、下一阶段建议。
- `reports/latest-audit.md`：将源码仓库 `AUDIT-REPORT.txt`（基线 `526397a`）迁移为 Markdown；保留技术细节，脱敏本地绝对路径。
- `reports/latest-test.md`：Sprint 01 实际执行的自动测试记录。
- `tasks/CURRENT-TASK.md`：用户已确认的 Sprint 01 任务与当前待决策项。
- `tasks/TASK-HISTORY.md`：审计、Sprint 01、报告仓库初始化的历史索引。
- `reports/history/README.md`：历史报告归档规则。

### Notes

- 原始审计报告提交：Spacer `b9d12a7`（仅新增 `AUDIT-REPORT.txt`）。
- 本次未修改、未提交、未推送 Spacer 源码仓库。
- 本次未上传源码副本、凭据、个人路径或用户私人数据。

## 2026-11-24 — Spacer Sprint 02 存档硬化与漂移平台修复（已上线）

### Changed

- `vector-lander/index.html`：+58 / −15；2255 行；SHA1 `ce1ad20b296a084961f7b9798d2d3d995e228192`。
- 源码 commit：`4d200989c3198fde50683d6cdcb375c3ba7a2480`。

### Fixed

- P2-5：漂移平台按完整漂移包络（基准中心 ± amp）检测重叠。
- SAVE-01：`vl_cfg` 数值范围/布尔类型、`vl_best`、`vl_stats`、`progress.stars` 全部校验。
- STATS-MODAL-01：统计面板打开时，`空格/Enter` 只关闭面板，不出发。
- P2-13：爆炸粒子增加 `PARTICLE_CAP=900` 上限。
- P2-9 / P2-10：删除 `drawPadLabel` 与未使用 `ax/ay`。

### Verification

- 合法旧存档完整保留；损坏存档安全回落；地图正常渲染，无 `window.error`。
- 第 8 关 240 次装载（padW 1.2 / 2.5）零重叠，最小间距 142.93 / 154.75。
- 统计面板第一次空格关面板，第二次空格出发。
- 十关启动 10/10；十关软着陆 10/10；触屏地图回归通过。
- 测试四键已清空，页面回到标题。

详见 [reports/latest-test.md](../reports/latest-test.md)。

### Commit status

- 已推送到 Spacer `main`：`4d200989c3198fde50683d6cdcb375c3ba7a2480`。
- GitHub Pages 已更新，线上文件 SHA1 核对为 `ce1ad20b296a084961f7b9798d2d3d995e228192`。

## 2026-11-23 — Spacer Sprint 01 核心稳定性修复（已上线）

### Changed

- `vector-lander/index.html`：+29 / −7；2212 行；SHA1 `9fa81257742fdfca0b705a62f364f77bd83177c4`。

### Fixed

- 解锁校验统一收口到 `launch()`；地图补渲染提示。
- 陨石创建补 `METEOR_R=9`；绘制与碰撞共用同一常量。
- `progress.unlocked` 增加类型/有限性/取整/范围校验。
- gameover 后地图按下一轮显示飞船数，避免 `×0`。
- 地图统计面板打开时阻止指针穿透。
- 移动端地图方向键只选择，不直接出发；消除按键残留。

### Verification

- 十关合法启动 10/10；十关软着陆 10/10。
- 未解锁键盘/鼠标/触屏均被拦截。
- 陨石碰撞 9.1 不撞 / 8.9 撞；视觉截图确认头部、辉光、拖尾。
- 存档 6 例（合法/负数/超范围/小数/字符串/坏 JSON）通过；最佳成绩与统计保留。
- 触屏地图、统计面板、着陆/坠毁/重开通过。
- 测试四键已清空，页面回到标题。

详见 [reports/latest-test.md](../reports/latest-test.md)。

### Commit status

- 已推送到 Spacer `main`：`dd6ac7268165eb1194b6ac968d43cee4b4eaa7ef`。
- GitHub Pages 已更新，线上文件 SHA1 核对为 `9fa81257742fdfca0b705a62f364f77bd83177c4`。
