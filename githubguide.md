# CS 1331 Guide to

![GitHub Logo] (http://doc.rultor.com/images/github-logo.png)

**Isabella Plonk**
**Fall 2016**

## Introduction

This document contains a brief overview of GitHub for students in CS 1331: Object-Oriented Programming at the Georgia Institute of Technology. It covers version control, repositories, and basic Git commands.

## What is GitHub?

### Version Control

Version control is a system that records changes to a file or a collection of files over time in order to recall specific versions later. If you have ever created a Google Doc, you may have noticed that each document keeps a history of every change made to it by every user and allows you to restore a previous version of your work. This is a small example of version control. In the same way version control is useful to a group creating an annotated bibliography for a project where there are multiple users and many additions and deletions, it is also useful to software developers. Having the complete history of code modifications enables us to recall previous versions of our code to identify the root causes of bugs. 

However, this is not the only way utilizing a Version Control System (VCS) is important for software developers. Additionally, the branching and merging capabilities of version control allow contributors to work on independent streams of change simultaneously. By creating a branch in a VCS, we can keep multiple streams of development independent from one another while also providing the facility to merge the work back together. In merging, collaborators can ensure changes do not conflict. Lastly, with version control we can easily trace each change made since changes are annotated with a message describing its purpose. This not only aids us in debugging our code but also in understanding what our code is doing and why our code is designed the way it is.


### The "Git" in GitHub

Now that we understand what version control is, what is Git? Git is an open source Distributed Version Control System (DVCS) developed in 2005 by Linus Torvalds, the creator of the Linux operating system kernel. A DVCS is a version control system that allows each developer to obtain a local copy of a project. Git was created when the relationship between the Linux kernel community and the company that developed BitKeeper, the Linux kernel's original DVCS, deteriorated. This prompted Torvalds to develop his own tool, taking into account the specific needs of the Linux kernel. Thus came the birth of Git, a new system designed for speed, non-linear development, and large projects. 


### The "Hub" in GitHub

While Git was originally developed for large communities of commercial software developers, it is now being used by a greater number of people for a wider variety of purposes. This has largely been because of online Git hosting repository services like GitHub, which is largest code host in the world, hosting more than 14 million users and more than 35 million repositories. Additionally, GitHub allows Git to be used for non-programming purposes such as for storing collections of word documents which require constant upkeep, by non-professionals such as for beginners’ working on their own personal projects, and for non-commercial purposes which allow for greater connectivity and sharing of code among individuals.

## The Command Line

There are many different ways to use Git. There are the original command line tools, and there are several IDEs which support Git. Because we highly recommend that CS 1331 students use text editors like Sublime and Atom to code, we will be using Git on the command line, Terminal in Mac or Command Prompt in Windows, for this guide.

## Installation of Git

Before you start using Git, you have to make it available on your computer. Even if you already have Git installed, you should update to the latest version. To identify which version of Git you currently have, run the following line:

```
git --version
```

### Windows

To download Git for Windows, follow the steps below:
 
1. Visit [git-scm.com](https://git-scm.com).
2. Select "Download for Windows" and the download should start automatically.
2. Double click on the download and open the package.
3. Follow the instructions on the pop-up window.


### Mac OS X

To download Git for Mac OS X, follow the steps below:

1. Download [homebrew](http://brew.sh).
2. Run ```brew install git```.


## Git Basics

### Setting Up a Repository

The first step to utilizing GitHub is to create a repository for your homework assignments. To create a repository, follow these steps:

1. Log into your GitHub account and select "New repository." 
2. Name your repository as instructed.
3. Set visibility to private. (For this class we will use github.gatech.edu which will allow us to create private repositories for free.)
3. Check the box for "Initialize your repository with a README."
4. Select "Java" in the dropbox for "Add .gitignore." 
5. Select "Create repository." 

![Create a New Repository] (https://guides.github.com/activities/hello-world/create-new-repo.png)

Now you can make a working copy of this repository on your computer. This allows you to make changes locally and then push to GitHub. To do this, cd into the directory in which you want to make your local repository and use ```git clone <repository url>``` to clone your repository. For example, if you wanted to clone the Git linkable library called libgit2, you would run the following line:

```
git clone https://github.com/libgit2/libgit2
```

**Congratulations!** You have now created your first repository.


### Adding Collaborators

For this course you will need to add all of the TAs as collaborators, so we can easily grade your assignments. In future courses you may have a repository for a group project and need to add your group members as collaborators. To add collaborators, follow these steps:

1. Log into GitHub and go to your repository main page.
2. Select "Settings."
3. Select "Collaborators."
4. In the text field, type in the user's username, full name, or email address and select "Add collaborator."

![Adding Collaborators] (https://help.github.com/assets/images/help/repository/repo-settings-collab-autofill.png)

### Recording Changes to the Repository

Now let's say you have been working hard on your local repository. You have been making modifications to your files, and now you are ready to update your repository with all of the new changes. The next step is to add, commit, and push your changes. However, before we go into the commands that you will utilize to do this, let's go a little deeper into Git's architecture.

What differentiates Git from other VCSs is how it stores its data. Instead of storing its information as a list of file-based changes, Git stores its data as a directed acyclic graph (DAG) which allows for non-linear development. Each commit contains information about its ancestors. A commit can have zero to infinitely many parent commits. This enables Git to reference previous files instead of storing the files again if in the last commit there were no changes made to those files and to determine the common ancestors of two merging branches as shown in the figure below.

![Git DAG] (http://git.mikeward.org/img/dag-commit-4.png)

This forms the foundation of Git’s architecture. With Git, developers check out or clone files from a public repository to their own local version of the code called a local repository, or working directory, allowing them to work simultaneously on the same project. A developer can then add his changes to the staging area where changes wait to be committed. When a developer makes a commit, the commit is still local to his device until he pushes it to a public repository.

![Git Architecture] (https://2.bp.blogspot.com/-XbBSjvS_c-o/VrsfPLHnnsI/AAAAAAAABYA/Kcy3rvEZAac/s1600/b.PNG)

#### git status

To check the status of your working directory and staging area at any time during the commit process, run ```git status```. If you run this line after cloning a repository, you should see something like this:

```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working directory clean
```

Otherwise, running this command will alert you to untracked files, changes to be commited, or changes not staged for commit.

#### git add

The ```git add``` command allows us to add changes from our working directory to the staging area. It puts the changes into the staging area to be included in the next commit.

To include a certain file or directory, run the following line:

```
git add <file/directory>
```

To include all changes, run the following line:

```
git add --all
```

#### git commit

Once you are satifised with the staged snapshot, you use ```git commit``` to commit it to your project history. Each commit has a message that corresponds to it. Be concise yet descriptive in your message, so you can retrace your commits easily when you view your commit log, which we will discuss in the next section.

```
git commit -m "Initial commit"
```

#### git push

Finally, you are ready to update the public repository with your changes. Run the following line to push your changes to your master branch on GitHub:

```
git push -u origin master
```
**Congratulations!** You have now created your first commit.

### Viewing the Commit Log

Now that we have made a commit, we can view our commit history. This can be done by logging into GitHub and selecting "[#] commits" at the top of your repository page. Then, each commit can be selected to see its additions and deletions.

From the command line, you can run ```git log``` to view this same history.

![Git Log] (http://gitready.com/images/graphfail.png)


## Summary

Now you should be able to create a respository, add collaborators, and push and view commits with GitHub. GitHub is an extremely useful tool for storing and sharing code. It is important that you become comfortable with how to use GitHub and Git as you will be required to use it in this course and your future CS courses. GitHub is not only important for your coursework but is also a main source for employers to view your personal projects. Once you become comfortable with the basics of GitHub, you can learn more about how to utilize all of the services it provides. To learn more about GitHub, visit guides.github.com for step-by-step tutorials or help.github.com for assistance on specific questions. To learn more about Git, visit git-scm.com.

## Works Cited

Adding collaborators. Digital image. *GitHub Help*. Github Inc. Web. 17 Dec. 2016.

Chacon, Scott, and Ben Straub. *Pro Git*. 2nd ed. Berkeley: Apress, 2014. *Git*. Web. 17 Dec. 2016.

Command line commit log. Digital image. *Git Ready*. Nick Quaranto. Web. 17 Dec. 2016.

Creating a repository. Digital image. *GitHub Guides*. GitHub Inc., 7 Apr. 2016. Web. 17 Dec. 2016.

DAG Repository. Digital image. *Git: An Introduction*. South FL PHP Group, 12 Oct. 2011. Web. 17 Dec. 2016.

"Getting Started." *Git Tutorial*. Atlassian, n.d. Web. 17 Dec. 2016.

Git architecture. Digital image. *NavTechno: A New Image of Technology*. NavTechno. Web. 17 Dec. 2016.





