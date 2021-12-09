# Git branching

To create a new local branch type:
```
git branch newBranchName

// To show how many branches we have and on which one we are working on type
git branch
```

To show all local and remote branches type:
```
git branch -a
```

To rename a branch type:
```
git branch -m oldBranchName newBranchName
```

List files in a branch
```
git ls-tree -r branchName
```

To show the remote enviroment (remote branches and what local branches track them)
```
git remote show remoteName // usually remote name is origin
```

To switch to a available branch type:
```
git switch branchName

git switch - // switch to the main (or master) branch

git checkout branchName // we can use checkout too (checkout == git switch && git restore)
```

A easier way to create and immediataly switch to that new branch use the command:
```
git checkout -b nameOfTheNewBranch
```

To delete a branch use:

`Note:` we can't delete the branch that we are currently working on.

```
git branch -D branchName

// A better way to delete branches is using -d, cause it prevent to delete branches
// that weren't merged yet.
git branch -d branchName
```

We can delete remote branches in local environment:

`Note:` it will not delete the branch locally, to do this use the earlier command
```
git push origin --delete remoteBranchName
```

to push a local branch to Github for the first time type:

`Note:` before pushing it to remote repo, you need to do a commit first!
remember to switch to the local branch you want to track with the remote one
```
// it will track the local project with the remote.
git push -u origin remoteBranchName

git push --set-upstream-to origin localBranchName // -u is the short version of this
```

track a remote branch with the local one type:

`Note:` it will track the remote branch with the branch pointed by HEAD
```
git branch -u remote/branchName
```

## Git Merging branches

* Fast-forward merging:

It is a simple way to merge branches. The ideia is to have a linear path of the
main branch to the secoundary branch ('dev' branch for example). The main branch
does not receive any change while we work on the dev branch. When all the work
is done and tested, we merge the two branches, so the main branch receives all
the commits of dev.

We can create a develoment branch called 'dev' and to make changes safaly when we
are happy with the results we can merge the dev branch with the main brench.

To merge two branches type:

`Note:` go to the main branch in which you want to merge.
```
git merge branchName // for example: in *main> git merge dev
```

* Three-Way-Merge:

It is another scenario when merging branches. This kind of merging happens when 
we are working in a branch and simultaneously someone else is making commits
to the main branch before we merged the two. It can lead to a problem called merge
conflicts.

Merge conflicts occurs when more then one developer is working on the same files,
git will try to avoid those conflicts, but some of them can still persist.

If you try to merge the branchs git will write a text in the conflicting file and
will rise a merge conflict warning.

to solve the problem we first need to decide which version we gonna keep, then we
remove the code that git has added, then we add the file to the stage area and use
git commit without -m flag. It will open a file where we can add the message

## Git Rebase

We can use git rebase to change the base commit to the last/newly commit on the
main/master branch.

It keeps the commit history cleaner then git merge, but it does not mean we have
to always use git rebase. Let's look at some scenarios:

Our main branch has a linear pattern of commit, let's say three commits in the
history. then we wnat to add a new feature, so we create a new branch called
`feature`. The commit on the main branch in which the new branch was created is
called the `base commit`.

We add two commits on the feature branch and now we say it is two commits ahead of
the main branch. Now, someone else adds a new commit to the main branch and it makes
our feature branch be one commit behind main.

To fix this scenario we can do:
```
// go to the feature branch
git switch feature

git rebase main

// go to the main branch
git switch main

git merge feature
```

What we did? very simple and clear! We reset the base commit on the main branch
to the newest one using git rebase, so now, the commit on the master branch is
visible on the feature branch too and it's not behind the main branch anymore. But
our feature branch is still ahead of our main branch, so we need to merge the changes
of the feature branch on the main one. Thats it, we did a fast-forward merging!
