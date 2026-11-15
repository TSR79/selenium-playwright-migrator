# Safety boundaries

This Power is designed to be local-first and instruction-only in its initial release.

- No MCP server is bundled.
- No network requests, telemetry, cloud storage or external AI API integration are implemented by this repository.
- Kiro's own model processing still applies; review the organization's Kiro data-handling and retention policy before using confidential source code.
- Agent instructions do not enforce operating-system security. Kiro permissions, workspace boundaries, endpoint controls and organizational policy are authoritative.
- Configure filesystem writes to ask for approval. Keep shell and network capabilities restricted according to company policy.
- Do not use production credentials or production personal data in sample projects.
- Review the Power source before importing it into a corporate environment.
