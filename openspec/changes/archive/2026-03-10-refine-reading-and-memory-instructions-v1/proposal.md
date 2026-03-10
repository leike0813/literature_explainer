## Why

当前 Agent 在论文初析与 QA 记忆写入上缺少细粒度指令，导致输出和记忆存在过度浓缩，影响后续学习笔记的信息完整性与可追溯性。

## What Changes

- 细化论文初析输出模板：采用半固定结构，核心章节固定，分章节总结可按论文结构动态增减。
- 细化 QA 记忆写入规则：用户问题完整入库，回答按长度阈值决定是否摘要。
- 调整记忆 schema：QA 记录在单条记录中分字段存储 `user_question` 与 `agent_answer_summary`。
- 约束学习笔记生成：使用记忆字段组织内容，不进行二次压缩，仅允许轻微润色。
- memory 引擎升级到 schema v2，并默认忽略旧 schema 记录。

## Capabilities

### New Capabilities
- `reading-memory-instruction-refinement`: 强化阅读摘要与记忆写入约束，减少信息丢失与过度压缩。

### Modified Capabilities
None.

## Impact

- 影响文件：`literature-explainer/SKILL.md`、`literature-explainer/scripts/memory_engine.py`、当前 change artifacts。
- 不新增外部依赖，不修改现有 `.memory` 存储路径。
