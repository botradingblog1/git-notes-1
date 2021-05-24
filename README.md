# Git Notes

## Overview
Here my notes to understanding git basics like workspace, stage, commits, branches and how to work with the basic git commands.

## Command Cheat Sheet
```
git --version
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
git clone
git status
git log
git log --oneline
git log --oneline -n2  (lines)
git add <file name> (this adds the new and modified files to staging for the next commit).
git restore --staged file1.txt  (this unstages file1 and excludes it from the commit)
git checkout -b “branch name” (create branch)
git branch (all local)
git branch -r (all remote)
git branch -a (all local and remote)
git commit -m "our first commit"
Git -a -m “asdfasd”  (adds all modified files to the commit)
git commit --amend -m "new commit message"  (change message)
git checkout <target> (change branch)
git checkout -- <file name> (undo changes to specific file)
git diff <branch 1> <branch 2> (diff between two branches)
git diff <commit sha 1> <commit sha 2> (diff between two commits)
```

## The Repository
When we talk about Git at the high level, we talk about collaborating in repositories. 

There are two common ways of starting work in a repository: We can either use the command git init to initialize a new local repository without any history and start our work there. This can even be done in a folder with content that is not under version control yet. More commonly, we use the command git clone to obtain a copy of a repository. The source of a repository is most often a private (i.e., Bitbucket on premises) or public (i.e., GitHub cloud) repository manager.

The local repository is tied to the source by a configuration called the remote.

## The Commit
The base unit of Git is the commit. Intuitively, a Git commit represents the full state of the workspace at a given point in time. A commit also contains the following metadata:
What commit(s) came before it
The author and committer
* A timestamp
* A commit message, with information on the content of the commit
* The previous commit is called the parent.
The very first commit in a repository is special as it has zero parents. This makes sense as nothing comes before the first commit. The first commit is also often referred to as the initial commit. 

## The Tag
The tag is the simplest reference in Git. It is simply a pointer to a commit. A commit use for tags is marking the commits that were released with a tag named after the concrete version.
A tag is never changing. That means that we at any time can back to a commit through a name. 
 
## The Branch
A branch is a file containing the sha of the commit it points to. 
Local branches are located under .git/refs/heads.
As we do development and create commits, the currently active branch moves along and points to the new commits that we create. The currently active branch is also said to be the branch that we have checked out.
 
Git uses a branch named master as its default. This means that we expect the master branch to be the main source of truth and the most important branch.
Setup
```
 git clone <remote-repository> <local-path>.
```

Example:
```
git clone https://github.com/eficode-academy/git-katas.git git-katas. 
```
To create a local branch:
```
git branch <branch-name> <commit>. 
 ```
 As an example: 
 ```git branch my-branch master. 
 ```
 This will create a branch in the repository. It will be called my-branch and point to the same commit as master. 

## The .git directory
Contains:
* The entire history of the repository, including data
* Local configuration
* Pointer to what is currently checked out
* Pointer to the origin that was cloned from

Check if git works:
git --version

## git status
git status
Git status tells you about the state of your workspace and how it compares to what is currently checked out. If the workspace is identical to what is checked out, the workspace is said to be clean. If the workspace contains changes, of any sort, the workspace is said to be dirty. Changes can be modified, deleted, added, or renamed files.

## git log
Git log is the most basic way we can look at the history of our repository.
git log

## The Workspace
As mentioned, our workspace can be either dirty or clean, when compared to the currently checked-out commit on the repository.

We can see the state of the workspace using the Git status command. As we change files in the repository and run the git status command, we can see how Git tells us that files become modified or deleted for files that are already tracked by Git, or how files that we add to our workspace for the first time show up in Git status as untracked.

## The Stage
In Git, files can be represented in three different locations, of which we have covered two so far: the workspace and the repository. There is a third one that lies between the two – that area is called the index or the stage. The logic of this stage is that it is the place where we fashion what will go into the commit that we make next. The flow of work goes as follows: We make some changes, we stage the changes that we want to be a part of the next commit, and finally we make a commit. 


A file can have different states from the git perspective:
* Unmodified: This file is identical in the workspace and in currently checked-out commit in the repository.
* Modified: This file is present in both workspace and repository, but is different.
* Staged: This file is in the workspace, current commit, and stage. Note that the file can be different in all three locations.
* Untracked: This file is in the workspace, but not in the current commit.
* Git Commit
What then happens is the message passed with the command-line flag -m and the changeset and some automatically generated content is persisted in the commit object. Afterward, the currently checked-out branch is updated to point to this newly created commit.


## .gitignore
Use .gitignore to exclude files and directories:

__pycache__/
*.py[cod]
*$py.class
*.so

## Branches
In Git, a branch is nothing more than a reference to a single commit. 
In Git, the branch that is currently active is said to be checked out. Git uses a file called HEAD to keep track of what is currently checked out. The HEAD pointer does not change. It keeps pointing to the branch that’s checked out.

## git checkout
git checkout <target>
Used to change branches.
First, it moves the HEAD pointer to the specific revision. Then, it takes what content is in that revision and moves it into the workspace, to make the workspace look like that revision.

## git diff
Changes between branches or commits.
git diff <branch 1> <branch 2> (diff between two branches)
git diff <commit sha 1> <commit sha 2> (diff between two commits)

## What is a ‘Detached Head’?

If you are working in your repo and do git checkout <SHA> you will be in a "detached HEAD". You are not on a branch (the commit is likely to be on multiple branches). You are checked out to a specific instance in the history.
 
A detached head can also occur when you are rebasing. You are checked out to a specific commit.
 
You would need to create a branch in order to commit/push changes because you would be creating commits that would be "in limbo" with no way to identify them other than the SHA. Git will remove the commit during its garbage collection because of it not being on a branch.

## Merging branches
Conceptually, when we want to merge two branches, we create a new commit containing the joint changeset from the two branches. This works by finding the point at which the branches diverged and joining the two changesets.

![alt text](https://github.com/justmobiledev/git-notes-1/edit/main/images/merge-branches-1.png?raw=true)
