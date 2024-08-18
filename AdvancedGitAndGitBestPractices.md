# Advanced Git and Git best practices

## GitHub pull requests

1. create a local branch of the changes you want to be merged into another branch
2. push the local branch to a remote branch
3. create a pull request

> HOW DO YOU USE BRANCHES WITH PULL REQUESTS? Each pull request you create should use a new, non-master branch. Because
> each pull request tracks the
> status (and any new commits) for a particular remote branch, you need to
> ensure that each branch is used for a separate pull request to avoid situations
> like adding a new commit to one pull request and having it show up in
> another. You should also avoid creating pull requests from the master branch,
> because this is generally the branch you will want to merge to. Additionally,GitHub sometimes doesn’t update the master
> branch if you push new commits to it after creating the pull request, so you’d need to create a new pull
> request for every change that needs to be made. This is less than ideal, because
> you lose all the existing context and comments.

### Merging a pull request from the same repository

1. Check out the `main` branch by running `git switch main`.
2. Ensure that all the remote branches are up-to-date by running `git fetch`.
3. Merge the remote `pr-test` branch into the `main` branch by running `git merge --no-ff origin/pr-test`
4. Push the updated `main` branch with `git push`
5. Delete the now-merged `pr-test` branch by running `git push --delete origin pr-test`

## GitHub Flow

* GitHub Flow is simple because it essentially involves only two types of branches: the default `main` branch and
  feature branches. A feature branch is one that is used only for the development of a single feature (or sometimes bug
  fix) and then deleted after being merged into another branch.
* In GitHub Flow:
* All commits are made on feature branches
* Feature branches are merged to the `main` branch after review in a pull request
* All commits to `main` are considered stable.

1. The initial commit to a repository is on the `main` branch and made with `git add` and `git commit`.
2. A new feature is being developed, so it’s branched off the master branch with `git checkout -b feature` or `git
   switch -c feature`.
3. Another feature is developed in parallel, so it too is branched off the master branch with `git checkout -b`
   or `git switch -c`.
4. Commits are made to both feature branches with git commit. They’re pushed periodically with `git push`
5. _**Commits may be rewritten locally with `git rebase --interactive` or `git commit --amend` before being pushed;
   but they’re never rewritten after being pushed, so `git push --force` is never required.**_
6. A feature branch is submitted for review in a pull request either through the GitHub web interface
7. When the branch is ready:
    1. merged to master with `git merge --no-ff`
    2. delete locally with `git branch --delete`
    3. delete remotely with `git push --delete`