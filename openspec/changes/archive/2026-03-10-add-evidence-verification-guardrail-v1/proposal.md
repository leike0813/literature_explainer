## Why

当前 Skill 虽要求证据化回答，但缺少“回答后自动核验”的硬约束与会话级纠偏机制，导致 Agent 可能输出不可查证来源而不被及时发现。

## What Changes

- 强化 Q&A 回答约束：每次回答必须给出可查证来源与验证关键词。
- 新增回答后执行的证据验证脚本，支持网页链接和参考文献标题核验。
- 增加会话级结果回显与幻觉处理机制：
  - 校验失败：触发内部纠偏指令 + 固定用户警告文案。
  - 校验不确定：强制回显“不确定”，不判定为幻觉。
- 将详细校验规则下放到脚本 `instructions`，`SKILL.md` 仅保留调用时机与命令约定。

## Capabilities

### New Capabilities
- `evidence-verification-guardrail`: 基于脚本化验证强化证据可查证性并提供幻觉处理流程。

### Modified Capabilities
None.

## Impact

- 影响文件：`literature-explainer/SKILL.md`、`literature-explainer/scripts/evidence_verifier.py`、当前 change artifacts。
- 不新增外部数据库，不改变已有 memory 模块接口。
