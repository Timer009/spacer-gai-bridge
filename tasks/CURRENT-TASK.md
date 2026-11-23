# CURRENT TASK — Spacer Sprint 06 iOS 旋转崩溃热修

> 这是**用户已确认**的当前开发任务记录。Sprint 01/02/03/04/05/06 均已推送并上线。
>
> 本文件之外的建议、审计 TODO、下一阶段规划都**不是**已批准任务。

## 1. 任务标识

| 字段 | 值 |
|---|---|
| Task ID | `SPACER-SPRINT-06` |
| 名称 | iOS Safari 旋转崩溃热修 |
| 确认时间 | 2026-11-24（用户反馈：横屏后 Safari 提示网页已崩溃） |
| 源码分支 | `main` |
| 本地 HEAD | `e56797efdd9c3c4ace9a8e4ce66ab15c28d07d95` |
| 远程 `origin/main` | `e56797efdd9c3c4ace9a8e4ce66ab15c28d07d95` |
| 工作区 | 干净 |
| 文件 | `vector-lander/index.html`，2628 行；SHA1 `7852b69f222129803ea364635d7a93649dd19855` |
| 状态 | **已完成 / 已推送 / 已上线** |

## 2. 已确认范围

- 移除 `requestFullscreen` / `screen.orientation.lock`，改为手动横屏说明。
- 横屏提示按钮改为「如何横屏」，显示关闭竖屏锁定的说明。
- `resize` / `orientationchange` 改为防抖，减少旋转时重复重建画布。
- 移除触控按钮 `backdrop-filter`，降低 iOS 合成压力。

## 3. 明确不做

- 不改 P2-6（漂移平台削平视觉）。
- 不改 P2-7 / P2-8（预测线精度/视距）。
- 不改重力、燃料、平台宽度、速度阈值等难度参数。
- 不开发 Ocean Recovery / Tower Catch。
- 不修改 Git 全局代理或系统代理。

## 4. 验收与证据

| 验收项 | 结果 |
|---|---|
| 崩溃 API 移除 | ✅ 源码无 `requestFullscreen` / `orientation.lock` |
| 横屏提示 | ✅ 只显示手动旋转说明 |
| 旋转后布局 | ✅ 防抖后 844×390 画布/横屏布局 |
| 合成压力 | ✅ `backdrop-filter` 已移除 |
| 十关回归 | ✅ 10/10 |
| 测试数据清理 | ✅ 四键为空 |

完整结果：[reports/latest-test.md](../reports/latest-test.md)

## 5. 当前待决策

1. 真机 iPhone 旋转后是否仍崩溃（重点确认）。
2. 是否继续处理 P2-6 / P2-7 / P2-8（会改变可见行为，建议单独一批）。
3. 是否批准新玩法；未批准前不得开始。
