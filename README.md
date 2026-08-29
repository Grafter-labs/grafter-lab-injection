# Grafter Lab: Workflow Injection

> [!WARNING]
> This public template intentionally contains GitHub Actions injection
> anti-patterns for education and detector testing. Do not reuse these
> workflows in production or add real secrets. Use only disposable forks.

Potential command execution and attacker-selected runner examples are disabled
with a job-level `if: ${{ false }}` or the nonexistent `grafter-no-runner`
label. Runnable examples are GitHub-hosted and limited to `GRAFTER_MARKER`
output, harmless files, and local test artifacts.
No workflow sends data externally, posts comments, authenticates to a cloud, or
publishes anything.

## Scenarios

| Workflow | Scenario | Mode | Safety boundary |
|---|---|---:|---|
| `script-injection.yml` | Event text interpolated directly into a shell script | Inert | Job-level false |
| `runner-control-injection.yml` | Dispatch input controls `runs-on` | Inert | Job-level false |
| `deprecated-commands.yml` | Deprecated workflow command is emitted | Inert | Job-level false condition |
| `bypassable-actor-allowlist-gate.yml` | Substring actor allowlist guards a dry-run sink | Inert | Nonexistent runner label |
| `filename-collision-download.yml` | Two inert downloads target the same filename | Inert | Job-level false; `.invalid` URLs |
| `secret-echoed-to-log.yml` | Secret-shaped literal is printed | Inert | Job-level false; literal is not a secret |

`.github/workflows/controls/` contains ignored nested control fixtures. GitHub
only loads workflow files directly inside `.github/workflows`, making the
nested directory useful for side-by-side scanner tests.
