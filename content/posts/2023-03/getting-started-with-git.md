---
layout: post
author: Angel
date: 2023-03-16T23:32:13-05:00
title: "Getting Started With Git"
tags: ["git", "github", "devops", "version control", "programming"]
description:
showToc: true
TocOpen: false
hidemeta: false
comments: true
disableHLJS: false # to disable highlightjs
disableShare: true
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: false
draft: false
---

[Git](https://git-scm.com/) is a powerful and widely used version control system that allows developers to manage changes to their codebase efficiently. 

Whether you are working on a solo project or collaborating with a team, Git provides a simple and effective way to keep track of changes and revert to previous versions if necessary. 

In this article, we will cover the basics of using Git, including creating a repository, making changes, committing those changes, and pushing them to a remote repository.

Here's a quick overview from [Fireship.io](https://fireship.io/).

{{< ytlazy hwP7WQkmECE >}}


## "Git" Started

Download the appropriate package for your system.

- [Windows Official Downloads](https://git-scm.com/download/win) or `choco install git`
- [Mac OS Official Downloads](https://git-scm.com/download/mac) or `brew install git`
- [Linux Official Downloads](https://git-scm.com/download/linux) or `apt install git` for Debian/Ubuntu.

Once you have installed Git, you can open a command prompt or terminal window and enter the following command to check that Git is installed and working correctly:

```
git --version
```

### Creating a Repository

Once Git is installed, you can start using it to manage your code. 

The first step is to create a new repository. A repository is a collection of files and directories that make up your project. 

To create a new repository, navigate to the directory where you want to store your project and enter the following command:

```
git init
```

This command initializes a new Git repository in the current directory. Git will create a hidden `.git` directory that contains all the information necessary to track changes to your code.

## Management

### Making Changes

With a repository created, you can start making changes to your code. 

To track changes in Git, you need to first stage the changes using the `git add` command. 

For example, to stage all changes in the current directory, enter the following command:

```
git add .
```

This command stages all changes in the current directory, including new files and modifications to existing files. 

You can also stage individual files or directories by specifying their names instead of the `.`.

### Committing Changes

Once you have staged your changes, you can commit them to the repository using the `git commit` command. 

A commit is a snapshot of your code at a specific point in time, and it includes a message describing the changes you made. 

To commit your changes, enter the following command:

```
git commit -m "Commit message"
```

Replace `Commit message` with a brief description of the changes you made. 

It's a good idea to keep commit messages short and descriptive, so that other developers can easily understand what changes were made.

### Pushing to a Remote Repository

By default, Git stores all changes in the local repository on your machine. 

However, you can also push changes to a remote repository, such as GitHub, GitLab, or Bitbucket. 

To push your changes to a remote repository, you need to first add the remote repository as a remote. 

For example, to add a remote named `origin` for a repository on GitHub, enter the following command:

```
git remote add origin https://github.com/username/repo.git
```

Replace `username` with your GitHub username and `repo` with the name of your repository. 

You can also use SSH instead of HTTPS if you prefer.

Once you have added a remote repository, you can push your changes using the `git push` command. 

For example, to push changes to the `main` branch of the `origin` remote, enter the following command:

```
git push origin main
```

Replace `main` with the name of the branch you want to push to. 

If you have never pushed to the remote repository before, Git may prompt you to enter your GitHub username and password.

### Revert Changes

To revert changes in Git, use the `git revert` command followed by the `commit hash` of the commit you want to undo. 

Git will create a new commit that undoes the changes made by the original commit. 

Use the git log command to find the commit hash of the commit you want to revert. This will display a list of all the commits in the repository, along with their commit hash, author, date, and commit message.

```
git log
```

Once you've found the commit you want to revert, use the git revert command followed by the commit hash to create a new commit that undoes the changes made by the original commit.

```
git revert <commit hash>
```

```
git revert 12a34b56c
```

Git will open a text editor for you to enter a commit message for the new revert commit.

Save and close the commit message file. Git will then create a new commit that undoes the changes made by the original commit.

Use the git log command again to confirm that the new revert commit was created and the changes were undone.

And that's it!

## Conclusion

In this article, we covered the basics of using Git to manage your code.

Git is a powerful tool for managing and versioning code and allows you to keep track of changes made to your codebase, collaborate with other developers, and easily revert changes when necessary.

Overall, Git is an essential tool for any IT professional looking to manage and version their code effectively.

### Learn More
- [Official Git Book](https://git-scm.com/book/en/v2)
- [Official Documentation](https://git-scm.com/docs)
- [Visual Cheat Sheet](https://ndpsoftware.com/git-cheatsheet.html#loc=index;)
- [Git Videos](https://git-scm.com/videos)
- [GitHub Cheat Sheets](https://training.github.com/downloads/github-git-cheat-sheet/)
- [GitHub Training Manual](https://githubtraining.github.io/training-manual/#/01_getting_ready_for_class)