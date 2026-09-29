# Domain Docs

本仓库采用 single-context 布局：根目录的 `CONTEXT.md` 和 `docs/adr/`。

## 探索代码前

- 阅读根目录的 `CONTEXT.md`，了解领域术语。
- 阅读 `docs/adr/` 中与当前任务相关的架构决策记录（ADR）。
- 如果这些文件不存在，直接继续，不提示缺失，也不提前建议创建。由 `domain-modeling` 技能在术语或决策明确后按需创建。

## 文件布局

```text
/
├── CONTEXT.md
└── docs/adr/
    └── 0001-<decision-slug>.md
```

## 使用术语表

Issue 标题、重构方案、假设和测试名称中的领域概念，应使用 `CONTEXT.md` 定义的术语，避免使用术语表明确排除的同义词。

如果缺少所需概念，先检查是否使用了项目中不存在的概念；确有缺口时，记录下来供 `domain-modeling` 后续处理。

## 明确指出 ADR 冲突

如果方案与已有 ADR 冲突，必须说明冲突的 ADR 及重新讨论该决策的原因，不能默默覆盖。
