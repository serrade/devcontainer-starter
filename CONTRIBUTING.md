# Contributing

Thanks for helping out! This repo is a multi-language [Dev Container](https://code.visualstudio.com/docs/remote/dev-containers) starter where each branch is a self-contained starter for a particular stack.

## Adding a new starter

1. Branch off `main`: `git switch main && git switch -c <language>`.
2. Add the language-specific bits to `.devcontainer/` (extensions, settings, apt packages, Dockerfile steps, compose services) and any sample files at the repo root.
3. Push the branch: `git push -u origin <language>`.
4. Update the branch table in [`README.md`](README.md) on `main` so the new starter is discoverable.

## Keeping variant branches in sync with `main`

Generic improvements (new shell alias, new base tool, doc updates) go on `main` first and then propagate forward into each variant branch.

For variant branches that share `main`'s history cleanly &mdash; e.g. `terraform`, which was branched off the generic `main` &mdash; a fast-forward merge is enough:

```bash
git switch terraform
git merge --ff-only main
git push origin terraform
```

For the `python` branch, **cherry-pick** instead of merging. The branch was snapshotted before `main` was refactored into a generic base, so a plain `git merge main` would replay the "remove Python bits" commit and wipe out the Python overlay.

```bash
git switch python
git cherry-pick <commit-on-main>
git push origin python
```

If you find yourself cherry-picking a lot, the cleaner long-term fix is to rebuild `python` on top of the new generic `main` with a single "add Python overlay" commit &mdash; then plain merges from `main` will work forever after. That's a one-time cleanup, not a daily cost.

## Commit style

Short, imperative subject lines (e.g. `Add Git install step to README setup guide`). One logical change per commit so cherry-picks stay clean.
