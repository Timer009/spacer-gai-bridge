# reports/history

本目录保存被替换下来的历史报告，作为不可更改的证据归档。

## 命名规则

```text
YYYY-MM-DD-<topic>.md
```

示例：

```text
2026-11-23-audit-baseline-526397a.md
2026-11-23-sprint-01-test.md
```

## 规则

- `reports/latest-*.md` 始终指向当前版本。
- 在覆盖 `latest-*.md` 之前，把旧版完整移入本目录，不要只保留摘要。
- 归档文件不修改、不删除，除非用户明确要求。
- 每份归档报告都应保留其对应的源码 commit SHA 与工作区状态。

当前尚无被替换的归档报告。
