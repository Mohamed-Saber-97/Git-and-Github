# Introduction to Git

# Local Git

## Initial setup

* Git uses a name and an email address to identify the author of a commit.
    * `git config --global user.name "Mohamed Saber"`
    * `git config --global user.email mohamedsaber.developer@gmail.com`
    * `git config --global user.email` output is  `mohamedsaber.developer@gmail.com`

## Creating a repository: `git init`

* `git init` to create the local Git repository in the current directory.
* `git init RepositoryName` to create the local Git repository in the target directory.

#### `git init` creates a _.git_ file which has the following:

```text
$ find .git/
.git/config //local configuration of the local repository
.git/description //file that describes the repository
.git/HEAD //Head Pointer that point to commits.
.git/logs/refs/heads //Branch Pointers that point to commits.
.git/refs/tags //Tag Pointers that point to commits.
.git/hooks/applypatch-msg.sample //Event Hooks (scripts that run on defined events)
.git/info/exclude //files that should be excluded from the repository
.git/info //Object information used for object storage and reference
.git/objects/pack //Pack files used for object storage and reference
```

## Creating a new commit: `git add`, `git commit`

* `git add` is used to add _modified_ or _untracked_ changes from current _directory_ to the _staging area_
    * `git add .` adds all the changes from the current directory and subdirectories
    * `git add fileName.extension` adds specific file
    * `git add ./DirectoryName` adds directory and subdirectories
* `git restore --staged` removes the changes from the staging area
    * `git restore --staged <file>` removes specific file
    * `git restore --staged .` removes all files
* `git commit -m "Commit Message"`
    * `git commit -a -m "Commit Message"` adds all files then commits
    * `git commit` opens the text editor

> WHY ARE SMALL COMMITS BETTER? Sometimes it’s desirable to pick only some
> changed files (or even some changed lines within files) to include in a commit and leave the other changes to be added
> in a future commit. Commits
> should be kept as small as possible. This allows their message to describe a single change rather than multiple changes
> that are unrelated but were worked
> on at the same time. Small commits keep the history readable; it’s easier when
> looking at a small commit in the future to understand exactly why the change
> was made. If a small commit is later found to be undesirable, it can be easily
> reverted. This is much more difficult if many unrelated changes are clumped
> together into a single commit and you wish to revert a single change.

> HOW SHOULD COMMIT MESSAGES BE FORMATTED? The commit message is
> structured like an email. The first line is treated as the subject and the rest as
> the body. The commit subject is used as a summary for that commit when
> only a single line of the commit message is shown, and it should be 50 characters or less. The remaining lines should be
> wrapped at 72 characters or less
> and separated from the subject by a single, blank line. The commit message
> should describe what the commit does in as much detail as is useful, in the
> present tense.

#### Example of Good Commit message

```text
Improve error handling for file uploads

Detailed description of the changes made: 
* Added error handling for file upload exceptions.
* Implemented retry logic for failed uploads.
* Improved error messages for user feedback.
```

## Viewing the differences between commits: `git diff`

* the branch is just a pointer a commit and the `HEAD` is a pointer to the last commit checked out
* `git diff` diff between the current working directory and the index staging area
* `git diff main` diff between the current working directory and the commit on top of main
* `git diff main~1 main` diff between the top of main (main~1) and the commit on top of main
* `git diff master~1 master <--file>`diff between the top of main (main~1) and the commit on top of main in a certain
  file

##  * Creating a new local branch from the current branch: `git branch`

* `git branch` to show the local branches
* `git checkout -b newBranch` or `git switch -c newBranch` to create a new branch and switch to it
* `git branch newBranch` is the equivalent of `git branch newBranch master` which creates a new branch

## Checking out a local branch: `git checkout`

* `git checkout newBranch` or `git switch newBranch`
* Make sure you’ve committed any changes on the current branch before checking out a new branch or use `git stash`

## Merging an existing branch into the current branch: `git merge`

* checkout to `main` and `git merge newBranch`
* A **_merge conflict_** occurs when both branches involved in the merge have changed
  the same part of the same file. Git will try to automatically resolve these conflicts but
  sometimes is unable to do so without human intervention
* We can delete the local branch after merging by using `git merge --delete newBranch`

# Remote Git

## Adding a remote repository: `git remote add`

* `git remote add origin https://github.com/Mohamed-Saber-97/Git-and-Github`
    * `git remote rename origin newName` to rename remote
*

```text
$ git remote -v
origin  https://github.com/Mohamed-Saber-97/Git-and-Github.git (fetch)
origin  https://github.com/Mohamed-Saber-97/Git-and-Github.git (push)
```

## Pushing changes to a remote repository: `git push`

* `git pull` performs two actions: fetching the changes from a remote repository and merging them into the current
  branch.
* `git push -u origin main` only the first time then it's equivalent to `git push origin main` when you type `git push`
* `git push --all origin main` pushes all branches and tags
* `git push --force` re-write history on the remote branch. _**This is very dangerous**_

## Cloning a remote/GitHub repository onto your local machine: `git clone`

* `git clone https://github.com/Mohamed-Saber-97/Git-and-Github`

## Pulling changes from another repository: `git pull`

* `git pull`
    * downloads the new commits from another repository and merges the remote branch into the current branch
    * directly equivalent to running `git fetch` && `git merge origin/master`
    * fast-forward merge, which means no merge commit was made.
* `git pull --rebase` performs a rebase rather than a merge

## Fetching changes from a remote without modifying local branches: `git fetch`

* `git fetch` performs the fetching action of downloading the new commits but skips the merge step (which you can
  manually perform later)

> SHOULD YOU USE PULL OR FETCH? I prefer to use git fetch over git pull.
> This means I can continue to fetch regularly in the background and only
> include these changes in my local branches when it’s convenient and using
> the method I find most appropriate, which may be merging, rebasing or resetting.

## Deleting a remote branch

* A short-running branch may be a single bug fix or feature that has been completed.
* After using the `git push` we can use `git push --delete origin newBranch`

  ## Tell Git to stop tracking changes to the file
  * `git ls-files` show files that are tracked by git 
  * `git update-index --assume-unchanged fileName`
