# Git Undoing Things

Quick cheatsheet for undoing changes in Git.

## 1. Amend Last Commit

Fix the **last commit** by adding forgotten changes or changing the message.

```bash
git add <file>
git commit --amend
```

⚠️ Avoid amending commits that have already been pushed.

---

## 2. Unstage a File

### Recommended: `git restore`

```bash
git restore --staged <file>
```

Moves the file from **staged → unstaged** without deleting changes.

### Older method

```bash
git reset HEAD <file>
```

---

## 3. Discard Changes

⚠️ **Deletes your uncommitted changes** in the file.

### Recommended: `git restore`

```bash
git restore <file>
```

### Older method

```bash
git checkout -- <file>
```

---

## Quick Cheatsheet

| Task                  | Command                       |
| --------------------- | ----------------------------- |
| Fix last commit       | `git commit --amend`          |
| Unstage file          | `git restore --staged <file>` |
| Unstage (old)         | `git reset HEAD <file>`       |
| Discard file changes  | `git restore <file>`          |
| Discard changes (old) | `git checkout -- <file>`      |

### ⚠️ Remember

* **Unstage** → changes are kept.
* **Restore** → uncommitted changes are discarded.
* **Amend** → replaces the previous commit.
* Committed work is generally recoverable; uncommitted discarded work may be lost.

