# Git Aliases

Git aliases let you create **shortcuts for frequently used commands**.

## Common Aliases

```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
```

Now:

```bash
git ci       # git commit
git st       # git status
git br       # git branch
git co       # git checkout
```

## Custom Aliases

### Unstage

```bash
git config --global alias.unstage 'reset HEAD --'
```

Usage:

```bash
git unstage fileA
```

Same as:

```bash
git reset HEAD -- fileA
```

### Last Commit

```bash
git config --global alias.last 'log -1 HEAD'
```

Usage:

```bash
git last
```

Shows the **last commit**.

## External Commands

Use `!` to run an external command.

```bash
git config --global alias.visual '!gitk'
```

Usage:

```bash
git visual
```

## Quick Cheatsheet

| Alias                | Equivalent                 |
| -------------------- | -------------------------- |
| `git co`             | `git checkout`             |
| `git br`             | `git branch`               |
| `git ci`             | `git commit`               |
| `git st`             | `git status`               |
| `git unstage <file>` | `git reset HEAD -- <file>` |
| `git last`           | `git log -1 HEAD`          |
| `git visual`         | `gitk`                     |

### Syntax

```bash
git config --global alias.<shortcut> '<command>'
```

