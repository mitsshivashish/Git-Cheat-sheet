# Git Hooks

## What are Git Hooks?

**Git Hooks** are scripts that Git automatically executes when certain Git events occur.

They can be used to automate tasks such as:

* Code validation
* Formatting
* Linting
* Running tests
* Checking commit messages
* Preventing invalid code from being committed

Git hooks are stored inside:

```text
.git/hooks/
```

---

# What are Pre-Commit Hooks?

A **pre-commit hook** runs **before a commit is created**.

It can check whether the code is valid before allowing the commit to happen.

### Example

Suppose you created:

```text
example.py
```

You want to make sure that the Python file passes a syntax/style check before committing it.

A **pre-commit hook** can automatically run `flake8` before the commit is created.

If the check fails, the commit is stopped.

---

# Where to Create a Pre-Commit Hook?

Inside your Git repository:

```text
.git/hooks/pre-commit
```

Navigate to the hooks directory:

```bash
cd .git/hooks
```

List the available sample hooks:

```bash
ls
```

You may see files such as:

```text
pre-commit.sample
pre-push.sample
commit-msg.sample
post-update.sample
```

---

# Creating a Pre-Commit Hook

Create the hook file:

```bash
touch .git/hooks/pre-commit
```

Open it in an editor and add:

```bash
#!/bin/bash

files=$(git diff --cached --name-only --diff-filter=ACM | grep "\.py$")

flake8 $files
```

---

# Understanding the Code

### 1. Find staged Python files

```bash
files=$(git diff --cached --name-only --diff-filter=ACM | grep "\.py$")
```

Breakdown:

```text
git diff --cached
```

Shows changes that are currently **staged**.

```text
--name-only
```

Shows only the names of the changed files.

```text
--diff-filter=ACM
```

Selects files that are:

* `A` → Added
* `C` → Copied
* `M` → Modified

```text
grep "\.py$"
```

Filters the results and keeps only files ending in `.py`.

The final list of Python files is stored in:

```bash
files
```

---

### 2. Run Flake8

```bash
flake8 $files
```

This runs **Flake8** against the staged Python files.

If Flake8 reports errors, the command returns a failure status and the commit can be stopped.

---

# Give the Hook Execute Permission

The hook needs execute permission.

You can use:

```bash
chmod +x .git/hooks/pre-commit
```

You may also see:

```bash
chmod 777 .git/hooks/pre-commit
```

However, **`chmod +x` is preferred** because it grants the execute permission without unnecessarily changing all other permissions.

---

# Complete Example

Suppose the project contains:

```text
my-project/
├── example.py
└── .git/
    └── hooks/
        └── pre-commit
```

### Step 1: Stage the Python file

```bash
git add example.py
```

### Step 2: Run the commit

```bash
git commit -m "Add example Python file"
```

Before the commit is created, Git automatically runs:

```text
.git/hooks/pre-commit
```

The hook finds the staged `.py` files:

```bash
files=$(git diff --cached --name-only --diff-filter=ACM | grep "\.py$")
```

Then runs:

```bash
flake8 $files
```

### If the code passes

```text
Flake8 → Pass
        ↓
Commit → Created
```

### If the code fails

```text
Flake8 → Errors
        ↓
Commit → Blocked
```

Fix the errors, stage the files again:

```bash
git add example.py
```

Then retry:

```bash
git commit -m "Add example Python file"
```

---

# Basic Git Hook Workflow

```text
git add
   ↓
Files enter Staging Area
   ↓
git commit
   ↓
Pre-Commit Hook
   ↓
Run checks
   ↓
 ┌───────────────┐
 │   Pass?       │
 └───────┬───────┘
       Yes / No
        /     \
       ↓       ↓
   Commit     Stop
   Created    Commit
```

---

# Quick Commands

| Command                          | Purpose                     |
| -------------------------------- | --------------------------- |
| `ls .git/hooks`                  | List available hooks        |
| `touch .git/hooks/pre-commit`    | Create pre-commit hook      |
| `chmod +x .git/hooks/pre-commit` | Make hook executable        |
| `git diff --cached --name-only`  | List staged file names      |
| `git commit`                     | Trigger the pre-commit hook |

---

## Key Points

* **Git Hooks** = Scripts triggered by Git events.
* **Pre-commit Hook** = Runs before a commit is created.
* Hooks are stored in **`.git/hooks/`**.
* The pre-commit hook file is **`.git/hooks/pre-commit`**.
* Use hooks to automate validation and quality checks.
* `chmod +x` makes the hook executable.
* A failed pre-commit check can prevent the commit from being created.

