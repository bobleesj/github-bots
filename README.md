# github-bots

Reusable GitHub Actions bots for consumer repositories. Each bot reads CI and repo state, then posts one PR comment with the result and the next step. Read that comment first. Open the Actions tab only if the bot reports that it could not parse the run.

Add a thin caller in the consumer repo and pin `@v0`. Bot logic stays in this repository.

## Use

Create `.github/workflows/pr-cleanup-guidance.yml` in the consumer repo:

```yaml
name: pr cleanup guidance
on:
  pull_request:
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

`pull_request` runs the caller from the PR branch, which is what you want while testing a new pin. `pull_request_target` runs from the default branch after the caller is merged, including on forks.

## Bots

| Bot | Workflow | Comment |
| --- | --- | --- |
| PR cleanup | `_pr-cleanup-guidance.yml` | Keep the feature branch until merge. Then delete it, remove the worktree, and update local `main`. |

Later bots will use the same comment for failed CI, leftover branches, and stale `main`. See `CHANGELOG.md` for what the current `@v0` pin includes.

## Versioning

Pin consumers at `@v0`. Develop on `main`, then fast-forward `v0` when a change should go live. Keep `CHANGELOG.md` in sync with that pin.
