---
page-title: "How to Revert a Commit in Git (PowerShell Git Tutorial)"
url: https://www.varonis.com/blog/revert-a-commit-in-git
date: "2023-12-22 08:58:45"
---
Whether you [write scripts](https://www.varonis.com/blog/how-to-get-started-with-powershell-and-active-directory-scripting/?hsLang=en) in isolation or work with a team, the ability to track versions of code is essential. You may add code that ends up not working out, and the ability to reverse these changes (without manually deleting code) can save your project. In this post, I will cover how to use a  `Git` `reset` command to revert to a previous commit of your code in the Git source control system, as well as the following topics:

### Discover your weak points and strengthen your resilience: Run a Free Ransomware Readiness Test

-   [How to Use Git](https://www.varonis.com/blog/revert-a-commit-in-git#howto)
-   [What Is Git and What Are Git Commits](https://www.varonis.com/blog/revert-a-commit-in-git#definition)
-   [Configuring a Local Git Repository](https://www.varonis.com/blog/revert-a-commit-in-git#configuration)
-   [Tracking and Committing Files in Git](https://www.varonis.com/blog/revert-a-commit-in-git#tracking)
-   [Committing Additional Changes in Git](https://www.varonis.com/blog/revert-a-commit-in-git#additions)
-   [Managing Git Commits](https://www.varonis.com/blog/revert-a-commit-in-git#management)
-   [Git Command Glossary](https://www.varonis.com/blog/revert-a-commit-in-git#glossary)

## Prerequisites: How To Use Git

You will need the Git client installed on your system. You can download the client [here](https://git-scm.com/downloads), and an installation guide is available [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git). The Git client allows running Git commands from the terminal. You will also need a file to modify and to track changes. In this post, I am using a [PowerShell](https://www.varonis.com/blog/powershell-tool-roundup/?hsLang=en) script, but you can use anything you like.

## What Is Git and What Are Git Commits

×

![an overview of the meanings behind Git and Git commits](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/Git-And-Git-Commits.png?width=1240&height=756&name=Git-And-Git-Commits.png)

Git is a common source control tool that keeps track of changes using commits. Creating a commit is like saving a version of a file or group of files. The commit [keeps track of the file versions](https://www.varonis.com/blog/secure-file-sharing/?hsLang=en) by associating a unique ID (or SHA or hash) with the commit. This unique ID allows for reverting to previously committed versions of files in the repository.

In a typical workflow, you would:

1.  1.  Pull files from the remote repository.
    2.  Make changes to the local files.
    3.  Commit the changes.
    4.  Push the new files up to the repository.

However, if you don’t have a centralized remote repository or pushing/pulling/merging code makes you nervous, you can still take advantage of Git by using it on your local system. You can commit changes to your code and revert those changes to familiarize yourself with commits.

## 1\. Configuring a Local Git Repository

The first command to start with is  `Git init`. This command initializes the current folder as a Git repository. In this example, I am initializing the project folder a Git repository.

1.  Git init

[![a screenshot of a Git init command in PowerShell](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/gitInit.png?width=777&height=60&name=gitInit.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/gitInit.png?hsLang=en)

The command adds a hidden folder named “.Git”, which keeps track of the current active branch, config files, aliases, and other [data](https://www.varonis.com/products/data-classification-engine/?hsLang=en).

[![a screenshot of a folder created by the Git init command](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/gitinitfolder.png?width=535&height=144&name=gitinitfolder.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/gitinitfolder.png?hsLang=en)

Next, I need a file to work with to track changes. I have a **[PowerShell script](https://www.varonis.com/blog/windows-powershell-tutorials/?hsLang=en)** file named “myScript.ps1”. The script contains a for loop that iterates five times and outputs to the screen. I’ll refer to this first loop as my outer loop. What the code is doing is not important, but I wanted to show code modifications for a simple script.

[![a screenshot of a PowerShell script file ](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/script1.png?width=717&height=366&name=script1.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/script1.png?hsLang=en)

The next step is to view the status of the repository by running  `Git status`. The status will show which branch I am on (for now, just know I am on the “master” branch). It will also show any new or changes files since the last commit by displaying them in red.

[![a screenshot of how to run running Git status](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/gitStatusUntracked.png?width=1070&height=328&name=gitStatusUntracked.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/gitStatusUntracked.png?hsLang=en)

## 2\. Tracking and Committing Files in Git

If I want to track files to commit their changes, I need to add them to the staging area using the  `Git add` command. The Git add command can specify one or multiple files to add to the staging area. In my case, I only have one file, so I add it by specifying the file name. I then check the repository status to view the script in the staging area.

1.  Git add myScript.ps1
2.  Git status

[![a screenshot of how to use the Git add command in PowerShell](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/gitAdd.png?width=650&height=299&name=gitAdd.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/gitAdd.png?hsLang=en)

Now that I am tracking the file in the staging area, I need to create a commit of the state of the repository. I use the  `Git commit`  command with the `-m` parameter to assign a message to the commit. The commit message should be short but descriptive to indicate what changes I made to the code. Once I complete the commit, I run another `Git status` to see that no other files are in the staging area or have been modified since the last commit.

1.  Git commit -m “first version of script - outer loop only”
2.  Git status

[![](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/gitCommit-1.png?width=685&height=165&name=gitCommit-1.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/gitCommit-1.png?hsLang=en)

## 3\. Committing Additional Changes

Now that I have my first commit message in my repository, I need to add an enhancement to my code. I add another for loop within the outer loop, which I’ll refer to add the inner loop.

[![a screenshot of how to track and commit files in Git using PowerShell](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/scriptAddedCode-1.png?width=624&height=437&name=scriptAddedCode-1.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/scriptAddedCode-1.png?hsLang=en)

If I run  `Git status` again, I’ll see the same results as I did earlier. It will show the file as being untracked as the script file has changed since the last commit. I will repeat the workflow of commands to add the file and commit it. My commit message will show I added the inner loop.

1.  Git status
2.  Git add myScript.ps1
3.  Git commit -m “Added inner loop”

[![a screenshot of a Git commit message](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/gitSecondWorkflow.png?width=1062&height=390&name=gitSecondWorkflow.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/gitSecondWorkflow.png?hsLang=en)

## 4\. Managing Git Commits

Now that I have a few commits in the repository, I can turn to the  `Git log` command. This command will show the previous commits along with commit messages. Each commit has a unique hash value to identify it. In this example, the latest commit is where I added the inner loop and is indicated by the HEAD pointer.

[![a screenshot of how to manage Git commits in PowerShell](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/gitLog-1.png?width=618&height=252&name=gitLog-1.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/gitLog-1.png?hsLang=en)

Now let’s say I don’t want my last change and want to revert to an earlier version of the script. I could manually delete the inner loop as this script is small enough to do that. However, larger coding projects could pose a problem. I might end up removing too much or not enough code and introduce new problems.

Instead, I can use the first seven characters of the commit log hash value to a previous version of the repository. To perform this reversion, I use the `Git reset` command while referencing the commit log hash:

1.  Git reset a6dd1c2

[![a screenshot of how to use the Git reset command in PowerShell](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/gitReset.png?width=513&height=91&name=gitReset.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/gitReset.png?hsLang=en)

This command resets HEAD to a specific commit. The screenshot shows that `myScript.ps1` is back to the staging area with the changes since the *`a6dd1c2`* commit. If I run `Git log` again, HEAD is now back to the previous commit, and the commit for adding the inner loop is removed.

[![a screenshot of how to use Git to revert to a previous commit](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/gitLogRevised.png?width=900&height=178&name=gitLogRevised.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/gitLogRevised.png?hsLang=en)

To switch back to the file, I need to check out the file from the commit using  `Git checkout`. Once I check out the file, I can view the file contents, which reveals just the outer loop is present. I then run Git status to show that the current tree does not have any changes to track.

[![a screenshot of how to check out a file from a commit using Git checkout](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/gitcheckout-1.png?width=957&height=105&name=gitcheckout-1.png)](https://info.varonis.com/hubfs/Imported_Blog_Media/gitcheckout-1.png?hsLang=en)

## Git Command Glossary

Here is a summary of each PowerShell Git command I used and its purpose:

×

![a glossary of common PowerShell Git commands](https://info.varonis.com/hs-fs/hubfs/Imported_Blog_Media/PowerShell-Git-Commands.png?width=1240&height=949&name=PowerShell-Git-Commands.png)

If you’re new to version control but don’t have the confidence to work with remote repositories, you can still work with a local repository and have the same benefits. You can use these fundamental Git commands to familiarize yourself with the process of how to use Git for version control.

### What you should do now

Below are three ways we can help you begin your journey to reducing data risk at your company:

1.  [Schedule a demo session with us](https://info.varonis.com/en/demo-request?hsLang=en), where we can show you around, answer your questions, and help you see if Varonis is right for you.
2.  [Download our free report](https://info.varonis.com/en/great-saas-data-exposure-report?hsLang=en) and learn the risks associated with SaaS data exposure.
3.  Share this blog post with someone you know who'd enjoy reading it. Share it with them via [email,](mailto:?subject=How%20to%20Revert%20a%20Commit%20in%20Git%20(PowerShell%20Git%20Tutorial)&body=I%20think%20you%20might%20find%20this%20interesting%3A%20https%3A%2F%2Fwww.varonis.com%2Fblog%2Frevert-a-commit-in-git) [LinkedIn,](https://www.linkedin.com/shareArticle?mini=true&url=https%3A%2F%2Fwww.varonis.com%2Fblog%2Frevert-a-commit-in-git&title=How%20to%20Revert%20a%20Commit%20in%20Git%20(PowerShell%20Git%20Tutorial)) [Reddit,](http://www.reddit.com/submit?url=https%3A%2F%2Fwww.varonis.com%2Fblog%2Frevert-a-commit-in-git&title=How%20to%20Revert%20a%20Commit%20in%20Git%20(PowerShell%20Git%20Tutorial)) or [Facebook.](https://www.facebook.com/sharer/sharer.php?u=https%3A%2F%2Fwww.varonis.com%2Fblog%2Frevert-a-commit-in-git)

×

![Jeff Brown](https://info.varonis.com/hubfs/jeff-brown-web-150x150.jpg)

##### Jeff Brown

Jeff Brown is a cloud engineer specializing in Microsoft technologies such as Office 365, Teams, Azure and PowerShell. You can find more of his content at https://jeffbrown.tech.