# Proposal: S3 QA Verification Loop Refinement

## Why

当前 S3 问答循环中，agent 机械地执行"回答→verify→回显→memory update→提问"的线性流程，导致：
1. 验证与修正割裂：验证失败后未立即修正草案，而是将问题抛给下一轮
2. 用户交互冗余：验证通过后额外发起一轮"下一轮动作提问"，增加交互轮次
3. 流程不自然：用户期望一次性获得"已验证的最终答案 + 下一步引导"，而非分步执行

本变更旨在优化 S3 执行流程，将验证 - 修正循环内嵌到回答生成阶段，确保用户收到的答案已是验证通过的最终版本。

## What Changes

- 修改 `SKILL.md` 中 S3 问答循环的执行步骤说明
- 将线性流程改为"草案→验证循环→定稿→记忆→用户交互"的内嵌循环模式
- 合并"最终回答文案"和"下一轮动作提问"为单条消息

## Capabilities

### New Capabilities
None.

### Modified Capabilities
- `skill-instruction-architecture`: S3 阶段执行流程从线性改为内嵌验证循环

## Impact

- 影响文件：`literature-explainer/SKILL.md`
- 不影响脚本接口或记忆 schema
- 仅改变 agent 执行流程的自然语言描述
