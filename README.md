# factory-ci

Reusable GitHub Actions workflows for the repositories built by the
[autonomous software factory](https://trysac.github.io/autonomous-software-factory/). Each generated repository's
`.github/workflows/ci.yml` calls one of them, so the CI of every repository changes with one release here instead of
one pull request per repository.

| Workflow | For | Jobs |
| --- | --- | --- |
| `python.yml` | Python libraries | local gates on Linux and Windows, Python 3.10-3.13; CI-only conformance tier with Semgrep CE and OSV-Scanner; gitleaks |
| `typescript.yml` | TypeScript libraries | local gates; CI-only conformance tier with the scanners; gitleaks |
| `go.yml` | Go libraries | local gates on Linux and Windows; CI-only conformance tier with the scanners; gitleaks |
| `webapp.yml` | Vite + React web apps | local gates, including Playwright, axe and Lighthouse budgets; gitleaks |

The workflows never contain a repository's gates: they run the repository's own `scripts/check`, so a repository
created before a release keeps running its own gates under the new CI.

## Releases

Callers use the major tag (`@v1`). A compatible change moves `v1` to the new release; a breaking change gets `v2`
and the factory moves its repositories with `fabrica fleet`.

MIT licensed.
