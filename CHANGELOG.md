# Changelog

Consumers pin `@v0`. This file is the contract for that pin: which bots exist and how to call them correctly. `v0` is not a release train. It stays on this set until a new bot or a comment-policy change is ready.

## v0

Pin every caller at `bobleesj/github-bots/.github/workflows/<workflow>.yml@v0`.

Caller recipe:

- Fork consumers use `pull_request_target` so the comment can write.
- Same-repository consumers may use `pull_request`.
- Set job-level permissions to `contents: read`, `issues: write`, and `pull-requests: write`. A workflow-level grant is not enough.
- Large-file and stale-base callers must include `synchronize`.

### PR cleanup (`_pr-cleanup-guidance.yml`)

Posts one comment with the branch lifetime: keep the feature branch until merge, then delete the remote branch if you own it, remove the dedicated worktree, and update local `main`.

### Large files (`_pr-large-files.yml`)

Comments when a changed file exceeds the repository size limits:

- any file at least 1 MB
- notebook at least 500 KB
- `.npy`, `.npz`, `.h5`, `.hdf5`, `.emd`, `.dm3`, `.dm4`, `.mrc`, `.tif`, `.tiff`, or `.html` at least 200 KB

The comment lists the files and links [how to store data and notebooks](docs/large-files.md): host arrays on Hugging Face, keep `save_state=False` or run `quantem github` for notebooks, and leave generated HTML to the documentation build. The check does not fail.

### Stale base (`_pr-stale-base.yml`)

Comments when GitHub `behind_by` is greater than 0. Detection is commit ancestry (`GET /repos/{base}/compare/{baseRef}...{head}`), not commit dates. Fetch the base remote and update local `main` before branching, or rebase before review. A warning is enough. The pull request may stay open while `main` moves. The check does not fail.
