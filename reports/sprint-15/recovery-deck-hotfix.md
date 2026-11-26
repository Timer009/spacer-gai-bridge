# 海上回收结算甲板绑定热修

正式 Pages 基线为 v2.0.15 / `32e1d6f682b05a50d58e2d4145f8497a57590cdf`。公网 HTML 的 Git blob `4eb8147d7e1ef1e44683ca83850277aa537d674c` 与正式分支一致。候选为 v2.0.15-hotfix.1-rc.1，Spacer `f4fb890d78d975a97c15bd5f4d586fbc75da74fc`。 [固定试玩](https://rawcdn.githack.com/Timer009/Spacer/f4fb890d78d975a97c15bd5f4d586fbc75da74fc/vector-lander/index.html) · [兼容横屏](https://rawcdn.githack.com/Timer009/Spacer/f4fb890d78d975a97c15bd5f4d586fbc75da74fc/vector-lander/index.html?compat=1)

## 根因与修复

海上回收成功时已停止独立积分和碰撞检查，也已停止推力。旧版仅在 `landed` 阶段调用 `rideDeck`。进入 `freeResult` 后场景时间继续推进，回收船随 `deckPose` 更新，火箭却停在最后的世界坐标。正式基线专项测试在进入 `freeResult` 的首个更新帧复现，约为辅助进近开始后 1.825 秒。

以着陆支脚中点在甲板上的投影保存实际纵向位置，成功后沿甲板法向贴合。在两个成功阶段的固定步更新中按相同场景时间重建世界姿态。重试、退出及重新进入会清理绑定。现有着陆阈值、轨迹预测、碰撞、镜头、UI 和浪效均沿用。塔架采用固定结构，机械臂根据挂点绘制，专项复查结算期间的承载姿态，未改塔架代码。

## 专项自动化证据

使用现有 `tests/mobile-hotfix.cjs` 的 `SPACER_RECOVERY_ONLY=1`，Chromium 158.0.8127.88 和 Playwright WebKit 26.5 均通过。

- 从常规出生点通过方向和推力输入完成海上回收。另以三组辅助接触验证甲板局部着陆位置 −48.72、+17.72、+48.00，接触相对倾角约 +4.58°、−4.58°、−0.01°。各组逐物理帧检查 18 秒，覆盖提前打开与自动打开结算，支脚始终贴合，船体保持升沉和横摇。
- Chromium 以正常动画循环在结算中连续观察 15.03 秒，采样 884 个渲染帧，甲板局部位置、法线间距和相对角度的各项最大误差均小于 1e-8。
- 验证仅生成一次成功结果、无油耗或独立运动、重试与退出清理绑定、存档隔离及原海上回收失败判定。
- 塔架从正常出生点完成捕获，结算后 18 秒承载姿态稳定，原失败边界通过。未发现同类脱离。

本轮为浏览器自动化专项，随后用户完成候选真机验收，反馈暂未发现异常，验收通过。

两个公网候选 URL 读取的 HTML 与 Spacer 提交的 Git blob 一致，SHA-256 为 `3c6214a3b5f20b25be57c564e804945831b10382e3ce1a88796bbf6ec8d09fb2`。

## 正式发布

发布前复跑 Chromium 回收专项通过，正常结算连续观察 15.04 秒，采样 893 帧。塔架专项一并通过。正式版 `v2.0.15-hotfix.1`，构建 `2.0.15.4`，Spacer `eaa334864b4bf251a82549b8670cad568bd2e355`。正式提交相对已验收候选仅更新构建元数据。 [正式游戏](https://timer009.github.io/Spacer/vector-lander/)

公网 Pages 回读显示正式版本号与构建编号，HTML Git blob `692a4741f0d17c287443dbadb3ce29a1feb02617` 与远程 main 一致，SHA-256 为 `e228afc711adba18e4965d3df1ab4f63ced436df9047412e5c261a7c3d9dd925`。
