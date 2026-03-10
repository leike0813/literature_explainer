## Why

当前 `literature-explainer/SKILL.md` 仍属于结构化初版，虽可用但缺少可检查的输入输出契约、证据分级规则、状态转换规则和学习笔记模板，导致执行一致性与可验证性不足。

## What Changes

- 将 `literature-explainer/SKILL.md` 升级为可发布初版，补全输入输出格式规范。
- 明确证据化回答规则（事实/证据/推断分层）与证据不足时的处理策略。
- 明确交互状态机（分析论文→确认意图→问答循环→笔记询问→结束）。
- 增加学习笔记生成模板和最小字段约束。
- 保持当前无脚本依赖，不新增目录或可选资源包。

## Capabilities

### New Capabilities
- `skill-workflow-refinement`: 提升 Skill 指令契约的完整度、一致性与可验证性。

### Modified Capabilities
None.

## Impact

- 影响文件：`literature-explainer/SKILL.md` 与当前 change 的 OpenSpec artifacts。
- 不涉及代码 API、数据类型、外部依赖和运行时服务。
