## Context

当前 Skill 已有证据分级表达，但没有把“证据真实性核验”作为回答后的强制步骤，也没有在失败时统一触发纠偏与用户提醒。

## Goals / Non-Goals

**Goals:**
- 在每次 Q&A 回答后执行证据核验并回显结果。
- 对 `fail` 和 `uncertain` 结果分别定义确定的会话行为。
- 将详细校验策略下放到脚本 `instructions` 输出。

**Non-Goals:**
- 不扩展到非 Q&A 回答场景。
- 不引入 Google Scholar 抓取或浏览器自动化。
- 不在本 change 中实现复杂评分模型。

## Decisions

1. 脚本仅两模式：`instructions` + `verify`。  
   备选：增加 `self-test` 或 `policy` 模式。  
   理由：保持接口最小，满足执行与规范下发。

2. 证据输入统一为 JSON 数组，不接受自由文本解析。  
   备选：自由文本或 Markdown 表格。  
   理由：便于稳定解析、校验和回显。

3. 核验后端固定为 Crossref/arXiv/Semantic Scholar。  
   备选：直接抓取 Google Scholar。  
   理由：API 更稳定且可脚本化，避免反爬风险。

## Risks / Trade-offs

- [Risk] 外部网络波动导致误判 → Mitigation：用 `uncertain` 区分不可达和明确失败。
- [Risk] 关键词选择不当导致网页误判失败 → Mitigation：规则设为“至少命中 1 个关键词”降低假阴性。
