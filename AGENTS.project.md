## Agent skills

### Issue tracker

Issues and specs are tracked in GitHub Issues using the `gh` CLI. See `docs/agents/issue-tracker.md`.

### Triage labels

Triage uses the default five canonical labels (`needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`). See `docs/agents/triage-labels.md`.

### Domain docs

Single-context documentation layout (`CONTEXT.md` and `docs/adr/` at repo root). See `docs/agents/domain.md`.

### Polyglot skills testing

Custom agent skills live in the dedicated skills catalog repository under `repositories/agent-skills/` and use Playwright for E2E testing. While the meta-workspace exclusively uses `uv` for Python, Node dependencies and browser tests are managed within the submodule via `npm test` inside `repositories/agent-skills`. See `docs/adr/0004-separate-skills-catalog-repository-from-meta-workspace.md`.

