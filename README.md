# github-bots

Reusable GitHub bots for Bob's repositories. Pin consumers at `@v0`. Develop on `main`, then update `v0`.

## PR cleanup guidance

In the consumer repo, add `.github/workflows/pr-cleanup-guidance.yml`:

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

`github-actions[bot]` then comments the keep / delete-branch / update-local-main checklist on each PR.
