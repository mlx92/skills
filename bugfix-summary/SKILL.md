---
name: bugfix-summary
description: Create concise post-fix summaries for bug tickets (such as ZenTao or Jira) after code changes and verification. Use when the user asks to summarize reproduction steps, root cause, fix details, self-test, and prevention actions, and when the summary should be saved as a markdown file in the project.
---

# Bugfix Summary

## Overview
Generate a concise, ticket-ready bugfix summary from completed troubleshooting and implementation context.

## Workflow
1. Collect confirmed facts from conversation, code diff, and test/lint results.
2. Fill the summary structure using the template in `assets/zentao-bugfix-summary-template.md`.
3. In section `问题原因` and `解决方案`, write a one-line `总结` sentence as the first line before detailed bullets.
4. Keep each item short and factual, focusing on what changed and how it was verified.
5. Try to infer `发生时间` and `产生人` from git history (for example `git log -S` and `git blame` on key bug-introducing snippets). If not confidently located, write `-- 待填写`.
6. Compute `持续时长` in days as `current_date - 发生时间`; if `发生时间` is `-- 待填写`, keep `持续时长` as `-- 待填写`.
7. Run a quick performance-risk scan by searching key changed snippets and checking complexity/reactivity impact; summarize in short conclusions.
8. Resolve current development branch using `git rev-parse --abbrev-ref HEAD` and write it in the final `开发分支` block. If unavailable, write `-- 待填写`.
9. Save the result as a markdown file under `docs/bugfix-summaries/`.

## Output Rules
- Use the fixed section order: `复现步骤`, `问题原因`, `发生时间`, `产生人`, `持续时长`, `解决方案`, `研发自测`, `如何避免`.
- Do not add numeric prefixes like `1.` to section titles.
- Render every section title as bold text on its own line in the format `**标题：**`.
- Keep section titles clean; do not append role notes like `-- QA补充` or `-- QA、研发补充`.
- Prefer one to four lines per section.
- Avoid speculative text, marketing tone, and long background descriptions.
- In `如何避免`, provide concrete QA and R&D prevention actions.
- Do not fabricate `发生时间` or `产生人`; use `-- 待填写` when evidence is insufficient.
- Format `发生时间` as `YYYY-MM-DD` only.
- Do not add explanatory parentheses in `发生时间`, `产生人`, or `持续时长`.
- Always append a final `开发分支` block with this format:
  `**开发分支：**`
  `- <current_branch>` (fallback `- -- 待填写`).
- In section `问题原因` and `解决方案`, the first line must be `总结：...` and should summarize the core point in one sentence.
- If a section becomes too long, compress wording and merge similar bullets while preserving all key facts (trigger, impact, fix action, verification result).

## File Naming
Use: `docs/bugfix-summaries/<topic>-<yyyy-mm-dd>.md`

## Resources
- Template: `assets/zentao-bugfix-summary-template.md`
- Writing rules: `references/writing-rules.md`
