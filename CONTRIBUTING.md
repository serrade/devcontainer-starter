# Contributing

Thanks for helping out! This repo is a multi-language [Dev Container](https://code.visualstudio.com/docs/remote/dev-containers) starter where each branch is a self-contained starter for a particular stack.

## Adding a new starter

1. Branch off `main`: `git switch main && git switch -c <name>`.
2. Add the stack-specific bits to `.devcontainer/` (extensions, settings, apt packages, Dockerfile steps, compose services) and any sample files at the repo root.
3. Push the branch: `git push -u origin <name>`.
4. Update the branch table in [`README.md`](README.md) on `main` so the new starter is discoverable.

## Keeping variant branches in sync with `main`

Generic improvements (new shell alias, new base tool, doc updates) go on `main` first, then forward into each variant branch.

If the variant was branched off the current generic `main`, a fast-forward merge is enough:

```bash
git switch <variant>
git merge --ff-only main
git push origin <variant>
```

If a plain merge would replay commits that conflict with the variant's overlay (for example, a variant that predates a refactor of `main`), cherry-pick the specific commits you want instead:

```bash
git switch <variant>
git cherry-pick <commit-on-main>
git push origin <variant>
```

## Commit style

Short, imperative subject lines. One logical change per commit so cherry-picks stay clean.
