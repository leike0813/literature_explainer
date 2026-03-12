- [x] 1.1 编写 `proposal.md`，锁定 `paper-memory-isolation` capability 与变更边界
- [x] 1.2 编写 `specs/paper-memory-isolation/spec.md`，覆盖 dispatcher key、按论文记忆隔离、note 唯一覆盖和 note 读取范围
- [x] 1.3 编写 `design.md`，说明 `paper_key` 来源、按论文路径隔离和 note 文件覆盖策略
- [x] 1.4 编写 `tasks.md`，按 artifacts、实现、校验三组组织任务

- [x] 2.1 更新 `literature-explainer/SKILL.md` 的输入输出、记忆和 note 契约
- [x] 2.2 更新 `literature-explainer/scripts/dispatch_source.py`，输出 `input_hash/paper_key` 并采用 `<tmp>/<paper_key>/...` 路径
- [x] 2.3 更新 `literature-explainer/scripts/memory_engine.py`，实现按论文拆分 memory 文件并移除 `stage=note` 写回

- [x] 3.1 运行 `openspec status --change "isolate-paper-memory-and-single-note-v1" --json`
- [x] 3.2 运行 `openspec instructions apply --change "isolate-paper-memory-and-single-note-v1" --json`
- [x] 3.3 运行 `openspec validate isolate-paper-memory-and-single-note-v1 --type change --json`
- [x] 3.4 运行 `conda run --no-capture-output -n DataProcessing python -u -m mypy literature-explainer/scripts`
- [x] 3.5 用最小样例验证 dispatcher 子目录隔离、按论文 memory 文件、note 文件覆盖写入
