---
layout: post
title: Git up and running!
bigimg: /img/path.jpg
published: true
---


### What do we need to start?

Download Git

windows:  
https://git-for-windows.github.io/

Linux: 
https://git-scm.com/book/en/v2/Getting-Started-Installing-Git

OSX/MAC: 
https://git-scm.com/download/mac

Git typically consists of three parts, 

Working Directory: This holds our actual files, we **add** from here.

Index: This acts as a staging area, we **commit** from the Index.

Head: This is pointing to the last commit we have actively made.


### Creating a new Repository
Create a new directory on the file system, open it and type the init command

    git init
    
We have now created/initiated a new git repository.

### Checking out a Repository
In order to checkout a remote repository, if it is remote we will use the following syntax:

    git clone symonk@github:/path/to/repository
    
If it is a local repository we will use the following syntax:

    git clone /Your/Directory/Here
    
### Adding files 
In order to add files to the staging area, we simply use the add command:

    git add fileName
    git add * (everything in the directory)
    
### Committing files
Once files are **added** we can *commit* them to the HEAD, we do this using the following syntax:

    git commit -m "My First Commit!"
    
### Pushing files to the Repository
Once committed our files still are not in the repository, we first need to push them.

git push origin *master* (WHERE master = the branch name)

### Connecting Repository to a remote server
If you haven't cloned an existing repository and want to connect your repo to a remote server, you can simply add it using the following:

    git remote add origin <127.0.0.1> Where <> is the Server of choice
    
### Branching
Typically branches are used to develop features.  The master branch is the default branch and typically contains a working releasable product.  Try using other branches for new feature development and merge them back in master later.

Create a Branch using the following:

    git checkout -b MyBranchName
    
Switch Branch using the following:

    git checkout master
    
Delete Branch using the following:

    git branch -d MyBranchName
    
If you want to make your branch available to other people, simply push it like so:

    git push origin MyBranchName
    
### Updating your local Repository with the latest
To update your repository to the latest version, simply use the pull command:

    git pull
    
To merge another branch into your active branch, using the merge command:

    git merge BranchNameHere
    
Git will try to automerge where possible, but this sometimes does not succeed and you will end up with conflicts to resolve.  Once corrected you can mark them as merged by using the add command again:

    git add myFileHere
    
You can also check the differences in your files by using the diff command:

    git diff FeatureABranch master (where master is the target and FeatureABranch is the source)
    
### Managing versions/Releases using tags
Typically you want to create tags for software releases.  we can achieve this with the tag command:

    git tag 2.5.1 1b2e1d63ff (2.5.1 is the tag, 1b2e1d63ff is the commit ID which we can get from the log
    
### Logs
To view logs, we can simply use the log command:

    git log
    
However we can choose to pass in some paramaters to affect our results.  Compact log, one line per commit:

    git log --pretty=oneline
    
an ASCII diagram of all the branches:

    git log --graph --oneline --decorate --all
    
All files which have changed:

    git log --name-status
    
To find more, use the log help:

   git log --help
