# git-fabric Global ADRs

Organization-wide Architecture Decision Records that apply to **all** git-fabric repositories.

## How it works

1. Global ADRs live here — the single source of truth for org-wide policy.
2. When a change merges to `main`, a GitHub Actions workflow dispatches sync events to every downstream repo.
3. Each downstream repo has a workflow that pulls the latest global ADRs into `adr/global/` and opens a PR.

## Structure

```
docs/                  # Global ADRs (org-wide policy)
  AI-ADR-012-...       # AI-specific global ADRs
docs/ai/               # AI-specific global ADRs (future)
.github/workflows/
  dispatch.yml         # Dispatches sync events on merge to main
```

## Downstream repo structure

Each repo that consumes global ADRs has:

```
adr/
  global/              # ← synced from this repo (do not edit directly)
    AI-ADR-012-...
  ADR-001-...          # ← repo-specific ADRs
  ai/
    AI-ADR-001-...     # ← repo-specific AI ADRs
```

## Adding a new global ADR

1. Branch from `main`
2. Add the ADR to `docs/`
3. Open a PR — human approval required
4. On merge, sync dispatches automatically to all downstream repos

## Downstream repos

Sync targets are defined in `.github/workflows/dispatch.yml`. To add a new repo, add it to the matrix.
