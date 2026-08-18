# github-bots

Reusable bots for Bob's repositories. The point is not more GitHub noise. The point is that **you should not have to read CI**.

CI logs are a machine format. A red X is not an explanation. These bots parse the run the way we already expect it to look, then write one comment: what failed, why it matters, and what to do next. If a PR is also leaving dirty state (feature branch, worktree, stale `main`), the same comment says so.

That is the whole motivation. Open the PR. Read the bot. Do not open the Actions tab unless the bot says the parse itself broke.

## What this grows into

A small system of reusable workflows, not a pile of one-off YAML in every repo.

- **CI parse:** failed job, failed test, missing artifact, skipped gate. One comment, expected shape.
- **State:** leftover branches, dirty worktrees, fork `main` behind upstream, too many open feature branches.
- **PR hygiene:** keep / delete / update-local-main after merge (this is the first bot).
- Later: the same comment surface can flag flaky retries, docs that did not rebuild, or a release tag that did not publish.

Consumers stay thin: a 10-line caller in the repo, logic lives here. Pin `@v0`. Develop on `main`, then update `v0` when a bot should go live.

## PR cleanup guidance

First shipped bot. Comments the keep / delete-branch / update-local-main checklist.

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
