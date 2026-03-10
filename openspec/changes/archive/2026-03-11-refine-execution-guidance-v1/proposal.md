## Why

当前 Skill 已具备主要能力，但对部分 Agent 来说，关键约束还不够显眼，阶段说明也偏“结果导向”而不够“执行导向”，容易出现规则被忽略、阶段动作不完整、该问用户时没有及时询问的问题。

## What Changes

- 重写 `SKILL.md` 中 S0-S5 的阶段说明，为每个阶段补齐操作步骤、问题与考量、何时询问用户。
- 统一强化关键约束写法，使用更强烈、更显眼的强调语气。
- 增强 `memory_engine.py` 与 `evidence_verifier.py` 的 `instructions` 说明层，补充执行步骤、注意事项、失败条件与下一步提醒。
- 保持现有主流程与 `update/read/verify` 的核心职责不变。

## Capabilities

### New Capabilities
- `execution-guidance-refinement`: 细化 Skill 各阶段执行指引、关键约束强调方式以及脚本 `instructions` 的说明层。

### Modified Capabilities
None.

## Impact

- 影响文件：`literature-explainer/SKILL.md`、`literature-explainer/scripts/memory_engine.py`、`literature-explainer/scripts/evidence_verifier.py`、当前 change artifacts。
- 不新增脚本，不新增模式，不重设主状态机。
