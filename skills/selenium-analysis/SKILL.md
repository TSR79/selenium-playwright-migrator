---
name: selenium-analysis
description: Analyse Java Selenium source projects using TestNG or JUnit, identifying tests, Page Objects, locators, helper methods, data and lifecycle behaviour without modifying source files.
---

# Java Selenium source analysis

Perform read-only analysis. Support Java Selenium with TestNG and JUnit 4/5 where identifiable.

## Inspect

- Test classes and methods
- `@Test`, `@Before*`, `@After*`, `@BeforeEach`, `@AfterEach`, `@BeforeAll`, `@AfterAll`
- TestNG `@DataProvider`, groups, dependencies, parameters and listeners
- JUnit `@ParameterizedTest`, `@MethodSource`, `@CsvSource`, extensions and lifecycle
- Page Objects and page factories
- `WebDriver`, `WebElement`, `By` locators
- waits (`WebDriverWait`, expected conditions, implicit waits)
- actions, JavaScript execution, frames, windows, alerts
- assertions and soft assertions
- screenshots, downloads, uploads
- custom utility/helper calls and their definitions
- test data sources and external dependencies

## Method implementation tracing

For every non-standard method call:
1. Search the supplied source project for its declaration.
2. Follow delegation to other methods when practical.
3. Record the implementation path and relevant call chain.
4. If implementation is absent, inaccessible, generated, reflection-driven or outside the supplied source, classify it as `UNRESOLVED`.
5. Never guess what a business-specific helper does based on its name.

## Output

Produce:
- Source project architecture
- Test framework identification (TestNG, JUnit 4, JUnit 5, mixed, or unknown)
- Test and lifecycle inventory
- Page Object inventory
- Locator and interaction inventory
- Helper method inventory with implementation evidence
- Data-provider/parameterization behaviour
- Dependencies and unsupported constructs
- Unresolved methods

Keep source code snippets short and avoid exposing secrets or real test data in the report.
