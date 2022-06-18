# Git Handbook <!-- omit in toc -->

## Table of Contents <!-- omit in toc -->

- [References](#references)
- [Git basics](#git-basics)
	- [What is Git?](#what-is-git)
	- [Three main components of a Git Project](#three-main-components-of-a-git-project)
- [Initializing a project](#initializing-a-project)
	- [New repository (Empty repo)](#new-repository-empty-repo)
	- [Clone a project](#clone-a-project)
- [Basic commands](#basic-commands)
	- [Git add](#git-add)
	- [Git ignore](#git-ignore)
	- [Git commit](#git-commit)
	- [Git status](#git-status)
	- [Git diff](#git-diff)
	- [Git log](#git-log)
	- [Git alias](#git-alias)
- [Branch](#branch)
	- [Create a new branch](#create-a-new-branch)
	- [Upstream branch](#upstream-branch)
	- [Show branches](#show-branches)
	- [Switch between branches](#switch-between-branches)
	- [Delete a branch](#delete-a-branch)
- [Tag](#tag)
	- [Create a tag](#create-a-tag)
	- [List tags](#list-tags)
	- [Check out a tag](#check-out-a-tag)
	- [Delete a tag](#delete-a-tag)
- [Some more important commands](#some-more-important-commands)
	- [Checkout specified commit](#checkout-specified-commit)
	- [Git reset: undo git add](#git-reset-undo-git-add)
	- [Git reset --hard](#git-reset---hard)
	- [Git push](#git-push)
	- [Git fetch](#git-fetch)
	- [Git pull](#git-pull)
	- [Git merge](#git-merge)
	- [Git rebase](#git-rebase)
- [Multiple Remotes](#multiple-remotes)
	- [Add new remotes](#add-new-remotes)
	- [Fetch remotes](#fetch-remotes)
- [Some other commands](#some-other-commands)
	- [Git stash](#git-stash)
	- [Git commit --amend](#git-commit---amend)
	- [Git merge --squash](#git-merge---squash)
	- [Git cherry pick](#git-cherry-pick)

## References

- <https://git-scm.com/book/en/v2/>
- <https://stackoverflow.com/>
- <https://stackoverflow.com/questions/804115/when-do-you-use-git-rebase-instead-of-git-merge>
- <https://support.nesi.org.nz/hc/en-gb/articles/360001508515-Git-Reference-Sheet/>
- <https://ma.ttias.be/pretty-git-log-in-one-line/>
- <https://www.atlassian.com/git/tutorials/>
- <https://www.w3schools.com/git/git_ignore.asp?remote=github>
- <https://www.edureka.co/blog/git-rebase-vs-merge>
- <https://www.freecodecamp.org/news/git-diff-command/>
- <https://www.youtube.com/watch?v=MyvyqdQ3OjI>
- <https://www.youtube.com/watch?v=wIY824wWpu4>

## Git basics

### What is Git?

Git is a distributed version control system for managing source code.

Version control is a system for tracking changes to files. As you modify files, the version control system records and saves each change. This allows you to restore a previous version of your code at any time.

In short, a version control system like Git makes it easy to:

- Keep track of code history
- Collaborate on code as a team
- See who made which changes
- Deploy code to staging or production

[Click here to install git](https://git-scm.com/downloads)

### Three main components of a Git Project

The repository, or repo, is the “container” that tracks the changes to your project files. It holds all of the commits — a snapshot of all your files at a point in time — that have been made.

- The local repository is a Git repository that is stored on your computer
- The remote repository is a Git repository that is stored on some remote computer

The working tree, or working directory, consists of files that you are currently working on. You can think of a working tree as a file system where you can view and modify files.

The index, or staging area, is where commits are prepared. The index compares the files in the working tree to the files in the local repository. When you make a change, the index marks the file as modified before it is committed.

![Git diagram](./images/Git%20Diagram.svg)

## Initializing a project

### New repository (Empty repo)

```bash
echo "# Describe your project" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin <repo_git>
git push -u origin main
```

### Clone a project

```bash
git clone <repo_git>
# Ex: git clone https://github.com/dev-tronghieu/git-handbook.git
```

## Basic commands

### Git add

```bash
# Working directory -> Staging area
git add .                        # add all the changes
git add <specified_file/folder>  # add specified changes
```

### [Git ignore](https://git-scm.com/docs/gitignore)

When sharing your code with others, there are often files or parts of your project, you do not want to share.

- log files
- temporary files
- hidden files
- personal files
- etc.

A `.gitignore` file **in the root of your local repo** specifies intentionally untracked files that Git should ignore. Files already tracked by Git are not affected.

```gitignore
# Example
# Ignore some personal files/ folders
.vs/
.vscode/

# Ignore all .log files
*.log

# Ignore any files in any directory named temp
temp/
```

### Git commit

```bash
# Staging area -> Local repository
git commit -m "title (must have)" -m "body (optional)"
```

It's time to learn git objects: <https://www.youtube.com/watch?v=MyvyqdQ3OjI>

### Git status

```bash
git status
git status -s # short format
```

In the [short-format](https://git-scm.com/docs/git-status#_short_format), the status of each path is shown as one of these forms

```txt
XY PATH
XY ORIG_PATH -> PATH
```

where `ORIG_PATH` is where the renamed/copied contents came from. `ORIG_PATH` is only shown when the entry is renamed or copied. The `XY` is a two-letter status code.

There are three different types of states that are shown using this format, and each one uses the `XY` syntax differently:

- When a merge is occurring and the merge was successful, or outside of a merge situation, `X` shows the status of the index and `Y` shows the status of the working tree.
- When a merge conflict has occurred and has not yet been resolved, `X` and `Y` show the state introduced by each head of the merge, relative to the common ancestor. These paths are said to be unmerged.
- When a path is untracked, `X` and `Y` are always the same, since they are unknown to the index. `??` is used for untracked paths. Ignored files are not listed unless --ignored is used; if it is, ignored files are indicated by `!!`.

Status:

- `' '` = unmodified
- `M` = modified
- `T` = file type changed (regular file, symbolic link or submodule)
- `A` = added
- `D` = deleted
- `R` = renamed
- `C` = copied
- `U` = updated but unmerged

### [Git diff](https://www.freecodecamp.org/news/git-diff-command/)

```bash
git diff
```

### Git log

```bash
# The standard output isn’t very terminal-friendly
git log        

# Less space, but missing crucial information like the date of the commit
git log --oneline

# A better git log command is
git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit
```

To make life easier, we can add a `git alias` so we don't have to remember the entire syntax.

```bash
git config --global alias.lo "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
git lo
```

### Git alias

If you don’t want to type the entire text of each of the Git commands, you can easily set up an `alias` for each command using git config.

Here are a couple of examples you may want to set up:

```bash
git config --global alias.co checkout
git config --global alias.st status

git config --global alias.cm "commit -m"
git config --global alias.lo "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

To unset an alias, use

```bash
# Unset a specified alias
git config --global --unset alias.<alias_name>

# Remove all aliases
git config --global --remove-section alias
```

## Branch

Learn how branches work: <https://www.youtube.com/watch?v=mhZQRBp8dXE>

### Create a new branch

```bash
git branch <branch>      # create a new branch
git branch -M <branch>   # create and switch to the new branch

# Create new branch from commit
git branch <branch> <commit_hash>
```

### Upstream branch

Upstream branch is the branch you can fetch, pull or push without arguments

```bash
# Set upstream branch
git push -u origin <branch>                     # method 1
git branch --set-upstream-to origin/<branch>    # method 2
git branch -u origin/<branch>  # short form

# Unset upstream branch
git branch --unset-upstream <branch>
```

### Show branches

```bash
# Show local branches
git branch

# Show remote branches
git branch --remote
git branch -r  # short form

# Show all branches
git branch --all
git branch -a  # short form
```

### Switch between branches

```bash
git switch <branch>
git checkout <branch>  # another method

git switch - # switch to the previous branch
```

### Delete a branch

```bash
# Delete a fully merged branch or in HEAD if no upstream was set
git branch --delete <branch>
git branch -d <branch>  # short form

# Delete the branch even if it is not merged
git branch -D <branch>

# Delete remote branch
git push -d origin <branch>
```

## Tag

### Create a tag

```bash
# Create an annotated tag
git tag -a <tag> -m "Tag message"
# Ex: git tag -a v1.0 -m "My version 1.0 message"

# Create a lightweight tag
git tag <tag>
# Ex: git tag v1.0-lw

# See the tag data
git show <tag>
# Ex: git show v1.0

# Push your tag
git push origin <tag>
# Ex: git push origin v1.0
```

### List tags

```bash
# List the tags in alphabetical order
git tag
git tag -l
git tag --list

# Search for tags that match a particular pattern
git tag -l "your_pattern"
# Ex: git tag -l "v1.8.5*"
# >> v1.8.5
# >> v1.8.5.1
# >> v1.8.5.2
```

### Check out a tag

```bash
git checkout <tag>
```

### Delete a tag

```bash
# Delete local tag
git tag -d <tag>

# Delete remote tag
git push -d origin <tag>
```

## Some more important commands

### Checkout specified commit

```bash
# Use git log to search for the desired commit hash
git log

# Checkout specified commit
git checkout <commit_hash>
# HEAD pointer will point to this commit
```

### Git reset: undo git add

```bash
git reset
git reset <specified_file/folder>
```

### [Git reset --hard](https://www.atlassian.com/git/tutorials/undoing-changes/git-reset)

This is the most direct, **DANGEROUS**, and frequently used option of `git reset`

- The Commit History ref pointers are updated to the specified commit
- The Staging Index and Working Directory are reset to match that of the specified commit
- Any previously pending changes to the Staging Index and the Working Directory gets reset to match the state of the Commit Tree

This means any pending work that was hanging out in the Staging Index and Working Directory will be lost.

```bash
# Reset your branch to specified commit
git reset --hard <commit_hash>

# Rollback to n commits back
git reset --hard HEAD~n
# Ex: git reset --hard HEAD~10
```

### Git push

```bash
# Local repository -> Remote repository

# Push to an upstream branch
git push

# Push to a specified remote branch
git push origin <branch>

# Push to all remote branches
git push --all origin

# Overwrite (replace) remote branch
git push -f origin <branch>

# Use git push to delete a remote branch
git push -d origin <branch>
```

If you "failed to push some refs", the error message states that a pushed branch is behind its remote. To fix this, you need to pull the latest changes from your remote branch.

### Git fetch

The `git fetch` command downloads commits, files, and refs from a remote repository into your local repo. Fetching is what you do when you want to see what everybody else has been working on.

When downloading content from a remote repo, `git pull` and `git fetch` commands are available to accomplish the task. You can consider git fetch the 'safe' version of the two commands.

- `git fetch` will download the remote content but not update your local repo's working state, leaving your current work intact
- `git pull`  is the more aggressive alternative; it will download the remote content for the active local branch and immediately execute `git merge` to create a merge commit for the new remote content

![Git fetch & Git pull](images/fetch-pull.png)

```bash
# Fetch all of the branches from this remote
git fetch <remote>

# Fetch a specified branch
git fetch <remote> <branch>

# Fetch all
git fetch --all

# You can apply the 'reset --hard' here
git reset --hard <remote>/<branch>
```

### Git pull

The git pull command is used to fetch and download content from a remote repository and immediately update the local repository to match that content.

In the simplest terms, `git pull` does a `git fetch` followed by a `git merge`.

That's why `git pull` local is a `git merge` as it does not execute the `git fetch`

```bash
# Pull an upstream branch
git pull

# Pull a specified branch
git pull <remote> <branch>
```

### [Git merge](https://www.atlassian.com/git/tutorials/using-branches/git-merge)

#### How git merge works <!-- omit in toc -->

Git merge will combine multiple sequences of commits into one unified history. In the most frequent use cases, git merge is used to combine two branches.

Git merge takes two commit pointers, usually the branch tips, and will find a common base commit between them. Once Git finds a common base commit it will create a new "merge commit" that combines the changes of each queued merge commit sequence.

![Git-merge-img-1](images/git-merge-01.png)

Invoking this command will merge the specified branch `feature` into the current branch, we'll assume `main`. Git will determine the merge algorithm automatically.

![Git-merge-img-2](images/git-merge-02.png)

Merge commits are unique against other commits in the fact that they have two parent commits. When creating a merge commit Git will attempt to auto magically merge the separate histories for you. If Git encounters a piece of data that is changed in both histories it will be unable to automatically combine them. This scenario is a version control conflict and Git will need user intervention to continue.

#### Steps to merge <!-- omit in toc -->

```bash
# Switch to the receiving branch
git switch <receiving_branch>

# Merge feature branch
git merge <feature_branch>

# Resolve conflicts (if have some) and commit
git add .
git commit -m "main merged feature_branch"

# Update remote branch
git push <remote> <receiving_branch>

# You can delete the feature branch if you want
git branch -d <feature_branch>
git push -d origin <feature_branch>
```

### Git rebase

Rebasing is the process of moving or combining a sequence of commits to a new base commit

![Git rebase](images/What%20is%20git%20rebase.svg)

| Merge | Rebase |
|---|---|
| Merge branches from Git | Integrate changes from one branch to another |
| All the commits on the feature branch will be combined as a single commit in the master branch | All the commits will be rebased and the same number of commits will be added to the master branch |
| Git Merge should be used when the target branch is shared branch | Git Rebase should be used when the target branch is private branch |

Learn more: <https://www.youtube.com/watch?v=f1wnYdLEpgI>

#### Steps to rebase <!-- omit in toc -->

```bash
git rebase <feature_branch>
# Then, resolve all conflicts manually
git add .
git rebase --continue
```

## Multiple Remotes

By convention, the original remote repo is called origin

```bash
git remote add <remote> <remote_url>
# Ex: git remote add origin https://github.com/dev-tronghieu/git-handbook.git
```

### Add new remotes

```bash
# By convention, the original remote repo is called origin
git remote add <remote> <remote_url>

# Multiple remote urls example
git remote add origin https://github.com/dev-tronghieu/git-handbook.git # origin remote
git remote add backup https://github.com/dev-tronghieu/git-backup.git   # backup remote
git remote add alt https://gitlab.com/ev-tronghieu/git-handbook.git # alternative remote

# Push a remote
git push <remote> <branch>

# List all remotes
git remote -v

# Remove a remote
git remote remove <remote>
```

### Fetch remotes

It is not possible to pull from multiple repos. However, we can fetch the data from the remote branch.

```bash
git fetch <remote> <branch>
# or git fetch --all
```

Reset the branch to match the state as on a specified remote.

```bash
git switch <branch>
git reset --hard <remote>/<branch>
```

## Some other commands

### Git stash

#### Stash your work <!-- omit in toc -->

```bash
# Simple way to stash
git stash

# Or you can stash with a description
git stash --save "stash message"

# Then, make some changes and commit them
```

#### Re-apply your stashed changes <!-- omit in toc -->

```bash
git stash apply  # throws away the (topmost, by default) stash after applying it
git stash pop    # leaves it in the stash list for possible later reuse
```

#### Stashing untracked or ignored files <!-- omit in toc -->

By default, `git stash` will not stash new files in your working tree that have not yet been staged or files that have been ignored.

```bash
# Stash the untracked files
git stash --include-untracked
git stash -u # short form

# Stash changes to ignored files
git stash --all
git stash -a # short form
```

#### Managing multiple stashes <!-- omit in toc -->

You aren't limited to a single stash. You can run git stash several times to create multiple stashes, and then use `git stash list` to view them.

By default, stashes are identified simply as a "WIP" – work in progress – on top of the branch and commit that you created the stash from.

```bash
git stash list
# > stash@{0}: WIP on main: 5002d47 commit message
# > stash@{1}: WIP on main: 5002d47 commit message
# > stash@{2}: WIP on main: 5002d47 commit message

# You can choose which stash to re-apply
# by passing its identifier as the last argument
git stash pop stash@{2}

# Or creating a branch from your stash
git stash branch <branch> stash@{1}

# Of course, you can clean up your stashes
git stash drop stash@{1} # specified one
git stash clear          # all stashes
```

### Git commit --amend

The `git commit --amend` command is a convenient way to modify the most recent commit. It lets you combine staged changes with the previous commit instead of creating an entirely new commit.

```bash
git commit --amend -m "commit message"
```

### Git merge --squash

```bash
git checkout main
git merge --squash feature
git commit -m "commit message"
```

This takes all the commits from the `feature`, squash them into 1 commit, and merge it with your `main`.

### Git cherry pick

Learn more: <https://www.youtube.com/watch?v=wIY824wWpu4>

```bash
git cherry-pick <commit_hash_1> <commit_hash_2> <commit_hash_n>

# Cherry-pick without making a new commit
git cherry-pick --no-commit <commit_hash>
git cherry-pick -n <commit_hash> # for short
```
