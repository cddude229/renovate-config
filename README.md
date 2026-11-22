# renovate-config

Shared Renovate config presets for my repos.

| Preset                               | Extend with                                             | What it does                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ------------------------------------ | ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `default.json`                       | `github>cddude229/renovate-config`                      | `base` plus `automerge-non-major`. Most repos start here.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `base.json`                          | `github>cddude229/renovate-config:base`                 | `config:recommended` plus config migration PRs, abandoned-package reporting and GitHub Action digest pinning with full-version comments, action and reusable workflow updates grouped into one `GitHub Actions` PR (majors in their own PR), OpenSSF Scorecard badges in PRs, conventional commit messages, assignee/reviewer, Pacific time, dependency updates between 5am and 7am on Wednesday and Saturday, 7-day minimum release age, 5 PRs/hour, OSV vulnerability checks with unresolved ones listed on the dashboard, security PRs at any time with a `security` label. |
| `automerge-non-major.json`           | `github>cddude229/renovate-config:automerge-non-major`  | Automerge minor, patch and digest updates, except minor bumps of `0.x` versions (breaking under semver).                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `lockfile-maintenance.json`          | `github>cddude229/renovate-config:lockfile-maintenance` | Lock file maintenance between 5am and 7am Pacific on Sunday, never automerged. Only npm/pnpm/Yarn lockfiles; Renovate has no lock file maintenance for `go.sum`.                                                                                                                                                                                                                                                                                                                                                                                                               |
| `npm.json` / `pnpm.json` / `go.json` | `github>cddude229/renovate-config:<name>`               | `npmDedupe` / `pnpmDedupe` / `gomodTidy` after updates. `go` also rewrites import paths on major updates and updates indirect dependencies only for security fixes.                                                                                                                                                                                                                                                                                                                                                                                                            |

Presets reference each other with absolute `github>cddude229/renovate-config:<name>` names rather than
relative `./<name>` paths, which only recent Renovate releases understand.

Settings a repo sets itself replace the preset's value, except for `packageRules`, `postUpdateOptions`,
`customManagers`, `ignoreDeps`, `vulnerabilityAlerts` and `lockFileMaintenance`, which merge with it.
Rules a repo adds therefore run after the preset's rules and win any conflict.

Changes here apply to every repo on its next Renovate run. Validate before merging:

```
npx --yes --package renovate -- renovate-config-validator --strict --no-global *.json
```

## Commit messages

This repo uses [Conventional Commits](https://www.conventionalcommits.org/) from now on: start each
commit message with a type such as `feat:`, `fix:`, `docs:` or `chore:`. Renovate's own commits
already follow this via `semanticCommits` in `base.json`.
