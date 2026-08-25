# Git Branching - Remote Branches

## Remote Branches

Remote branches are references to branches stored on a remote repository.

### Remote-Tracking Branches

Remote-tracking branches show the state of remote branches from your last fetch.

    <remote>/<branch>

Examples:

    origin/main
    origin/serverfix

`origin` is simply the default remote name created by `git clone`.

### View Remote Branches

    git branch -r
    git branch -a
    git remote show origin
    git ls-remote origin

### Fetch

Download changes from a remote:

    git fetch origin

Fetch from all remotes:

    git fetch --all

`git fetch` updates remote-tracking branches but does **not** modify your working directory.

### Push

Push a local branch:

    git push origin <branch>

Example:

    git push origin serverfix

Push to a differently named remote branch:

    git push origin serverfix:awesomebranch

### Work with Remote Branches

Merge a remote branch:

    git fetch origin
    git merge origin/serverfix

Create a local branch from a remote branch:

    git checkout -b serverfix origin/serverfix

Modern Git:

    git switch -c serverfix origin/serverfix

### Tracking Branches

Create a tracking branch:

    git checkout --track origin/serverfix

Set or change the upstream branch:

    git branch -u origin/serverfix

View tracking information:

    git branch -vv

`ahead` → local commits not pushed  
`behind` → remote commits not merged

For updated information:

    git fetch --all
    git branch -vv

Upstream shortcuts:

    @{upstream}
    @{u}

Example:

    git merge @{u}

### Pull

`git pull` generally performs:

    git fetch
    git merge

So:

    git pull

fetches changes from the tracked remote branch and merges them into the current branch.

### Delete Remote Branch

    git push origin --delete <branch>

Example:

    git push origin --delete serverfix

## Quick Cheatsheet

| Task | Command |
|---|---|
| List remote branches | `git branch -r` |
| List all branches | `git branch -a` |
| Show remote info | `git remote show origin` |
| Fetch remote | `git fetch origin` |
| Fetch all remotes | `git fetch --all` |
| Push branch | `git push origin <branch>` |
| Merge remote branch | `git merge origin/<branch>` |
| Create tracking branch | `git checkout --track origin/<branch>` |
| Set upstream | `git branch -u origin/<branch>` |
| View tracking info | `git branch -vv` |
| Pull changes | `git pull` |
| Delete remote branch | `git push origin --delete <branch>` |

> **Remember:** `fetch` = download, `pull` = fetch + merge, `push` = upload, `origin/<branch>` = remote-tracking branch.
