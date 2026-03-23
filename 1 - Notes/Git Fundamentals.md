**Dated:** 15-03-2026
**Indexes:** [[comp-sci]] | [[git]]
___

**What is Git?**
- Git is a Distributed Version Control System
- It is a tool used for tracking changes across a project
- Changes are tracked as versions

**What is a Git Hosting Service?**
- A Git Hosting Service is an online service to host a Git repository
- Such a service also allows for a common platform for collaboration

**Git Architecture**
- There is a local work environment
- There is a remote work environment
- People (often) work locally, push their changes to the remote
- Remote is (often) used for collaborative tasks, serving as the common ground for multiple users to work on the same repository

**Understanding Local**
- A local is simply a git repository on a local machine
- Changes can be made to any file
- Changes staged in the staging area are the only changes that can be and need to be committed
- A Commit is simply a save where we version our project with the latest changes

**Understanding Remote**
- Workflow between Local and Remote
- A Remote is simply a hosted repository on a Git Hosting Service

**Basic Workflows on Local**

```bash
$ git --version
```

- Commits need a username and email to identify who made the changes
- The username and email should be the same as the Remote service providers'
  
```shell
$ git config --global user.name UserName
$ git config --global user.email UserEmail
```

- To initialize a project as a Git repository
- This creates a `.git` directory in the project that tracks all the changes and git related ideas/meta
   
```shell
$ git init
```

- An repository existing on the remote can also be cloned onto local

```shell
$ git clone remote-repository-url
```

- To track changes in a git repository

```shell
$ git status
```

- Staging Changes `git add`
- `git add pattern` adds the selected pattern to the staging area for a commit

```shell
$ git add file1 file2 file3
# adds only the selected files

$ git add .
# adds everything changed

$ git add -A
# adds everything changed, as well as any changes in another repository inside the working one

$ git add *
# adds everything changed, except for deleted files (NOT deleted changes)

$ git add -p pattern
# You can selectively add changes from all files identified by specified pattern
```

- Changes can be unstaged using `git reset`

```shell
$ git reset
# Unstages all changes such that deleted files remain deleted

$ git reset --hard
# unstages all changes such that deleted files are restored

$ git reset pattern
$ git reset --hard pattern
```

- Changes on a stage can be committed using `git commit`
- This generates a unique identifier to the commit
- The idea behind a commit is that we can check back how the project looked like at the moment the commit was made

```shell
$ git commit -m "a descriptive message describing the changes"

$ git commit
# Opens up the text editor to allow for a longer commit message

$ git reset HEAD~
# Discards the last commit, staging the changed files
```

- `git rm` is used to manage removal of files the git way

```shell
$ git rm file
# Deletes the file and stages the deletion
# Shorthand for rm file && git add file

$ git rm -f file
# Force deletes a file with uncommitted changes and stages the deletion

$ git rm --cached pattern
# Removes (NOT deletes) a file from staging
```

- `git log` is the way to check the commit history of the repository

```shell
$ git log --oneline --graph
```

- Branching is a way to create alternate lines of development independent of the `main` branch
- This ensures that main still remains usable while other work is done and being committed
- There will always be one common commit between two branches (start of a new branch) and always be one common commit that merges the two branches (Created automatically by Git)

```shell
$ git branch
# lists out the branches present

$ git branch alternate
# creates a branch named "alternate" with the current commit on the current branch as the common commit (initial commit for alternate)

$ git checkout branchname

$ git merge branchname
# merges the branch named "branchname" with your current branch

$ git merge --abort
# discard a merge and move back to the previous commit, discarding merge conflicts and any merged changes
```

- When merging two branches, if same parts of a file are modified in one way on first branch and in other way on the second branch, a merge conflict occurs
- A conflict can be resolved by accepting either change, or by accepting both the changes or by writing an entirely new change
- In case if when merging a merge conflict occurs, the conflict needs to be resolved before the merge commit is made.
  (try merge -> if conflict then resolve -> merge again)
- To checkout a previous commit from a commit-ID identifiable by `git log`

```shell
$ git checkout commit-ID
```

- `git diff` highlights the changes in files between two different commits
- It can be used to compare older-commit to a newer-commit but that is a slippery slope of confusion. Just compare a newer one to an older one 

```shell
$ git diff newer-commit older-commit
```

- `git push` sends changes (as a branch) to the remote
- `git fetch` brings in changes from remote to the local without merging them
- `git pull` brings in changes from remote to the local and merges them

```shell
$ git push origin branchname
# Here, origin is the name used to identify the remote. It could be set to anything!

$ git remote add remote-name remote-url

$ git fetch origin branchname
$ git merge

$ git pull origin branchname
```

- To undo local, uncommitted changes, use `git restore`

```shell
$ git restore pattern
# Restores the selected files, discarding all uncommitted changes

$ git restore --staged pattern
# Restores the selected files from staging, keeping uncommited changes
# same as git rm --cached pattern
```

- To stash unfinished changes temporarily, use `git stash`
- This is needed when you do not wish to commit your changes yet but need to do something else like checking out another branch or commit

```shell
$ git stash
# Stashes the unfinished changes with a stash name

$ git stash list

$ git stash pop stashname
# brings in the changes from a stash onto working area and removes the stash

$ git stash apply stashname
# brings in the changes from a stash onto working area while keeping the stash as is
```

- `git revert` creates a new commit that brings the project back to a previous commit

```shell
$ git revert commit-id
```

DO NOT USE GIT REBASE, EVER!!!
IT REWRITES COMMIT HISTORIES. DO NOT LOOK INTO IT.
MERGING IS ALL YOU NEED.

**Meta**
1. Use conventional commit messages
2. Understand/Create the branching strategy for a project beforehand
3. A fork is a copy of a remote for pushing personal work
4. Use Pull Requests (Not a git feature but a common feature on most remotes) to communicate changes from a fork onto a repository you do not have access to
___
## References
