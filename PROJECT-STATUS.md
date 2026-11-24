# PROJECT STATUS — Spacer / 矢量着陆

Sprint 14 已归档为 v2.0.14，正式 Pages 已回读。专项真机指标继续待确认。


Sprint 13 已归档。触控及结算防误触的真机确认仍待补齐。


Sprint 12 真机验收通过，四浏览器回归通过。正式游戏与 sprint-12 标签指向 `3ef190dc18f8a4f918ebede83ea9b895eca4b843`。Pages 回读的 Git blob 为 `113be2c17753f89bfacbcb9871ace6f0282f879b`，与发布文件一致。


> 本文件是 Spacer 项目的当前状态快照。其他 Agent 应先读本文件，再读审计与测试报告。
> 本文件不是任务批准文件；只有 `tasks/CURRENT-TASK.md` 中记录的内容才是用户已确认任务。

## 当前开发 · Sprint 14

`v2.0.14-rc.1` 等待验收，源码 `bddbd34bc96174bec293db9a2e497d00bcea130c`。 [试玩](https://rawcdn.githack.com/Timer009/Spacer/bddbd34bc96174bec293db9a2e497d00bcea130c/vector-lander/index.html) · [阶段与测试](reports/sprint-14/realistic-visuals.md)

## 正式发布 · Sprint 13

正式 Pages 为 `v2.0.13`，提交 `b61e1af9c2915186687e7066d00d009e21f57879`。 [验收边界与归档](reports/sprint-13/release.md)

## 正式发布 · Sprint 12

[真机验收与 Pages 归档](reports/sprint-12/release.md)

## 正式发布 · Sprint 11

- 三种模式、横屏设置滚动、平台倍率位置与轻型月面着陆器已归档。 [归档与回归](reports/sprint-11/release.md)

## 正式发布 · Sprint 10

- 用户试玩后批准归档。Sprint 10 为 `5536ffcfeb7428497e20614474c9556fbd0ab550`，标签 `sprint-10`。三种独立飞行型号和旧存档兼容性均已回归。 [发布归档](reports/sprint-10/release.md)
- Sprint 11 获批在独立分支开发。夸克横屏 P1-4 继续暂缓。 [当前任务](tasks/CURRENT-TASK.md)

## 发布基线 · Sprint 09

- 发布版本为 `fbc8e0f2f6d37beabb5a4545c46e54a54e1c7d42`，归档标签为 `sprint-09`。移动布局、HUD、旋转、兼容横屏、冰筏与轨迹预测的验收记录见 [发布归档](reports/sprint-09/release.md)。
- 用户确认 iOS Safari、iOS Chrome、iOS Edge、Android Chrome 和 Android Edge 真机横屏通过。两端夸克 P1-4 作为已知兼容缺陷暂缓，后续阶段可以继续。 [专项记录](reports/sprint-09/browser-closeout.md)
- Sprint 10 已批准，仅在独立开发分支交付三种飞船物理。Sprint 11–16 仍等待逐项批准。 [当前任务](tasks/CURRENT-TASK.md) · [路线图](ROADMAP.md)

## 1. 基本信息

| 字段 | 值 |
|---|---|
| 项目名称 | 矢量着陆 Vector Lander — 太阳系航线（仓库名 `Spacer`） |
| 最后更新时间 | 2026-11-24 15:11 +0800 |
| 源码仓库 | <https://github.com/Timer009/Spacer> |
| 报告仓库 | <https://github.com/Timer009/spacer-gai-bridge> |
| 线上游戏 | <https://timer009.github.io/Spacer/vector-lander/> |
| 当前分支 | `sprint-14-realistic-visuals` |
| 当前完整 Git commit SHA | `bddbd34bc96174bec293db9a2e497d00bcea130c` |
| 远程 `origin/main` | `b61e1af9c2915186687e7066d00d009e21f57879` |
| 工作区 | 干净 |
| 最近一次审计基线 | `526397a3c1b63445b33802f8f436b69ca475841a` |
| 当前开发阶段 | Sprint 13 正式发布，Sprint 14 候选待验收 |
| 最新审计报告 | [reports/latest-audit.md](reports/latest-audit.md) |
| 最新测试报告 | [reports/latest-test.md](reports/latest-test.md) |
| 当前任务 | [tasks/CURRENT-TASK.md](tasks/CURRENT-TASK.md) |
| 变更记录 | [changes/CHANGELOG.md](changes/CHANGELOG.md) |

## 2. 源码版本状态

```text
branch       : sprint-14-realistic-visuals
HEAD         : bddbd34bc96174bec293db9a2e497d00bcea130c
origin/main  : b61e1af9c2915186687e7066d00d009e21f57879
file         : vector-lander/index.html
lines        : 3828
SHA256       : 1d098fc7f95e6cfb9c7450568a8b1c4c6243c6804e3da8bde11ddef9263d4f7c
```

Sprint 09 的发布文件见标签 `sprint-09`。此前 Sprint 08 的 Pages 回读记录如下。

```text
Pages hash : 226ae26e6e4c6c12b72cc632f30fb63916440eb4
状态       : 已通过 Pages 页面哈希核对（2026-11-24）
```

重要说明：

- **Sprint 01**：`dd6ac7268165eb1194b6ac968d43cee4b4eaa7ef`，已上线。
- **Sprint 02**：`4d200989c3198fde50683d6cdcb375c3ba7a2480`，已上线。
- **Sprint 03（手机端 + 皮肤）**：`8cd40cd501abba4c55bd5d000cc984a9b1e84c95`，已上线。
- **Sprint 04（手机横屏布局）**：`0d99d8af86b88bef82ca270b0b1eb08a5211a385`，已上线。
- **Sprint 05（横屏入口 + 长按菜单修复）**：`eab719daf6f7360ca24eda82b3daa61695da5f07`，已上线。
- **Sprint 06（iOS 旋转崩溃热修）**：`e56797efdd9c3c4ace9a8e4ce66ab15c28d07d95`，已上线。
- **Sprint 07（安卓横屏画布/网格修复）**：`69c959abcd8d9084f0bd53f78f745b63f9884d4e`，已上线。
- **Sprint 08（竖屏 HUD 瘦身 + D5 避让）**：`264194f6b1a40a2990c0d544d60c2b61e8b8bee1`，已推送、Pages 已核对。
- **Sprint 09**：`fbc8e0f`，作为后续开发及发布基线。 [发布归档](reports/sprint-09/release.md)

## 3. 任务状态

### 已完成

- 十站太阳系战役、平台三形态、天象系统、六种障碍、星级/解锁/统计/航线图。
- 2026-11-23：只读审计（基线 `526397a`），产出 P0/P1/P2 问题清单。
- Sprint 01（`dd6ac72`，已上线）：
  - 解锁校验统一入口
  - 陨石半径/渲染修复
  - 存档 `unlocked` 校验
  - gameover 后地图飞船数显示
  - 移动端地图输入
  - 统计面板指针穿透
- Sprint 02（`4d20098`，已上线）：
  - 漂移平台完整包络重叠检测（P2-5）
  - 存档进一步硬化（`vl_cfg`、`vl_best`、`vl_stats`、`progress.stars`）
  - 统计面板键盘确认键只关面板
  - 爆炸粒子上限 900（P2-13）
  - 删除 `drawPadLabel` 与未使用 `ax/ay`（P2-9 / P2-10）
- Sprint 03（`8cd40cd`，已上线）：
  - D4 HUD/开场显示「小行星带」而非「带」
  - 手机端触控按钮仅在飞行状态显示，HUD 上移避开按钮与安全区
  - 手机竖屏航线图改纵向列表；点选站点，再点一次出发；地图增加统计按钮
  - 长按系统菜单/选择提示抑制；触屏按钮 pointer capture
  - 三套飞船皮肤：经典矢量、猎鹰 9、星舰；设置面板切换并持久化
- Sprint 04（`0d99d8a`，已上线）：
  - 手机竖屏显示「请横屏游玩」提示，旋转中暂停；可继续竖屏
  - 横屏标题改左右双栏，短屏文字不再重叠
  - 横屏航线图使用触屏提示与统计按钮，站点标签区域可点选
  - HUD 支持左右安全区，横屏按钮与信息保持间距
- Sprint 05（`eab719d`，已上线）：
  - 横屏提示增加「尝试自动横屏」；设置面板增加横屏入口
  - `orientationchange` 后强制 resize，修复旋转后仍是竖屏布局
  - 触控键改 CSS 箭头、齿轮/统计改 SVG，移除可选中文字
  - 全局 user-select/touch-callout/contextmenu/selectstart 抑制并清空选区
- Sprint 06（`e56797e`，已上线）：
  - 移除 `requestFullscreen` / `screen.orientation.lock`，避免 iOS 旋转崩溃
  - 横屏按钮改为「如何横屏」，只显示关闭竖屏锁定的说明
  - resize/orientationchange 改为防抖，减少旋转时重复重建画布
  - 移除触控按钮 `backdrop-filter`，降低 iOS 合成压力
- Sprint 07（`69c959a`，已上线）：
  - Canvas CSS 尺寸与 `innerWidth/innerHeight` 精确同步，并每帧自愈
  - 手机横屏航线图改 5×2 网格，修复标题/站点/星级拥挤
  - HUD 上移条件加入 `maxTouchPoints`，安卓横屏按钮不再压住燃料条
  - 横屏标题右栏增加暗色底板
- Sprint 08（`264194f`，已上线）：
  - 竖屏燃料条缩为 132×8，HUD 上移量降到 92px
  - `W<700` 时风标移到站名下方，ATM 移到右上
  - 关卡开场名称/提示字号按屏宽自适应，修复 D5 长名称贴边

### 进行中

- Sprint 14 候选等待用户真机验收。
- 已知夸克 P1-4 暂缓。Sprint 13–16 等待各阶段批准。

### 当前任务边界

- 当前正式版本为 Sprint 11。以下历史审计统计以 Sprint 08 为基线。
- 报告中的“下一阶段建议”不是已批准任务。

## 4. 问题统计

统计口径：

- “审计条目”按 `reports/latest-audit.md` 的 P0/P1/P2 编号。
- P2 共 13 条，其中 P2-11 经复核不成立，P2-12 为信息性/既定取舍；可执行条目为 11 条。
- 当前线上 `264194f` 包含 Sprint 01–08。
- P1-3 与 P1-4 属于 Sprint 09 测试分支，以下历史审计统计沿用 Sprint 08 线上口径。
- Sprint 03–08 是手机端与皮肤/横屏功能，不新增审计条目，也不改变下列审计问题统计。

| 严重度 | 可执行条目 | 当前线上 `264194f` 仍开放 |
|---|---:|---:|
| P0 | 1 | 0 |
| P1 | 2 | 1 |
| P2 | 11 | 3 |
| **合计** | **14** | **4** |

> 对比：Sprint 01 刚上线时仍有 8 项开放；Sprint 02 上线后降至 4 项；Sprint 03–08 不改变该数量。

### 已修复

| 阶段 | 编号 | 修复 |
|---|---|---|
| Sprint 01 | P0-1 | 统一解锁校验 |
| Sprint 01 | P1-1 | 陨石头部/辉光 |
| Sprint 01 | P2-1 | `progress.unlocked` 校验 |
| Sprint 01 | P2-2 | gameover 地图飞船数 |
| Sprint 01 | P2-3 | 触屏地图误发车 |
| Sprint 01 | P2-4 | 统计面板指针穿透 |
| Sprint 02 | P2-5 | 漂移平台重叠检测 |
| Sprint 02 | P2-9 | 死代码 `drawPadLabel` |
| Sprint 02 | P2-10 | 未使用 `ax/ay` |
| Sprint 02 | P2-13 | 爆炸粒子上限 |
| Sprint 02 | SAVE-01 | `vl_cfg` / `vl_best` / `vl_stats` / `stars` 存档硬化（审计外新增） |
| Sprint 02 | STATS-MODAL-01 | 统计面板键盘确认键（审计外新增） |
| Sprint 03 | HUD-01 | D4 HUD/开场显示站点名「小行星带」（审计外新增） |
| Sprint 03 | MOBILE-01 | 手机端触控/HUD/航线图/系统菜单交互（审计外新增） |
| Sprint 03 | SKIN-01 | 三套飞船皮肤与外观选择（审计外新增） |
| Sprint 04 | MOBILE-02 | 手机横屏布局、旋转提示、横屏标题/地图/HUD（审计外新增） |
| Sprint 05 | MOBILE-03 | 横屏入口缺失、旋转后未 resize、iOS 长按按钮弹系统菜单（审计外新增） |
| Sprint 06 | MOBILE-04 | iOS Safari 旋转时调用 Fullscreen/Orientation Lock 导致网页崩溃（审计外新增） |
| Sprint 07 | MOBILE-05 | 安卓横屏 Canvas 被拉伸（圆变椭圆）、航线图文字拥挤、按钮压燃料条（审计外新增） |
| Sprint 08 | MOBILE-06 | 竖屏燃料条占空间；D5 风标/站名/开场长名称拥挤（审计外新增） |

### 仍开放的问题

| 编号 | 问题 | 状态 / 说明 |
|---|---|---|
| P1-2 | 仓库本地 `http.proxy` 配置 | 环境项。配置仍为 `http://127.0.0.1:10808`；当前端口可用。Sprint 01/02/03 推送均已验证。 |
| P1-3 | iPhone Safari 旋转后曾保持竖屏 | 用户最新真机反馈 iOS Safari 横屏正常。 |
| P1-4 | iOS 和 Android 夸克仍无法正常横屏 | 用户批准暂缓。自动横屏根因仍待真机诊断，兼容模式可直接进入。 |
| P2-6 | 漂移平台削平地形留下“无平台平地” | 已确认是视觉问题；`amp < w/2`，冰筏不会漂出削平段。未修改。 |
| P2-7 | 预测线不模拟旋转，忽略岩柱/陨石/间歇泉 | 已确认；预测用中心点，真实碰撞用船体点。未修改。 |
| P2-8 | 预测视距固定 4 秒 | 高空低重力时可能到不了地面，无撞击标记。未修改。 |

### 不成立 / 信息性条目

| 编号 | 结论 |
|---|---|
| P2-11 | **不成立**。源码不存在 `P.GM`；`P` 仅有 `{cx, cy, R, craters}`，引力只读 `levelDef.GM`。 |
| P2-12 | 信息性/既定取舍。`window.game` 测试钩子随单文件生产包发布；正常 UI 无入口。 |

### 残余风险

- 统计面板打开时，方向键仍可改变 `mapSel`；确认键已只关闭面板。
- `window.game.jump()` 是测试钩子，仍可绕过解锁；正常 UI 无入口。
- P2-6/P2-7/P2-8 的视觉/预测差异仍在。
- 手机端与皮肤目前用合成触控/桌面视口验证；iPhone 真机长按菜单、`pointer:coarse` 按钮显示、旋转提示、音频仍需人工确认。
- 安卓横屏已修 Canvas CSS/像素尺寸同步与 5×2 网格；真机 Chrome 下的圆度、文字间距与按钮间距需人工确认。
- 竖屏燃料条已缩为 132×8；D5 风标/ATM 已避开站名，开场名称字号已自适应；真机仍建议确认字距。
- iPhone 控制中心若开启「竖屏锁定」，网页无法强制横屏；游戏只提示关闭锁定后手动旋转，不再调用 Fullscreen/Orientation Lock。
- 横屏标题右栏已加暗色底板；如真机上仍觉得背景干扰可继续调不透明度。
- 皮肤碰撞点从 7 点加密到 16 点（猎鹰 9 / 星舰），包络仍为机头 −14、底部 +9；极端接触判定可能比旧 7 点更精确。

## 5. Sprint 01–08 自动测试记录

完整记录见 [reports/latest-test.md](reports/latest-test.md)。摘要：

### Sprint 01（已上线）

| 项目 | 结果 |
|---|---|
| 十关合法启动 | 10/10 |
| 未解锁绕过（键盘/鼠标/触屏） | 3/3 拦截 |
| 十关软着陆 | 10/10，均 3★（传送辅助） |
| 坠毁/重生/结束 | 通过 |
| gameover 地图飞船数 | 内部 `lives=0`，地图显示 `×N`；再出发恢复 |
| 陨石渲染/碰撞 | 截图确认；9.1 不撞 / 8.9 撞 |
| 存档 `unlocked` 异常 | 6 例通过；best/stats 保留 |
| 移动端地图/统计面板 | 通过 |

### Sprint 02（已上线 `4d20098`）

| 项目 | 结果 |
|---|---|
| 合法旧存档完整保留 | 通过：星级、解锁、最佳分、统计、全部设置值不变 |
| 损坏存档安全回落 | 通过：巨大星级→3；字符串/负数/Infinity→0；坏设置回落/限幅；地图正常渲染，无 `window.error` |
| 第 8 关漂移平台 | 240 次装载（padW 1.2 / 2.5）零重叠；最小间距 142.93 / 154.75 |
| 统计面板键盘 | 第一次空格只关面板；第二次空格正常出发 |
| 十关启动回归 | 10/10 |
| 十关软着陆回归 | 10/10，均 3★ |
| 触屏地图回归 | `▲` 不发车；`◀/▶` 只选择 |
| 死代码 | `drawPadLabel`、未使用 `ax/ay` 已移除，页面正常 |
| 测试数据清理 | 四键已删除，页面回标题 |

### Sprint 03（已上线 `8cd40cd`）

| 项目 | 结果 |
|---|---|
| D4 HUD/开场名称 | 显示「小行星带」，不再只有「带」 |
| 手机竖屏航线图 | 390×844 纵向列表；点行选择、再点出发；320×568 统计面板自适应 |
| 触控按钮显示范围 | 仅飞行状态显示；地图/标题/暂停/设置面板均隐藏 |
| HUD 与按钮间距 | 390×844 燃料/速度上移，按钮与 HUD 不重叠 |
| 长按系统菜单 | `contextmenu` / `selectstart` 均被拦截；`user-select:none` |
| 触控推力 | 按住 −1.8 燃料；手指滑出仍继续；抬起停止 |
| 三套皮肤 | 经典/猎鹰 9/星舰 各十关软着陆 30/30，均 3★ |
| 皮肤碰撞包络 | 三套均 `minY=486 / maxY=509`（中心 500，机头 −14、底部 +9） |
| 皮肤坠毁 | 三套均正常进入 `crashed`，无 `window.error` |
| 皮肤存档 | 合法 `skin` 保留；非法/旧档回落经典；面板切换持久化 |
| 面板布局 | 390px 宽 300px、320px 宽 292px，三个按钮不溢出 |
| 桌面回归 | 地图点击、十关软着陆通过 |

### Sprint 04（已上线 `0d99d8a`）

| 项目 | 结果 |
|---|---|
| 竖屏旋转提示 | 竖屏显示提示并暂停；点「继续竖屏」恢复 |
| 横屏标题 | 844×390 / 667×375 / 568×320 双栏布局，文字不重叠 |
| 横屏航线图 | 触屏提示与统计按钮；站点标签区域可点选 |
| 横屏 HUD | 按钮与燃料/ALT/VX/VY 间距约 14–17px |
| 安全区 | HUD 左右内缩，横屏刘海不遮挡信息 |
| 桌面回归 | 地图点击、十关软着陆仍通过 |
| 测试数据清理 | 四键已删除，页面回标题 |

### Sprint 05（已上线 `eab719d`）

| 项目 | 结果 |
|---|---|
| 触控键文字 | ✅ 三个按钮无文本节点，箭头由 CSS 绘制 |
| 齿轮/统计按钮 | ✅ 改为 SVG，点击正常 |
| 长按菜单抑制 | ✅ `contextmenu`/`selectstart` 拦截；清除选区 |
| 自动横屏入口 | ✅ 竖屏提示有「尝试自动横屏」；失败显示说明 |
| 旋转后布局 | ✅ `orientationchange` 后画布变为 844×390，切横屏 |
| 设置横屏入口 | ✅ 触屏设备面板显示「尝试横屏」 |
| 触控推力 | ✅ 按住/滑出/抬起行为保持 |
| 十关回归 | ✅ 10/10 |
| 测试数据清理 | ✅ 四键已删除 |

### Sprint 06（已上线 `e56797e`）

| 项目 | 结果 |
|---|---|
| 移除崩溃 API | ✅ 源码无 `requestFullscreen` / `screen.orientation.lock` |
| 横屏提示 | ✅ 「如何横屏」只显示关闭竖屏锁定说明 |
| 旋转后 resize | ✅ 防抖后 844×390 画布/横屏布局 |
| 合成压力 | ✅ 触控按钮 `backdrop-filter` 已移除 |
| 触控推力 | ✅ 按住/滑出/抬起保持 |
| 十关回归 | ✅ 10/10 |
| 测试数据清理 | ✅ 四键已删除 |

### Sprint 07（已上线 `69c959a`）

| 项目 | 结果 |
|---|---|
| Canvas 尺寸 | ✅ CSS/像素比例 1:1（640×360 实测） |
| 横屏地图 | ✅ 5×2 网格，标题/站点/星级不重叠 |
| 横屏 HUD/按钮 | ✅ 燃料/速度与按钮间距 13–28px |
| 横屏标题 | ✅ 右栏暗色底板，文字可读 |
| 圆度 | ✅ 地图圆点/太阳/天体不再椭圆 |
| 十关回归 | ✅ 10/10 |
| 测试数据清理 | ✅ 四键已删除 |

### Sprint 08（已上线 `264194f`）

| 项目 | 结果 |
|---|---|
| 竖屏燃料条 | ✅ 132×8，HUD 上移 92px |
| D5 风标/ATM | ✅ 风标移到站名下方，ATM 移到右上，不重叠 |
| D5 开场长名称 | ✅ 字号自适应，390×844 不贴边 |
| HUD/按钮间距 | ✅ 竖屏仍保持安全间距 |
| 十关回归 | ✅ 10/10 |
| 测试数据清理 | ✅ 四键已删除 |

## 6. 需要人工测试

- **真机触屏**：按钮可见性依赖 `@media (pointer:coarse)`；自动测试使用合成 `PointerEvent`，iPhone/Android 真机仍需确认。
- **安卓横屏圆度/间距**：640×360、844×390 已用 Canvas 截图与比例检查；真机 Chrome 的 DPR、地址栏与刘海安全区需确认。
- **D5/竖屏 HUD**：390×844 已核对风标/ATM/燃料条/开场名称；真机小屏字号与字距需确认。
- **iPhone 旋转提示**：竖屏提示依赖 iOS Safari 的 `orientation:portrait` 与 `pointer:coarse`；自动 Fullscreen/Orientation Lock 已移除，改为手动旋转说明。
- **iPhone 旋转崩溃**：已移除 `requestFullscreen` / `screen.orientation.lock` 与按钮 `backdrop-filter`；真机旋转后是否仍崩溃需重点确认。
- **iPhone 竖屏锁定**：若系统开启竖屏锁定，网页无法强制横屏；需人工关闭锁定后旋转。
- **iPhone 横屏标题/地图**：844×390 等尺寸已用 Canvas 截图核对；真机刘海安全区与 Safari 地址栏下的实际布局需确认。
- **iPhone 系统菜单**：已加 `-webkit-touch-callout` / `user-select` / `contextmenu` / `selectstart` 抑制；需在真机长按按钮与页面确认不再出现复制/翻译条。
- **皮肤观感**：三套皮肤已在桌面 Canvas 截图核对；真机小屏缩放下的辨识度建议人工确认。
- **音频**：首次手势解锁、推力音、爆炸/着陆音、环境音、静音效果。
- **完整人工试玩**：十关软着陆为传送辅助验证；难度数值未改。
- **移动端横屏/安全区**：本次主要验证 390×844 竖屏与 320×568 小屏；横屏与刘海屏安全区需人工确认。
- **长时间运行**：连续坠毁的粒子峰值与内存曲线未做长时压测。

## 7. 最近代码修改摘要

### Sprint 01 — 已上线

| 项 | 内容 |
|---|---|
| commit | `dd6ac7268165eb1194b6ac968d43cee4b4eaa7ef` |
| 文件 | `vector-lander/index.html` |
| 规模 | +29 / −7；2212 行 |
| SHA1 | `9fa81257742fdfca0b705a62f364f77bd83177c4` |
| 内容 | 解锁校验、陨石渲染、存档 `unlocked`、地图飞船数、触屏地图、统计面板指针 |
| 状态 | 已推送、已上线 |

### Sprint 02 — 已上线

| 项 | 内容 |
|---|---|
| commit | `4d200989c3198fde50683d6cdcb375c3ba7a2480` |
| 文件 | `vector-lander/index.html` |
| 规模 | +58 / −15；2255 行 |
| SHA1 | `ce1ad20b296a084961f7b9798d2d3d995e228192` |
| 内容 | 存档硬化、漂移平台包络、统计面板键盘、爆炸粒子上限、死代码清理 |
| 状态 | 已推送、已上线；Pages 哈希已核对 |

### Sprint 03 — 已上线

| 项 | 内容 |
|---|---|
| commits | `7d3a5cf`（站点名）、`7e5cb67`（触控/HUD）、`92df820`（地图/UI）、`8cd40cd`（皮肤） |
| 文件 | `vector-lander/index.html` + `README.md` |
| 规模 | 最终 2501 行；相对 `4d20098` 为多项小批提交 |
| SHA1 | `cf002d2ba86f0c98503f35d5e0aed5abbdd8ce58` |
| 内容 | 手机竖屏地图、触控/HUD、系统菜单抑制、三套飞船皮肤 |
| 状态 | 已推送、已上线；Pages 哈希已核对 |

### Sprint 04 — 已上线

| 项 | 内容 |
|---|---|
| commit | `0d99d8af86b88bef82ca270b0b1eb08a5211a385` |
| 文件 | `vector-lander/index.html` + `README.md` |
| 规模 | 2582 行 |
| SHA1 | `9fab3e5ed88882a04a7b68b54465241ca9799c6a` |
| 内容 | 竖屏旋转提示、横屏双栏标题、横屏地图/HUD、安全区 |
| 状态 | 已推送、已上线；Pages 哈希已核对 |

### Sprint 05 — 已上线

| 项 | 内容 |
|---|---|
| commit | `eab719daf6f7360ca24eda82b3daa61695da5f07` |
| 文件 | `vector-lander/index.html` |
| 规模 | 2639 行 |
| SHA1 | `b9e23824ae73768ad84fb1d1162298edc81d4e61` |
| 内容 | 自动横屏入口、旋转后 resize、CSS/SVG 图标、长按菜单抑制 |
| 状态 | 已推送、已上线；Pages 哈希已核对 |

### Sprint 06 — 已上线

| 项 | 内容 |
|---|---|
| commit | `e56797efdd9c3c4ace9a8e4ce66ab15c28d07d95` |
| 文件 | `vector-lander/index.html` |
| 规模 | 2628 行 |
| SHA1 | `7852b69f222129803ea364635d7a93649dd19855` |
| 内容 | 移除 iOS Fullscreen/Orientation Lock、防抖 resize、移除 backdrop-filter |
| 状态 | 已推送、已上线；Pages 哈希已核对 |

### Sprint 07 — 已上线

| 项 | 内容 |
|---|---|
| commit | `69c959abcd8d9084f0bd53f78f745b63f9884d4e` |
| 文件 | `vector-lander/index.html` |
| 规模 | 2709 行 |
| SHA1 | `51b734839acc87045190c0614df52cac67d20877` |
| 内容 | Canvas 尺寸自愈、横屏 5×2 网格地图、HUD 上移、标题底板 |
| 状态 | 已推送、已上线；Pages 哈希已核对 |

### Sprint 08 — 已上线

| 项 | 内容 |
|---|---|
| commit | `264194f6b1a40a2990c0d544d60c2b61e8b8bee1` |
| 文件 | `vector-lander/index.html` |
| 规模 | 2732 行 |
| SHA1 | `226ae26e6e4c6c12b72cc632f30fb63916440eb4` |
| 内容 | 竖屏 HUD 瘦身、D5 风标/ATM 避让、开场字号自适应 |
| 状态 | 已推送、已上线；Pages 哈希已核对 |

## 8. 下一阶段建议（未批准）

1. 若继续修缺陷，处理 P2-6（视觉）、P2-7/P2-8（预测精度）；这三项会改变可见行为，建议单独一批。
2. 真机 iPhone 旋转/竖屏锁定、安卓横屏圆度/间距、D5/竖屏 HUD、长按菜单、皮肤观感与音频应优先人工验证。
3. 新玩法（Ocean Recovery / Tower Catch）必须等用户单独确认；不得把本报告建议当作批准。
