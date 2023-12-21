---
jupyter:
  jupytext:
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.16.0
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
---

<!-- #region jp-MarkdownHeadingCollapsed=true -->
# Resolving Initial Conflict

The typical initial workflow involves creating a local git repository and a corresponding repo on git hub. We create the initial project files in the local repo and then push to the remote repo. But sometimes the remote repo might have created components that get defined during the creation of the repo, for eg Readme.md. When we try to push our local repo to the remote repo in such a situation git will throw an error.

```python

# Access project directory
cd ~/path/to/dir

# Initiat a git repository in project directory
git init

# Implement Feature
# Create .gitignore and filter Jupyter Notebooks and Pdfs
touch .gitignore
echo "# Files to Ignore for Git Version Control" >> .gitignore
echo "*.ipynb" >> .gitignore
echo "*.pdf" >> .gitignore

# Stage new files
git add .

# Commit to Local Repo
git commit -m "Added Git-Ignore File"

# Add Remote ie Origin to Local Repo 
git remote add origin "https://www.example.com/user/repo.git"

# Verify Remote Locations
git remote -v

# Rename default 'master' branch to 'main' to comply with github conventions
git branch -M main

# Finally Push changes to Remote Repo
git push -u origin main


```

We will encounter the following error:

```bash
error: failed to push some refs to 'https://www.example.com/user/repo.git'
```

This happens because our Remote Repo contains Work which the Local Repo does not have. This might happen when Another Repo has Pushed to the Remote Repo. To Resolve this Conflict Git suggets that we perform a 'Pull' on the 'main' branch of our Local Repo to Integrate with Changes on the 'Origin' (Remote Repo).

```bash
git pull origin main
```

But this will also return another error:

```bash
hint: You have divergent branches and need to specify how to reconcile them.
```

To Resolve this we have to execute one of the following commands based on our selected strategy: 

```bash
git config pull.rebase false  # merge (the default strategy)
git config pull.rebase true   # rebase
git config pull.ff only       # fast-forward only
 
# We can replace "git config" with "git config --global" to set a default preference for all repositories.
```

Right now we want to simply 'Merge' the changes in our case so we choose the first option

Performing the 'Pull' action once again now gives use a **New** error :)

```bash
fatal: refusing to merge unrelated histories
```

Finally we perform the 'Pull' using the '--allow-unrelated-histories' parameter to Force Git to Merge

```bash
git pull origin main --allow-unrelated-histories
```

This will open an editable Template in our default terminal text editor for us to input the 'Merge' commit message. Once we save this commit message both our Local and Remote Repos will be in Sync.

Now performing a Git Status will display the following:
```bash
git status

On branch main
nothing to commit, working tree clean

```

We can now 'Push' from our Local Repo to the Remote Repo

```bash
git push -u origin main
```

We can now verify that both our Local and Remote Repos are in Sync and we have pulled new changes from the Remote Repo to our Local Repo and pushed our local changes to the Remote Repo.
<!-- #endregion -->
