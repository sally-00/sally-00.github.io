---
layout: post
title: useful git command memo
date: 2022-10-05 17:39:00
description: 
tags: git
---

To clone a repository: 
```bash
$ git clone repository_name
```
When pushing a cloned repo to github, [manage upstream depends on if you want to pull changes from that repo](https://stackoverflow.com/questions/18200248/cloning-a-repo-from-someone-elses-github-and-pushing-it-to-a-repo-on-my-github). More about origin and upstream [here](https://stackoverflow.com/questions/9257533/what-is-the-difference-between-origin-and-upstream-on-github).

To add locally hosted code to github: 
Firstly, create a repo on the github website. 
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

To ignore files in the folder, create a file named ".gitignore" and put all the files' name inside.

Switching between different commits, temporarily and hard delete:
[A good explanation here](https://stackoverflow.com/questions/4114095/how-do-i-revert-a-git-repository-to-a-previous-commit)

Working with others:
Pull the repo without it overwriting the changes you have made:
```bash
$ git stash
$ git pull
$ git stash pop
```
[source](https://stackoverflow.com/questions/19216411/how-do-i-pull-files-from-remote-without-overwriting-local-files)

Or.

Commit changes and then pull. Use `--rebase` so it is not a merge commit and the history wil be linear.
```bash
$ git pull --rebase
```
[git pull with local commits](https://happygitwithr.com/pull-tricky.html#git-pull-with-local-commits)