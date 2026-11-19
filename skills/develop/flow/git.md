# Develop: git handling (read only when git integration is on)

Read this only when the nearest `AGENTS.md` `## Git` block says `integration: on`. Absent or `off` → do no active git; the engineer manages branches and commits, and the read only freshness checks still apply. Git is the one hard dependency; skip silently if there is no repo.

Read the setting: `integration` and `branch prefix` (default `feat/`). `commit` values are legacy: ignore them for behavior and never create commits. Integration means branch guidance and proposed commit notes. It never stages, commits, pushes, or creates pull requests.

**Ensure a repo exists first.** If integration is on and the project is not yet a git repo (`git rev-parse` fails), offer to run `git init`. Never stage or commit existing files automatically.

## Branch (before building, in the freshness & collaboration check)

- On the default branch (`main`/`master`) → **offer to branch** (recommended): `<prefix><feature-slug>` from the scope feature name (kebab case; e.g. `feat/accounts-sign-in`). Never build on the default branch.
- On a feature branch already → reuse it; do not create another.
- Resuming a half built feature (Step 3) → check out that feature's branch first if it exists and you are not on it.
- Use the change type for the prefix when it is not a feature (`fix/`, `refine/`), else the setting's default.

## Commit notes (never create commits)

When a milestone lands and its typecheck is green, add one proposed commit subject to `docs/commit-notes.md`. Create the file with `# Commit notes` if it does not exist.

Use a one line Conventional Commit subject. Type from the work (`feat`, `fix`, `refactor`, `test`, `chore`), optional scope from the feature, summary in the imperative:

```
feat(auth): add session persistence
```

Append an entry under the current date and include the branch and the milestone or feature:

```
## 2026-11-19

- `feat(auth): add session persistence` on `feat/accounts-sign-in` (auth milestone)
```

Keep entries append only. Do not create, amend, stage, or delete commits. Never run `git push`. The engineer reviews `docs/commit-notes.md`, stages the actual changes, and commits manually.

## Report

Add one line to the `/develop` summary: the branch you are on and the proposed subject recorded in `docs/commit-notes.md`. If integration is off or absent, say nothing about git.
