---
name: code-generation
description: Generate migration proposals that fit the discovered Playwright TypeScript framework, preserving separate Page Object and runner/test classes and reusing verified framework methods.
---

# Target code generation

Generate proposed code only after framework discovery, Selenium analysis and method mapping are complete.

## Architecture preservation

- Follow the actual target framework layout, not a generic template.
- Keep page interaction logic in the target's Page Object layer when that is its convention.
- Keep test registration, test lifecycle, assertions and runner responsibilities in the target's test/runner layer.
- Do not put all migrated code into one class.
- Preserve fixture injection, constructor conventions, imports, aliases, naming, test annotations/tags and reporting conventions.
- Do not create a second framework config, package file, base class or common utility when one already exists.

## Reuse

- Call verified existing target utility methods using their exact signature.
- Do not create duplicate click/type/clear/wait/assert methods.
- Do not assume utility methods are static or instance methods.
- Do not assume a locator parameter type. Confirm it.
- If a required helper does not exist, propose either native Playwright usage consistent with the framework or a new helper. Mark any new helper as a separate proposed file/change requiring approval.

## Java-to-TypeScript considerations

Handle Java types, visibility, constructors, exceptions, collections, loops, conditionals and strings idiomatically in TypeScript. Preserve behaviour rather than syntax.

For TestNG/JUnit:
- Map test cases to the target runner's test registration pattern.
- Preserve setup/teardown semantics where possible.
- Translate data providers/parameterized tests into target-supported parameterization only after inspecting existing examples.
- Map assertions to the target framework's assertion convention.
- Flag listeners, extensions, retries, dependencies, groups, ordering and soft assertions if no equivalent is established.

## Locators

Prefer the target framework's established locator strategy. Do not mechanically preserve brittle XPath if a stronger role/label/test-id locator is justified by available DOM evidence. Do not invent accessible names or test IDs. If only a Selenium locator is known, translate conservatively and flag ambiguity.

## Output before approval

For every proposed file:
- exact target path
- action: `CREATE` or `MODIFY`
- reason
- source class(es)
- target conventions followed
- complete proposed content or unified diff
- dependencies/imports
- unresolved items and risks

No file writes are allowed as part of this skill's generation stage.
