# Git Log — Viewing Commit History

`git log` is used to view the **commit history** of a Git repository.

## Basic Command

```bash
git log
```

Shows:

* Commit SHA
* Author
* Date
* Commit message

Latest commits appear first.

## Useful Commands

| Command                   | Purpose                                   |
| ------------------------- | ----------------------------------------- |
| `git log`                 | View commit history                       |
| `git log -2`              | Show last 2 commits                       |
| `git log -p`              | Show changes/diff for each commit         |
| `git log --stat`          | Show files changed + insertions/deletions |
| `git log --name-only`     | Show modified file names                  |
| `git log --name-status`   | Show added/modified/deleted files         |
| `git log --oneline`       | Compact one-line history                  |
| `git log --graph`         | Show branch/merge graph                   |
| `git log --abbrev-commit` | Show shortened commit SHA                 |
| `git log --relative-date` | Show relative dates                       |

## Custom Format

```bash
git log --pretty=format:"%h - %an, %ar : %s"
```

Useful format specifiers:

| Specifier | Meaning              |
| --------- | -------------------- |
| `%H`      | Full commit hash     |
| `%h`      | Short commit hash    |
| `%an`     | Author name          |
| `%ae`     | Author email         |
| `%ad`     | Author date          |
| `%ar`     | Relative author date |
| `%cn`     | Committer name       |
| `%s`      | Commit message       |

## Limit / Filter Commits

```bash
git log -5
git log --since="2 weeks ago"
git log --until="2026-08-22"
git log --author="Name"
git log --committer="Name"
git log --grep="keyword"
git log -S "function_name"
git log -- path/to/file
```

### Common Filters

* `-<n>` → Last **n** commits
* `--since / --after` → Commits after a date
* `--until / --before` → Commits before a date
* `--author` → Filter by author
* `--committer` → Filter by committer
* `--grep` → Search commit messages
* `-S` → Find commits that added/removed a string
* `-- path/to/file` → History of a specific file

## Most Useful Cheatsheet

```bash
git log
git log --oneline
git log --oneline --graph
git log -p -2
git log --stat
git log --author="Name"
git log --grep="keyword"
git log --since="2 weeks ago"
git log -S "function_name"
git log -- path/to/file
```

