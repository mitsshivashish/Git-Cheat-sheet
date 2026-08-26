# Distributed Git - Contributing to a Project

## Contributing to a Project

Git contribution workflows depend on:
- Number of contributors
- Project workflow
- Your commit/push access
- How contributions are accepted

## Commit Guidelines

Check whitespace before committing:

    git diff --check

Keep commits:
- Small and logically separate
- Focused on one issue/feature
- Easy to review or revert

Partially stage changes:

    git add --patch

Good commit message format:

    Short, capitalized summary (≤ 50 chars)

    Detailed explanation if needed.
    Explain motivation and implementation.

Use the **imperative mood**:

    Fix bug
    Add feature

## Private Small Team

Typical workflow:

    git pull
    # make changes
    git add .
    git commit
    git push

If push is rejected because someone else pushed first:

    git fetch origin
    git merge origin/master
    git push origin master

For feature work, use topic branches:

    git checkout -b featureA
    # work + commit
    git push -u origin featureA

## Managed Team

Teams can work on separate branches while integrators control the main branch.

Example:

    featureA → integrator
    featureB → integrator
              ↓
            master

Useful commands:

    git checkout -b featureA
    git push -u origin featureA
    git fetch origin
    git merge origin/featureBee
    git push -u origin featureB:featureBee

## Forked Public Project

Typical workflow:

    git clone <url>
    git checkout -b featureA
    # work + commits

Add your fork:

    git remote add myfork <url>

Push your branch:

    git push -u myfork featureA

Request maintainers to pull your work:

    git request-pull origin/master myfork

Keep each contribution in a separate topic branch.

If the main project changes, rebase your branch:

    git fetch origin
    git checkout featureA
    git rebase origin/master
    git push -f myfork featureA

For a revised version:

    git checkout -b featureBv2 origin/master
    git merge --squash featureB
    # make changes
    git commit
    git push myfork featureBv2

## Public Project Over Email

Create a topic branch:

    git checkout -b topicA
    # work + commits

Generate patch files:

    git format-patch -M origin/master

Send patches by email:

    git send-email *.patch

Patches can also be sent using:

    git imap-send

## Quick Cheatsheet

| Task | Command |
|---|---|
| Check whitespace | `git diff --check` |
| Partial staging | `git add --patch` |
| Create feature branch | `git checkout -b <branch>` |
| Fetch updates | `git fetch origin` |
| Merge remote work | `git merge origin/master` |
| Push branch | `git push -u origin <branch>` |
| Add fork | `git remote add myfork <url>` |
| Request pull | `git request-pull origin/master myfork` |
| Rebase on main | `git rebase origin/master` |
| Squash branch | `git merge --squash <branch>` |
| Create email patches | `git format-patch -M origin/master` |
| Send patches | `git send-email *.patch` |

> **Remember:** Keep commits clean, use topic branches for isolated work, update from the main repository before submitting, and follow the project's contribution workflow.
