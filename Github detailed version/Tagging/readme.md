# Git Tagging

Tags mark **specific commits**, commonly used for releases like `v1.0`, `v2.0`.

## List Tags

```bash
git tag
git tag -l "v1.8.5*"
```

> `-l` / `--list` is required when using a wildcard pattern.

## Create Tags

### Annotated Tag — Recommended

Stores tagger, date, message, and commit information.

```bash
git tag -a v1.0 -m "Release v1.0"
```

View tag:

```bash
git show v1.0
```

### Lightweight Tag

Simple pointer to a commit.

```bash
git tag v1.0
```

## Tag an Older Commit

```bash
git tag -a v1.2 <commit-hash>
```

Example:

```bash
git tag -a v1.2 9fceb02
```

## Push Tags

Push one tag:

```bash
git push origin v1.0
```

Push all tags:

```bash
git push origin --tags
```

Push annotated tags:

```bash
git push origin --follow-tags
```

## Delete Tags

### Local

```bash
git tag -d v1.0
```

### Remote

```bash
git push origin --delete v1.0
```

## Checkout a Tag

```bash
git checkout v1.0
```

⚠️ This puts you in **detached HEAD** state.

If you want to make changes from that tag, create a branch:

```bash
git checkout -b version1 v1.0
```

## Quick Cheatsheet

| Task              | Command                          |
| ----------------- | -------------------------------- |
| List tags         | `git tag`                        |
| Search tags       | `git tag -l "pattern"`           |
| Annotated tag     | `git tag -a <tag> -m "message"`  |
| Lightweight tag   | `git tag <tag>`                  |
| Tag old commit    | `git tag -a <tag> <commit>`      |
| Show tag          | `git show <tag>`                 |
| Push tag          | `git push origin <tag>`          |
| Push all tags     | `git push origin --tags`         |
| Delete local tag  | `git tag -d <tag>`               |
| Delete remote tag | `git push origin --delete <tag>` |
| Checkout tag      | `git checkout <tag>`             |
| Branch from tag   | `git checkout -b <branch> <tag>` |

