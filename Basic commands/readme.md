# Git Basics

## What is Git?

**Git** is a **Version Control System (VCS)** used to manage different versions of source code and track changes in repositories.

It helps developers:

* Track changes in code
* Maintain different versions of a project
* Revert changes when needed
* Collaborate with other developers

---

## Git vs GitHub, GitLab & Bitbucket

| Tool          | What it is                                   |
| ------------- | -------------------------------------------- |
| **Git**       | Version Control System that runs locally     |
| **GitHub**    | Cloud platform for hosting Git repositories  |
| **GitLab**    | Git repository hosting and DevOps platform   |
| **Bitbucket** | Git repository hosting platform by Atlassian |

**Simple way to remember:**

> Git = Tool for version control
> GitHub/GitLab/Bitbucket = Platforms for hosting and collaborating on Git repositories

---

## Installing Git

For Windows, download **Git SCM (Git for Windows)**.

On most Unix/Linux-based systems, Git is commonly available through the package manager or may already be installed.

Check whether Git is installed:

```bash
git --version
```

---

## Initialize a Git Repository

Create an empty Git repository in the current directory:

```bash
git init
```

This creates a hidden `.git` directory that stores Git's repository information.

---

## Git Staging Area

Add a file to the **staging area**:

```bash
git add <filename>
```

Example:

```bash
git add README.md
```

---

## Unstage a File

Remove a file from the staging area without deleting the file:

```bash
git rm --cached <filename>
```

Example:

```bash
git rm --cached README.md
```

---

## Commit Changes

Save the staged changes as a commit:

```bash
git commit -m "message"
```

Example:

```bash
git commit -m "Add README file"
```

> **Note:** A commit records the staged changes in Git's version history.

---

## What If We Delete a File?

If a tracked file is deleted and you want to restore it to its previous state:

```bash
git restore <filename>
```

Example:

```bash
git restore README.md
```

This restores the file from the last committed version.

---

## Basic Git Workflow

```text
Working Directory
       ↓
   git add
       ↓
Staging Area
       ↓
 git commit
       ↓
Git Repository
```

### Quick Command Reference

| Command                      | Purpose                         |
| ---------------------------- | ------------------------------- |
| `git --version`              | Check Git version               |
| `git init`                   | Initialize a Git repository     |
| `git add <filename>`         | Add file to staging area        |
| `git rm --cached <filename>` | Unstage a file                  |
| `git commit -m "message"`    | Commit staged changes           |
| `git restore <filename>`     | Restore a deleted/modified file |

