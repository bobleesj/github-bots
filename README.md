# github-bots

Reusable GitHub Actions bots for consumer repositories. Each bot reads CI and repo state, then posts one PR comment with the result and the next step. Read that comment first. Open the Actions tab only if the bot reports that it could not parse the run.

Add a thin caller in the consumer repo and pin `@v0`. Bot logic stays in this repository.

## Use

Create one workflow file per bot. Example: PR cleanup.

`.github/workflows/pr-cleanup-guidance.yml`

```yaml
name: pr cleanup guidance
on:
  pull_request_target:
    types: [opened, reopened, closed]
permissions:
  contents: read
  issues: write
  pull-requests: write
jobs:
  guidance:
    permissions:
      contents: read
      issues: write
      pull-requests: write
    uses: bobleesj/github-bots/.github/workflows/_pr-cleanup-guidance.yml@v0
```

For fork repos, keep `pull_request_target` so the comment can write. Same-repo callers may also use `pull_request`. Large-file and stale-base callers should include `synchronize`.

## Bots

| Bot | Workflow | Comment |
| --- | --- | --- |
| PR cleanup | `_pr-cleanup-guidance.yml` | Keep the feature branch until merge. Then delete it, remove the worktree, and update local `main`. |
| Large files | `_pr-large-files.yml` | Warn if the PR adds fat arrays, HTML, or notebook widget state. Use Hugging Face and `quantem github` / `save_state=False`. |
| Stale base | `_pr-stale-base.yml` | Warn if GitHub `behind_by` is greater than 0: fetch the base remote and update local `main` before you branch, or rebase before review. Warning only. |

See `CHANGELOG.md` for what the current `@v0` pin includes.

## Versioning

Pin consumers at `@v0`. Develop on `main`, then fast-forward `v0` when a change should go live. Keep `CHANGELOG.md` in sync with that pin.
