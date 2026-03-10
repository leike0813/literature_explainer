## Why

当前项目已经可以生成学习笔记，但 note 阶段还只有原则性约束，缺少稳定的章节结构和明确的生成/结束分叉，导致最终产物容易在内容组织和信息密度上漂移。

## What Changes

- 明确学习笔记生成是显式可选动作，用户可选择不生成并直接结束。
- 将学习笔记固定为“单段论文摘要 + 以问答为核心的主体结构”。
- 强化 `SKILL.md` 中 S2/S4/S5 的切换规则和 note 阶段固定执行顺序。
- 强化 `memory_engine.py` 的 `instructions --stage note`，明确固定章节、Q&A 四项结构、只消费结构化记忆字段，以及生成后写回 `stage=note` 记录。

## Capabilities

### New Capabilities
- `note-generation-stability`: 稳定学习笔记生成结构、记忆消费规则和可选生成流程。

### Modified Capabilities
None.

## Impact

- 影响文件：`literature-explainer/SKILL.md`、`literature-explainer/scripts/memory_engine.py`、当前 change artifacts。
- 不新增新脚本，不修改 `read` 基本过滤接口，不改变 Q&A 与证据验证的既有职责。
