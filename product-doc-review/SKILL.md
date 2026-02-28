---
name: product-doc-review
description: Analyze, optimize, scope and schedule product documents. Use when user provides or uploads a product doc (PRD, requirement doc, feature spec) and wants to (1) review completeness and quality, (2) check feature requirements for clear boundaries and flows, (3) get design improvement suggestions, or (4) get a list of impacted features vs existing code with rough prioritization and timeline. Trigger on product document analysis, 产品文档分析, 优化, 目标划分, 排期.
---

# Product Document Review

Structured workflow to review a product document: run completeness checks, validate feature requirements, suggest optimizations, and (when codebase is available) map changes to existing code with scope and schedule.

## Inputs

- **Required**: Product document (pasted, uploaded, or linked)—PRD, feature spec, or requirement list.
- **Optional**: Codebase context. If the user wants "功能与排期" (features and schedule) tied to code, search or read relevant `src/views/`, `src/components/`, `src/utils/api/` (or project-equivalent) to compare proposed changes with current implementation.

## Workflow (four phases)

Execute in order. Output a single review report; split by phase only if the document is very long.

### Phase 1: Completeness check

Verify the document against these items. Mark each as **✓ / ✗ / 部分** and note gaps.

| 检查项 | 说明 |
|--------|------|
| 产品背景说明 | 是否有背景、目标用户、要解决的问题或机会 |
| 用户痛点描述 | 是否描述当前痛点或期望与现状差距 |
| 功能需求列表 | 是否有明确的功能/需求列表 |
| 优先级说明 | 是否标注 P0/P1/P2 或类似优先级 |
| 验收标准 | 可选；若有则检查是否可执行、可验证 |

**Output**: Short table (e.g. checklist) + 1–2 sentences per missing item.

### Phase 2: Feature requirement quality

For **each** item in the 功能需求列表, verify:

- **边界定义**：功能范围是否清晰（包含/不包含什么、与相邻功能的边界）。
- **正常流程**：主流程步骤是否写清（谁在什么条件下做什么、结果是什么）。
- **异常流程**：异常/错误分支是否说明（失败、超时、权限不足、数据异常等）。
- **前置条件**：依赖的系统、数据、权限、配置或其它功能是否列出。

Mark each feature with **✓ / ✗ / 部分** per dimension. Call out the most critical gaps (e.g. missing exception handling or unclear preconditions).

**Output**: Per-feature summary table + bullet list of main issues.

### Phase 3: Design critique and optimization

- **不合理之处**：指出逻辑矛盾、遗漏、与常见实践或项目规范不符、难以实现或易误解的设计。
- **优化建议**：针对每类问题给出具体改进建议（改写表述、补充流程、拆分/合并需求、调整优先级等）。

Base critique on: clarity, completeness, consistency, implementability, and (if applicable) project conventions (e.g. naming, API style, RTL, permissions).

**Output**: "不合理 / 风险" list with short explanation + "优化建议" list with actionable items.

### Phase 4: Impact vs code and schedule (when codebase is in scope)

Only when the user asks for 功能与排期 and codebase is available:

1. **需改动功能列表**：从产品文档提炼出所有“需要开发或修改”的功能点（含新建、改造、下线）。
2. **对照已有代码**：在项目中定位相关模块（如 `src/views/…`, `src/utils/api/…`, router, store）。对每个功能标注：**新建 / 改造现有 / 无直接对应**，并注明涉及文件或模块。
3. **功能与排期**：  
   - 按依赖关系与优先级整理成有序功能列表。  
   - 给出粗略排期（如按迭代/周），标注不确定处（如“依赖后端接口”）。  
   - 若文档无明确优先级，先按依赖和风险给出建议优先级，再排期。

**Output**: Table or list of 功能 → 类型(新建/改造) → 涉及模块/文件 → 建议优先级/迭代；加一段简短排期说明与风险/假设。

## Report structure

Produce one report with the following sections (omit Phase 4 if codebase or “排期” was not in scope):

```markdown
# 产品文档评审：[文档标题或主题]

## 1. 完整性检查
[Phase 1 checklist and gap summary]

## 2. 功能需求质量
[Phase 2 per-feature summary and main issues]

## 3. 设计不合理与优化建议
[Phase 3 critique and optimization list]

## 4. 功能与排期
[Phase 4 impact list and schedule when requested]
```

Keep language consistent with the document (e.g. Chinese if the doc is in Chinese).

## Reference

- **Detailed checklist**: See [references/checklist.md](references/checklist.md) for expanded check items and examples when you need more granular guidance.
