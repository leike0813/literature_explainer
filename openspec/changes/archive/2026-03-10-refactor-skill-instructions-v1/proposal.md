## Why

当前项目的核心能力已经具备，但 `SKILL.md` 累积了多轮 change 的增量规则，主流程、细则、脚本协议交织在一起，不利于发布与后续维护。现在需要把现有能力重组为一版更稳定的发布版指令体系。

## What Changes

- 重构 `SKILL.md` 为“主流程优先”的发布版主指令文档。
- 收敛证据、记忆、学习笔记规则，避免同一规则分散在多个章节重复出现。
- 统一 `memory_engine.py` 与 `evidence_verifier.py` 的 `instructions` 输出风格。
- 保留现有核心能力与 CLI 行为，只调整主文档与 `instructions` 协议表达。

## Capabilities

### New Capabilities
- `skill-instruction-architecture`: 定义发布版 Skill 主指令结构以及脚本 `instructions` 的统一协议风格。

### Modified Capabilities
None.

## Impact

- 影响文件：`literature-explainer/SKILL.md`、`literature-explainer/scripts/memory_engine.py`、`literature-explainer/scripts/evidence_verifier.py`、当前 change artifacts。
- 不新增脚本、不新增目录、不改变 `update/read/verify` 的核心职责。
