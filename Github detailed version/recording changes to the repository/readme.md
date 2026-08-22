# Git Basics — Recording Changes

## File States

```text
Untracked → Staged → Committed
              ↑
Modified ─────┘
```

| State       | Meaning                          |
| ----------- | -------------------------------- |
| `Untracked` | Git doesn't know the file        |
| `Modified`  | Tracked file changed             |
| `Staged`    | Changes selected for next commit |
| `Committed` | Saved in Git history             |

---

## Check Status

```bash
git status
git status -s        # Short
git status --short
```

### Short Status

```text
?? file     # Untracked
A  file     # Staged new file
 M file     # Modified, unstaged
M  file     # Modified, staged
MM file     # Staged + modified again
```

```text
XY
││
│└── Working tree
└─── Staging area
```

---

## Track / Stage Files

```bash
git add file.txt
git add .
git add directory/
git add *.c
```

> `git add` = **add this content to the next commit**

### Important

If you modify a file **after** `git add`, stage it again:

```bash
git add file.txt
```

---

## `.gitignore`

Create:

```text
.gitignore
```

Example:

```gitignore
*.log
*.tmp
*.o
*.a
build/
```

### Patterns

```gitignore
*.log        # Match files
/build/      # Only root build/
build/       # Directories named build
!important.log  # Don't ignore this
# comment
```

### Glob basics

```text
*       → 0 or more characters
?       → 1 character
[abc]   → a, b, or c
[0-9]   → 0 through 9
**      → Nested directories
```

Example:

```gitignore
doc/*.txt
doc/**/*.pdf
```

> `.gitignore` can exist in the repository root or in subdirectories.

---

## View Changes

### Unstaged Changes

```bash
git diff
```

```text
Working Tree
     ↓
Staging Area
```

Shows changes **not yet staged**.

### Staged Changes

```bash
git diff --staged
git diff --cached
```

```text
Staging Area
     ↓
Last Commit
```

Shows changes that **will go into the next commit**.

### External Diff Tool

```bash
git difftool
git difftool --tool-help
```

---

## Commit

### Normal Commit

```bash
git commit
```

Opens the configured editor for the commit message.

### Commit with Message

```bash
git commit -m "Add new feature"
```

### Show Diff While Committing

```bash
git commit -v
```

---

## Skip Staging for Tracked Files

```bash
git commit -a -m "Update files"
```

Automatically stages **modified/deleted tracked files** and commits them.

⚠️ Does **not** include new untracked files.

```text
Tracked changes  → included
Untracked files  → NOT included
```

---

## Remove Files

### Delete + Stage Removal

```bash
git rm file.txt
```

Then:

```bash
git commit -m "Remove file"
```

### Force Remove

```bash
git rm -f file.txt
```

Use when the file has modifications/staged changes that would otherwise prevent removal.

### Stop Tracking but Keep File

```bash
git rm --cached file.txt
```

Useful when a file was accidentally tracked and should now be ignored.

Example:

```bash
git rm --cached README
```

---

## Remove Multiple Files

```bash
git rm log/\*.log
git rm \*~
```

Can use:

* Files
* Directories
* Glob patterns

---

## Rename / Move Files

### Recommended Shortcut

```bash
git mv old.txt new.txt
```

Equivalent to:

```bash
mv old.txt new.txt
git rm old.txt
git add new.txt
```

Git detects renames based on the resulting content; `git mv` is mainly a convenient one-command operation.

---

# Essential Workflow

```bash
# Check
git status

# Stage
git add <file>

# Review staged changes
git diff --staged

# Commit
git commit -m "message"

# Check again
git status
```

### Modify → Stage → Commit

```text
Modify
  ↓
git status
  ↓
git add
  ↓
git diff --staged
  ↓
git commit
```

### Remember

```text
git status       → What's changed?
git add          → What goes into next commit?
git diff         → What's unstaged?
git diff --staged → What's staged?
git commit       → Save snapshot
git rm           → Delete + stage removal
git rm --cached  → Stop tracking, keep file
git mv           → Rename/move
.gitignore       → Ignore unwanted files
```

