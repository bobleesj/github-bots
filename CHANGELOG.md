# Changelog

Consumers pin `@v0`. This file lists what that pin currently includes.

## v0

- `_pr-cleanup-guidance.yml`: comment on a PR to keep the feature branch until merge, then delete it, remove the worktree, and update local `main`. Callers must pass `issues: write` and `pull-requests: write` on the job.
- `_pr-large-files.yml`: warn when a PR adds files over about 1 MB, or notebooks over about 500 KB. Points at Hugging Face and stripped notebook / `save_state=False` workflows.
- `_pr-stale-base.yml`: warn when the PR is `behind_by` the base branch. Fetch and update local `main` before branching, or rebase before review. Does not fail the check.
