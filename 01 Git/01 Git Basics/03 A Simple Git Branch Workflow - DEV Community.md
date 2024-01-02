---
page-title: "A Simple Git Branch Workflow - DEV Community"
url: https://dev.to/levi/a-simple-git-branch-workflow-24hh
date: "2023-12-23 12:52:42"
---
## [](https://dev.to/levi/a-simple-git-branch-workflow-24hh#why)Why?

Git is the preeminent tool for version control–that is, keeping track of and managing changes. This post is about implementing a simple but powerful workflow for managing and tracking the changes of a project as it grows and matures. A branching workflow allows us to carefully make and track changes to our project without risking the integrity of its core.

Version control gives us a better handle on the animal of our code base. Every project warrants a repository, an observed and organized container for code. If you're serious about grooming a project that lasts, you owe it to yourself to use Git. For the purposes of this illustration, we'll use Github as the example of an online host for Git.

## [](https://dev.to/levi/a-simple-git-branch-workflow-24hh#how)How

### [](https://dev.to/levi/a-simple-git-branch-workflow-24hh#getting-started)Getting Started

New projects must be started either locally or with a new repository on Github. This new repository may be either initialized with files or linked with an existing local directory. Mind the checkbox labelled "Initialize with a README" when creating a new repository (here on out referred to as a **repo**).

[![Mind this checkbox](https://res.cloudinary.com/practicaldev/image/fetch/s---mawpLv2--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/yqaw3s7k8qjf968vq0lk.png)](https://res.cloudinary.com/practicaldev/image/fetch/s---mawpLv2--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/yqaw3s7k8qjf968vq0lk.png)

If you have already started a project on your computer you will be "importing an existing repository," so take Github's advice and do *not* check this box. Checking the box will make it more complicated to link your local directory with the remote repo. Instead, "push \[this\] existing repository on the command line" by opening a terminal window, moving into the project's directory, and executing the following three lines:  

```
$ git init
$ git remote add origin git@github.com:USERNAME/REPO-NAME.git
$ git push -u origin master
```

`git init` initializes the local directory as a new, empty git repo (`$` denotes that we're executing this command in the terminal). This command generates an invisible `.git` file and endows the directory space with all the powers that Git affords. `git remote add` adds a remote (i.e. server) of the name `origin` at the address `git@github.com:USERNAME/REPO-NAME.git`. This command links the local repository to a server that will also host the repository. `git push -u origin master` pushes, or uploads, the contents in the master branch of the directory to the origin server. `-u` sets this remote repository as the default upstream reference, meaning `origin` will be the default remote repository from which things are pulled and to which things are pushed.

If you're starting your project from scratch and have no local work, feel free to check the box and have the resulting generated README.md serve as your first project file!

Below is an illustration of the state of our project. The shapes with dashed borders represent the project on the remote repository, while the solid-bordered shapes represent the local project. Each circle is a commit. A huge thanks to the [Learn Git Branching Applet](https://learngitbranching.js.org/) for providing a means of simulating and visualizing Git workflows. We'll use these diagrams to grasp what we're doing.

[![Local synced with remote, two commits](https://res.cloudinary.com/practicaldev/image/fetch/s--gCg1wXKP--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/qgkytb8guots0ogsia6q.png)](https://res.cloudinary.com/practicaldev/image/fetch/s--gCg1wXKP--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/qgkytb8guots0ogsia6q.png)

In the image above, our local repo is synced with the remote repo–both have two commits. The boxes pointing at the commits point to the where (or, more accurately, when) in the project a branch is. Here, the master branch is at the latest commit, C2. The **head** is denoted by the asterisk (\*) indicates where in a project's history we are working. Most often, the head points to the latest checkpoint, like a tape recorder *head* might rest on the freshest spot of tape, or a record player needle might point to the most recent song.

### [](https://dev.to/levi/a-simple-git-branch-workflow-24hh#saving-progress)Saving Progress

In plain English, let's talk about the meat and and potatoes of a Git workflow: staging, committing, and pushing. These actions are essential to saving changes to your work. You should do them every time you make a substantial change.

To **stage**, we execute `git add` in our project's directory. Innocuous enough! `git add .` and `git add FILE.js` will **stage** *all* files in the directory or *only* the `FILE.js` file, respectively. By **stage**, we mean *tell Git we want to track the changes made to these files*.

To **commit**, we execute `git commit -m "COMMIT MESSAGE` to record the changes made to staged files in our project's git history. Committing is roughly the same thing as saving, though the only thing we're saving is the *changes* to the files, not the files themselves. See [How to Write Useful Commit Messages](https://dev.to/jacobherrington/how-to-write-useful-commit-messages-my-commit-message-template-20n9) for advice on how to do just that. The following illustration shows the state of our project after the previous two commands. Our local project repo is ahead of the remote by one commit!

[![New local commit](https://res.cloudinary.com/practicaldev/image/fetch/s--F0w6MI10--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/5xbbvgkvxou5336d29c8.png)](https://res.cloudinary.com/practicaldev/image/fetch/s--F0w6MI10--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/5xbbvgkvxou5336d29c8.png)

To **push**, we execute `git push`. By default, this command will upload our code in its current branch to a server (known as the *remote* in Git parlance and named `origin` by default). We can specify which branch to push by passing it in as an option like so : `git push REMOTE_NAME BRANCH_NAME`.

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s---GX4i_mQ--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/rd0o2oq2s3tczod8vfwb.png)](https://res.cloudinary.com/practicaldev/image/fetch/s---GX4i_mQ--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/rd0o2oq2s3tczod8vfwb.png)

Now our local and remote repos are in sync! With `add`, `commit`, and `push` at our disposal, we're equipped to track changes to our project. Lugging this verbiage around begs the question, *"When will we ever need this?"* Commit *every* substantial change to your work. Commit! Set up your sessions controller? Implementing authorization and just amended your user model? Commit! Fix a bug? Commit!

Stage and commit every little milestone of your work. When you finish a work session, or as needed, push these changes so they're accessible to others. In short (and for example):

1.  `git add .`
2.  `git commit -m "Refactor custom Account model methods"`
3.  `git push`

### [](https://dev.to/levi/a-simple-git-branch-workflow-24hh#damage-control-with-branches)Damage Control with Branches

Many are tempted to work exclusively in the `master` branch. This behavior would be akin to me writing this blog post in pen longhand, while sitting at a rolling desk on a rocking boat yelling, "I make no mistakes!" Consider the `master` branch to be your `final draft` branch, the public face of your project. As we work on our projects, the `master` branch will be where our changes come home to rest, but those changes will first be conceived and nurtured in their own branches before being merged.

A branch of a Git project is a parallel universe. When we create a branch, we are able to make changes to our project as it existed in the moment we branched while protecting the `master` branch from new, more volatile code.

Before you go about turning your dreams into reality, consider giving spirit form by identifying the distinct building blocks of your project. A web application, for example, often adheres to a Model-View-Controller architecture, with separate models, controllers, and views for different aspects of the application. As we work on our project with Git, it behooves us to create new branches for each model, controller, and view as they're implemented. Further on down the road, we may create branches for new features or bug fixes.

Branching in Git is as simple as `git branch BRANCH_NAME`. This command creates a new branch. To work in that branch, we need to check it out, like we would a book at the library. `git checkout BRANCH_NAME` does the trick. Since we're lucky enough to be working in a field where laziness is a virtue, we can abridge this process. `git checkout -b BRANCH_NAME` will both create and checkout a branch.

Once we've created a branch, we can save our progress with `add` and `commit` as usual. Remember that executing `git push` will upload our project as it exists in the last commit in the current branch. The diagram below shows the state of our project after doing all of the above. Note the location of the asterisk! It is on *account-m* on account of us being in that particular branch.

[![Creating a new branch, committing and pushing](https://res.cloudinary.com/practicaldev/image/fetch/s--fCWW2kA5--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/x38e8dyyccaxcrk3wd47.png)](https://res.cloudinary.com/practicaldev/image/fetch/s--fCWW2kA5--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/x38e8dyyccaxcrk3wd47.png)

The image above shows the `master` branch pointing to an earlier commit than the `account-m` branch. Since we've committed in `account-m`, `master` is behind! When the purpose of a feature branch has been fulfilled and its quality is satisfactory, it's time to **merge** that branch back into the `master` branch. Intuitively enough, we accomplish this feat with `git merge`.

First, we checkout the master branch, then we execute `git merge BRANCH_NAME`.

[![Checking out the master branch](https://res.cloudinary.com/practicaldev/image/fetch/s--JhOeVs_9--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/7odwx9sa24dxxib7jxki.png)](https://res.cloudinary.com/practicaldev/image/fetch/s--JhOeVs_9--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/7odwx9sa24dxxib7jxki.png)

Notice the location of the asterisk! We're now in the master branch. Now merge the `account-model` branch and push our changes to remote.

[![Checking out the master branch, merging the other branch, and pushing](https://res.cloudinary.com/practicaldev/image/fetch/s--fQmMH-fn--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/ljwc5n51dufc9sab9lig.png)](https://res.cloudinary.com/practicaldev/image/fetch/s--fQmMH-fn--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/ljwc5n51dufc9sab9lig.png)

In short, we've accomplished the following...:

1.  `$ git checkout -b account-model`
2.  A half-hour of thought and toil passes...
3.  `$ git add .`
4.  `$ git commit -m "Create basic Account migration and model"`
5.  `$ git checkout master`
6.  `$ git merge account-model`

### [](https://dev.to/levi/a-simple-git-branch-workflow-24hh#putting-it-all-together)Putting It All Together

We now know how to save our progress and to create progress in a safe place before making it a lasting part of our project. Now let's look at how this workflow plays with others.

Say we're working with someone else on this project. They are going to, say, flesh out the controller for the accounts model we created previously. They go off, clone (aka download) our repository, work, faithfully commit, and push their changes to remote. If we want to see their work on *our* machine, we need to **pull** what is on the remote, with `git pull`.

[![Pulling a partner's woork](https://res.cloudinary.com/practicaldev/image/fetch/s--ezgRZEWP--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/bho0ukc57vuc63pm2z8d.png)](https://res.cloudinary.com/practicaldev/image/fetch/s--ezgRZEWP--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/bho0ukc57vuc63pm2z8d.png)

Notice that the asterisk is on the master branch, two commits behind our colleague's branch. Our colleague isn't quite done yet, so we decide to work on a separate feature on a separate branch. We do so, and make a couple commits' worth of progress.

[![Making our own progress](https://res.cloudinary.com/practicaldev/image/fetch/s--3mkh4B2v--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/tl41kb49mhbhungntgzo.png)](https://res.cloudinary.com/practicaldev/image/fetch/s--3mkh4B2v--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/tl41kb49mhbhungntgzo.png)

In the meantime, our colleague finished and pushed their last commit for their branch. We promptly pull it to stay abreast.

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--YN04GJrh--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/uyuth572i203iq7bnncd.png)](https://res.cloudinary.com/practicaldev/image/fetch/s--YN04GJrh--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/uyuth572i203iq7bnncd.png)

We finish with our work, and decide it's time to put everything together, merging and (of course!) pushing the result to the remote so our team can work from it.

[![Merging everyone's work](https://res.cloudinary.com/practicaldev/image/fetch/s--1vXeMVta--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/b6tyu5wxl32gsncn0xt1.png)](https://res.cloudinary.com/practicaldev/image/fetch/s--1vXeMVta--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/b6tyu5wxl32gsncn0xt1.png)

This process is the basic unit of a Git branching workflow. Each member of a team project works on a branch appropriate to a particular feature, component, or variation of the project. Commits are made and pushed with every milestone. When a particular branch has served its purpose and is ready for the big time, it is merged into the master branch. And on and on it goes!

## [](https://dev.to/levi/a-simple-git-branch-workflow-24hh#resolving-conflicts)Resolving Conflicts

Invariably, you will run into conflicts. Resolving them is beyond the scope of this blog post, but here are a tip for avoiding them and resources for dealing with them.

To avoid merge conflicts, each branch has contain changes that only pertain to separate files. If the branches being merged both have variations of the same file, it'll be time to resolve conflict.

Resolving merge conflicts is far from terrible! [Visual Studio Code](https://code.visualstudio.com/docs/editor/versioncontrol#_merge-conflicts), [Github](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/resolving-a-merge-conflict-on-github) (if you're making pull requests on the repo instead of locally merging), and even your native terminal provide tools for editing and resolving differences between conflicting files.

## [](https://dev.to/levi/a-simple-git-branch-workflow-24hh#now-what)Now What?

Many of us, when we first start learning Git, do so just out of the demands of interfacing with others through our job or the Internet. Maybe we want to host our projects on Github and share our work with the world! Maybe we can only take a crack at someone else's work by accessing it through Bitbucket.

Strictly speaking, you don't have to be plugged in to the Web to use Git. Whether we're working alone, in pairs, or in a small group, a couple of guidelines and handful of Git commands will enhance our ability to organize, collaborate, and more fully realize the vision of our projects. Whatever software you start or contribute to, and even if you're working alone, take care to employ Git with best practices so you reap the rewards of a well-managed project.

## [](https://dev.to/levi/a-simple-git-branch-workflow-24hh#resources-and-references)Resources and References

-   [git Documentation](https://git-scm.com/docs)
-   [Atlassian: Saving Changes](https://www.atlassian.com/git/tutorials/saving-changes)
-   [Learn Git Branching Applet](https://learngitbranching.js.org/)