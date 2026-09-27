---
status: accepted
---

# 0004: Separate Skills Catalog Repository from Meta-Workspace

## Context & Decision

Previously, custom polyglot skills (`wayfinder-ui`, `grill-with-docs-ui`) and centralized Playwright E2E browser tests resided directly in the root of the `agent-skills` repository. However, the root repository is fundamentally configured as an `.ai-workspace` meta-workspace intended to aggregate repositories, configure workspace-wide linters/hooks, and orchestrate skill distribution across AI coding tools. Placing skill implementations and testing artifacts directly in the meta-workspace root mixed orchestration concerns with skill domain logic and prevented skills from being independently versioned, tested, and distributed outside this specific workspace harness.

We decided to decouple the meta-workspace from custom skill artifacts:
1. **Dedicated Skills Catalog Repository (`cachemoney/agent-skills`):**
   - Scaffold a standalone GitHub repository (`repositories/agent-skills`) dedicated solely to housing custom agent skills in a `skills/` monorepo layout.
   - Relocate skill implementations (`grill-with-docs-ui`, `wayfinder-ui`), the Playwright browser test harness (`playwright.config.mjs`, `package.json`, `test/`), and autonomous CI to the skills catalog repository. This supersedes ADR 0003's centralized root test placement.
2. **Meta-Workspace Harness (`cachemoney/agent-workspace`):**
   - Rename the meta-workspace repository to `agent-workspace` to reflect its true domain role as an aggregator and developer environment.
   - Consume the skills catalog as a git submodule mounted at `repositories/agent-skills`.
3. **Skill Proxy Links:**
   - Link each active skill into the meta-workspace via relative symlinks in `skills/` pointing to `../repositories/agent-skills/skills/<skill-name>`.
   - Preserve `.ai-workspace/scripts/transpile-skills.py` and `ai-workspace.toml` conventions without modifying core workspace schemas.

## Consequences

- The skills catalog repository is self-contained, with independent versioning, issue tracking, and automated CI (`npm test`).
- The meta-workspace root remains clean of implementation artifacts, node modules, and test dependencies.
- Zero changes to workspace distribution tooling are required: workspace transpilation continues to find skills in `skills/` and symlink them directly into IDE target directories.
