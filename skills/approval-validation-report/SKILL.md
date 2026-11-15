---
name: approval-validation-report
description: Enforce per-file preview and explicit approval before any migration write, then validate approved changes and produce an auditable migration report.
---

# Approval, validation and reporting

## Hard stop before writes

For each file separately:
1. Show the exact path relative to the target project root.
2. Show whether it will be created or modified.
3. Show the complete proposed file content for a new file, or a diff for an existing file.
4. Explain why the change is needed and list unresolved items.
5. Ask: `Approve this specific file change?`
6. Wait for an explicit yes/approve response naming or clearly referring to that file.
7. If approved, write only that file and then report the result.
8. If declined or ambiguous, do not write it.

Do not treat "migrate this project", "go ahead with the migration plan", or approval of one file as approval for every file. Approval is per file and per proposed content. If content changes after approval, obtain approval again.

Kiro's native filesystem permission prompt must remain enabled for writes. The conversational approval workflow is an additional review step, not a replacement for Kiro's permission system.

## Protected operations

Never perform these without separate explicit approval:
- overwrite or delete existing files
- modify package/config/lock files
- install or upgrade packages
- execute tests or arbitrary shell commands
- change environment files or credentials
- commit, push, publish or upload source code

Do not read secrets merely to populate reports. Redact secret-like values if encountered incidentally.

## Validation

After approved writes, propose validation commands first. Prefer low-risk, non-mutating checks such as TypeScript type checking or linting, but inspect package scripts before recommending commands. Ask before running commands if Kiro's permission settings require it.

Never say validation passed unless command output confirms it. Distinguish:
- static/type validation
- test execution
- browser execution
- manual review

## Migration report

Create the report only after showing its path and getting approval for that file too.

Suggested report sections:
1. Source and target project identifiers (avoid sensitive absolute paths where unnecessary)
2. Source framework: Selenium + TestNG/JUnit
3. Target Playwright framework conventions discovered
4. Files created/modified and approval outcomes
5. Mapping totals by status
6. Unresolved source methods with class and call site
7. Behavioural differences and assumptions
8. Validation commands and observed results
9. Remaining manual actions

Never include credentials, tokens, production data, full source files or unnecessary personal information in the report.
