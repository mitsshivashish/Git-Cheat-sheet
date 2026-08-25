# Git Branching - Rebasing

## Rebase

`git rebase` replays commits from one branch on top of another to create a **clean, linear history**.

### Basic Rebase

    git switch feature
    git rebase main

Then:

    git switch main
    git merge feature

### Rebase vs Merge

- `merge` → preserves branch history and may create a merge commit.
- `rebase` → rewrites commits and creates a linear history.

### Rebase with `--onto`

    git rebase --onto main server client

Moves the `client` commits that are after `server` onto `main`.

### Rebase Another Branch

    git rebase main server

### ⚠️ Golden Rule

**Do not rebase shared/public commits that others may have based work on.**

Rebase rewrites commit history and can cause collaboration problems.

Safe:
- Local/private commits
- Commits nobody else depends on

Avoid:
- Shared/public commits

### Pull with Rebase

    git pull --rebase

Set rebase as default:

    git config --global pull.rebase true

## Quick Cheatsheet

| Task | Command |
|---|---|
| Rebase current branch | `git rebase main` |
| Rebase specific branch | `git rebase main feature` |
| Rebase with `--onto` | `git rebase --onto main server client` |
| Pull with rebase | `git pull --rebase` |
| Default pull rebase | `git config --global pull.rebase true` |

> **Remember:** Rebase = cleaner history, but it rewrites commits. Rebase your own work; avoid rebasing shared history.
