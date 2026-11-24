# SPACER-SPRINT-09 · 跨浏览器兼容性收尾

## 当前状态

用户反馈 iOS Safari、iOS 和 Android 的 Chrome 与 Edge 横屏正常。两端夸克仍未通过，P1-4 保持开放。以 `319d54ac4256d50cc1fa931fe133c265c89f5315` 为基线收尾，提供兼容横屏直达入口和同页成对采样。等待夸克真机验收及正式发布批准。 [证据、预览与真机操作](../reports/sprint-09/browser-closeout.md)

## Sprint 09 原始任务

用户于 2026-11-24 批准执行。Codex 接管本轮，Z Code 暂停参与。

源码基线为 `264194f6b1a40a2990c0d544d60c2b61e8b8bee1`。开发分支为 `sprint-09-mobile-quality`。

- 审计标题、航线图、关卡开场、飞行 HUD、暂停、设置、统计、成功与失败。修复重叠、截断、图标及触控热区，适配安全区及旋转。
- 验证 iOS Safari、Android Chrome 的竖屏、横屏、旋转、多指和长按。分别记录桌面模拟和真机结果。
- 修复 P2-6、P2-7、P2-8。预测独立提交，维持实际飞行物理及难度。
- 验证 320×568、375×667、390×844、430×932 及对应横屏，以及平板和桌面。保存截图并回归十关启动与着陆、三套皮肤、存档、解锁、暂停、重生和性能。
- 分批提交并推送，保留 main 与线上版本，等待用户验收及正式发布批准。
- 本轮只执行 Sprint 09。Sprint 10–16 等待批准，见 [ROADMAP.md](../ROADMAP.md)。

## 交接状态

开发及桌面模拟回归已完成。云端推送返回 HTTP 403，Windows 本机已通过增量 Git bundle 恢复并发布两个原始分支。首次远程回读与云端 SHA 一致。本机复测、独立预览和待验收事项见 [最新测试](../reports/latest-test.md) 及 [Windows 交接记录](../reports/sprint-09/windows-handoff.md)。真机验收及正式发布批准待完成。
