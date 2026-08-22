# Git Basics — Getting a Git Repository

## 1. Get a Git Repository

### Two ways

```text
1. Existing local project → git init
2. Existing remote repo   → git clone
```

---

## 2. Initialize Existing Project

```bash
cd <project-directory>
git init
```

Creates:

```text
.git/
```

### Start tracking files

```bash
git add <file>
git add .
git add *.c
```

### Initial commit

```bash
git commit -m "Initial project version"
```

### Complete flow

```bash
cd my_project
git init
git add .
git commit -m "Initial project version"
```

---

## 3. Clone Existing Repository

```bash
git clone <repository-url>
```

Example:

```bash
git clone https://github.com/libgit2/libgit2
```

Then:

```bash
cd libgit2
```

### Clone with custom directory name

```bash
git clone <repository-url> <directory-name>
```

Example:

```bash
git clone https://github.com/libgit2/libgit2 mylibgit
```

---

## 4. Clone Protocols

### HTTPS

```bash
git clone https://github.com/user/repo.git
```

### Git Protocol

```bash
git clone git://server/path/to/repo.git
```

### SSH

```bash
git clone user@server:path/to/repo.git
```

---

## 5. `git init` vs `git clone`

```text
git init
→ Create a NEW repository
→ Existing local project
→ Creates .git/
→ Files are initially untracked

git clone
→ Copy an EXISTING repository
→ Gets project + Git history
→ Creates .git/
→ Ready to work
```

---

## 6. Essential Commands

```bash
# Initialize repository
git init

# Check status
git status

# Stage one file
git add file.txt

# Stage everything
git add .

# Stage matching files
git add *.c

# Commit
git commit -m "message"

# Clone repository
git clone <url>

# Clone with custom directory
git clone <url> <directory>

# Enter repository
cd <directory>
```

---

## 7. Quick Workflow

### New Local Project

```bash
cd project
git init
git add .
git commit -m "Initial commit"
```

### Existing Remote Project

```bash
git clone <url>
cd <repository>
```

---

## 8. Memory Trick

```text
git init    → Start Git
git clone   → Get existing Git repo
git add     → Stage
git commit  → Save snapshot
```

