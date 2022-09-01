# Git Case Study

## One
Here's a situation that happens quite commonly. You have some changes (newImage) and another set of changes (caption) that are related, so they are stacked on top of each other in your repository (aka one after another).

The tricky thing is that sometimes you need to make a small modification to an earlier commit. In this case, design wants us to change the dimensions of newImage slightly, even though that commit is way back in our history!!

We will overcome this difficulty by doing the following:

- We will re-order the commits so the one we want to change is on top with git rebase -i
- We will git commit --amend to make the slight modification
- Then we will re-order the commits back to how they were previously with git rebase -i
- Finally, we will move main to this updated part of the tree to finish the level (via the method of your choosing)


