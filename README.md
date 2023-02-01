# Day 2 - Git |Configuration |Usage

Created: January 31, 2023 8:48 AM
Last Edited Time: February 1, 2023 2:24 AM
Status: completed
Type: cheat-sheet

# **Git**

Git is a free, open-source distributed version control system used for tracking changes in source code during development. It allows multiple people to collaborate on the same codebase and keeps a history of changes, making it easy to revert to previous versions.

## Configuration of Git

### To add username

```bash
git config --global [user.name](http://user.name) “name”
```

### To set email

```bash
 git config --global [user.email](http://user.email) your_email
```

### To set the default editor

```bash
git config --global core.editor "code --wait"
```

### To edit the setting file using defualt editor

```bash
git config --global -e
```

### To configure git to handle “end of lines” for windows user users :

cr = carriage return

lf = line feed

```bash
git config --global core.autocrlf true
```

### To configure git to handle “end of lines” for mac/linux user users :

```bash
git config --global core.autocrlf input
```

# Using Git

## Initializing a repository

```bash
git init 
```

## Staging files

```bash
git add filename        # stages a single file
git add file1 file2     # Stages multiple files
git add *.txt           # Stages with a pattern
git add .               # Stages the current directory and all its content
```

## Viewing the status

```bash
git status              # Full status
git status -s           # Short status
```

## Committing the staged files

```bash
git commit -m “Message” # Commits with a one-line message 
git commit              # Opens the default editor to type a long message
```

## Skipping the staging area

```bash
git commit -am “Message”
```

## Removing files

```bash
git rm file1.js          # Removes from working directory and staging area
git rm --cached file1.js # Removes from staging area only
```

## Renaming or moving files

```bash
git mv file1.js file1.txt
```

## Viewing the staged/unstaged changes

```bash
git diff                  # Shows unstaged changes
git diff --staged         # Shows staged changes
git diff --cached         # Same as the above
```

## Viewing the history

```bash
git log                    # Full history
git log --oneline          # Summary
git log --reverse          # Lists the commits from the oldest to the newest
```

## Viewing a commit

```bash
git show 921a2ff            # Shows the given commit
git show HEAD               # Shows the last commit
git show HEAD~2             # Two steps before the last commit
git show HEAD:file.js       # Shows the version of file.js stored in the last commit
```

## Un staging files (undoing git add)

```bash
git restore --staged file.js  # Copies the last version of file.js from repo to index
```

## Discarding local changes

```bash
git restore file.js             # Copies file.js from index to working directory
git restore file1.js file2.js   # Restores multiple files in working directory
git restore .                   # Discards all local changes (except untracked files)
git clean -fd                   # Removes all untracked files
```

## Restoring an earlier version of a file

```bash

git restore --source=HEAD~2 file.js
```

## Branching & Merging

### Managing branches

```bash
git branch bugfix               # Creates a new branch called bugfix
git checkout bugfix             # Switches to the bugfix branch
git switch bugfix               # Same as the above
git switch -C bugfix            # Creates and switches
git branch -d bugfix            # Deletes the bugfix branch
```

### Comparing branches

```bash
git log master..bugfix           # Lists the commits in the bugfix branch not in master
git diff master..bugfix          # Shows the summary of changes
```

### Stashing

```bash
git stash push -m “New tax rules” # Creates a new stash
git stash list                  # Lists all the stashes
git stash show stash@{1}        # Shows the given stash
git stash show 1                # shortcut for stash@{1}
git stash apply 1               # Applies the given stash to the working dir
git stash drop 1                # Deletes the given stash
git stash clear                 # Deletes all the stashes
```

### Merging

```bash
git merge bugfix                 # Merges the bugfix branch into the current branch
git merge --no-ff bugfix         # Creates a merge commit even if FF is possible
git merge --squash bugfix        # Performs a squash merge
git merge --abort                # Aborts the merge
```

### Viewing the merged branches

```bash
git branch --merged              # Shows the merged branches
git branch --no-merged           # Shows the unmerged branches
```

### Rebasing

```bash
git rebase master               # Changes the base of the current branch
```

### Cherry picking

```bash
git cherry-pick dad47ed         # Applies the given commit on the current branch
```

## Collaboration

### Cloning a repository

```bash
git clone url
```

### Syncing with remotes

```bash
git fetch origin master           # Fetches master from origin
git fetch origin                  # Fetches all objects from origin
git fetch                         # Shortcut for “git fetch origin”
git pull                          # Fetch + merge
git push origin master            # Pushes master to origin
git push                          # Shortcut for “git push origin master”
```

### Sharing tags

```bash
git push origin v1.0              # Pushes tag v1.0 to origin
git push origin —delete v1.0
```

### Sharing branches

```bash
git branch -r                     # Shows remote tracking branches
git branch -vv                    # Shows local & remote tracking branches
git push -u origin bugfix         # Pushes bugfix to origin
git push -d origin bugfix         # Removes bugfix from origin
```

### Managing remotes

```bash
git remote                        # Shows remote repos
git remote add upstream url       # Adds a new remote called upstream
git remote rm upstream            # Remotes upstream
```

## Rewriting History

### Undoing commits

```bash
git reset --soft HEAD^            # Removes the last commit, keeps changed staged
git reset --mixed HEAD^           # Unstages the changes as well
git reset --hard HEAD^            # Discards local changes
```

### Reverting commits

```bash
git revert 72856ea                # Reverts the given commit
git revert HEAD~3..               # Reverts the last three commits
git revert --no-commit HEAD~3..
```

### Recovering lost commits

```bash
git reflog                        # Shows the history of HEAD
git reflog show bugfix            # Shows the history of bugfix pointer
```

### Amending the last commit

```bash
git commit --amend
```

### Interactive rebasing

```bash
git rebase -i HEAD~5
```
