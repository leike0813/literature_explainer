## Why

当前记忆系统将所有论文记录写入同一个 JSONL 文件，学习笔记输出也默认使用固定文件名。这会导致同目录处理多篇论文时，记忆和最终笔记都存在相互覆盖或混淆的风险。

## What Changes

- 引入以 `input_hash` 派生的稳定 `paper_key`，作为论文级主键。
- 将 dispatcher 的标准化输出改为按 `paper_key` 子目录隔离。
- 将记忆存储改为按论文拆分文件，并把 `stage=note` 更新改为覆盖式写入。
- 将学习笔记文件改为按 `paper_key` 唯一命名，并明确重复生成时覆盖同一路径。
- 明确 note 生成范围为“初析全局复用，QA 仅限当前 session”。

## Capabilities

### New Capabilities
- `paper-memory-isolation`: 以论文级 key 隔离 dispatch 产物、记忆文件和最终学习笔记，并保证 note 记录与 note 文件唯一。

### Modified Capabilities

## Impact

- 影响 `literature-explainer/SKILL.md` 的输入输出契约、记忆规则和 note 规则。
- 影响 `literature-explainer/scripts/dispatch_source.py` 的 metadata 与默认输出路径。
- 影响 `literature-explainer/scripts/memory_engine.py` 的默认存储路径与 `stage=note` 更新语义。
