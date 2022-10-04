# Git Case Study

## Case 1
Here's a situation that happens quite commonly. You have some changes (newImage) and another set of changes (caption) that are related, so they are stacked on top of each other in your repository (aka one after another).

The tricky thing is that sometimes you need to make a small modification to an earlier commit. In this case, design wants us to change the dimensions of newImage slightly, even though that commit is way back in our history!!

We will overcome this difficulty by doing the following:

- We will re-order the commits so the one we want to change is on top with git rebase -i
- We will git commit --amend to make the slight modification
- Then we will re-order the commits back to how they were previously with git rebase -i
- Finally, we will move main to this updated part of the tree to finish the level (via the method of your choosing)


## Case 2

### Remote Rejected!
If you work on a large collaborative team it's likely that main is locked and requires some Pull Request process to merge changes. If you commit directly to main locally and try pushing you will be greeted with a message similar to this:

    ! [remote rejected] main -> main (TF402455: Pushes to this branch are not permitted; you must use a pull request to update this branch.)

### Why was it rejected?
The remote rejected the push of commits directly to main because of the policy on main requiring pull requests to instead be used.

You meant to follow the process creating a branch then pushing that branch and doing a pull request, but you forgot and committed directly to main. Now you are stuck and cannot push your changes.

### The solution
Create another branch called feature and push that to the remote. Also reset your main back to be in sync with the remote otherwise you may have issues next time you do a pull and someone else's commit conflicts with yours.

## Case 3
#### Stuatuion
Accidentally push a file to the remote repo that is actually not needed.

#### Solution
- Need to get back to the previous state of the file

		git checkout BRANCH_NAME~1 FILE_NAME

- Commit current Change
- Push again to the remote
- [resource](https://stackoverflow.com/a/725893/4245112)



## Case 4
#### Stuatuion
Accidentally push a branch with the wrong name.

#### Solution
- [Rename Branch in local and remote](https://stackoverflow.com/a/45561865/4245112)

