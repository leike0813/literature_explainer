## Why

当前 `SKILL.md` 已经具备证据回答、验证回显、记忆更新和笔记生成规则，但每轮 Q&A 的最终输出外观仍不够固定，阶段切换前也缺少明确检查清单。这会导致 Agent 在高风险场景下容易漏项、跳步，尤其是在多问题输入、澄清、验证失败后的修正链路上。

## What Changes

- 固定 S3 每轮 Q&A 的标准回答模板，并将验证结果回显纳入同一轮输出契约。
- 为 S1、S3、S4 增加“离开本阶段前必须确认”的退出检查清单。
- 增加多问题输入处理规则、最小化澄清原则，以及验证失败后的修正规则。
- 同步增强记忆脚本和证据验证脚本的 `instructions` 说明层，明确 QA 记忆写入前置条件和 `fail/uncertain` 后续动作。

## Capabilities

### New Capabilities
- `response-contract-stability`: 固定问答输出契约、阶段退出检查以及验证失败后的修正规则，减少执行漂移。

### Modified Capabilities

## Impact

- 影响 `literature-explainer/SKILL.md` 的 S1-S4 指令结构与自然语言契约。
- 影响 `literature-explainer/scripts/memory_engine.py` 与 `literature-explainer/scripts/evidence_verifier.py` 的 `instructions` 输出说明层。
- 不修改 `verify/update/read` 的 CLI 行为，不引入新脚本或新持久化格式。
