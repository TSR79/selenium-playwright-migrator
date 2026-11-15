# Selenium-to-Playwright Migrator

A Kiro Power for migrating Java Selenium projects (TestNG and JUnit) into an **existing** Playwright TypeScript framework.

## Core guarantees

- Analyse the target Playwright framework before generating code.
- Preserve the target framework's existing folder structure, naming, imports, fixtures, runner conventions, reporting and configuration.
- Reuse existing target-framework methods when their implementation and signature are understood.
- Do not invent the behaviour of unavailable Selenium helper methods.
- Keep Page Objects and test/runner classes separate, following the target framework's conventions.
- Preview proposed changes and obtain explicit approval before each file write.
- Never delete files or overwrite existing files without explicit approval.
- Produce a migration report distinguishing `CONVERTED`, `REUSED`, `UNRESOLVED`, `NEEDS_REVIEW` and `NOT_MIGRATED`.

## Supported source scope (initial release)

- Java Selenium.
- TestNG.
- JUnit 4 and JUnit 5 annotations and assertions, where identifiable.
- Page Object Model and common Java test-framework patterns.

## Target scope

Any existing Playwright TypeScript framework. The Power must discover the framework rather than assume a fixed layout or fixed utility method names.

## Install locally in Kiro

1. Extract this repository or ZIP.
2. In Kiro, open **Powers** → **Add Custom Power** → **Import power from a folder**.
3. Select the extracted `selenium-playwright-migrator` directory (the directory containing `plugin.json`).
4. Start a new task and ask Kiro to migrate a Java Selenium test into the currently open Playwright TypeScript framework.

## Suggested first prompt

> Analyse the Selenium source project and the existing Playwright TypeScript target project. Do not modify anything. First inventory the target architecture and reusable methods, then analyse the source tests, create a mapping table, identify unresolved methods, and show a proposed file-by-file migration plan.

## Critical permission configuration

The Skills instruct the agent to stop before writing and request approval for every file. Also configure Kiro's own filesystem-write permission to **Ask** in the user's Kiro permission settings. Agent instructions are not a security boundary; Kiro's permission controls are the enforcement layer. Keep shell execution restricted/approval-based too.

The first release intentionally contains no MCP server, network client, telemetry, external API integration, or automatic Git operations.

## Current limitations

This is an instruction-first starter Power. It does not claim that all Java constructs can be translated automatically. Reflection, custom frameworks, complex waits, asynchronous behaviour, browser-specific APIs, data providers, hooks, listeners, and business-specific helper methods may require manual review. Missing source implementations must remain unresolved.

## Development status

Version `0.1.0` — initial workflow and safety policy scaffold. Helper scripts and automated structural validation will be added in later phases.
