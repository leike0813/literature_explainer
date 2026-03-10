## Context

项目当前只有 OpenSpec 框架与 AGENTS 约束，业务 Skill 包目录为空。目标是先建立可执行的最小骨架，作为后续 Change 的稳定基线。

## Goals / Non-Goals

**Goals:**
- 提供最小可用 Skill 包结构。
- 交付可执行的 `SKILL.md` 结构化初版。
- 将实现范围限制在“骨架初始化”。

**Non-Goals:**
- 不创建脚本与资源目录。
- 不添加 UI metadata（如 `agents/openai.yaml`）。
- 不做发布级细化和自动化扩展。

## Decisions

1. 决策 1：采用最小根包策略，仅创建 `literature-explainer/SKILL.md`。  
   备选方案：同时创建 `references/`、`scripts/`、`assets/`、`agents/`。  
   选择理由：最小化范围，确保 Change 边界清晰，避免初始化阶段过度设计。

2. 决策 2：`SKILL.md` 采用结构化初版，而非 TODO 占位。  
   备选方案：先写空模板后续再补。  
   选择理由：结构化初版可以立即支持 Agent 执行，减少后续返工。

3. 决策 3：本 Change 不引入脚本与额外依赖。  
   备选方案：初始化阶段即加入辅助脚本。  
   选择理由：当前核心是建立指令骨架，脚本应在后续专门 Change 中按需引入。

## Risks / Trade-offs

- [Risk] 最小骨架可能无法覆盖后续复杂场景 → Mitigation：后续通过独立 Change 增量补充目录与脚本。
- [Risk] 初版指令可能不够细致 → Mitigation：在下一轮基于真实问答流程补全细节并验证。
