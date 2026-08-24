# Git Branch Management

Branch management helps you **inspect, delete, and rename branches**.

## List Branches

```bash
git branch
```

`*` = current branch (`HEAD`).

```bash
git branch -v
```

Shows the latest commit on each branch.

```bash
git branch --all
```

Shows local + remote branches.

## Check Merge Status

### Already Merged

```bash
git branch --merged
```

Safe to delete merged branches:

```bash
git branch -d <branch>
```

### Not Merged

```bash
git branch --no-merged
```

Force delete an unmerged branch:

```bash
git branch -D <branch>
```

> ⚠️ `-D` can delete unmerged work.

Check against a specific branch:

```bash
git branch --no-merged main
```

## Rename a Branch

Rename locally:

```bash
git branch --move <old-name> <new-name>
```

Push the renamed branch:

```bash
git push --set-upstream origin <new-name>
```

Delete the old remote branch:

```bash
git push origin --delete <old-name>
```

### Example

```bash
git branch -m bad-name good-name
git push -u origin good-name
git push origin --delete bad-name
```

## Rename `master` → `main`

```bash
git branch -m master main
git push -u origin main
```

Before deleting the old remote branch, update:

- Repository default branch
- CI/CD & build scripts
- Documentation
- Integrations
- Pull requests
- Other references to `master`

Then:

```bash
git push origin --delete master
```

## Quick Cheatsheet

| Task | Command |
|---|---|
| List branches | `git branch` |
| Show latest commits | `git branch -v` |
| Show all branches | `git branch --all` |
| Merged branches | `git branch --merged` |
| Unmerged branches | `git branch --no-merged` |
| Delete branch | `git branch -d <branch>` |
| Force delete | `git branch -D <branch>` |
| Rename branch | `git branch -m <old> <new>` |
| Push renamed branch | `git push -u origin <new>` |
| Delete remote branch | `git push origin --delete <branch>` |

> **Remember:** `-d` = safe delete check, `-D` = force delete.

