## Context

当前 Skill 已有稳定的论文分析和问答流程，但没有外部化记忆模块。为避免把“总结规则与记忆更新逻辑”完全压给 LLM，需要新增脚本作为确定性支撑。

## Goals / Non-Goals

**Goals:**
- 提供脚本驱动的记忆模块，服务最终学习笔记生成。
- 固定三种调用模式：`instructions`、`update`、`read`。
- 固定存储介质与路径：工作目录 `.memory` 下单文件 JSONL。

**Non-Goals:**
- 不做每次提问前的动态记忆读取注入。
- 不接入外部数据库、向量库或检索服务。
- 不在本 change 内实现复杂的记忆压缩策略。

## Decisions

1. 采用三模式并列接口：`instructions/update/read`。  
   备选：仅两模式或把读取并入更新。  
   理由：满足“脚本给指令 + 执行更新 + 学习笔记时读取”的独立职责。

2. 持久化使用单文件 JSONL（`$PWD/.memory/literature-explainer.memory.jsonl`）。  
   备选：SQLite 或多文件分片。  
   理由：可读性强、实现最轻、适合当前规模。

3. `SKILL.md` 仅描述调用时机和命令，不嵌详细 prompt。  
   备选：在 SKILL 内写详细总结提示词。  
   理由：提示细则放在 `instructions` 输出，降低主文档噪声与维护成本。

## Risks / Trade-offs

- [Risk] JSONL 长期增长影响读取效率 → Mitigation：`read` 提供 `paper_key/session_key/limit` 过滤。
- [Risk] Agent 传入 payload 缺字段导致脏数据 → Mitigation：`update` 执行必填字段校验并返回错误信息。
