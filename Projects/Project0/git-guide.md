# Project 0 - Git Guide

## Command line git

- status
  - Shows status of the local repository. This status includes:
    - number of local commits that have not been synced with remote (GitHub)
    - list of files in local folder than are NOT being tracked by git
    - list of files in local folder that have changes that need to be committed
  - `git status`
- clone
  - Points at existing repo and make a clone of that repo in a new directory or location
    - creates remote-tracking branches for each branch in the cloned repository
  - `git clone 'url' `
- add
  - Adds a change in the working directory to the staging area, ready to be committed
    - tells git to include updates to the file in the next commit
  - `git add  'filename'`
- rm
  - Remove files from the current branch
    - deletes file from the staging area, and the deletion will be confirmed with the next commit
  - `git rm 'filename'`
- commit
  - Record changes to the repository
  - `git commit 'filename' -m "commit message"`
- push
  - Upload the local repository to remote
    - transfer commits from local to remote
  - `git push 'remote' 'branch'`
- fetch
  - Download the remote repository to local
  - `git fetch 'repository'`
- merge
  - Join two or more development changes together
    - incorperates the changes from commits from another branch into the current one
  - `git merge 'topic'`
- pull
  - Fetch from and integrate another repository or branch into the current repository
  - `git merge 'repository'`
- branch
  - Allows you to list, create, or delete branches
  - `git branch [option]` such as -d, -m, or -c
- checkout
  - Switch branches or restore working tree files
  - `git checkout 'branch'`
- ~~init~~
- ~~remote~~

## git files & folders

- .git folder
  - contains all information necessary for the project and all information relating to commits, remote address, etc.
  - also contains commit history log
- .gitignore file
  - plaintext file that contains patterns for files or directories to ignore
- ~~.git/hooks~~

## GitHub

- Pull requests
  - Allows you to tell others in the repository about what changes you've pushed to a branch on github
  - Allows discussion on the changes with collaborators
  - You can make additional commits before they are merged into the base branch
- SSH authentication to repositories
  - Provides a secure channel to access GitHub repositories from a personal device
- ~~Actions~~
