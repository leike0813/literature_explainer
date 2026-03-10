## Why

当前仓库尚未具备可执行的 Skill 包骨架，导致后续能力迭代（流程细化、脚本补充、验收归档）缺少稳定入口。先建立最小骨架可以让后续 Change 在统一结构上推进。

## What Changes

- 新增最小 Skill 包结构：`literature-explainer/` 根目录及 `SKILL.md`。
- 编写可执行的 `SKILL.md` 结构化初版（frontmatter + 流程与约束）。
- 明确本次不创建可选目录（`references/`、`scripts/`、`assets/`、`agents/`）。

## Capabilities

### New Capabilities
- `skill-package-scaffold`: 初始化 Skill 包最小骨架并提供可执行初版指令文档。

### Modified Capabilities
None.

## Impact

- 影响范围仅限 Skill 包目录和 OpenSpec 变更文档。
- 不引入外部依赖，不涉及 API、协议或数据类型变更。
