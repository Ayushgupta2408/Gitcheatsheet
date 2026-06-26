## Gitcheatsheet
# Git Fundamentals & Configuration
# Initial Setup & Global Configuration
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
