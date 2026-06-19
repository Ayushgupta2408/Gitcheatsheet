# Gitcheatsheet
Git & GitHub Cheat Sheet
1. Configure Git (First Time)
git config --global user.name "Ayush Kumar Gupta"
git config --global user.email "your_email@example.com"

Check configuration:

git config --list
2. Create a New Repository

Initialize Git:

git init

Check status:

git status
3. Add & Commit Changes

Add specific file:

git add filename

Add all files:

git add .

Commit changes:

git commit -m "Initial commit"

Commit tracked files directly:

git commit -am "Updated project"
4. Connect to GitHub

Add remote repository:

git remote add origin https://github.com/username/repository.git

Check remote:

git remote -v
5. Push Code to GitHub

First push:

git push -u origin main

or

git push -u origin master

After making changes:

git add .
git commit -m "Updated project"
git push
6. Clone Existing Repository
git clone https://github.com/username/repository.git
7. Pull Latest Changes
git pull origin main

or simply:

git pull
8. Branch Commands

Create branch:

git branch feature

Switch branch:

git checkout feature

Create & switch:

git checkout -b feature

Modern command:

git switch -c feature

List branches:

git branch

Delete branch:

git branch -d feature
9. Merge Branches

Switch to main:

git checkout main

Merge feature branch:

git merge feature
10. View History
git log

Compact view:

git log --oneline

Graph view:

git log --oneline --graph --all
11. Undo Changes

Discard file changes:

git restore filename

Discard all changes:

git restore .

Unstage file:

git restore --staged filename

Remove last commit (keep files):

git reset --soft HEAD~1

Remove last commit completely:

git reset --hard HEAD~1
12. Stash Changes

Save work temporarily:

git stash

View stashes:

git stash list

Restore stash:

git stash pop
13. Common Daily Workflow
git status
git add .
git commit -m "Added new feature"
git push

Get latest code:

git pull
14. GitHub Authentication (PAT)

If password authentication fails:

Go to GitHub → Settings → Developer Settings → Personal Access Tokens.
Generate a token.
Use:
Username: your_github_username
Password: Personal Access Token
15. Most Important Commands for Interviews
git init
git clone
git status
git add .
git commit -m "message"
git push
git pull
git branch
git checkout
git merge
git rebase
git stash
git log --oneline
git reset
git revert
Emergency Commands
git status
git add .
git commit -m "fix"
git push
After Editing Code
git add .
git commit -m "Updated project"
git push
