### git-practice-page
# The Odin Project - Ruby Course: A deeper look at Git

## Changing the last commit

```git commit --amend``` 
- only amend commits that have NOT been pushed anywhere
- does NOT edit the last commit, it **REPLACES** that commit with an entirely new one. This means that you could potentially destroy a commit other developers are basing their work on.

## Changing multiple commits

```git rebase -i``` is a command which allows us to interactively stop after each commit we’re trying to modify, and then make whatever changes we wish. We do have to tell this command which is the last commit we want to edit. For example, ```git rebase -i HEAD~2``` allows us to edit the last two commits.

## Squashing commits

Refers to the process of combining multiple commits into a single, larger commit. This can be useful for keeping your commit history clean and concise, especially when you're working on a feature branch or preparing to merge changes into a main branch.

When you squash commits, you essentially condense the changes made in several commits into one commit. This can make it easier to review the history of changes and to understand the evolution of the codebase. It's often done before merging a feature branch into the main branch or before submitting a pull request for review.

```git rebase -i --root``` rebase all the way to the root commit

```pick``` that first commit, as the one which the second commit is being squashed into with ```squash```

Use ```git rebase -i HEAD~n``` where n is the number of commits you want to squash

## Splitting up a commit

```git reset``` is used to reset the state of your working directory and staging area to a specific point in the commit history. It can be used to undo changes, unstage files, or move the HEAD and branch pointers to a different commit.

```git reset HEAD^``` resets the commit to the one right before HEAD. 

### Soft Reset 

```git reset --soft <commit>``` This mode resets the HEAD pointer to the specified commit, but leaves the changes staged. It doesn't modify the working directory or undo any changes. This is useful if you want to **"undo"** a commit but keep the changes ready to be committed again.

### Mixed Reset 

```git reset --mixed <commit>``` This mode is the default behavior if you don't specify a mode. It resets the HEAD pointer to the specified commit and **unstages** the changes, but leaves them in your working directory. This means the changes are still present, but you'll need to add them again to the staging area if you want to commit them.

### Hard Reset 

```git reset --hard <commit>``` This mode resets the HEAD pointer to the specified commit and discards all changes in both the staging area and the working directory. It effectively reverts your working directory to the state of the specified commit. In other words, it overwrites the files in the working directory to make it look exactly like the staging area of wherever HEAD ends up pointing to. 

Be cautious when using this mode, as it **permanently removes any changes** you haven't committed.

## Git Push --Force

```git push --force``` is used to forcefully update the remote repository with your local changes, potentially overwriting any changes that may exist on the remote branch. It's a powerful and potentially risky command, so it should be used with caution and only in certain situations.

## Git revert

```git revert``` is used to create a new commit that undoes the changes introduced by a specified commit or range of commits. Unlike commands like git reset or git rebase, which alter the commit history, git revert creates a new commit that effectively reverses the changes made in previous commits while preserving the commit history.

```git revert``` does NOT remove the original commit(s) from the history; instead, it adds a new commit that **undoes** their changes. As a result, the repository's history remains intact, and the original commit(s) remain visible in the commit history.

## Warnings

1. ```git amend``` : never amend commits that have been pushed to remote repositories
2. ```git rebase``` : never rebase a repository that others may work off of
3. ```git reset``` : never reset commits that have been pushed to remote repositories
4. ```git push --force``` : only use it when appropriate, use it with caution, and preferably default to using ```git push --force-with-lease```

