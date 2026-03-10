## Context

项目当前的能力已经覆盖论文初析、证据化问答、记忆更新和学习笔记生成，但 `SKILL.md` 已演化为多轮增量叠加文档，阅读顺序不再贴合实际执行顺序。同时，两个脚本的 `instructions` 输出风格不一致，增加了 Agent 的切换成本。

## Goals / Non-Goals

**Goals:**
- 将 `SKILL.md` 重写为主流程优先的发布版主指令。
- 将证据、记忆、学习笔记规则分别收敛到单一主落点。
- 统一两个脚本 `instructions` 的顶层 JSON 结构。
- 保留现有 CLI 行为与业务能力。

**Non-Goals:**
- 不新增新的脚本或新的状态。
- 不引入 `references/` 或 playbook。
- 不改变 `memory_engine.py` 的 `update/read` 语义，也不改变 `evidence_verifier.py` 的 `verify` verdict 语义。

## Decisions

1. `SKILL.md` 采用“主流程优先”结构。
   理由：让 Agent 先读到任务目标、状态机、硬约束，再读到脚本调用细节。

2. `SKILL.md` 只保留主规则与调用时机，字段级细则下放到脚本 `instructions`。
   理由：避免主文档继续膨胀，同时保持脚本协议是单一事实来源。

3. 两个脚本的 `instructions` 统一为同一顶层结构。
   理由：降低 Agent 调用多个脚本时的协议切换成本。

## Risks / Trade-offs

- [Risk] 过度下放细则后，主文档可能变得过于抽象。
  Mitigation：保留状态机、硬约束、调用顺序和最终产物要求在 `SKILL.md` 中。
- [Risk] 统一 `instructions` 结构时可能破坏既有调用预期。
  Mitigation：只重构 `instructions` 输出，不改 `update/read/verify` 的 CLI 入口和核心职责。
