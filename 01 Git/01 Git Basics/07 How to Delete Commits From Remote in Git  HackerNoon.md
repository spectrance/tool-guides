---
page-title: "How to Delete Commits From Remote in Git | HackerNoon"
url: https://hackernoon.com/how-to-delete-commits-from-remote-in-git
date: "2024-01-16 20:47:57"
---
Manipulating history is very common for developers who work with Git regularly. Indeed, developers often need to remove commits from the Git history. Luckily, Git provides many commands to make this operation possible.

Let’s get to it 😎.

## Step 0 - Preparation

Before manipulating the Git history, ensure that your working directory is clean of any changes using the [git status](https://timmousk.com/blog/git-status/?ref=hackernoon.com) command.

## Step 1 - Delete commits locally

To delete commits from a remote server, first, you will need to remove them from your local history.

### 1.1 For consecutive commits from the top

If the commits you want to remove are placed at the top of your commit history, use the `git reset --hard` command with the `HEAD` object and the number of commits you want to remove.

```
git reset --hard HEAD~1
```

This command will remove the **latest commit**.

```
git reset --hard HEAD~3
```

This command will remove the **latest three commits**.

You can also remove up to a specific commit using a commit’s hash, like so:

```
git reset --hard <hash>
```

### 1.2 For non-consecutive commits

![[_resources/How to Delete Commits From Remote in Git  HackerNoon/7c0468a65b11fa22737726364a0ece63_MD5.gif]]

If, however you want to remove non-consecutive commits, you’ll need to use an interactive rebase.

-   \[ \]Find the last commit hash containing all of the commits you want to remove using the `git reflog` command.
-   \[ \]Start an interactive rebase with `git rebase -i <hash>`.
-   \[ \]In the edit screen, find the commit lines you want to remove and remove them.
-   \[ \]Save and exit (you may need to resolve the conflicts)
-   \[ \]End the interactive rebase with `git rebase --continue` or start over by [aborting the rebase](https://timmousk.com/blog/git-rebase-abort/?ref=hackernoon.com).

## Step 2 - Delete the commits from remote

To delete commits from remote, you will need to push your local changes to the remote using the [git push](https://timmousk.com/blog/git-push/?ref=hackernoon.com) command.

```
git push origin HEAD --force
```

Since your local history diverges from the remote history, you need to use the `force` option.

## Final thoughts

As you can see, Git makes it easy to delete commits from a remote server.

However, you need to be careful when using the `git push` command with the `force` option because you could lose progress if you are not cautious.

![[_resources/How to Delete Commits From Remote in Git  HackerNoon/7c0468a65b11fa22737726364a0ece63_MD5.gif]]

Thank you for reading!