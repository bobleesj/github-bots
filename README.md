# github-bots

Reusable GitHub Actions bots. They parse CI and repo state, then leave one PR comment with the result and the next step. Read the comment. Open the Actions tab only if the bot says the parse failed.

Logic lives here. Consumer repos keep a thin caller and pin `@v0`.

## Use

Add a workflow in the consumer repo. Example: PR cleanup.

`.github/workflows/pr-cleanup-guidance.yml`

```yaml
name: pr cleanup guidance
on:
  pull_request_target:
    types: [opened, reopened, closed]
permissions:
  contents: read
  issues: write
  pull-requests: read
jobs:
  guidance:
    uses: bobleesj/github-bots/.github/workflows/_pr-cleanup-guidance.yml@v0
```

## Bots

| Bot | Workflow | Comment |
| --- | --- | --- |
| PR cleanup | `_pr-cleanup-guidance.yml` | Keep the feature branch until merge. Then delete it, drop the worktree, and update local `main`. |

Next bots will use the same comment surface for failed CI, leftover branches, and stale `main`.

## Versioning

- Consumers pin `@v0`.
- Develop on `main`.
- Fast-forward `v0` when a bot should go live.
