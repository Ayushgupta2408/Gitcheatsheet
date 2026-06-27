## Gitcheatsheet
## Git Fundamentals & Configuration
### Initial Setup & Global Configuration
```sh
   # Essential global configuration
git config --global user.name "Your Full Name"
git config --global user.email "your.email@example.com"
git config --global init.defaultBranch main

# Editor configuration
git config --global core.editor "code --wait"     # VS Code
git config --global core.editor "vim"             # Vim
git config --global core.editor "nano"            # Nano
git config --global core.editor "subl -n -w"     # Sublime Text

# Line ending configuration
git config --global core.autocrlf true           # Windows
git config --global core.autocrlf input          # macOS/Linux
git config --global core.autocrlf false          # Manual control

# Advanced configuration options
git config --global color.ui auto                # Colored output
git config --global core.filemode false          # Ignore file mode changes
git config --global core.ignorecase false        # Case sensitive file names
git config --global pull.rebase false            # Merge on pull (default)
git config --global push.default simple          # Push behavior
git config --global rerere.enabled true          # Remember conflict resolutions

# Credential management
git config --global credential.helper cache      # Linux/macOS
git config --global credential.helper manager    # Windows
git config --global credential.helper store      # Plain text (not recommended)

# Advanced aliases for productivity
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual '!gitk'
git config --global alias.graph 'log --oneline --graph --decorate --all'
git config --global alias.aliases 'config --get-regexp alias'

# Complex aliases
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
git config --global alias.contributors "shortlog -sn"
git config --global alias.amend "commit --amend --no-edit"
git config --global alias.force "push --force-with-lease"
git config --global alias.root "rev-parse --show-toplevel"

# View configuration
git config --list                                # All config
git config --global --list                       # Global config only
git config --local --list                        # Local repo config only
git config --get user.name                       # Specific value
git config --get-regexp alias                    # All aliases

# Per-repository configuration
git config user.name "Different Name"            # Override for this repo
git config user.email "work@company.com"         # Work email for work repos
   ```
### Repository Initialization & Cloning
```sh
  # Initialize new repository
git init                                         # Current directory
git init my-project                              # New directory
git init --bare shared-repo.git                 # Bare repository for sharing

# Clone repositories
git clone https://github.com/user/repo.git      # HTTPS clone
git clone git@github.com:user/repo.git          # SSH clone
git clone repo-url my-folder                    # Custom folder name
git clone --depth 1 repo-url                    # Shallow clone (latest commit only)
git clone --branch develop repo-url             # Clone specific branch
git clone --recursive repo-url                  # Include submodules

# Advanced cloning options
git clone --single-branch --branch main repo-url # Only main branch
git clone --mirror repo-url                     # Mirror clone
git clone --bare repo-url                       # Bare clone
git clone --filter=blob:limit=1m repo-url       # Partial clone (large repos)

# Clone with different protocols
git clone https://github.com/user/repo.git      # HTTPS
git clone git@github.com:user/repo.git          # SSH
git clone file:///path/to/repo.git              # Local file system
   ```
# Core Git Operations
## Staging & Committing Advanced Patterns
```sh
  # Status checking with various options
git status                                       # Full status
git status -s                                   # Short format
git status --porcelain                          # Machine-readable format
git status --ignored                            # Show ignored files
git status -u                                   # Show untracked files
git status --column                             # Columnar output

# Advanced staging techniques
git add .                                        # All files in current directory
git add -A                                       # All files including deleted
git add -u                                       # Only tracked files
git add *.js                                     # All JavaScript files
git add -p                                       # Interactive staging (patch mode)
git add -i                                       # Interactive staging menu
git add -N file.txt                             # Add intent to track
git add --chmod=+x script.sh                    # Add with execute permission

# Interactive staging in detail
git add -p                                       # Patch mode options:
# y - stage this hunk
# n - do not stage this hunk
# q - quit; do not stage this hunk or any remaining ones
# a - stage this hunk and all later hunks in the file
# d - do not stage this hunk or any later hunks in the file
# s - split the current hunk into smaller hunks
# e - manually edit the current hunk

# Unstaging files
git reset HEAD file.txt                         # Unstage specific file
git reset HEAD .                                # Unstage all files
git restore --staged file.txt                  # Modern syntax (Git 2.23+)
git restore --staged .                         # Unstage all (modern)

# Committing with various options
git commit -m "Your commit message"             # Basic commit
git commit -am "Message"                        # Add and commit tracked files
git commit --amend -m "New message"             # Amend last commit message
git commit --amend --no-edit                    # Amend without changing message
git commit -v                                   # Verbose (shows diff in editor)
git commit --allow-empty -m "Trigger CI"        # Empty commit
git commit --fixup HEAD~2                       # Create fixup commit
git commit --squash HEAD~1                      # Create squash commit

# Advanced commit options
git commit --author="John Doe <john@example.com>" -m "Message"  # Different author
git commit --date="2023-01-01T12:00:00" -m "Message"           # Specific date
git commit --gpg-sign -m "Message"                             # GPG signed commit
git commit --no-verify -m "Message"                            # Skip pre-commit hooks

# Commit message templates
git config --global commit.template ~/.gitmessage

# Example .gitmessage template:
# [type]([scope]): [subject]
#
# [body]
#
# [footer]
#
# Types: feat, fix, docs, style, refactor, test, chore
# Scope: component, file, or feature affected
# Subject: imperative mood, no period, < 50 chars
# Body: explain what and why, not how (wrap at 72 chars)
# Footer: breaking changes, issue references
   ```
## Viewing History & Changes
```sh
   # Basic log viewing
git log                                          # Full log
git log --oneline                               # Compact format
git log --graph                                 # Visual branch graph
git log --decorate                              # Show branch/tag names
git log --all                                   # All branches
git log --stat                                  # Show file change statistics
git log -p                                      # Show patches/diffs

# Advanced log formatting
git log --pretty=format:"%h %an %ar %s"        # Custom format
git log --pretty=fuller                        # More detailed info
git log --format=medium                        # Standard format
git log --format=short                         # Abbreviated format

# Filtering log output
git log --author="John Doe"                    # Filter by author
git log --committer="Jane Smith"               # Filter by committer
git log --since="2 weeks ago"                  # Time-based filtering
git log --until="2023-12-31"                   # Before specific date
git log --after="2023-01-01"                   # After specific date
git log --grep="bug fix"                       # Search commit messages
git log -S"function_name"                      # Search code content (pickaxe)
git log -G"regex_pattern"                      # Grep in diff content
git log --all-match --author="John" --grep="bug" # Multiple filters (AND)

# File-specific history
git log file.txt                               # History of specific file
git log --follow file.txt                      # Follow renames
git log -L 10,20:file.txt                      # History of specific lines
git log --oneline -- '*.js'                    # History of JS files only

# Branch comparison logs
git log main..feature                          # Commits in feature not in main
git log feature..main                          # Commits in main not in feature
git log main...feature                         # Symmetric difference
git log --left-right main...feature            # Show which side commits are from

# Advanced log options
git log --reverse                               # Oldest first
git log --first-parent                          # Follow only merge commits
git log --merges                                # Only merge commits
git log --no-merges                             # Exclude merge commits
git log --cherry-pick --left-right main...feature # Show equivalent commits

# Viewing specific commits
git show HEAD                                   # Show last commit
git show HEAD~2                                 # Show commit 2 steps back
git show HEAD^2                                 # Show second parent of merge
git show commit-hash                            # Show specific commit
git show --name-only HEAD                       # Show only file names
git show --stat HEAD                            # Show change statistics

# Viewing differences
git diff                                        # Unstaged changes
git diff --staged                              # Staged changes
git diff HEAD                                   # All changes since last commit
git diff HEAD~1                                 # Changes since previous commit
git diff main..feature                         # Between branches
git diff main...feature                        # Against common ancestor
git diff --name-only                           # Only file names
git diff --name-status                         # Names with change type
git diff --color-words                         # Word-level diff
git diff --ignore-whitespace                   # Ignore whitespace changes

# Blame and annotation
git blame file.txt                             # Show who changed each line
git blame -L 10,20 file.txt                    # Blame specific lines
git blame -C file.txt                          # Detect moved/copied lines
git annotate file.txt                          # Alternative to blame
   ```
# Branching & Merging Mastery
## Branch Management Advanced Techniques
```sh
  # Listing branches with detailed info
git branch                                      # Local branches
git branch -r                                  # Remote branches
git branch -a                                  # All branches
git branch -v                                  # Verbose (show last commit)
git branch -vv                                 # Very verbose (show upstream)
git branch --merged                            # Branches merged into current
git branch --no-merged                         # Branches not merged
git branch --sort=-committerdate               # Sort by recent commits

# Creating branches
git branch feature-name                        # Create branch (stay on current)
git checkout -b feature-name                   # Create and switch
git switch -c feature-name                     # Modern syntax (Git 2.23+)
git checkout -b feature origin/feature         # Create from remote branch
git checkout --orphan new-root                 # Create orphan branch

# Branch creation from specific points
git checkout -b hotfix HEAD~3                  # From 3 commits back
git checkout -b release v1.0                   # From tag
git checkout -b experiment commit-hash         # From specific commit

# Switching branches
git checkout branch-name                       # Switch to branch
git switch branch-name                         # Modern syntax
git checkout -                                 # Switch to previous branch
git switch -                                   # Switch to previous (modern)

# Branch renaming and management
git branch -m old-name new-name                # Rename branch
git branch -m new-name                         # Rename current branch
git branch -c copy-branch                      # Copy current branch
git branch -d branch-name                      # Delete merged branch
git branch -D branch-name                      # Force delete branch
git branch --delete --remotes origin/branch    # Delete remote tracking

# Advanced branch operations
git branch --set-upstream-to=origin/main       # Set upstream for current branch
git branch -u origin/main                      # Shorthand for upstream
git branch --unset-upstream                    # Remove upstream
git branch --edit-description                  # Edit branch description
   ```
## Merging Strategies & Conflict Resolution
```sh
   # Different merge strategies
git merge feature-branch                       # Default merge (fast-forward if possible)
git merge --no-ff feature-branch               # Always create merge commit
git merge --ff-only feature-branch             # Only if fast-forward possible
git merge --squash feature-branch              # Squash all commits into one

# Merge with custom commit message
git merge -m "Merge feature X into main" feature-branch

# Advanced merge options
git merge -X ours feature-branch               # Favor current branch in conflicts
git merge -X theirs feature-branch             # Favor merging branch in conflicts
git merge --strategy=ours feature-branch       # Use 'ours' strategy
git merge --strategy=recursive -X patience feature-branch # Use patience algorithm

# Conflict resolution workflow
git merge feature-branch                       # Start merge (conflicts occur)
git status                                     # See conflicted files
# Edit files to resolve conflicts:
# <<<<<<< HEAD
# Current branch content
# =======
# Incoming branch content
# >>>>>>> feature-branch

# After resolving conflicts
git add resolved-file.txt                      # Mark as resolved
git merge --continue                           # Complete merge
# Or abort if needed
git merge --abort                              # Cancel merge

# Using merge tools
git config --global merge.tool vimdiff         # Set merge tool
git mergetool                                  # Launch merge tool
git mergetool --tool=code                      # Use specific tool

# Advanced conflict resolution
git checkout --ours file.txt                   # Use current branch version
git checkout --theirs file.txt                 # Use incoming branch version
git add file.txt                              # Stage resolution
   ```
 ## Rebasing Advanced Techniques
```sh
  # Basic rebase operations
git rebase main                                # Rebase current branch onto main
git rebase main feature-branch                # Rebase feature-branch onto main
git rebase --onto main feature1 feature2      # Rebase feature2 onto main (was on feature1)

# Interactive rebasing (powerful editing)
git rebase -i HEAD~3                          # Interactive rebase last 3 commits
git rebase -i main                            # Interactive rebase against main

# Interactive rebase commands:
# pick (p) = use commit
# reword (r) = use commit, but edit the commit message
# edit (e) = use commit, but stop for amending
# squash (s) = use commit, but meld into previous commit
# fixup (f) = like squash, but discard this commit's message
# exec (x) = run command (the rest of the line) using shell
# break (b) = stop here (continue rebase later with 'git rebase --continue')
# drop (d) = remove commit
# label (l) = label current HEAD with a name
# reset (t) = reset HEAD to a label
# merge (m) = create a merge commit using the original message

# Rebase continuation and control
git rebase --continue                          # Continue after resolving conflicts
git rebase --skip                              # Skip current commit
git rebase --abort                             # Cancel rebase operation
git rebase --edit-todo                         # Edit the todo list during rebase

# Advanced rebase options
git rebase --preserve-merges main              # Keep merge commits
git rebase --rebase-merges main                # Recreate merge structure
git rebase -x "npm test" HEAD~5               # Run tests after each commit
git rebase --autosquash -i HEAD~10            # Auto-arrange fixup/squash commits

# Rebase with different strategies
git rebase -X ours main                        # Favor current branch in conflicts
git rebase -X theirs main                      # Favor target branch in conflicts
git rebase --strategy=resolve main             # Use resolve strategy

# Golden rule: Never rebase public/shared branches!
# Safe rebasing workflow:
git checkout feature-branch
git rebase main                                # Rebase private branch
git push --force-with-lease origin feature-branch  # Safe force push
   ```
# Remote Repository Management
## Working with Remotes
```sh
  # Remote management
git remote                                     # List remote names
git remote -v                                  # List remotes with URLs
git remote show origin                         # Detailed info about origin
git remote get-url origin                      # Get remote URL

# Adding and modifying remotes
git remote add origin https://github.com/user/repo.git
git remote add upstream https://github.com/original/repo.git
git remote rename origin old-origin            # Rename remote
git remote remove upstream                     # Remove remote
git remote set-url origin git@github.com:user/repo.git  # Change URL

# Multiple remotes for different purposes
git remote add origin git@github.com:myuser/repo.git     # Your fork
git remote add upstream git@github.com:original/repo.git # Original repo
git remote add deploy git@server.com:repo.git            # Deploy server

# Remote branch management
git remote prune origin                        # Remove stale remote branches
git remote prune origin --dry-run              # Show what would be removed
git remote update                              # Update all remote refs
git remote set-head origin -a                 # Set default branch for remote
   ```
 # Push & Pull Advanced Patterns
 ```sh
 # Basic push operations
git push                                       # Push to default upstream
git push origin main                           # Push specific branch
git push origin feature-branch                # Push feature branch
git push -u origin feature-branch             # Push and set upstream
git push --all origin                          # Push all branches
git push --tags                                # Push all tags

# Advanced push options
git push --force-with-lease                    # Safer force push
git push --force-with-lease=main:abc123        # Force with specific expected SHA
git push --force                               # Dangerous force push
git push --dry-run                             # Show what would be pushed
git push -v                                    # Verbose output

# Push specific commits or ranges
git push origin HEAD                           # Push current branch
git push origin HEAD~3:main                    # Push specific commit to main
git push origin :branch-name                   # Delete remote branch
git push origin --delete branch-name           # Delete remote branch (explicit)

# Pull operations and strategies
git pull                                       # Fetch and merge
git pull --rebase                              # Fetch and rebase
git pull --ff-only                             # Only fast-forward merges
git pull --no-commit                           # Fetch and merge but don't commit

# Advanced pull options
git pull origin main                           # Pull specific branch
git pull --all                                 # Fetch all remotes
git pull --dry-run                             # Show what would be pulled
git pull -X ours                               # Resolve conflicts favoring local
git pull -X theirs                             # Resolve conflicts favoring remote

# Fetch operations (safer than pull)
git fetch                                      # Fetch all remotes
git fetch origin                               # Fetch specific remote
git fetch origin main                          # Fetch specific branch
git fetch --all                                # Fetch all remotes
git fetch --prune                              # Remove deleted remote branches
git fetch --depth=1                            # Shallow fetch
   ```
# Fork and Upstream Workflow
```sh
# Standard fork workflow setup
git clone https://github.com/yourusername/forked-repo.git
cd forked-repo
git remote add upstream https://github.com/original/repo.git
git remote -v                                  # Verify remotes

# Keeping fork in sync
git fetch upstream                             # Get latest from upstream
git checkout main                              # Switch to main branch
git merge upstream/main                        # Merge upstream changes
git push origin main                           # Update your fork

# Alternative: rebase instead of merge
git fetch upstream
git checkout main
git rebase upstream/main
git push --force-with-lease origin main

# Working on features in fork
git checkout -b new-feature upstream/main      # Create feature branch from upstream
# Make changes and commit
git push -u origin new-feature                 # Push feature branch to fork
# Create pull request through GitHub interface

# Cleanup after PR merge
git checkout main
git pull upstream main                         # Get merged changes
git branch -d new-feature                      # Delete local feature branch
git push origin --delete new-feature          # Delete remote feature branch
   ```
# Advanced Git Operations
## Stashing & Temporary Storage
```sh
   # Basic stashing
git stash                                      # Stash current changes
git stash save "Work in progress on feature X" # Stash with message
git stash -u                                   # Include untracked files
git stash -a                                   # Include all files (even ignored)
git stash -k                                   # Keep staged changes in index
git stash --include-untracked                  # Long form of -u

# Advanced stashing options
git stash -p                                   # Interactive stashing
git stash --patch                              # Same as -p
git stash branch feature-branch                # Create branch from stash

# Managing stashes
git stash list                                 # Show all stashes
git stash show                                 # Show latest stash diff
git stash show -p                              # Show detailed diff
git stash show stash@{2}                       # Show specific stash
git stash show --stat stash@{1}                # Show change statistics

# Applying and removing stashes
git stash apply                                # Apply latest stash (keep in stash list)
git stash apply stash@{2}                      # Apply specific stash
git stash pop                                  # Apply latest stash and remove from list
git stash pop stash@{1}                        # Pop specific stash
git stash drop                                 # Delete latest stash
git stash drop stash@{2}                       # Delete specific stash
git stash clear                                # Delete all stashes

# Stash advanced workflows
git stash branch new-branch stash@{1}          # Create branch from stash
git stash create                               # Create stash object without storing
git stash store -m "message" <stash-sha>       # Store stash object
   ```
## Reset, Revert & History Manipulation
```sh
  # Reset operations (DANGEROUS - changes history)
git reset --soft HEAD~1                       # Undo commit, keep changes staged
git reset HEAD~1                               # Undo commit, unstage changes (default --mixed)
git reset --mixed HEAD~1                      # Same as above (explicit)
git reset --hard HEAD~1                       # Undo commit, discard all changes
git reset --hard origin/main                  # Reset to match remote exactly

# Reset to specific commit
git reset --hard abc1234                      # Reset to specific commit
git reset --hard HEAD@{2}                     # Reset using reflog

# Selective reset
git reset HEAD -- file.txt                    # Unstage specific file
git reset --patch                              # Interactive reset

# Revert operations (SAFE - creates new commits)
git revert HEAD                                # Revert last commit
git revert HEAD~1                              # Revert specific commit
git revert abc1234                             # Revert commit by hash
git revert HEAD~3..HEAD                        # Revert range of commits
git revert -m 1 merge-commit-hash              # Revert merge commit

# Advanced revert options
git revert --no-commit HEAD~3..HEAD            # Revert multiple commits without committing
git revert --no-edit HEAD                      # Revert without opening editor
git revert --strategy=recursive -X theirs HEAD # Revert with merge strategy

# Clean operations
git clean -n                                   # Dry run - show what would be deleted
git clean -f                                   # Delete untracked files
git clean -fd                                  # Delete untracked files and directories
git clean -fx                                  # Delete ignored files too
git clean -i                                   # Interactive cleaning

# Reflog - safety net for lost commits
git reflog                                     # Show reference log
git reflog show HEAD                           # Show HEAD changes
git reflog show main                           # Show branch changes
git reflog expire --expire=90.days refs/heads/main # Expire old reflog entries

# Recovering lost commits
git reflog                                     # Find lost commit hash
git cherry-pick abc1234                       # Recover specific commit
git merge abc1234                              # Recover as merge
git reset --hard abc1234                      # Reset to lost commit
   ```
# Cherry-picking & Patch Management
```sh
  # Basic cherry-picking
git cherry-pick commit-hash                    # Apply specific commit
git cherry-pick HEAD~3                         # Cherry-pick by relative reference
git cherry-pick feature-branch                 # Cherry-pick branch HEAD

# Cherry-pick ranges and multiple commits
git cherry-pick commit1..commit3               # Range (exclusive start)
git cherry-pick commit1^..commit3              # Range (inclusive start)
git cherry-pick commit1 commit2 commit3        # Multiple specific commits

# Advanced cherry-pick options
git cherry-pick --no-commit commit-hash        # Apply without committing
git cherry-pick -x commit-hash                 # Add source commit reference
git cherry-pick -s commit-hash                 # Add signed-off-by line
git cherry-pick -e commit-hash                 # Edit commit message

# Cherry-pick with merge resolution
git cherry-pick -m 1 merge-commit-hash         # Cherry-pick merge commit (parent 1)
git cherry-pick -X ours commit-hash            # Favor current branch in conflicts
git cherry-pick -X theirs commit-hash          # Favor cherry-picked commit in conflicts

# Cherry-pick continuation and control
git cherry-pick --continue                     # Continue after resolving conflicts
git cherry-pick --abort                        # Abort cherry-pick operation
git cherry-pick --skip                         # Skip current commit
git cherry-pick --quit                         # Exit cherry-pick mode

# Creating and applying patches
git format-patch HEAD~3                        # Create patches for last 3 commits
git format-patch HEAD~3 --output-directory patches/ # Save to directory
git format-patch main..feature                 # Create patches for branch diff

# Applying patches
git apply patch.patch                          # Apply patch (no commit)
git apply --check patch.patch                  # Check if patch applies cleanly
git apply --3way patch.patch                   # Apply with 3-way merge
git am patch.patch                             # Apply patch with commit (from format-patch)
git am --3way patch.patch                      # Apply with 3-way merge
   ```
# Tagging & Release Management
## Tag Creation & Management
```sh
  # Lightweight tags (simple pointer to commit)
git tag v1.0                                   # Tag current commit
git tag v1.0.1 HEAD~2                          # Tag specific commit
git tag experimental                           # Development tag

# Annotated tags (recommended for releases)
git tag -a v1.0.0 -m "Version 1.0.0 release"  # Create annotated tag
git tag -a v1.0.0 -m "Release version 1.0.0" commit-hash # Tag specific commit
git tag -a v2.0.0-beta -m "Beta release"       # Pre-release tag

# GPG signed tags (for security)
git tag -s v1.0.0 -m "Signed release v1.0.0"  # Create signed tag
git tag -v v1.0.0                              # Verify signed tag

# Listing and inspecting tags
git tag                                        # List all tags
git tag -l "v1.*"                              # List tags matching pattern
git tag -l --sort=-version:refname             # Sort by version
git tag -l --sort=-creatordate                 # Sort by creation date
git tag -n                                     # Show tag messages
git tag -n5                                    # Show first 5 lines of tag messages

# Tag information
git show v1.0.0                                # Show tag and commit info
git show --name-only v1.0.0                    # Show files in tagged commit
git describe                                   # Describe current commit with tag
git describe --tags                            # Include lightweight tags
git describe --abbrev=0                        # Only tag name
git describe --match "v*"                      # Match specific pattern

# Managing tags
git tag -d v1.0.0                              # Delete local tag
git push origin :v1.0.0                        # Delete remote tag
git push origin --delete v1.0.0                # Delete remote tag (explicit)
git push origin v1.0.0                         # Push specific tag
git push --tags                                # Push all tags
git push --follow-tags                         # Push tags along with commits

# Tag-based operations
git checkout v1.0.0                            # Checkout specific tag (detached HEAD)
git checkout -b hotfix-v1.0.1 v1.0.0          # Create branch from tag
git archive --format=zip --prefix=project-v1.0.0/ v1.0.0 > project-v1.0.0.zip
   ```
# Release Workflow Patterns
```sh
  # Semantic versioning workflow
# MAJOR.MINOR.PATCH (1.2.3)
# MAJOR: incompatible API changes
# MINOR: backwards-compatible functionality
# PATCH: backwards-compatible bug fixes

# Release preparation
git checkout main
git pull origin main
git checkout -b release/v1.2.0                 # Create release branch

# Update version numbers, changelog, etc.
# Commit preparation changes
git commit -am "Prepare release v1.2.0"

# Create release tag
git tag -a v1.2.0 -m "Release version 1.2.0

Features:
- Added user authentication
- Improved error handling

Bug fixes:
- Fixed login redirect issue
- Resolved memory leak in parser

Breaking changes:
- API endpoint /users now requires authentication"

# Push release
git push origin release/v1.2.0
git push origin v1.2.0

# Merge back to main and develop
git checkout main
git merge release/v1.2.0
git push origin main

git checkout develop
git merge release/v1.2.0
git push origin develop

# Cleanup
git branch -d release/v1.2.0
git push origin --delete release/v1.2.0

# Hotfix workflow
git checkout main
git checkout -b hotfix/v1.2.1 v1.2.0           # Branch from release tag
# Fix critical bug
git commit -am "Fix critical security vulnerability"
git tag -a v1.2.1 -m "Hotfix release v1.2.1"
git push origin hotfix/v1.2.1
git push origin v1.2.1

# Merge hotfix
git checkout main
git merge hotfix/v1.2.1
git checkout develop
git merge hotfix/v1.2.1
git push origin main develop
   ```
# GitHub Specific Features
## GitHub CLI (gh) Mastery
```sh
# Installation and setup
gh --version                                   # Check version
gh auth login                                  # Authenticate with GitHub
gh auth status                                 # Check authentication status
gh auth logout                                 # Logout
gh config set editor vim                       # Set preferred editor

# Repository operations
gh repo create my-new-repo                     # Create repository
gh repo create my-org/repo-name --public       # Create in organization
gh repo create --private                       # Create private repo
gh repo clone user/repo                        # Clone repository
gh repo fork user/repo                         # Fork repository
gh repo view                                   # View current repository
gh repo view user/repo                         # View specific repository
gh repo delete user/repo                       # Delete repository (careful!)

# Advanced repository operations
gh repo create my-repo --template user/template-repo # From template
gh repo create my-repo --gitignore Node --license MIT # With gitignore and license
gh repo rename new-name                        # Rename repository
gh repo edit --description "New description"   # Edit repository settings
gh repo sync                                   # Sync fork with upstream

# Issues management
gh issue list                                  # List issues
gh issue list --state closed                   # List closed issues
gh issue list --assignee @me                   # Issues assigned to you
gh issue list --author user                    # Issues by specific author
gh issue list --label bug                      # Issues with specific label

# Create and manage issues
gh issue create --title "Bug report" --body "Description of bug"
gh issue create --template bug_report.md       # Use issue template
gh issue view 123                              # View specific issue
gh issue edit 123                              # Edit issue
gh issue close 123                             # Close issue
gh issue reopen 123                            # Reopen issue
gh issue comment 123 --body "Additional info"  # Add comment

# Pull request operations
gh pr list                                     # List pull requests
gh pr list --state closed                      # List closed PRs
gh pr list --author @me                        # Your pull requests
gh pr list --assignee user                     # PRs assigned to user

# Create pull requests
gh pr create                                   # Interactive PR creation
gh pr create --title "Feature: New login" --body "Implements new login system"
gh pr create --draft                           # Create draft PR
gh pr create --base develop --head feature     # Specify base and head branches

# Manage pull requests
gh pr view 123                                 # View PR details
gh pr checkout 123                             # Checkout PR locally
gh pr diff 123                                 # Show PR diff
gh pr merge 123                                # Merge PR
gh pr merge 123 --squash                       # Squash merge
gh pr merge 123 --rebase                       # Rebase merge
gh pr close 123                                # Close PR without merging

# Pull request reviews
gh pr review 123                               # Start interactive review
gh pr review 123 --approve                     # Approve PR
gh pr review 123 --request-changes -b "Needs fixes" # Request changes
gh pr review 123 --comment -b "Looks good"     # Add review comment

# Advanced GitHub operations
gh workflow list                               # List GitHub Actions workflows
gh workflow run workflow-name                  # Trigger workflow
gh run list                                    # List workflow runs
gh run view 123456789                          # View specific run
gh run watch                                   # Watch current run

# GitHub releases
gh release list                                # List releases
gh release view v1.0.0                         # View specific release
gh release create v1.0.0                       # Create release
gh release create v1.0.0 --notes "Release notes" --title "Version 1.0.0"
gh release upload v1.0.0 dist/*                # Upload assets to release
gh release delete v1.0.0                       # Delete release

# GitHub Pages
gh repo view --web                             # Open repo in browser
gh browse                                      # Open current repo in browser
gh browse issues                               # Open issues page
gh browse pulls                                # Open pull requests page
   ```
# GitHub Actions Integration
```sh
   # Managing GitHub Actions from CLI
gh workflow list                               # List all workflows
gh workflow view                               # View workflow details
gh workflow run ci.yml                         # Trigger specific workflow
gh workflow run ci.yml -f environment=production # With inputs

# Monitoring workflow runs
gh run list                                    # List recent runs
gh run list --workflow=ci.yml                  # Runs for specific workflow
gh run view                                    # View latest run
gh run view 123456789                          # View specific run
gh run watch                                   # Watch current run in real-time
gh run download 123456789                      # Download run artifacts

# Workflow file examples (.github/workflows/ci.yml)
name: CI
on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - uses: actions/setup-node@v3
      with:
        node-version: '18'
        cache: 'npm'
    - run: npm ci
    - run: npm test
    - run: npm run build

# Repository secrets management (through web interface)
gh secret list                                # List repository secrets
gh secret set SECRET_NAME                     # Set secret (will prompt for value)
gh secret delete SECRET_NAME                  # Delete secret
   ```
# Git Workflows & Branching Strategies
## Git Flow Workflow
```sh
   # Git Flow branch structure:
# - main: production-ready code
# - develop: integration branch for features
# - feature/*: feature development
# - release/*: release preparation
# - hotfix/*: production fixes

# Initialize Git Flow (optional git-flow extension)
git flow init                                  # Interactive setup

# Feature development workflow
git checkout develop
git pull origin develop
git checkout -b feature/user-authentication
# Develop feature...
git add .
git commit -m "Add user authentication system"
git push -u origin feature/user-authentication

# Create pull request to develop branch
gh pr create --base develop --title "Feature: User Authentication"

# After PR approval and merge
git checkout develop
git pull origin develop
git branch -d feature/user-authentication
git push origin --delete feature/user-authentication

# Release workflow
git checkout develop
git pull origin develop
git checkout -b release/1.2.0
# Update version numbers, documentation
git commit -am "Bump version to 1.2.0"
git push -u origin release/1.2.0

# After testing and fixes in release branch
git checkout main
git merge release/1.2.0
git tag -a v1.2.0 -m "Release version 1.2.0"
git push origin main --tags

git checkout develop
git merge release/1.2.0
git push origin develop

git branch -d release/1.2.0
git push origin --delete release/1.2.0

# Hotfix workflow
git checkout main
git checkout -b hotfix/1.2.1
# Fix critical issue
git commit -am "Fix critical security bug"
git checkout main
git merge hotfix/1.2.1
git tag -a v1.2.1 -m "Hotfix version 1.2.1"
git push origin main --tags

git checkout develop
git merge hotfix/1.2.1
git push origin develop

git branch -d hotfix/1.2.1
   ```
# GitHub Flow (Simplified)
```sh
  # GitHub Flow is simpler: main branch + feature branches + pull requests

# Start new feature
git checkout main
git pull origin main
git checkout -b feature/improve-search

# Develop and commit frequently
git add search.js
git commit -m "Improve search algorithm performance"
git push -u origin feature/improve-search

# Create pull request early (can be draft)
gh pr create --draft --title "Improve search performance"

# Continue development
git add tests/search.test.js
git commit -m "Add tests for search improvements"
git push

# Mark PR as ready for review
gh pr ready

# After review and approval
gh pr merge --squash                           # Squash merge to main

# Cleanup
git checkout main
git pull origin main
git branch -d feature/improve-search
   ```
# Team Collaboration Patterns
```sh
   # Code review workflow
# 1. Create feature branch
git checkout -b feature/new-api-endpoint

# 2. Develop and push regularly
git add .
git commit -m "Add new API endpoint structure"
git push -u origin feature/new-api-endpoint

# 3. Create PR for early feedback
gh pr create --draft --title "WIP: New API endpoint"

# 4. Address feedback and update
git add .
git commit -m "Address review feedback - add validation"
git push

# 5. Request final review
gh pr ready
gh pr review --request-changes # If you're reviewing others' code

# Handling merge conflicts in PRs
git checkout feature/my-feature
git fetch origin
git merge origin/main                          # Or rebase: git rebase origin/main
# Resolve conflicts
git add .
git commit -m "Resolve merge conflicts with main"
git push

# Collaborative feature development
# Developer A creates feature branch
git checkout -b feature/shared-component
git push -u origin feature/shared-component

# Developer B joins development
git fetch origin
git checkout feature/shared-component
# Make changes
git commit -am "Add styling to shared component"
git push

# Synchronizing work
git pull --rebase                              # Keep linear history
# Or
git pull                                       # Create merge commit
   ```
# Advanced Git Configuration & Optimization
## Git Hooks & Automation
```sh
  # Git hooks are scripts in .git/hooks/ directory
# Common hooks: pre-commit, pre-push, post-merge, prepare-commit-msg

# Pre-commit hook example (.git/hooks/pre-commit)
#!/bin/sh
# Run tests before commit
npm test
if [ $? -ne 0 ]; then
    echo "Tests failed. Commit aborted."
    exit 1
fi

# Run linter
npm run lint
if [ $? -ne 0 ]; then
    echo "Linting failed. Commit aborted."
    exit 1
fi

echo "Pre-commit checks passed."

# Make hook executable
chmod +x .git/hooks/pre-commit

# Pre-push hook example (.git/hooks/pre-push)
#!/bin/sh
protected_branch='main'
current_branch=$(git symbolic-ref HEAD | sed -e 's,.*/\(.*\),\1,')

if [ $protected_branch = $current_branch ]; then
    echo "Direct push to main branch is not allowed"
    exit 1
fi

# Commit message hook (.git/hooks/prepare-commit-msg)
#!/bin/sh
# Add branch name to commit message
branch_name=$(git symbolic-ref --short HEAD)
if [ -n "$branch_name" ] && [ "$branch_name" != "main" ] && [ "$branch_name" != "develop" ]; then
    echo "[$branch_name] $(cat $1)" > $1
fi

# Global git hooks (Git 2.9+)
git config --global core.hooksPath ~/.git-hooks

# Using tools like husky for JavaScript projects
npm install --save-dev husky
npx husky install
npx husky add .husky/pre-commit "npm test"
npx husky add .husky/pre-push "npm run build"
   ```
# Performance Optimization
```sh
# Git configuration for better performance
git config --global core.preloadindex true    # Preload index
git config --global core.fscache true         # File system cache (Windows)
git config --global gc.auto 256               # Garbage collection trigger

# Repository maintenance
git gc                                         # Garbage collection
git gc --aggressive                            # Aggressive optimization
git gc --prune=now                             # Remove unreachable objects immediately
git repack -ad                                 # Repack repository
git count-objects -v                           # Show repository statistics

# Large repository optimization
git config core.preloadindex true             # Per-repo optimization
git config core.untrackedCache true           # Cache untracked files
git config status.submoduleSummary true       # Submodule status summary

# Partial clone for large repositories (Git 2.19+)
git clone --filter=blob:limit=1m <url>        # Skip large files initially
git clone --filter=tree:0 <url>               # Skip trees, fetch on demand

# Working with large files (Git LFS)
git lfs install                                # Install LFS globally
git lfs track "*.psd"                          # Track Photoshop files
git lfs track "*.mp4"                          # Track video files
git add .gitattributes                         # Commit LFS configuration
git lfs ls-files                               # List tracked files
git lfs migrate import --include="*.zip"       # Migrate existing files to LFS

# Optimizing git log performance
git config --global log.abbrevCommit true     # Shorter commit hashes
git config --global log.decorate auto         # Auto decoration
git config --global alias.lg "log --oneline --graph --decorate --all"
   ```
# Security & Best Practices
```sh
   # GPG signing setup
gpg --gen-key                                  # Generate GPG key
gpg --list-secret-keys --keyid-format LONG    # List keys
git config --global user.signingkey KEY_ID    # Set signing key
git config --global commit.gpgsign true       # Sign all commits
git config --global tag.gpgSign true          # Sign all tags

# SSH key setup for GitHub
ssh-keygen -t ed25519 -C "your.email@example.com" # Generate SSH key
eval "$(ssh-agent -s)"                        # Start ssh-agent
ssh-add ~/.ssh/id_ed25519                      # Add key to agent
# Add public key to GitHub account

# Security-focused configuration
git config --global credential.helper manager # Secure credential storage
git config --global http.sslverify true       # Verify SSL certificates
git config --global transfer.fsckobjects true # Check objects on transfer
git config --global fetch.fsckobjects true    # Check objects on fetch

# Protecting sensitive data
# Create .gitignore for sensitive files
echo "*.env" >> .gitignore
echo "config/database.yml" >> .gitignore
echo "*.log" >> .gitignore
echo "node_modules/" >> .gitignore

# Global .gitignore
git config --global core.excludesfile ~/.gitignore_global

# Example ~/.gitignore_global
# OS generated files
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db

# IDE files
.vscode/
.idea/
*.swp
*.swo

# Removing sensitive data from history (DANGEROUS)
git filter-branch --force --index-filter \
'git rm --cached --ignore-unmatch secrets.txt' \
--prune-empty --tag-name-filter cat -- --all

# Alternative: using BFG Repo-Cleaner (recommended)
java -jar bfg.jar --delete-files secrets.txt my-repo.git
   ```

## Key Areas Covered in this cheatsheet :-
## Git Fundamentals: Configuration, initialization, basic operations
## Core Operations: Staging, committing, viewing history with advanced options
## Branching & Merging: Advanced branch management and conflict resolution
## Remote Management: Working with remotes, push/pull strategies, fork workflows
## Advanced Operations: Stashing, reset/revert, cherry-picking, patch management
## Tagging & Releases: Version management and release workflows
## GitHub Features: GitHub CLI mastery, Actions integration, collaboration
## Workflows: Git Flow, GitHub Flow, team collaboration patterns
## Configuration: Hooks, automation, performance optimization
## Security: GPG signing, SSH setup, protecting sensitive data
