## What is Git & SCM
* Git is a distributed Source Code Management tool.
* Types of SCM:
  * Local: only on one machine.
  * Remote: central server like SVN.
  * Distributed: every developer has full repo (Git).
* Git allows offline work, full history, collaboration.

## Installing and Setting Up Git
* Install: `yum install git` or `apt install git`
* Check: `git --version`
* Configure:
  * `git config --global user.name "Name"`
  * `git config --global user.email "Email"`
  * `git config --global core.editor "vim"`

## SSH Setup
* Generate: `ssh-keygen -t rsa -b 4096 -C "email"`
* Add public key to GitHub.

## Starting a Repository
* Create folder: `mkdir demo && cd demo`
* Init repo: `git init`
* Check hidden files: `ls -a`
* `.git` stores full history.

## Four Areas of Git
* Working Tree: editable files.
* Staging Area (Index): prepared changes.
* Local Repository: commits stored locally.
* Remote Repository: GitHub or GitLab.

## Basic Workflow
* Create files: `touch Abc.txt Xyz.txt`
* Stage: `git add Abc.txt`
* Commit: `git commit -m "msg"`
* Add remote: `git remote add origin <url>`
* Push: `git push origin main`

## Viewing Changes
* Unstaged: `git diff`
* Staged: `git diff --cached`
* Status: `git status`

## Logs and Commit Info
* History: `git log`
* Visual: `git log --oneline --graph --decorate --all`
* Show commit: `git show <commit>`
* Line history: `git blame file`

## Staging and Committing
* Stage: `git add file.txt`
* Interactive stage: `git add -p`
* Unstage: `git restore --staged file.txt`
* Amend: `git commit --amend`

## Branching and Merging
* List: `git branch`
* All branches: `git branch -a`
* Create and switch: `git switch -c feature/x`
* Switch: `git switch feature/x`
* Merge: `git merge feature/x`
* Rebase: `git rebase master`
* Delete: `git branch -d name`

## Remote Repositories
* Show: `git remote -v`
* Fetch: `git fetch`
* Pull: `git pull`
* Push: `git push -u origin feature/x`
* Change URL: `git remote set-url origin <newurl>`

## Tags
* Create: `git tag v1.0.0`
* Annotated: `git tag -a v1.0.0 -m "msg"`
* Push tag: `git push origin v1.0.0`

## Stashing
* Stash: `git stash`
* List: `git stash list`
* Apply: `git stash apply`
* Pop: `git stash pop`

## Undoing and Fixing
* Revert: `git revert <commit>`
* Soft reset: `git reset --soft HEAD~1`
* Mixed reset: `git reset --mixed HEAD~1`
* Hard reset: `git reset --hard HEAD~1`
* Recover: `git reflog`

## Searching
* Search text: `git grep "text"`
* Search commits: `git log --grep="keyword"`

## Git Ignore and Attributes
* Ignore: `echo "node_modules/" >> .gitignore`
* Check ignore: `git check-ignore -v file`

## Best Practices
* Fetch all: `git fetch --all --prune`
* Check merged: `git branch --merged`
* Pull rebase: `git config pull.rebase true`

## Common Workflows
* Feature branch:
  * `git switch -c feature/x`
  * Work → `git add .` → `git commit -m "msg"` → `git push -u origin feature/x`
* Rebase before merge:
  * `git fetch origin`
  * `git rebase origin/main`
* Merge:
  * `git merge --no-ff feature/x`
