# Latest Test Report — Spacer Sprint 01 / Sprint 02

> 本报告只记录实际执行过的测试。未执行的测试在文末明确标记为“需要人工测试”，不把推断当作结果。

## 1. 测试对象（Sprint 01）

| 字段 | 值 |
|---|---|
| 测试时间 | 2026-11-23 22:00–23:20 +08:00（Asia/Shanghai） |
| 源码仓库 | <https://github.com/Timer009/Spacer> |
| 分支 | `main` |
| 源码 commit（测试基线） | `b9d12a75a379033bb5747027b4b8e785592524ed` |
| 工作区状态（测试时） | `M vector-lander/index.html`（+29 / −7） |
| 被测文件 | `vector-lander/index.html`，2212 行 |
| 文件 SHA1 | `9fa81257742fdfca0b705a62f364f77bd83177c4` |
| 测试环境 | Windows，本地静态 HTTP 服务，内置浏览器 |
| 视口 | 1280×720（桌面）与 390×844（移动竖屏） |
| 驱动方式 | `window.game` 测试钩子 + 合成 `KeyboardEvent` / `PointerEvent` + 同步 `game.tick(ms)` |
| 部署状态 | Sprint 01 已推送为 `dd6ac72`；Sprint 02 已推送为 `4d20098` |

### 重要说明

- Sprint 01 已作为 `dd6ac7268165eb1194b6ac968d43cee4b4eaa7ef` 推送，Pages 已核对为 Sprint 01 哈希。
- Sprint 02 已作为 `4d200989c3198fde50683d6cdcb375c3ba7a2480` 推送，Pages 已核对为 Sprint 02 哈希；结果见第 4 节。
- 本报告第 2–3 节的测试基线为 `b9d12a7` + Sprint 01 工作区修改；该修改随后作为 `dd6ac72` 上线。
- 十关着陆测试使用 `game.jump()` 装载关卡，再用 `teleport()` 把飞船放到平台上方缓降；这验证的是碰撞、判定、结算与状态机路径，不等同于真人完整试玩。
- 解锁门槛另用地图 UI 路径单独测试（不经过 `jump()`）。
- 触屏测试使用合成 `PointerEvent`；内置浏览器未模拟 `pointer:coarse` 媒体特性，真机按钮可见性需人工确认。

## 2. 结果总览

| ID | 测试 | 结果 |
|---|---|---|
| T01 | 未解锁关卡：键盘绕过 | ✅ 拦截 |
| T02 | 未解锁关卡：鼠标点击 | ✅ 拦截 |
| T03 | 未解锁关卡：触屏点击 | ✅ 拦截 |
| T04 | 十关合法启动 | ✅ 10/10 |
| T05 | 十关软着陆 | ✅ 10/10 |
| T06 | 坠毁、重生与结束 | ✅ 通过 |
| T07 | gameover 后地图飞船数 | ✅ 显示正确 |
| T08 | 陨石自然生成半径 | ✅ 5/5 `r=9` |
| T09 | 陨石头部/辉光/拖尾 | ✅ 截图确认 |
| T10 | 陨石碰撞半径 | ✅ 9 单位不变 |
| T11 | 合法旧存档 | ✅ 保留 |
| T12 | 非法存档 5 种 | ✅ 安全回落 |
| T13 | 最佳成绩与统计未被清空 | ✅ 保留 |
| T14 | 触屏地图方向键 | ✅ 只选择不发车 |
| T15 | 触屏地图按键残留 | ✅ 无残余推力 |
| T16 | 游戏中触屏推力 | ✅ 可推、松开即停 |
| T17 | 统计面板点击穿透 | ✅ 不穿透 |
| T18 | 清档与标题恢复 | ✅ 四键为空 |
| T19 | 十关启动异常监听 | ✅ 无未处理异常 |
| T20 | 最终改动后冒烟回归 | ✅ 通过 |

## 3. 详细结果

### T01–T03 未解锁拦截

设置 `progress.unlocked = 0`，在地图上选择第 10 关（index 9）。

| 入口 | 操作 | 结果 |
|---|---|---|
| 键盘 | `Space` | `state=map`，`level=0`，`mapSel=9`，未进入关卡 |
| 鼠标 | 点击第 10 关节点 | `state=map`，`level=0`，未进入关卡 |
| 触屏 | 合成 PointerEvent 点击节点 | `state=map`，`level=0`，未进入关卡 |

- 地图显示「站点未解锁 / 需先通关前一站」。
- `progress.unlocked` 保持 0。
- `score`、`lives`、`level` 均未改变。

### T04 十关合法启动

设置 `progress.unlocked = 9`，通过地图方向键选择站点、`Space` 出发。

| 关卡 | 天体 | 结果 |
|---|---|---|
| 0 | 月球（静海） | `levelIntro` |
| 1 | 月球（风暴洋） | `levelIntro` |
| 2 | 月球（暗面） | `levelIntro` |
| 3 | 带（小行星带） | `levelIntro` |
| 4 | 火星（水手谷） | `levelIntro` |
| 5 | 火卫一（引力井） | `levelIntro` |
| 6 | 木卫一（火山地带） | `levelIntro` |
| 7 | 木卫二（冰原） | `levelIntro` |
| 8 | 木星（云海） | `levelIntro` |
| 9 | 冥王星（斯普特尼克） | `levelIntro` |

- 10/10 关卡索引、天体、关卡类型正确。
- 平台探测在 9 个非 `planetoid` 关卡返回有限 `cx/y`；第 6 关为弧形平台，`padProbe()` 的 `cx/y` 为 `NaN` 属预期。
- 启动期间安装的 `window.error` 监听未捕获未处理异常。

### T05 十关软着陆

方法：`game.jump(i)` → `teleport(pad.cx, pad.y - 12, 0, 8, 0)` → `tick(400)`。

| 关卡 | 类型 | 结果 | 星级 |
|---|---|---|---|
| 0 | terrain | `landed` | 3★ |
| 1 | terrain | `landed` | 3★ |
| 2 | terrain | `landed` | 3★ |
| 3 | terrain | `landed` | 3★ |
| 4 | terrain | `landed` | 3★ |
| 5 | planetoid | `landed` | 3★ |
| 6 | terrain | `landed` | 3★ |
| 7 | terrain（漂移冰筏） | `landed` | 3★ |
| 8 | float（移动坞站） | `landed` | 3★ |
| 9 | terrain | `landed` | 3★ |

- 10/10 进入 `landed`，`progress.stars[i]` 写入 3。
- `stats.landings` 与 `stats.perfects` 每次 +1。
- 漂移平台着陆后由 `update()` 的 `landed` 分支跟随，状态未被破坏。

### T06 坠毁、重生与结束

`settings.lives = 2`，第 4 关两次高速触地（`teleport` 到平台上 20 单位，`vy=60`）。

| 步骤 | 结果 |
|---|---|
| 第一次坠毁 | `state=crashed`，`lives=1`，`stats.crashes+1` |
| 等待 1.8s + 0.9s | `state=levelIntro → playing`，`lives=1` |
| 第二次坠毁 | `state=crashed`，`lives=0` |
| 等待 1.8s | `state=gameover` |

### T07 gameover 后地图飞船数

- 内部状态：`state=map`，`lives=0`，`runFresh=true`（内部变量，非测试钩子暴露）。
- 地图截图显示：`飞船 ×2`（`settings.lives=2`），不再显示 `×0`。
- 在地图上按 `Space` 启动下一关：`lives` 恢复为 2，`score=0`，进入 `levelIntro`。
- 说明：修复只改地图显示；生命数仍在 `launch()` 时恢复，原有失败/重开规则未变。

### T08–T10 陨石

自然生成：

- 第 4 关推进约 16 秒后，场景中 5 颗陨石全部 `r = 9`。
- 创建字段：`{x, y, vy, r}`。

视觉：

- 暂停画面后截图核对：陨石头部亮点、外圈辉光、向上拖尾均可见。
- 测试时使用一颗 `vy=0` 的陨石固定在飞船附近，确保截图稳定；绘制代码与自然陨石相同。

碰撞：

- 在船头正上方 9.1 单位放置陨石 → `state=playing`（不撞）。
- 在船头正上方 8.9 单位放置陨石 → `state=crashed`。
- 结论：碰撞半径仍是 9，未被视觉修复改变。
- 另在自然陨石雨中观察到一次 `CRASH · 陨石雨撞击`，说明自然路径碰撞正常。

### T11–T13 存档

通过 `localStorage.setItem('vl_progress', raw)` + 刷新页面测试。

| 用例 | 输入 `unlocked` | 读取结果 | 地图 `mapSel` | 结果 |
|---|---|---:|---:|---|
| 合法旧档 | `3`（`stars=[1,0,2,…]`） | 3 | 3 | ✅ 星级保留 |
| 负数 | `-3` | 0 | 0 | ✅ |
| 超范围 | `999` | 9 | 9 | ✅ |
| 小数 | `2.7` | 2 | 2 | ✅ |
| 字符串 | `"3"` | 0 | 0 | ✅ |
| 坏 JSON | `{bad` | 0 | 0 | ✅ |

- 每个用例同时写入 `vl_best=1234`、`vl_stats={landings:7,crashes:3,perfects:2}`。
- 所有用例刷新后 `best=1234`、统计值保持不变。
- 合法旧档的 `stars` 数组内容保持不变。

### T14–T16 移动端输入（390×844）

- 地图态 `▲`：`state=map`，`level` 不变，不发车。
- 地图态 `◀/▶`：`mapSel` 分别 -1 / +1，状态保持 `map`。
- 地图态点过 `▲` 后再从地图出发：进入关卡并推进 1.4 秒后，燃料 `120`，等于关卡初始燃料 `120`，说明没有残余推力。
- 游戏中按住 `▲` 300ms：燃料 `120 → 118.2`（−1.8）；松开后再推进 300ms，燃料保持 `118.2`，推力已停止。

### T17 统计面板

- 地图 `mapSel=9`，按 `S` 打开统计面板。
- 点击第 10 关节点：`state=map`，`mapSel=9`，`level` 不变；面板关闭，未发车。
- 面板关闭后再次点击同一点：正常启动第 10 关（`state=levelIntro`）。
- 结论：打开时阻止穿透，关闭后恢复原有交互。

### T18 清档

删除以下四个键并刷新：

```text
vl_best
vl_cfg
vl_progress
vl_stats
```

结果：

- 四键均为 `null`。
- `progress.unlocked=0`，`stars` 全 0。
- `best=0`，`stats` 全 0。
- 设置恢复默认（`gScale=0.9`、`thrust=44`、`burn=6`、`vyMax=36`、`vxMax=26`、`padW=1.2`、`spawnH=380`、`lives=4`）。
- 页面回到标题画面。

### T19 异常监听

- 十关启动流程中安装 `window.error` 监听，结果为空数组。
- 这不是完整的 console 错误捕获；只证明没有未处理的 `window.error`。

### T20 最终改动后冒烟回归

在最后一次代码改动（碰撞判定改用 `METEOR_R`）后重新加载页面：

- 解锁门槛：仍拦截。
- 自然陨石：`r=9`。
- 碰撞：9.1 不撞，8.9 撞。
- 第 1 关软着陆：`landed`，3★。
- 页面无加载失败。

## 4. Sprint 02 追加测试（2026-11-24）

### 4.1 测试对象

| 字段 | 值 |
|---|---|
| 测试时间 | 2026-11-24 00:00–00:03 +08:00 |
| 本地 HEAD | `4d200989c3198fde50683d6cdcb375c3ba7a2480` |
| 远程 `origin/main` | `4d200989c3198fde50683d6cdcb375c3ba7a2480`（Sprint 02，已上线） |
| 工作区 | 干净 |
| 被测文件 | `vector-lander/index.html`，2255 行 |
| 文件 SHA1 | `ce1ad20b296a084961f7b9798d2d3d995e228192` |
| 部署状态 | **已推送 `4d20098`，已上线**；Pages 哈希 `ce1ad20…` 已核对 |

### 4.2 结果总览

| ID | 测试 | 结果 |
|---|---|---|
| T21 | 合法旧存档完整保留 | ✅ |
| T22 | 损坏存档安全回落 | ✅ |
| T23 | 第 8 关漂移平台重叠 | ✅ 240 次装载零重叠 |
| T24 | 统计面板键盘确认键 | ✅ 第一次只关面板，第二次才出发 |
| T25 | 十关启动回归 | ✅ 10/10 |
| T26 | 十关软着陆回归 | ✅ 10/10 |
| T27 | 触屏地图回归 | ✅ |
| T28 | 死代码清理 | ✅ 无引用，页面正常 |
| T29 | 测试数据清理 | ✅ 四键为空 |
| T30 | 加载与异常监听 | ✅ 无 `window.error` |

### 4.3 详细结果

#### T21 合法旧存档完整保留

写入并刷新：

```text
vl_progress = { stars:[1,2,3,0,0,0,0,0,0,0], unlocked:5 }
vl_best     = 1234
vl_stats    = { landings:7, crashes:3, perfects:2 }
vl_cfg      = { gScale:1.0, thrust:50, burn:8, vyMax:40, vxMax:30,
                padW:1.5, spawnH:500, lives:6,
                trail:false, unlockAll:true, shake:false }
```

刷新后逐项完全一致：

- `stars=[1,2,3,0,0,0,0,0,0,0]`，`unlocked=5`
- `best=1234`，`stats={7,3,2}`
- 全部 8 个数值设置与 3 个布尔设置保持原值

#### T22 损坏存档安全回落

写入极端值并刷新：

```text
progress.stars = [1000000000, -5, 2.7, "3", null, 4, 0, 0, 0, 0]
progress.unlocked = "3"
vl_best = "abc"
vl_stats = { landings:"7", crashes:-2, perfects:1e999 }
vl_cfg = { gScale:"x", thrust:999, burn:-1, vyMax:null, vxMax:0,
           padW:99, spawnH:"y", lives:0,
           trail:"yes", unlockAll:1, shake:null }
```

刷新后：

| 字段 | 结果 |
|---|---|
| `stars` | `[3,0,2,0,0,3,0,0,0,0]` |
| `unlocked` | 0 |
| `best` | 0 |
| `stats` | `{0,0,0}` |
| `gScale` | 0.9（异常→默认） |
| `thrust` | 70（999→上限） |
| `burn` | 2（负数→下限） |
| `vyMax` | 36（null→默认） |
| `vxMax` | 8（0→下限） |
| `padW` | 2.5（99→上限） |
| `spawnH` | 380（字符串→默认） |
| `lives` | 2（0→下限） |
| `trail` / `unlockAll` / `shake` | `true / false / true`（非布尔→默认） |

- 进入地图后正常渲染 3★/2★/3★，未捕获 `window.error`。
- 说明：这是针对明确构造的损坏值；不构成全集模糊测试。

#### T23 第 8 关漂移平台重叠

方法：连续 `game.jump(7)` 装载第 8 关，读取两块冰筏的 `cx/amp/w`，计算完整漂移包络 `[cx-amp-w/2, cx+amp+w/2]`，检查相邻包络间距。

| `padW` | 装载次数 | 最小间距 | 重叠次数 | 非有限值 |
|---:|---:|---:|---:|---:|
| 1.2（默认） | 120 | 142.93 | 0 | 0 |
| 2.5（最宽） | 120 | 154.75 | 0 | 0 |

生成器要求至少 140 的间距；240 次随机装载均满足。

#### T24 统计面板键盘确认键

- 地图态按 `S` 打开统计面板。
- 第一次按 `Space`：`state=map`，`level=0`，未出发；面板关闭。
- 第二次按 `Space`：正常出发第 1 关，`state=levelIntro`。
- 结论：统计面板打开时，确认键只关闭面板，不再穿透出发。

#### T25 / T26 十关回归

- 十关通过地图方向键 + `Space` 启动：10/10 进入 `levelIntro`，关卡索引与天体正确。
- 十关通过 `jump` + 平台上方缓降：10/10 `landed`，均 3★。
- 第 8 关漂移冰筏、第 9 关浮空坞站着陆后状态正常。

#### T27 触屏地图回归

- 地图态 `▲`：`state=map`，`level` 不变，不发车。
- 地图态 `◀/▶`：`mapSel` 分别 -1 / +1。
- 结论：Sprint 01 的触屏行为保持。

#### T28 死代码清理

- 全文件搜索：`drawPadLabel` 无定义、无调用。
- `const [ax, ay] = shipPt(...)` 未使用行已删除；`explode()` 中的 `ax/ay` 正常保留。
- 页面加载与十关回归正常。

#### T29 测试数据清理

删除 `vl_best / vl_cfg / vl_progress / vl_stats` 后刷新：

- 四键均为 `null`。
- 进度、最佳分、统计全零，设置恢复默认。
- 页面回到标题。

#### T30 粒子上限说明

- `explode()` 后新增 `PARTICLE_CAP = 900` 裁剪。
- 这是代码级上限验证；**没有**对实际粒子数量/内存曲线做定量测量，见第 5 节。

## 5. 未执行 / 需要人工测试

以下项目**没有**在本次自动化中完成，不得视为通过：

- 真机触屏：按钮可见性、热区、手指滑出、多指、iOS Safari。
- 音频：首次手势解锁、推力音、爆炸/着陆音、环境音、静音。
- 真人完整十关试玩（本次着陆为传送辅助）。
- 移动端横屏、安全区、刘海屏。
- 长时间运行的内存/粒子峰值；Sprint 02 的 900 上限未做定量粒子测量。
- 屏幕极窄（320px）下 HUD 与生命图标重叠。
- 第 8 关漂移平台为 240 次随机装载抽样，不是所有随机种子的形式化证明。
- 损坏存档测试为明确构造的样本，不是全集模糊测试；跨版本迁移矩阵仍未覆盖。

## 6. 结论

- **Sprint 01** 已作为 `dd6ac7268165eb1194b6ac968d43cee4b4eaa7ef` 推送，Pages 文件哈希已核对为 `9fa8125…`。
- **Sprint 02** 已作为 `4d200989c3198fde50683d6cdcb375c3ba7a2480` 推送，Pages 文件哈希已核对为 `ce1ad20…`；A–F 之外的 5 项低风险修复与存档硬化均已上线。
- 测试数据已清理；本报告可作为两次上线后行为的证据。
