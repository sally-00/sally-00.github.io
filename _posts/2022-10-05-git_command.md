---
layout: post
title: useful git command memo
date: 2022-10-05 17:39:00
description: project memo
tags: git
---

To clone a repository: 
```bash
$ git clone repository_name
```

To add locally hosted code to github: 
Firstly, create a repo on github website. 
Secondly, do the following on the directory of the project: 
``` bash
$ git init && git symbolic-ref HEAD refs/heads/main
$ git add .
# Adds the files in the local repository and stages them for commit. To unstage a file or a folder, use 'git reset YOUR-FILE-OR-FOLDER'.
$ git commit -m "First commit"
# Commits the tracked changes and prepares them to be pushed to a remote repository. To remove this commit and modify the file, use 'git reset --soft HEAD~1' and commit and add the file again.
$ git remote add origin <REMOTE_URL>
# Sets the new remote
$ git remote -v
# Verifies the new remote URL
$ git push origin main
# Pushes the changes in your local repository up to the remote repository you specified as the origin
```

``` bash
$ git status
$ git add --all
$ git reset path/to/file_or_folder
$ git commit -m "Comment here"
$ git push
```

Branch management:
```bash
# create a new branch
$ git branch <branch_name>
# switch to an other branch
$ git checkout <branch_name>
# list all branch
$ git branch -a
```
