# Git Branching — Basic Branching & Merging

Branching lets you work on features or fixes **independently** and merge them later.

## Create + Switch Branch

```bash
git checkout -b <branch>
```

Modern:

```bash
git switch -c <branch>
```

Equivalent to:

```bash
git branch <branch>
git checkout <branch>
```

## Typical Workflow

```text
main
 │
 ├── iss53 → feature work
 │
 └── hotfix → fix → merge into main
```

### Hotfix Workflow

```bash
git switch main
git switch -c hotfix

# make changes
git add .
git commit -m "Fix critical issue"

git switch main
git merge hotfix
git branch -d hotfix
```

A **fast-forward merge** happens when the branch being merged is directly ahead of the current branch.

## Merge a Feature Branch

```bash
git switch main
git merge iss53
```

If histories have diverged, Git creates a **merge commit** using a three-way merge.

```text
      C---D  iss53
     /
A---B
     \
      E---F  main

        ↓ merge

      C---D
     /     \
A---B       M
     \     /
      E---F
```

## Merge Conflicts

A conflict occurs when Git cannot automatically combine changes.

```bash
git merge iss53
```

Check conflicts:

```bash
git status
```

Git marks conflicts like:

```text
<<<<<<< HEAD
Your changes
=======
Incoming changes
>>>>>>> iss53
```

### Resolve Conflict

1. Open the conflicted file.
2. Choose/combine the correct changes.
3. Remove `<<<<<<<`, `=======`, `>>>>>>>`.
4. Stage the resolved file.

```bash
git add <file>
```

5. Complete the merge:

```bash
git commit
```

### Abort a Merge

If you want to cancel the merge:

```bash
git merge --abort
```

## Merge Tool

```bash
git mergetool
```

Opens a graphical tool to help resolve conflicts.

## Delete Branch

After merging:

```bash
git branch -d <branch>
```

## Quick Cheatsheet

| Task                   | Command                  |
| ---------------------- | ------------------------ |
| Create + switch        | `git switch -c <branch>` |
| Switch branch          | `git switch <branch>`    |
| Merge branch           | `git merge <branch>`     |
| Check conflicts        | `git status`             |
| Mark conflict resolved | `git add <file>`         |
| Finish merge           | `git commit`             |
| Abort merge            | `git merge --abort`      |
| Open merge tool        | `git mergetool`          |
| Delete merged branch   | `git branch -d <branch>` |

> **Remember:** `git merge` combines branches. If Git can't combine changes automatically, resolve the conflicts, `git add` the files, then `git commit`.

