# Git Essentials
## Filesystem interactions
### Renaming or moving a file: `git mv`
* When you move or rename a file, Git doesn’t see that a file was moved; it sees that there’s a file with a new 
  filename, and the file with the old filename was deleted
* `git mv oldFileName newFileName`
* `git mv --force` to force move the file and override the existing file
###  Removing a file: `git rm`
* Git only interacts with the Git repository so before removing a file make sure it's committed
* `git rm fileName`
* `git rm -f` to delete a file with uncommited changes
* `git rm -n` (or `--dry-run`) This will print the output of the command as if it were running normally and indicate success or failure, but without removing the file.
* `git rm -r` `-r` stands for _recursive_ 
###   Temporarily stashing some changes: `git stash`
* `git stash`, `git stash list`, `git stash clear` and `git stash pop`
* `git stash apply` do the same as `pop` but doesn't remove the element from top of stack
### History visualization
* `git log --oneline --decorate --graph`
* `git log --author "Mohamed Saber" --after "Nov 10 2023"` can be replaced with `Nov 10 2013`, `2014-01-30`, `midnight`, or `yesterday`
* `git show main` to get details about the last commit
* `git log --format="%ar %an did: %s"`
  * `%ar` is the relative format date on which the commit was authored
  * `%an` is the name of the author of the commit.
  * did: is text that’s displayed the same in every commit and isn’t a placeholder
  * `%s` is the commit message subject (the first line).
  * check more using `git log --help`
* `git blame fileName` to get all information about changes in the file
* `git bisect start` to find which commit caused a particular bug
  * `git bisect good SHA-1` for files that doesn't have the bug in the file
  * `git bisect bad SHA-1` for the files that has the bug in the file
  * `git bisect reset` to clear the bisect reference
### Creating a tag: `git tag`
* A `tag` is another ref (or pointer) for a single commit
* `git tag tagName`
* `git tag --list` show tags
* `git tag --force`  flag updates a tag to point to the new commit
* `git tag --delete` flag deletes a tag
* `git push -tag`
* `git describe --tags` o generate a version number for a software project based on existing tags in the repository 
### Adding a single commit to the current branch: `git cherry-pick`
* Sometimes you may wish to include only a single commit from a branch onto the current branch rather than merging the entire branch.
* `git cherry-pick tagNumber` or `git cherry-pick SHA-1`
* `git cherry-pick --edit` prompts you for a commit message before committing.
* `git cherry-pick --continue` or `git cherry-pick --abort` instead of `git commit` after resolving a conflict
## Rewriting history and disaster recovery
### Reverting a previous commit: `git revert`
* `git revert SHA-1` undo a commit
* `git restore --staged fileName` to unstage
* `git restore fileName` to discard changes in working directory
### Listing all changes including history rewrites: `git reflog`
* Git’s `reflog` (or _reference log_) is updated whenever a commit pointer is updated (like a _HEAD_ pointer or branch pointer)
* `git reflog main` view how the `main` branch has changed over time 
> ARE REFLOGS SHARED BETWEEN REPOSITORIES? Reflogs are per repository.
They aren’t shared with other repositories when you git push and aren’t
fetched when you git fetch. As a result, they can only be used to see actions
that were made in the Git repository on your local machine. Bear this in mind
when you’re rewriting history: you can easily view the previous state on your
current machine, but not that from other machines.
###  Resetting a branch to a previous commit: `git reset`
* `git reset --hard` with uncommitted changes is easily recoverable using `git reflog` for 90 days after the changes were made
* `git reset --hard` reset both the index staging area and the working directory to the state of the previous commit on this branch
* `git reset --mixed` resets the index staging area but not the contents of the working directory
* `git reset --soft` resets neither the staging area nor the working tree but just changes the `HEAD` pointer to point to the previous commit.
### Rebasing commits on top of another branch: `git rebase`
* The rebase runs through the list of commits from top to bottom and follows the command for each listed commit (skipping any that have been
  removed).
* The `pick` command means the commit should be included in the rebase as is. If this file is saved and closed without modification, every commit is picked
*  `squash` = use commit, but meld into previous commit
*  `fixup` = like `squash`, but discard this commits log message
* `git rebase -i SHA-1` or `git rebase -i HEAD~5`