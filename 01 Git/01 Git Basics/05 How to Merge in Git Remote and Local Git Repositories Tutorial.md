---
page-title: "How to Merge in Git: Remote and Local Git Repositories Tutorial"
url: https://www.varonis.com/blog/how-to-merge-in-git
date: "2023-12-22 09:03:05"
---
In my previous article “[How to Revert a Commit in Git](https://www.varonis.com/blog/revert-a-commit-in-git/?hsLang=en)” (a PowerShell Git tutorial), I showed how you can use a local PowerShell Git repository and utilize the benefits of local source control. Using Git, you can create commits or snapshots of your code and revert to previous versions. Typically when working with Git and code repositories, you create the remote one first, then download it to your local system.

However, if you start a project on your local system first and need to then connect to a remote repository, you will need a way to merge the repositories. In this post, I will show how to merge in Git, meaning how you can take a local Git repository and merge it into a remote repository in your GitHub account.

### Get a Free Data Risk Assessment

To follow along with this [PowerShell Git](https://www.varonis.com/blog/how-to-get-started-with-powershell-and-active-directory-scripting/?hsLang=en) tutorial on how to merge in Git, you will need:

-   The PowerShell Git client installed on your system ([download](https://git-scm.com/downloads) and [installation guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git))
-   [A free GitHub account](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/signing-up-for-github)
-   [Connect to GitHub with SSH](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/connecting-to-github-with-ssh)
-   Project files

## 1\. Create the Local GitRepository

First, you will need to create a local repository for your project. I will be [using PowerShell for this tutorial](https://www.varonis.com/blog/powershell-tool-roundup/?hsLang=en), but you can use any other terminal available to you. However, you will need to use equivalent commands for creating folders and navigating the directory structure so that you understand how to merge in Git.

Start by creating a folder for storing your project files, followed by changing the console to that directory. You then initialize the folder as a Git repository using the git init command.

1.  New-Item my\_project -ItemType Directory
2.  Set-Location .\\my\_project\\
3.  git init

[![](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/Configuring-Local-Git-Repository.png?width=1092&height=443&name=Configuring-Local-Git-Repository.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/Configuring-Local-Git-Repository.png?hsLang=en)

### 2\. Create the First Git Commit

Once you have created the local Git repository, you need to add some files to the project. I will create a PowerShell script that outputs “Hello World!” to the console and then verify the script’s output.

1.  New-Item -Name HelloWorld.ps1 -ItemType File
2.  Add-Content -Value ‘“Hello World!”’ -Path .\\HelloWorld.ps1
3.  .\\HelloWorld.ps1

[![a screenshot of how to create a Powershell script ahead of merging in Git](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/Creating-a-PowerShell-script-for-the-project.png?width=1385&height=443&name=Creating-a-PowerShell-script-for-the-project.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/Creating-a-PowerShell-script-for-the-project.png?hsLang=en)

The repository has an untracked file to use to create the first commit. You can view untracked files by running the git status command. You can add the file to the staging area using the git add command and specifying the file name. Next, create a commit using the git commit with the –*m* switch to add a message to the commit.

1.  git status
2.  git add .\\HelloWorld.ps1
3.  git commit -m “<commit message>”

[![a screenshot of creating an initial Git commit before merging in Git](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/Creating-the-first-commit.png?width=1374&height=551&name=Creating-the-first-commit.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/Creating-the-first-commit.png?hsLang=en)

## 3\. Create the GitHub Repository

While working with a local Git repository is helpful, source control’s primary purpose is to collaborate on projects with other people. Now you need to take the local Git repository and put it into a remote, centrally-located repository so others can collaborate on the project. By storing the project code into a central, remote repository, other collaborators can copy the code to their system for modification.

There are many ways to have a central Git repository, but an easy option is storing it in GitHub. GitHub is a popular implementation of Git that has a free tier for hosting repositories.

On your GitHub profile page, select **Repositories** at the top, then click **New**.

[![a screenshot of how to create a new GitHub repository in Powershell](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/create-a-new-GitHub-repository.png?width=808&height=179&name=create-a-new-GitHub-repository.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/create-a-new-GitHub-repository.png?hsLang=en)

In the **Create a new repository screen**, enter a unique repository name that doesn’t exist in your account. I recommend giving it the same name as the project on your local system, in this case, my\_project. Follow this by entering a description of the project, whether the project is Public or Private, and choose any of the options to initialize additional project files. Since you are importing an existing repository, you should not need to select any of the additional files as they should exist in the local repository (if you create them). Once you configured all the settings, select **Create repository**.

[![a screenshot o show to configuring repository options in Git ahead of merging in Git](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/configuring-respository-options.png?width=929&height=602&name=configuring-respository-options.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/configuring-respository-options.png?hsLang=en)

## 4\. Push Existing Local Git Repository

Once created, GitHub presents several options for getting started with the new Git repository. You can copy it to your local system, create a new repository on your system and link to it, or import code from another repository.

In our case, we want to push an existing Git repository from the command line. We already have a local Git repository that we want to link with our new remote GitHub repository and push our code into it. Select the copy icon to save this code snippet to run back in our PowerShell terminal.

[![a screenshot of how to copy a code snippet for pushing existing Git repository](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/copy-code-snippet-for-pushing-existing-repository.png?width=1162&height=771&name=copy-code-snippet-for-pushing-existing-repository.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/copy-code-snippet-for-pushing-existing-repository.png?hsLang=en)

Before I run the code in my PowerShell terminal, let’s understand the purpose of each command — each of which is essential to understanding how to merge in Git.

### Git Remote Add Origin

1.  git remote add origin https://github.com/JeffBrownTech/my\_project.git

This command will configure the new GitHub repository as the remote repository and make it the source moving forward. As other collaborators make changes to the repository hosted in GitHub, you can then pull those updates down to your local system. You can verify the changed setting by running *git remote -v* to verify the origin’s URL matches the remote repository.

1.  git remote -v

[![a screenshot of how to add a remote URL ahead of merging in Git](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/Adding-the-remote-URL.png?width=1579&height=188&name=Adding-the-remote-URL.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/Adding-the-remote-URL.png?hsLang=en)

The “origin” name here can be anything you want; however, the industry standard is to call the repository’s remote connection “origin.”

### Git Branch

1.  git branch -M main

This command will force rename the local branch to main to ensure it matches the GitHub repository’s main branch name. This step may not be necessary, but it is good to run it to verify the branch names match.

Finally, we need to push our local repository to the remote GitHub repository using the *git push* command.

### Git Push

1.  git push -u origin main

Here, *origin* refers to the remote repository we configured earlier, and *main* refers to the branch from the local repository to copy to the remote repository.

Since this is the first time we are pushing code into the remote GitHub repository for the main branch, we need to specify the -u parameter, which is an alias for —*set-upstream*. Setting the upstream branch will configure the default remote branch for the current local branch. We can see this relationship configured in the output of the push command.

[![a screenshot of how to push a local Git repository into GitHub](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/pushing-local-repository-into-GitHub.png?width=896&height=450&name=pushing-local-repository-into-GitHub.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/pushing-local-repository-into-GitHub.png?hsLang=en)

## 5\. View Updated GitHub Repository

Back in GitHub, refresh the repository’s page currently display the code examples, and you should see your local files now available in the repository. For my project, I can see the HelloWorld.ps1 script with my commit message.

[![a screenshot of a GitHub repository updated with local project files](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/GitHub-repository-updated-with-local-project-files.png?width=1302&height=441&name=GitHub-repository-updated-with-local-project-files.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/GitHub-repository-updated-with-local-project-files.png?hsLang=en)

When creating the GitHub repository, there is an option to initialize the repository with several files, like a README.md file. This file is written in markdown and displays its content in the repository page. It is often used to explain the project or provide documentation on how to use it.

Since I was going to import an existing repository from my local system, there was no need to initialize the repository with this file. However, let’s examine a scenario where I create the remote repository with files and need to sync it with my local repository.

Back in GitHub, I’ve created a new repository named *my\_project\_2* for storing my second PowerShell project. I checked the box to include a README.md file during the repository configuration. Here’s is what this new project repository looks like (note the contents of the README file displayed):

[![a screenshot of a GitHub repository initialized with a README file](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/GitHub-repository-initialized-with-a-README-file.png?width=768&height=608&name=GitHub-repository-initialized-with-a-README-file.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/GitHub-repository-initialized-with-a-README-file.png?hsLang=en)

Before switching back to my terminal, I need the URL for this repository so I can add it as my origin in my local repository. You can find this by selecting the **Code** button and copying the HTTPS URL.

[![a screenshot of a copy of a GitHub repository URL as part of a tutorial on how to merge in Git](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/copy-the-GitHub-repository-URL.png?width=526&height=444&name=copy-the-GitHub-repository-URL.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/copy-the-GitHub-repository-URL.png?hsLang=en)

Now let’s switch back to my PowerShell window where I have already created the local repository and made the first commit. First, I need to add the URL I just copied as the source repository named origin:

1.  git remote add origin https://github.com/JeffBrownTech/my\_project\_2.git
2.  git remote -v

Next, I want to pull down the contents of the GitHub remote repository to my local system, which is just the README.md file. I can accomplish using the git pull command and specifying the origin remote repository and the local main branch:

1.  git pull origin main

However, this command will result in a fatal error:

*Fatal: refusing to merge unrelated histories*

[![a screenshot of a fatal unrelated histories message in Git as part of a tutorial on how to merge in Git](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/fatal-unrelated-histories-message.png?width=830&height=288&name=fatal-unrelated-histories-message.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/fatal-unrelated-histories-message.png?hsLang=en)

Since we have two unrelated projects with different histories, Git is refusing to merge the two. Each project has its own set of commit histories that are not compatible with each other. Luckily, we can force Git to merge the two despite the unrelated histories with the —*allow-unrelated-histories* parameter, like this:

1.  git pull origin main --allow-unrelated-histories

Now the README.md file from the remote GitHub repository is available in my local project. From here, I can make modifications to the README.nd file locally, commit the changes, and push them back to GitHub.

[![a screenshot of how to merge unrelated projects in Git as part of a Powershell tutorial](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/Merging-unrelated-projects.png?width=1179&height=583&name=Merging-unrelated-projects.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/Merging-unrelated-projects.png?hsLang=en)

In this post, I covered how to merge in Git by taking a local code repository and connecting it to a remote GitHub repository. By putting your code in a remote-hosted repository, other people can collaborate with you by pushing their changes to the project code. Working with Git and repositories is an essential skill for any developer or administrator who needs to collaborate on or share a coding project.

×

![Jeff Brown](https://info.varonis.com/hubfs/jeff-brown-web-150x150.jpg)

##### Jeff Brown

Jeff Brown is a cloud engineer specializing in Microsoft technologies such as Office 365, Teams, Azure and PowerShell. You can find more of his content at https://jeffbrown.tech.