# Git Basics — README

## What is Git?

**Git** is a **distributed version control system (VCS)** used to track changes in a project.

In simple words:

> Git keeps a history of your project so you can track, compare, undo, and manage changes.

---

## 1. Snapshots, Not Differences

Traditional VCSs generally think in terms of **changes/deltas**:

```text
Version 1
   ↓ changes
Version 2
   ↓ changes
Version 3
```

Git thinks more like a series of **snapshots**:

```text
Snapshot 1 → Snapshot 2 → Snapshot 3
```

Every time you `commit`, Git records the state of the project at that point.

If a file hasn't changed, Git can reference the existing stored content instead of unnecessarily storing another complete copy.

### Key idea

```text
Git = Stream of project snapshots
```

This snapshot-based design is one reason Git's branching and merging are powerful.

---

## 2. Nearly Every Git Operation Is Local

Git stores the project's history in your **local repository**.

```text
Your Computer
├── Working Tree
├── Staging Area
└── .git/
    └── Git history + database
```

Because the history is local, many commands work without an internet connection:

```bash
git status
git log
git diff
git commit
git branch
```

You mainly need a network connection when working with a remote repository:

```bash
git fetch
git pull
git push
```

### Benefit

You can:

* View history offline
* Compare changes offline
* Create commits offline
* Create and manage branches offline
* Continue working without a VPN/network connection

---

## 3. Git Has Integrity

Git uses **hashes** to identify and verify its stored data.

Git has historically used **SHA-1** object IDs such as:

```text
24b9da6552252987aa493b52f8696cd6d3b00373
```

Conceptually:

```text
File/Data
   ↓
Hash function
   ↓
Hash/Object ID
```

If the content changes, its hash changes.

This allows Git to detect unexpected changes or corruption.

### Important

Git identifies stored objects using their **content-based object IDs**, rather than simply relying on normal filenames.

---

## 4. Git Generally Only Adds Data

Most Git operations add information to Git's database instead of immediately destroying existing history.

For example:

```bash
git commit -m "Add feature"
```

creates a new snapshot.

This makes experimentation and recovery easier.

### Important

Uncommitted changes are **not automatically safe**.

Once changes are committed, they are generally much easier to recover, especially when the repository is also pushed to another repository.

---

# 5. The Three Git States

A file can be in three important states:

```text
Modified → Staged → Committed
```

## Modified

You changed a file, but haven't staged the changes.

```text
Working Tree
    ↓
 Modified
```

Example:

```bash
vim app.py
```

---

## Staged

You selected changes to be included in the next commit.

```bash
git add app.py
```

```text
Working Tree
    ↓ git add
Staging Area
    ↓
  Staged
```

---

## Committed

The staged snapshot has been saved into Git's local database.

```bash
git commit -m "Update app"
```

```text
Staging Area
    ↓ git commit
Git Directory
    ↓
 Committed
```

---

# 6. Three Main Areas of a Git Repository

```text
┌──────────────────┐
│   Working Tree   │
│                  │
│   Your files     │
└────────┬─────────┘
         │ git add
         ↓
┌──────────────────┐
│  Staging Area    │
│                  │
│  Next commit     │
└────────┬─────────┘
         │ git commit
         ↓
┌──────────────────┐
│   Git Directory  │
│      .git/       │
│                  │
│  Git database    │
└──────────────────┘
```

## Working Tree

The files you actually work on.

Example:

```text
project/
├── app.py
├── README.md
└── config.txt
```

Changes made here are **modified** until staged.

---

## Staging Area

The staging area contains information about **what will go into the next commit**.

Its technical name in Git is:

```text
Index
```

Command:

```bash
git add <file>
```

---

## Git Directory

Usually:

```text
.git/
```

This contains Git's metadata and object database, including the repository's history.

It is the most important internal part of a Git repository.

---

# 7. Basic Git Workflow

The standard workflow is:

```text
1. Modify files
       ↓
2. Stage changes
       ↓
3. Commit changes
```

Commands:

```bash
# Check current state
git status

# Stage a file
git add file.txt

# Stage all changes
git add .

# Commit staged changes
git commit -m "Add file"
```

### Complete flow

```text
Edit file
   ↓
Modified
   ↓ git add
Staged
   ↓ git commit
Committed
```

---

# 8. Installing Git

Check whether Git is installed:

```bash
git --version
```

Example:

```text
git version 2.x.x
```

## Debian / Ubuntu

```bash
sudo apt install git-all
```

## Fedora / RHEL

```bash
sudo dnf install git-all
```

## macOS

Run:

```bash
git --version
```

If Git is not installed, macOS can prompt you to install the Xcode Command Line Tools.

## Windows

Install **Git for Windows**.

Official downloads:

* Git: https://git-scm.com/downloads
* Git for Windows: https://gitforwindows.org/

---

# 9. Git vs GitHub

Git and GitHub are **not the same thing**.

| Git                    | GitHub                                    |
| ---------------------- | ----------------------------------------- |
| Version control system | Repository hosting/collaboration platform |
| Runs locally           | Primarily online                          |
| Tracks project history | Hosts Git repositories                    |
| Works offline          | Usually requires internet                 |
| Uses `git commit`      | Provides PRs, Issues, collaboration, etc. |

Typical relationship:

```text
Git
 ↓
Local Repository
 ↓ git push
GitHub
 ↓
Remote Repository
```

---

# 10. Essential Git Commands

```bash
# Check Git version
git --version

# Check repository status
git status

# View commit history
git log

# View unstaged changes
git diff

# Stage a specific file
git add file.txt

# Stage all changes
git add .

# Create a commit
git commit -m "Commit message"

# Copy an existing remote repository
git clone <repository-url>

# Download remote changes without integrating them
git fetch

# Fetch and integrate remote changes
git pull

# Upload local commits
git push
```

---

# 11. Quick Mental Model

Remember Git using this flow:

```text
                    GIT
                     │
          ┌──────────┴──────────┐
          │                     │
      Snapshots              Local
      not deltas             history
          │                     │
          └──────────┬──────────┘
                     │
              Three Main Areas
                     │
        ┌────────────┼────────────┐
        ↓            ↓            ↓
   Working Tree → Staging →     .git/
    Modified       Staged       Committed
        │             │             │
        └─ git add ───┘             │
                       git commit ──┘
```

---

# 12. Important Points to Remember

* **Git = Distributed Version Control System**
* Git thinks in terms of **snapshots**, not just file differences.
* Most Git operations are **local**.
* Git uses **hashes/object IDs** to identify and verify data.
* Git generally **adds data rather than immediately destroying history**.
* The three important states are:

  * **Modified**
  * **Staged**
  * **Committed**
* The three important areas are:

  * **Working Tree**
  * **Staging Area**
  * **Git Directory (`.git/`)**
* `git add` moves changes toward the **staging area**.
* `git commit` saves the staged snapshot into the **local Git repository**.
* `git push` sends local commits to a **remote repository**.
* Git and GitHub are **different things**.

---

## One-Line Summary

> **Git is a distributed version control system that stores project history as snapshots, keeps that history locally, verifies data using hashes, and manages changes through Working Tree → Staging Area → Git Repository.**

