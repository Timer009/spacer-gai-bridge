# 游戏版本登记

每轮候选及正式发布使用[永久交付规范](DELIVERY.md)。


候选使用 `v2.0.<Sprint>-rc.<N>`，同一 Sprint 每次交付递增。正式归档时移除 `-rc.<N>`，构建编号继续递增，并更新 UTC 构建时间和发布渠道。交付以对应源码提交的完整 SHA 固定试玩链接。

| 版本 | 构建编号 | UTC 构建时间 | 渠道 | Spacer Git SHA | 试玩 |
|---|---|---|---|---|---|
| v2.0.13-rc.5 | 2.0.13.5 | 2026-11-24T12:06:24Z | 候选预览 | `a724b6aca344169199e2a1e1991523f099ca5196` | [固定版](https://rawcdn.githack.com/Timer009/Spacer/a724b6aca344169199e2a1e1991523f099ca5196/vector-lander/index.html) |
| v2.0.13-rc.6 | 2.0.13.6 | 2026-11-24T13:11:16Z | 候选预览 | `e219406c94737749b0b57e6d0505de33df76018d` | [固定版](https://rawcdn.githack.com/Timer009/Spacer/e219406c94737749b0b57e6d0505de33df76018d/vector-lander/index.html) |
| v2.0.13 | 2.0.13.7 | 2026-11-24T13:34:16Z | 正式发布 | `b61e1af9c2915186687e7066d00d009e21f57879` | [Pages](https://timer009.github.io/Spacer/vector-lander/) |
| v2.0.14-rc.1 | 2.0.14.1 | 2026-11-24T13:37:47Z | 候选预览 | `bddbd34bc96174bec293db9a2e497d00bcea130c` | [固定版](https://rawcdn.githack.com/Timer009/Spacer/bddbd34bc96174bec293db9a2e497d00bcea130c/vector-lander/index.html) |
| v2.0.14 | 2.0.14.2 | 2026-11-24T14:03:32Z | 正式发布 | `951d13b58e4800d0f9afa57bf362d2b15a186aac` | [Pages](https://timer009.github.io/Spacer/vector-lander/) |
| v2.0.15-rc.1 | 2.0.15.1 | 2026-11-24T14:07:09Z | 候选预览 | `b9c872526e7b4e23e639ddee407a51d933d1a632` | [固定版](https://rawcdn.githack.com/Timer009/Spacer/b9c872526e7b4e23e639ddee407a51d933d1a632/vector-lander/index.html) |
| v2.0.15-rc.2a | 2.0.15.2a | 2026-11-24T15:57:33Z | 候选预览 | `265c40e0166ae7a7643f46f1da2086841aa7056f` | [固定版](https://rawcdn.githack.com/Timer009/Spacer/265c40e0166ae7a7643f46f1da2086841aa7056f/vector-lander/index.html) |
| v2.0.15-rc.2b | 2.0.15.2b | 2026-11-24T16:37:16Z | 候选预览 | `487f691011f3036548c5b31c6e74bce842b4df14` | [固定版](https://rawcdn.githack.com/Timer009/Spacer/487f691011f3036548c5b31c6e74bce842b4df14/vector-lander/index.html) |

rc.5 接续此前四次 Sprint 13 候选交付，是首个在页面显示构建身份的版本。上一横屏候选 `8817c4822e4dba98a9807ed632a5e00ba6dd2bb9` 使用旧页面模板。
