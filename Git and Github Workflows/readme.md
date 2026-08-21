# Git & GitHub Workflow

## 1. Create an Empty Git Repository

### Using CLI

Initialize a Git repository in the current folder:

```bash
git init
```

This creates a `.git` directory and turns the folder into a Git repository.

### Using GitHub GUI

1. Go to GitHub.
2. Open **Repositories**.
3. Click **New repository**.
4. Enter the repository name.
5. Click **Create repository**.

---

# 2. How Does GitHub Know Who Is Accessing Git?

When using GitHub from the CLI, GitHub needs to authenticate you.

Common authentication methods are:

* **Personal Access Token (PAT)** — commonly used with HTTPS
* **SSH Key** — recommended for convenient long-term CLI access

---

# 3. Personal Access Token (PAT)

A **Personal Access Token (PAT)** acts as a secure credential for authenticating with GitHub over HTTPS.

### Generate a PAT

On GitHub:

1. Go to **Settings**.
2. Go to **Developer settings**.
3. Select **Personal access tokens**.
4. Choose **Tokens (classic)** or the newer fine-grained token option.
5. Generate a token.
6. Copy and securely store the token.

> ⚠️ Never share your PAT or commit it to a repository.

### Important

Do **not** put your PAT directly inside the remote URL like this:

```bash
https://PAT@github.com/username/repository.git
```

Instead, use Git's credential manager or another secure authentication method.

---

# 4. Set the Remote Origin

If you already created a GitHub repository and want to connect your local repository to it:

```bash
git remote add origin https://github.com/username/repository.git
```

Check the configured remote:

```bash
git remote -v
```

Example output:

```text
origin  https://github.com/username/repository.git (fetch)
origin  https://github.com/username/repository.git (push)
```

### Change an Existing Origin

If `origin` already exists:

```bash
git remote set-url origin https://github.com/username/repository.git
```

---

# 5. Push Code to GitHub

Push a branch to GitHub:

```bash
git push origin <branch-name>
```

Example:

```bash
git push origin main
```

For the first push, you can also set the upstream branch:

```bash
git push -u origin main
```

After this, you can often use:

```bash
git push
```

---

# 6. Fork vs Clone

## Fork

**Fork = GitHub → GitHub**

A fork creates your own copy of someone else's repository under your GitHub account.

Typical workflow:

```text
Original GitHub Repository
          ↓
        Fork
          ↓
Your GitHub Repository
```

Forks are commonly used when contributing to open-source projects.

---

## Clone

**Clone = GitHub → Local Computer**

Clone downloads a GitHub repository to your local machine.

```bash
git clone <repository-url>
```

Example:

```bash
git clone https://github.com/username/repository.git
```

Typical workflow:

```text
GitHub Repository
       ↓
     clone
       ↓
Local Repository
```

---

# 7. Pull Changes from GitHub

To synchronize your local branch with the remote repository:

```bash
git pull origin <branch-name>
```

Example:

```bash
git pull origin main
```

`git pull` basically fetches the remote changes and integrates them into your current branch.

---

# 8. SSH Authentication with GitHub

SSH allows you to authenticate with GitHub using an SSH key instead of entering HTTPS credentials repeatedly.

### Step 1: Generate an SSH Key

Run:

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Press Enter to accept the default location, and optionally set a passphrase.

---

### Step 2: Start the SSH Agent

```bash
eval "$(ssh-agent -s)"
```

---

### Step 3: Add Your SSH Key

```bash
ssh-add ~/.ssh/id_ed25519
```

---

### Step 4: Copy Your Public Key

Linux/macOS:

```bash
cat ~/.ssh/id_ed25519.pub
```

On Windows Git Bash:

```bash
cat ~/.ssh/id_ed25519.pub
```

Copy the complete output.

> Only share the `.pub` key. Never share your private key (`id_ed25519`).

---

### Step 5: Add the Key to GitHub

On GitHub:

```text
Settings
   ↓
SSH and GPG keys
   ↓
New SSH key
   ↓
Paste public key
   ↓
Add SSH key
```

---

### Step 6: Test the Connection

```bash
ssh -T git@github.com
```

If authentication is successful, GitHub will confirm that you have authenticated.

---

### Step 7: Use the SSH Remote

Instead of HTTPS:

```bash
git remote set-url origin git@github.com:username/repository.git
```

Check it:

```bash
git remote -v
```

---

# 9. What Are Branches?

A **branch** is an independent line of development in a Git repository.

Instead of making all changes directly on `main`, developers can create separate branches.

Example:

```text
main
  │
  └── staging
        │
        └── dev
              │
              ├── feature-login
              ├── feature-payment
              └── feature-dashboard
```

Branches help developers work on different features without directly affecting the main codebase.

---

# 10. Branch Commands

### List Branches

```bash
git branch
```

---

### Create a New Branch

```bash
git branch <branch-name>
```

Example:

```bash
git branch feature-login
```

---

### Switch to a Branch

Using `checkout`:

```bash
git checkout <branch-name>
```

Example:

```bash
git checkout feature-login
```

Using the newer `switch` command:

```bash
git switch <branch-name>
```

---

### Create and Switch to a Branch

With `checkout`:

```bash
git checkout -b <branch-name>
```

With `switch`:

```bash
git switch -c <branch-name>
```

Example:

```bash
git switch -c feature-login
```

---

# 11. Git Log

View commit history:

```bash
git log
```

For a shorter version:

```bash
git log --oneline
```

Example:

```text
a82f91c Add login functionality
91bc721 Fix navbar bug
72af310 Initial commit
```

The first value is the commit's shortened hash.

---

# 12. Example Branching Strategy

A simple development workflow can look like:

```text
main
  │
  └── staging
        │
        └── dev
              │
              ├── feature-login
              ├── feature-payment
              └── feature-dashboard
```

### Typical Flow

```text
feature branch
      ↓
     dev
      ↓
   staging
      ↓
    main
```

The exact branching strategy depends on the team's workflow.

---

# 13. How to Create a Pull Request

A **Pull Request (PR)** is a request to merge changes from one branch into another branch.

For example:

```text
feature-login
      ↓
 Pull Request
      ↓
     dev
```

### Step 1: Create a Feature Branch

```bash
git switch -c feature-login
```

### Step 2: Make Your Changes

Edit or create your files.

### Step 3: Check Your Changes

```bash
git status
```

### Step 4: Stage the Changes

```bash
git add .
```

Or add a specific file:

```bash
git add <filename>
```

### Step 5: Commit

```bash
git commit -m "Add login functionality"
```

### Step 6: Push the Branch

```bash
git push -u origin feature-login
```

### Step 7: Create the Pull Request

On GitHub:

1. Open the repository.
2. GitHub will usually show a **Compare & pull request** option for the newly pushed branch.
3. Select the source and target branches.
4. Add a title.
5. Describe the changes.
6. Add reviewers if required.
7. Click **Create pull request**.

---

# 14. How to Rectify/Fix a Pull Request

If the reviewer finds a problem, **do not necessarily create a new PR**.

Simply make the required changes on the **same branch** used by the PR.

### Step 1: Make the Fix

```bash
git switch feature-login
```

Modify the required files.

### Step 2: Stage the Changes

```bash
git add .
```

### Step 3: Commit the Fix

```bash
git commit -m "Fix login validation"
```

### Step 4: Push Again

```bash
git push
```

The existing Pull Request will automatically update with the new commit.

```text
Existing PR
    ↓
Make corrections
    ↓
git add
    ↓
git commit
    ↓
git push
    ↓
Existing PR gets updated
```

---

# 15. Complete GitHub Workflow

A common workflow looks like this:

```text
Create GitHub Repository
          ↓
       git clone
          ↓
    Local Repository
          ↓
    Create Branch
          ↓
    Make Changes
          ↓
      git add
          ↓
     git commit
          ↓
      git push
          ↓
   Create Pull Request
          ↓
      Code Review
          ↓
   Fix if Required
          ↓
      git push
          ↓
    PR Updated
          ↓
       Merge
          ↓
        main
```

---

# Quick Command Reference

| Command                           | Purpose                           |
| --------------------------------- | --------------------------------- |
| `git init`                        | Initialize a local Git repository |
| `git clone <url>`                 | Clone a repository                |
| `git remote add origin <url>`     | Add a remote repository           |
| `git remote -v`                   | View remote URLs                  |
| `git remote set-url origin <url>` | Change remote URL                 |
| `git push origin <branch>`        | Push branch to GitHub             |
| `git pull origin <branch>`        | Pull changes from GitHub          |
| `git branch`                      | List branches                     |
| `git branch <name>`               | Create a branch                   |
| `git checkout <name>`             | Switch branches                   |
| `git switch <name>`               | Switch branches                   |
| `git switch -c <name>`            | Create and switch to a branch     |
| `git log --oneline`               | View compact commit history       |
| `git status`                      | Check repository status           |
| `git add .`                       | Stage all changes                 |
| `git commit -m "message"`         | Create a commit                   |

---

## Key Concepts

```text
Git
 └── Version Control System

GitHub
 └── Remote hosting & collaboration platform

Repository
 └── Project managed by Git

Commit
 └── Snapshot of changes

Branch
 └── Separate line of development

Remote
 └── Connection to a remote repository

Origin
 └── Default name commonly given to the remote repository

Fork
 └── GitHub → GitHub

Clone
 └── GitHub → Local

Pull
 └── Remote → Local

Push
 └── Local → Remote

Pull Request
 └── Request to merge changes from one branch into another
```

