# Writing Rules

- Keep content concise and actionable.
- Describe confirmed facts only.
- Focus on changed behavior and verification evidence.
- Keep each section to one to four lines.
- Use bold section headers in the format `**标题：**`, and do not add numeric prefixes.
- Keep section headers clean without role suffixes (for example, no `-- QA补充`).
- Split prevention actions clearly between QA and R&D.
- Infer `发生时间/产生人` from git only when evidence is clear; otherwise write `-- 待填写`.
- If `发生时间` is known, calculate `持续时长` by days from current date; if unknown, write `-- 待填写`.
- Output `发生时间` in `YYYY-MM-DD` format only.
- Do not append parenthetical explanations in `发生时间`, `产生人`, and `持续时长`.
- Add one short performance-risk conclusion based on key changed code snippets.
- Output the branch in a final two-line block:
  `**开发分支：**`
  `- <current_branch>`.
- If branch resolution fails, use `- -- 待填写`.
- In `问题原因` and `解决方案`, make the first line `总结：...` as a one-sentence summary.
- If detail text is long, compress repeated content and keep only key facts: cause, impact, fix steps, and validation evidence.
