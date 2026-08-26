# Distributed Git - Maintaining a Project

## Maintaining a Project

Maintaining a Git project involves **reviewing, testing, integrating, and releasing contributed work**.

## Topic Branches

Use temporary topic branches when testing or integrating contributions.

    git checkout -b <topic> master

This keeps experimental work isolated from long-running branches.

## Apply Patches

### `git apply`

Used for patches created from `git diff`.

    git apply <patch-file>

Check whether a patch applies cleanly:

    git apply --check <patch-file>

`git apply` modifies files but does **not create a commit**.

### `git am`

Used for patches created with `git format-patch`.

    git am <patch-file>

It preserves:
- Author information
- Commit message
- Commit history

If a patch conflicts:

    git add <file>
    git am --resolved

Other options:

    git am --skip
    git am --abort
    git am -3 <patch-file>

## Fetch a Contributor's Branch

    git remote add <name> <url>
    git fetch <name>
    git checkout -b <local-branch> <name>/<remote-branch>

One-time pull without saving the remote:

    git pull <url>

## Review Contributed Work

Show commits in a contribution branch that aren't in `master`:

    git log contrib --not master

Show the changes introduced by the branch:

    git diff master...contrib

`...` compares the branch with its common ancestor.

## Integrate Contributions

### Merge

    git checkout master
    git merge <topic-branch>

### Rebase

    git checkout <topic-branch>
    git rebase master
    git checkout master
    git merge <topic-branch>

Creates a cleaner, linear history.

### Cherry-Pick

Apply a specific commit to the current branch:

    git cherry-pick <commit>

Useful when you want only one commit from a topic branch.

## Rerere

`rerere` = **Reuse Recorded Resolution**

It remembers conflict resolutions and can reuse them later.

Enable it:

    git config --global rerere.enabled true

## Release Tagging

Create a signed release tag:

    git tag -s v1.5 -m "Release v1.5"

Push tags:

    git push --tags

## Describe a Build

Generate a human-readable version from the latest tag and commits:

    git describe master

Example:

    v1.6.2-rc1-20-g8c5b85c

## Create Release Archives

Tarball:

    git archive master --prefix='project/' | gzip > release.tar.gz

ZIP:

    git archive master --prefix='project/' --format=zip > release.zip

## Generate Changelog

Summarize commits since a release:

    git shortlog --no-merges master --not v1.0.1

## Quick Cheatsheet

| Task | Command |
|---|---|
| Create topic branch | `git checkout -b <branch> master` |
| Check patch | `git apply --check <patch>` |
| Apply diff patch | `git apply <patch>` |
| Apply email patch | `git am <patch>` |
| Resolve `git am` | `git am --resolved` |
| Skip patch | `git am --skip` |
| Abort patch | `git am --abort` |
| Fetch contributor | `git fetch <remote>` |
| Review commits | `git log <branch> --not master` |
| Review changes | `git diff master...<branch>` |
| Merge work | `git merge <branch>` |
| Rebase work | `git rebase master` |
| Apply one commit | `git cherry-pick <commit>` |
| Enable rerere | `git config --global rerere.enabled true` |
| Create signed tag | `git tag -s <tag> -m "message"` |
| Describe build | `git describe <commit>` |
| Create archive | `git archive <branch>` |
| Create changelog | `git shortlog` |

> **Remember:** Review contributions in topic branches first, then merge, rebase, or cherry-pick them into long-running branches. Tag releases and use `git describe`, `git archive`, and `git shortlog` to prepare releases.
