---
name: method-mapping
description: Map Java Selenium operations and helper methods to verified methods in the user's existing Playwright TypeScript framework, without inventing missing behaviour.
---

# Selenium-to-Playwright method mapping

Use the source analysis and target framework inventory. Do not write files.

## Mapping rules

For each source operation or helper, choose exactly one status:

- `REUSED`: a verified existing target framework method provides equivalent behaviour and its call contract is known.
- `CONVERTED`: a direct Playwright API or target-framework pattern can safely express the source behaviour.
- `UNRESOLVED`: source helper implementation is unavailable or its behaviour cannot be established.
- `NEEDS_REVIEW`: a possible mapping exists but semantic equivalence, signature, side effects or lifecycle behaviour is uncertain.
- `NOT_MIGRATED`: deliberately excluded with a reason.

## Reuse priority

1. Existing target framework custom method with verified implementation and compatible signature.
2. Existing target framework fixture, wrapper or page abstraction.
3. Existing project-approved helper in another target file.
4. Native Playwright API, only when consistent with target conventions and no existing abstraction should be used.
5. Propose a new helper only when required, and identify it as a proposed addition requiring separate approval.

Never invent method names, argument order, imports or return types. Use exact names and signatures discovered in target files.

## Semantic checks

Consider:
- `click` vs `dblclick`, force, modifiers and navigation effects
- `sendKeys` vs `fill` vs `press` and key sequences
- clearing vs replacing field contents
- implicit/explicit waits vs Playwright auto-waiting
- stale element handling vs locator re-resolution
- displayed/enabled/selected state
- window/tab and frame handling
- alert handling
- JavaScript execution
- downloads/uploads
- assertion timing and soft assertion aggregation
- test lifecycle and data-provider semantics

Do not translate fixed sleeps mechanically. Explain whether Playwright auto-waiting or an explicit condition is appropriate.

## Unavailable source helper

If Selenium calls `calculatePremium()` and its implementation is not present:
- classify it `UNRESOLVED`
- report the original class and call site
- state that only the call name/signature is known (if even that)
- do not invent a Playwright implementation
- do not claim the business operation is migrated
- ask the user to supply the method implementation or define the desired replacement

A placeholder may be included only in the proposed preview, clearly marked non-executable and requiring user decision. Never silently insert a fake method body.

## Required mapping table

| Source file and call | Source behaviour evidence | Target method/API | Target file and signature | Status | Notes |
|---|---|---|---|---|---|

Every mapping must include evidence. If evidence is missing, use `UNRESOLVED` or `NEEDS_REVIEW`.
