---
page-title: "Basic Git Commands | Atlassian Git Tutorial"
url: https://www.atlassian.com/git/glossary#commands
date: "2024-01-17 15:24:30"
---
## Commands

### Git clean

Removes untracked files from the working directory. This is the logical counterpart to git reset, which (typically) only operates on tracked files.

#### Related tutorials

[Undoing changes: git clean](https://www.atlassian.com/git/tutorials/undoing-changes/git-clean)

### git commit --amend

Passing the --amend flag to git commit lets you amend the most recent commit. This is very useful when you forget to stage a file or omit important information from the commit message.

#### Related tutorials

[Rewriting history: git commit --amend](https://www.atlassian.com/git/tutorials/rewriting-history)

### git fetch

Fetching downloads a branch from another repository, along with all of its associated commits and files. But, it doesn't try to integrate anything into your local repository. This gives you a chance to inspect changes before merging them with your project.

#### Related tutorials

[Syncing: git fetch](https://www.atlassian.com/git/tutorials/syncing/git-fetch)

[Refs and the reflog: Refspecs](https://www.atlassian.com/git/tutorials/refs-and-the-reflog#refspecs)

[Syncing: git pull](https://www.atlassian.com/git/tutorials/syncing/git-pull)

### git init

Initializes a new Git repository. If you want to place a project under revision control, this is the first command you need to learn.

#### Related tutorials

[Setting up a repository: git init](https://www.atlassian.com/git/tutorials/setting-up-a-repository/git-init)

### git rebase -i

The -i flag is used to begin an interactive rebasing session. This provides all the benefits of a normal rebase, but gives you the opportunity to add, edit, or delete commits along the way.

#### Related tutorials

[Rewriting history: git rebase -i](https://www.atlassian.com/git/tutorials/rewriting-history#git-rebase-i)

### git reflog

Git keeps track of updates to the tip of branches using a mechanism called reflog. This allows you to go back to changesets even though they are not referenced by any branch or tag.

#### Related tutorials

[Rewriting history: git reflog](https://www.atlassian.com/git/tutorials/rewriting-history/git-reflog)

### git remote

A convenient tool for administering remote connections. Instead of passing the full URL to the fetch, pull, and push commands, it lets you use a more meaningful shortcut.

#### Related tutorials

[Syncing: git remote](https://www.atlassian.com/git/tutorials/syncing)

### Centralized workflow

If your developers are already comfortable with Subversion, the Centralized Workflow lets you experience the benefits of Git without having to adapt to an entirely new process. It also serves as a friendly transition into more Git-oriented workflows.

#### Related tutorials

[Comparing workflows: Feature branch workflow](https://www.atlassian.com/git/tutorials/comparing-workflows#feature-branch-workflow)

### Forking

Instead of using a single server-side repository to act as the “central” codebase, forking gives every developer a server-side repository. This means that each contributor has not one, but two Git repositories: a private local one and a public server-side one.

#### Related tutorials

[Comparing workflows: Forking workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/forking-workflow)

[Making a pull request: How it works](https://www.atlassian.com/git/tutorials/making-a-pull-request#how-it-works)

### Main

The default development branch. Whenever you create a git repository, a branch named "main" is created, and becomes the active branch.

#### Related tutorials

[Comparing workflows: Gitflow workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)

[Comparing workflows: Feature branch workflow](https://www.atlassian.com/git/tutorials/comparing-workflows#feature-branch-workflow)

[Git stash](https://www.atlassian.com/git/tutorials/saving-changes/git-stash)

[Learn Git with Bitbucket Cloud: Use a Git branch to merge a file](https://www.atlassian.com/git/tutorials/learn-git-with-bitbucket-cloud#git-branch-to-merge)

### Working tree

The tree of actual checked out files, normally containing the contents of the HEAD commit's tree and any local changes you've made but haven't yet committed.

#### Related tutorials

[Git stash](https://www.atlassian.com/git/tutorials/saving-changes/git-stash)