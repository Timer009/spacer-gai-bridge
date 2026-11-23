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

## 2026-11-23 — Spacer Sprint 01 核心稳定性修复（工作区，未提交）

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

- **未提交、未推送**。远程 Spacer `main` 仍为 `b9d12a7`。
