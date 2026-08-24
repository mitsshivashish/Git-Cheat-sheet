# Git Branching — Branches in a Nutshell

A **branch** is a lightweight pointer to a commit that lets you work independently without affecting another branch.

## Key Concepts

* Git stores **snapshots**, not just changes.
* A commit points to its **parent commit** and a snapshot.
* A branch is simply a **movable pointer to a commit**.
* `HEAD` points to the **branch you're currently on**.
* Branches are cheap and fast to create.

## Create a Branch

```bash
git branch testing
```

Creates a branch but **does not switch** to it.

## Switch Branch

```bash
git checkout testing
```

Recommended modern command:

```bash
git switch testing
```

## Create + Switch

Old:

```bash
git checkout -b testing
```

Modern:

```bash
git switch -c testing
```

## Check Branches

```bash
git branch
git log --oneline --decorate
```

Show all branch history:

```bash
git log --oneline --decorate --graph --all
```

## How Branches Work

Example:

```text
A---B---C  main
         \
          D---E  testing
```

* `main` and `testing` started from the same commit.
* Commits on `testing` don't move `main`.
* Commits on `main` don't move `testing`.
* This creates **divergent history**.

## Switch Back

```bash
git switch main
```

or:

```bash
git checkout main
```

Switching branches also changes your working directory to match that branch.

## Switch to Previous Branch

```bash
git switch -
```

## Why Git Branches Are Lightweight

A Git branch is essentially a pointer containing a commit's SHA-1.

Therefore:

* Creating a branch is nearly instantaneous.
* Switching branches is fast.
* Git encourages frequent branching and merging.

## Quick Cheatsheet

| Task                | Command                  |
| ------------------- | ------------------------ |
| Create branch       | `git branch <name>`      |
| Switch branch       | `git switch <name>`      |
| Create + switch     | `git switch -c <name>`   |
| Old create + switch | `git checkout -b <name>` |
| Previous branch     | `git switch -`           |
| Show branches       | `git branch`             |
| Show all history    | `git log --all --graph`  |

> **Remember:** `git branch` creates a branch; `git switch` moves `HEAD` to a branch.

