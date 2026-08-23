# Git Remotes

Git remotes are references to repositories hosted elsewhere (GitHub, another server, or even another local repository).

## View Remotes

```bash
git remote
git remote -v
```

* `git remote` → Show remote names
* `git remote -v` → Show fetch & push URLs
* `origin` → Default remote name after `git clone`

## Add Remote

```bash
git remote add <name> <url>
```

Example:

```bash
git remote add origin https://github.com/user/repo.git
```

## Fetch Changes

```bash
git fetch <remote>
```

Downloads new data/branches **without merging** into your current branch.

```bash
git fetch origin
```

## Pull Changes

```bash
git pull
```

Fetches + merges changes from the tracked remote branch.

```bash
git pull origin main
```

### Pull Rebase Configuration

```bash
git config --global pull.rebase false   # merge
git config --global pull.rebase true    # rebase
```

## Push Changes

```bash
git push <remote> <branch>
```

Example:

```bash
git push origin main
```

Push may be rejected if the remote contains changes you don't have locally. Fetch and integrate those changes first.

## Inspect Remote

```bash
git remote show <remote>
```

Example:

```bash
git remote show origin
```

Shows:

* Remote URLs
* Remote branches
* Tracking branches
* Push/pull configuration

## Rename Remote

```bash
git remote rename <old> <new>
```

Example:

```bash
git remote rename pb paul
```

## Remove Remote

```bash
git remote remove <name>
# or
git remote rm <name>
```

Removes the remote and its associated remote-tracking branches/configuration.

## Quick Cheatsheet

| Task             | Command                         |
| ---------------- | ------------------------------- |
| List remotes     | `git remote`                    |
| Show URLs        | `git remote -v`                 |
| Add remote       | `git remote add <name> <url>`   |
| Download changes | `git fetch <remote>`            |
| Fetch + merge    | `git pull`                      |
| Upload changes   | `git push <remote> <branch>`    |
| Inspect remote   | `git remote show <remote>`      |
| Rename remote    | `git remote rename <old> <new>` |
| Remove remote    | `git remote remove <name>`      |

