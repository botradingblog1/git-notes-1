# Git Notes

## Overview
Here my notes to understanding git basics like workspace, stage, commits, branches and how to work with the basic git commands.

## Command Cheat Sheet
```
git --version
git init <directory> (create local repo)
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
git clone
git status
git log
git log --oneline
git log --oneline -n2  (lines)
git log --oneline --graph --all (branch graph)
git add <file name> (this adds the new and modified files to staging for the next commit).
git restore --staged file1.txt  (this unstages file1 and excludes it from the commit)
git checkout -b "branch name" (create branch)
git branch (all local)
git branch -r (all remote)
git branch -a (all local and remote)
git commit -m "our first commit"
Git -a -m "asdfasd"  (adds all modified files to the commit)
git commit --amend -m "new commit message"  (change message)
git checkout <target> (change branch)
git checkout -- <file name> (undo changes to specific file)
git diff <branch 1> <branch 2> (diff between two branches)
git diff <commit sha 1> <commit sha 2> (diff between two commits)
git merge <branch name> (merges the branch specified into the current branch)
git merge --abort (aborts the merge)
git tag (list tags)
git tag <tag note> <commit sha or branch name> (lightweight tag)
git tag <tag note> <commit sha or branch name> -m "message" (annotated tag)
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

Detached head is a completely normal situation and it is easily remedied. A detached head simply means that HEAD is pointing to a commit rather than a branch. The consequence of this is that commits created while in a detached head situation do not have any references pointing to them. 
 
 This can make them disappear from git log, become garbage collected, or simply be unnecessarily difficult to get back to. The two most common ways to end up in detached HEAD are by explicitly checking out a commit or by checking out a tag.
 
 

## Merging branches
Conceptually, when we want to merge two branches, we create a new commit containing the joint changeset from the two branches. This works by finding the point at which the branches diverged and joining the two changesets.
 
<img src="https://github.com/justmobiledev/git-notes-1/blob/main/images/merge-branches-1.jpg" width="600">
 
## Merging
 
The common way to use the merge command is with the form `git merge branch` which will merge the changeset from branch into the branch currently checked out, for example:
```
git merge feature-123.
```
 
### Fast-forward Merges
 A fast-forward merge happens when there has been no divergence between the branches you are merging. This occurs when a branch is a continuation of another. In this scenario, one branch is linearly ahead of another. To merge the change, all we need to do is to move the second branch pointer to the commit the ahead branch points to.
 
 This also means that there is no possibility for any conflict doing a fast-forward merge. For this reason, fast-forward merges can be considered safe.
 
<img src="https://github.com/justmobiledev/git-notes-1/blob/main/images/fast-forward-merge-1.jpg" width="600">
 
## Three-way Merge
Three-way merges are named as such because three points are involved in the merge – both end states as well as the point from which both branches depart. We name these the source, target, and merge base, respectively. 
 
  <img src="https://github.com/justmobiledev/git-notes-1/blob/main/images/three-way-merge-2.jpg" width="600">
 
These occur when both of the branches that we are merging contain work that is only on one branch. Commonly, what happens is that while we were developing on our feature branch, some other developer has delivered some changes to the master branch. As such, the point at which we branched out from the master branch is no longer the newest commit on the master branch. As commits represent a specific state of the workspace, we need to create a new commit that contains the state of the workspace after grabbing both changesets.
 
 <img src="https://github.com/justmobiledev/git-notes-1/blob/main/images/three-way-merge-1.jpg" width="600">

## Merge Conflicts
It can be the case that Git is unable to determine what the result should be from merging branches. In this case, Git will ask for the user to resolve the merge and resume the process. This situation is called a merge conflict.
 
 ## Rebase
An alternative to the three-way merge is the rebase. In contrast to the three-way merge that creates a new commit representing the workspace resulting from merging two branches, the rebase intuitively moves the commits. This is technically wrong, but we’ll keep the intuition for now. When we rebase our branch on top of another branch, intuitively we move the commits on our branch and apply them on top of the target branch.
 
 We use the git rebase <target> command to rebase HEAD on top of <target>. Assuming feature is checked out, we would write git rebase master to rebase the feature branch on top of master. 
  <img src="https://github.com/justmobiledev/git-notes-1/blob/main/images/merge-rebase-1.png" width="600">

## Merge or Rebase?
 It is key that the entire team works in a way that results in a consistent history no matter who delivers a given changeset. This most likely means everyone rebases or everyone merges. As rebasing changes the commit shas, it is considered bad practice to rebase branches that are public and that you work on as a team.
 
 Second, if you are not working on a shared branch, you should always rebase. This leaves your history clean and bundles your commits nicely together for a concise delivery. 
 
 ## Tags
 There are two types of tags, lightweight and annotated. 
 
 Lightweight tags are like branches except they are static. This means that they are simply a reference to a commit with no additional information. 
 
 Annotated tags are full objects in the Git object database, takes a message, and provides additional information. Annotated commits are created by adding -a, -s, or -m to the tag command. The tag command looks like this: git tag <target> for lightweight tags. For example, git tag v1.6.2 a233b will create a lightweight tag pointing at the commit with the prefix a233b.
 
 
 
 
