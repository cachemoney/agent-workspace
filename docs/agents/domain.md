# Domain Docs

How the engineering skills should consume this repo's domain documentation when exploring the codebase.

## Before exploring, read these

- **`CONTEXT-MAP.md`** at the repo root: it points at one `CONTEXT.md` per context (root workspace and `repositories/<submodule>/` projects). Read each one relevant to the topic.
- **`CONTEXT.md`** at the repo root (workspace-level glossary) and **`repositories/<context>/CONTEXT.md`** for the target submodule/project.
- **`docs/adr/`**: read system-wide ADRs at the repo root and context-scoped ADRs under `repositories/<context>/docs/adr/` (or `src/<context>/docs/adr/`) that touch the area you're about to work in.

If any of these files don't exist, **proceed silently**. Don't flag their absence; don't suggest creating them upfront. The `/domain-modeling` skill (reached via `/grill-with-docs` and `/improve-codebase-architecture`) creates them lazily when terms or decisions actually get resolved.

## File structure

Multi-context meta-workspace (presence of `CONTEXT-MAP.md` at the root):

```
/
├── CONTEXT-MAP.md
├── CONTEXT.md                             ← workspace-level glossary
├── docs/adr/                              ← workspace-wide decisions
└── repositories/
    ├── agent-skills/
    │   ├── CONTEXT.md
    │   └── docs/adr/                      ← context-specific decisions
    └── t3code-bar/
        ├── CONTEXT.md
        └── docs/adr/                      ← context-specific decisions
```

Single-context repo (when operating standalone inside a single repo):

```
/
├── CONTEXT.md
├── docs/adr/
│   ├── 0001-event-sourced-orders.md
│   └── 0002-postgres-for-write-model.md
└── src/
```

## Use the glossary's vocabulary

When your output names a domain concept (in an issue title, a refactor proposal, a hypothesis, a test name), use the term as defined in the relevant `CONTEXT.md`. Don't drift to synonyms the glossary explicitly avoids.

If the concept you need isn't in the glossary yet, that's a signal: either you're inventing language the project doesn't use (reconsider) or there's a real gap (note it for `/domain-modeling`).

## Flag ADR conflicts

If your output contradicts an existing ADR, surface it explicitly rather than silently overriding:

> _Contradicts ADR-0007 (event-sourced orders), but worth reopening because…_
