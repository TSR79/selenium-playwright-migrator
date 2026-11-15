---
name: framework-discovery
description: Inspect an existing Playwright TypeScript framework and catalogue its architecture, conventions, fixtures, utilities and reusable methods before migration.
---

# Target Playwright framework discovery

Perform read-only inspection. Do not create, edit, rename or delete files.

## 1. Identify the project

Look for (do not assume all exist):
- `package.json` and lockfiles
- `playwright.config.ts` or equivalent config
- TypeScript configuration
- test directories and test naming conventions
- Page Object directories
- fixtures and custom test extensions
- common actions/utilities
- API helpers, data utilities, environment configuration
- reporting, logging, screenshot and attachment utilities
- README and project-specific guidance

Do not read secrets or environment files merely because they exist. If configuration values are needed, report the variable names without exposing values. Avoid `.env`, credentials, certificates, private keys, tokens and production datasets.

## 2. Build an architecture map

Record:
- Root directory and relevant subdirectories
- Page Object naming and constructor patterns
- Runner/test naming and test registration patterns
- How `Page`, `BrowserContext`, fixtures and test data are passed
- Import aliases and relative import conventions
- How tests are tagged, grouped, retried and configured
- Assertion library and reporting conventions
- Whether tests use `@playwright/test` or another wrapper

Use evidence: file path plus class/function/method name. Do not infer architecture from folder names alone.

## 3. Catalogue reusable methods

Inspect implementation, not only method names. For each relevant method record:
- Exact exported symbol and class/module
- File path
- Visibility/export style
- Parameters and types
- Return type
- Whether it is async
- What it actually does
- Locator type accepted (`Locator`, string, `Page`, etc.)
- Error handling, logging and side effects
- One valid usage example from the project, if available

Prioritise click, type/fill, clear, select, hover, waits, text/value retrieval, assertions, screenshots, scrolling, dropdowns, frames, alerts, navigation, downloads, uploads and reporting.

## 4. Avoid false equivalence

Two methods with similar names are not necessarily equivalent. If implementation or call contract cannot be confirmed, classify the candidate as `NEEDS_REVIEW`; do not map it as reusable.

## 5. Output

Return:
1. Architecture tree (relevant files only).
2. Framework conventions.
3. Reusable method catalogue.
4. Missing capabilities, if relevant.
5. Files intentionally not inspected and why (e.g. secrets or generated output).

Do not write anything to the target project.
