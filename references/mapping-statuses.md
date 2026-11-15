# Migration status definitions

- **REUSED** — verified existing Playwright framework method reused with confirmed signature and semantics.
- **CONVERTED** — source operation safely expressed using native Playwright or an established target pattern.
- **UNRESOLVED** — source helper implementation is missing or behaviour cannot be established.
- **NEEDS_REVIEW** — likely mapping exists but equivalence or execution semantics need human confirmation.
- **NOT_MIGRATED** — intentionally excluded, with a documented reason.

Do not count UNRESOLVED or NEEDS_REVIEW items as successfully migrated.
