# Context Map

## Contexts

- [Meta-Workspace & Agent Skills](./CONTEXT.md): workspace-level orchestration, skill distribution, and interactive planning/grilling skills (`wayfinder-ui`, `grill-with-docs-ui`)
- [Agent Skills Catalog](./repositories/agent-skills/CONTEXT.md): dedicated submodule repository housing custom polyglot agent skills and their Playwright/unit test suites
- [T3 Code Bar](./repositories/t3code-bar/CONTEXT.md): desktop (Tauri) and native Omarchy (`omarchy-shell` / Quickshell QML) bar companions for T3 Code (`bar-core`, `bar-bridge`, `bar-threads`, `bar-usage`, `bar-limits`)

## Relationships

- **Meta-Workspace ↔ Agent Skills Catalog**: Meta-Workspace symlinks skills from `repositories/agent-skills/` via Skill Proxy Links in `skills/` and distributes them to IDE/agent directories via `transpile-skills.py`.
- **Meta-Workspace → T3 Code Bar**: Meta-Workspace provides the engineering skills (`wayfinder`, `grill-with-docs`, `prototype`, `to-spec`, `to-tickets`, `implement`) and issue-tracker/domain conventions used to design and build `repositories/t3code-bar`.
