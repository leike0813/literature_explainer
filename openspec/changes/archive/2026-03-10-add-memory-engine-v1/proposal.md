## Why

当前 Skill 缺少可复用的结构化记忆支撑，学习笔记生成只能依赖当轮上下文，难以稳定复盘多轮问答中的关键事实、证据和未决问题。需要一个脚本驱动的记忆模块来降低 LLM 负担并提高可追溯性。

## What Changes

- 新增记忆引擎脚本，提供 `instructions`、`update`、`read` 三种调用模式。
- 记忆持久化到调用工作目录下 `.memory/literature-explainer.memory.jsonl`。
- 约定触发时机：论文初析后更新一次；每轮 Q&A 结束后更新一次；学习笔记生成前读取原始记忆条目。
- 更新 `SKILL.md`，仅声明脚本调用时机与命令，不内嵌详细提示词。

## Capabilities

### New Capabilities
- `memory-engine`: 通过脚本化方式管理学习笔记支撑记忆，提供取指令、更新和读取能力。

### Modified Capabilities
None.

## Impact

- 影响文件：`literature-explainer/SKILL.md`、`literature-explainer/scripts/memory_engine.py`、本 change artifacts。
- 不引入外部数据库，不修改已有对外 API。
