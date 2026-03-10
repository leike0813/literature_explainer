## Why

当前流程已要求问答后做证据验证，但“回答文本、记忆条目、学习笔记”三处尚未形成一致的证据原文追溯链路，导致后续复核和笔记复用时可能丢失证据原文。

## What Changes

- 强化 Q&A 输出约束：每次回答必须显式给出结构化证据数组。
- 强化 QA 记忆写入约束：每轮问答记忆必须完整保存证据条目，且 `source` 原文逐字一致。
- 强化学习笔记约束：`问答`章节按轮次逐条列出证据原文，不改写不省略。
- 升级记忆协议到 schema v3：在 `stage=qa` 新增必填 `evidence_items`。

## Capabilities

### New Capabilities
- `evidence-traceability`: 在回答、记忆与学习笔记之间建立可逐条追溯的证据链路。

### Modified Capabilities
None.

## Impact

- 影响文件：`literature-explainer/SKILL.md`、`literature-explainer/scripts/memory_engine.py`、当前 change artifacts。
- 不新增外部依赖、不修改现有验证脚本模式、不改变主状态机阶段划分。
