# Git Branching - Branching Workflows

## Branching Workflows

Git branching workflows help organize development using **stable branches, development branches, and short-lived topic branches**.

### Long-Running Branches

Long-running branches stay active for different **stages of stability**.

Typical workflow:

    topic branches → develop/next → master

- `master` → stable/release-ready code
- `develop` / `next` → development and testing
- `proposed` / `pu` → experimental or not-yet-ready changes

Branches can act as **work silos**. Once changes are fully tested, they can be merged into a more stable branch.

> Multiple long-running branches are optional but can be useful for large or complex projects.

### Topic Branches

A topic branch is a **short-lived branch** created for a specific feature, bug, or related work.

Typical workflow:

    Create → Work → Test → Merge → Delete

Example:

    master
     ├── iss91
     │    └── iss91v2
     │
     └── dumbidea

You can experiment with different solutions independently and merge only the changes you decide to keep.

Topic branches are useful because they:

- Isolate specific work
- Make code review easier
- Allow quick context switching
- Keep unrelated changes separate
- Can be created and deleted frequently

### Important

Branches are **completely local**.

Creating, committing, merging, and deleting branches happens inside your local Git repository. These operations **do not communicate with the remote server**.

## Quick Cheatsheet

| Branch | Purpose |
|---|---|
| `master` | Stable/release-ready code |
| `develop` / `next` | Development & testing |
| `proposed` / `pu` | Experimental changes |
| Topic branch | Feature/bug-specific work |

| Workflow | Purpose |
|---|---|
| Long-running branches | Manage stability levels |
| Topic branches | Isolate specific work |
| Create → Work → Merge → Delete | Common feature workflow |

> **Remember:** Long-running branches manage **stability levels**, while topic branches isolate **specific pieces of work**.
