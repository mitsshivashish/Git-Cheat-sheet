# Distributed Git - Distributed Workflows

## Distributed Workflows

Git is a **distributed VCS**, so every developer can contribute to and maintain repositories.

## 1. Centralized Workflow

One central repository acts as the main hub.

    Developer A ──┐
    Developer B ──┼──> Central Repository
    Developer C ──┘

Typical workflow:

    git pull
    # make changes
    git add .
    git commit -m "message"
    git push

If another developer pushes first, your push may be rejected. Fetch/merge their changes before pushing.

**Best for:** teams using a simple central-repository model.

## 2. Integration-Manager Workflow

Each contributor has their own public repository/fork.

    Contributor → Own Repository → Maintainer → Main Repository

Workflow:

1. Maintainer publishes the main repository.
2. Contributor clones/forks it.
3. Contributor makes changes.
4. Contributor pushes to their repository.
5. Contributor asks the maintainer to pull the changes.
6. Maintainer fetches and merges the changes.
7. Maintainer pushes them to the main repository.

**Best for:** GitHub/GitLab-style contribution workflows.

## 3. Dictator & Lieutenants Workflow

Used for very large or hierarchical projects.

    Developers
        ↓
    Lieutenants
        ↓
    Benevolent Dictator
        ↓
    Reference Repository

Workflow:

1. Developers work on topic branches and rebase onto `master`.
2. Lieutenants merge developers' work.
3. Dictator merges the lieutenants' `master` branches.
4. Dictator pushes the final `master` to the reference repository.

**Best for:** large projects with many contributors and multiple integration levels.

## Quick Comparison

| Workflow | Structure | Best For |
|---|---|---|
| Centralized | One main repository | Simple team collaboration |
| Integration Manager | Forks + maintainer | Open-source style projects |
| Dictator & Lieutenants | Multiple integration levels | Very large projects |

> **Remember:** Git's distributed model lets teams choose or combine workflows based on project size, collaboration style, and level of control.
