- [x] 1.1 编写 `proposal.md`，锁定 `response-contract-stability` capability 与变更边界
- [x] 1.2 编写 `specs/response-contract-stability/spec.md`，覆盖固定回答模板、多问题处理、最小化澄清、验证失败修正、阶段退出检查
- [x] 1.3 编写 `design.md`，说明 contract-first、无 schema 扩展与 fail repair 设计决策
- [x] 1.4 编写 `tasks.md`，按 artifacts、实现、校验三组组织任务

- [x] 2.1 重写 `literature-explainer/SKILL.md` 的 S1-S4 契约，增加固定回答模板、退出检查、多问题与最小化澄清规则
- [x] 2.2 更新 `literature-explainer/scripts/memory_engine.py` 的 `instructions --stage qa` 说明层，补充 QA 记忆写入前置条件与 fail 后最终摘要要求
- [x] 2.3 更新 `literature-explainer/scripts/evidence_verifier.py` 的 `instructions` 说明层，补充验证结果回显方式与 fail 后修正动作顺序

- [x] 3.1 运行 `openspec status --change "stabilize-response-contract-v1" --json`
- [x] 3.2 运行 `openspec instructions apply --change "stabilize-response-contract-v1" --json`
- [x] 3.3 运行 `openspec validate stabilize-response-contract-v1 --type change --json`
- [x] 3.4 运行 `conda run --no-capture-output -n DataProcessing python -u -m mypy literature-explainer/scripts`
- [x] 3.5 人工抽查多问题输入与 `verify=fail` 修正链路的文档与脚本说明
