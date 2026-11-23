# CHANGELOG

本文件记录报告仓库的初始化/更新，以及 Spacer 源码变更摘要。源码的完整历史以 <https://github.com/Timer009/Spacer> 为准。

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
