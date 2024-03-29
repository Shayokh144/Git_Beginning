- Download git from [here](https://git-scm.com/download/win) for windows  : 
- Then install
- If there is any problem watch [this](https://www.youtube.com/watch?v=SmbAn2_5uGs)

- Create a folder anywhere.

- Create a txt file. I created "first.txt".

- Now, right click on mouse in that folder and click on "Git Bash Here".[for windows user only]
> linux or Mac user just open terminal
- A command promt [ Git bash ] will open which is used to perform various version controlling operation.

- First we have to get logged in. For this we nedd to write on that cmd:
		
		i)	git config --global user.email "abcd@gmail.com"
		
		ii)	git config --global user.name "something"
		
		**** Any valid email address and username can be used.
		**** if you want to configure this only for specific repo just remove the --global from avove command and run it.
- Now we are ready to perform version controlling. At first we have to create a git repository by using this command:

		git init
		**** After this an empty repository is created.
		


## Git Work Flow


- In git there are [three types of things](https://www.quora.com/What-is-the-meaning-of-commit-and-stage-in-git) we have to deal with:  


		i)  Working copy: 
		When we create a file it remains in the working copy. Here, "first.txt" is in working copy now.

		ii) Staging area: 
		When we use "git add ." cmd then all files in the current directory goes to staging area. Now, open the             "first.txt" file and write something on it. I write "Thsi is my first git prac from master." Then write this cmd in git bash:
			a)  git add .
			this cmd(a)  adds all modified and new (untracked) files in the current directory and all subdirectories to the staging area (a.k.a. the index), thus preparing them to be included in the next git commit.
			So, the first.txt file is now in the staging area.

		iii) Git Repository: It stores the current contents of the index/staging area in a new commit along with a log message from the user describing the changes. So, commit means takes a snap shot of files and save it in the repository finally.
		So, we have to commit by using this command:

		a) git commit -m "This is my first commit"
		here, "This is my first commit" is the commiting message, anything can be written.
		After writing this command all files are saved in git repository.

		We can watch commit history by using :
		a) git log
		or only for specific author's commit history,
		a) git log --author="author's username"



## Git Branch

8- By default when we initiate a git repository we are in master branch. To check this write:

		i) git branch
		this cmd shows the names of branches. As we didn't create any branch it will show only "master" branch.

- To creat a new branch from current branch :

		i) git branch slave
		This cmd create a new branch named "slave" from current branch [ we are currently in master branch]. 
		To find out if the new branch is created or not use this cmd: git branch
		it will show the names of branches and an asteric symbol beside the current branch name.

- Now, if we want to go another branch [slave] from current branch [master] :

		i) git checkout slave
		after writing this, we are in  the slave branch which is the copy of master branch because we create slave branch from master branch.

- This time open the "first.txt" file and you can see the same thing that was in the master branch. Now change the text. I add a new line "I am from slave" after the existing line and save this. Now, we have to commit these changes to the current slave branch. So, write:

		i)  git add .
		ii) git commit -m "This is my first commit from slave"		

- To understand the branching effect we have to go to the master branch using:

		i) git checkout master
- Now open the "first.txt" file you only find the text "Thsi is my first git prac." that we wrote and commit when we were in the master branch.

- To delete any branch use :

		i) git branch -D Branch_Name


## Merge


- In projects we nedd the change or updated codes from one branch to another. Like , If we want to get the changes from slave branch to master branch. To do this we have to merge them. First we have to go master branch, so write: 
     
		i)  git checkout master
- now we are in the master branch. We want here the update from slave branch. So write:

		ii) git merge slave 
- We are done. Open the file First.txt and find the magic of git :) . 
- But there are some situations where merge conflict occurs, read [here](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging) for more information.

 
 
## upload from desktop to github

- read [here](https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/)
- more [info](https://help.github.com/articles/adding-a-remote/)
 
 
## RESET


- Read [this](https://davidzych.com/difference-between-git-reset-soft-mixed-and-hard/) 


		git reset --hard
 		**** the above command remove all uncommited change . (Dangerous!!)
 
		git reset --hard <SOME-COMMIT> 
 		**** Make your current branch (typically master) back to point at <SOME-COMMIT>.Then make the files in your working tree and the index ("staging area") the same as the versionscommitted in <SOME-COMMIT>.

		git clean -f
		**** remove untracked changes.
 
 
## Remove all uncommited change

- [undo uncommited changes](https://stackoverflow.com/questions/14075581/git-undo-all-uncommitted-or-unsaved-changes)
		
		1. git reset
		2. git checkout .
		3. git clean -fdx


## [Edit file that goes in last commited push](https://medium.com/@igor_marques/git-basics-adding-more-changes-to-your-last-commit-1629344cb9a8)


suppose there is a file "Abc.cpp" in which you changed and pushed. Suddenly you realize there should be a small change needed. There are two ways to do it -> 

		i)  Commit and push again with new change
		ii) edit the last commit and then push 
Second one is better for small changes. It will kepp working tree cleaner. To do this follow the below steps:

		i)   git status
		ii)  find the desired file name with path like : "modified:  File_Path/Abc.cpp"
		iii) git add  File_Path/Abc.cpp
		iv)  git commit --amend --no-edit 
		*** if you dont want to chage the commit message use above command otherwise use git commit --amend
		v)  git push origin "BRANCH_NAME"





## pull vs pull --rebase
- read [this](https://stackoverflow.com/questions/2472254/when-should-i-use-git-pull-rebase)




## All about STASH


- Find all list of stash 
	- ***git stash list***
- Stash files using message 
	- ***git stash push -m "message"***
- Apply particular stash from stash list 
	- ***git stash apply stash@{Nth}***
- Delete particular stash from list 
	- ***git stash drop stash@{Nth}***
- Apply and delete stash from stack at a time 
	- ***git stash pop stash@{Nth}***
- Show stash summary 
	- ***git stash show -p***




## Undo Redo Most Recent Commit


		$ git commit -m "Something terribly misguided"             # (1) commit done
		$ git reset HEAD~                                          # (2) get back committed changes
		<< edit files as necessary >>                              # (3)
		$ git add ...                                              # (4) add again
		$ git commit -c ORIG_HEAD                                  # (5) commit again




## discard change of a file / get back to the previous state of a file


		git checkout -- file_name



## merge conflict


when merge conflict occurs, our local changes are shown inside the HEAD block and remote changes will be slown after three `=====` block, like below:

	<<<<< HEAD
	*** here will be our local changes
	=====================
	Here will be the remote changes
	>>>>>>>>



## untrack a file


- command for untracking a file:

		git rm --cached filepath+Name

		*** after running this command git will not track the file, but it will remain in the file system of computer 



## Go back to a previous commit, then back to the latest commit



- go back to any previous commit:

		git checkout <commit_hash>

- This would detach the head. So, to get back to the latest commit run the following command:
		
		git checkout BRANCH_NAME

- [details](https://stackoverflow.com/a/39197098/4245112)



# GIT ALIAS


* using alias we can shotening git commands
	* ***git config --global alias.logo 'log --oneline'***
		* after running above command we can use 'git logo' instead of 'git log --oneline'
	* ***git config --global alias.cane 'commit --amend --no-edit'***
		* after running this command we can use 'git cane' instead of 'git commit --amend --no-edit'
* find list of all alias:
	* ***git config --list | grep alias***
	* it will show:
		- alias.logo=log --oneline
		- alias.cane=commit --amend --no-edit



## Go to prevoius or next head


- Moving upwards one commit at a time with `^`
- Moving upwards a number of times with `~<number of times>`


### caret ^ operator


- Let's look at the Caret (^) operator first. Each time you append that to a ref name, you are telling Git to find the parent of the specified commit.
- So saying main^ is equivalent to "the first parent of main".
- main^^ is the grandparent (second-generation ancestor) of main

		git checkout main^

		*** this will move the head to the parent of main


## Git Cherry-pick
- git cherry-pick will plop down a commit from anywhere in the tree onto HEAD (as long as that commit isn't an ancestor of HEAD)
- The first command in this series is called **git cherry-pick**. It takes on the following form:

		git cherry-pick <Commit1> <Commit2> <...>

		*** It's a very straightforward way of saying that you would like to copy a series of commits below your current location (HEAD).

## Git Interactive Rebase

- Git cherry-pick is great when you know which commits you want (and you know their corresponding hashes) -- it's hard to beat the simplicity it provides. But what about the situation where you don't know what commits you want? Thankfully git has you covered there as well! We can use interactive rebasing for this -- it's the best way to review a series of commits you're about to rebase.

- All interactive rebase means Git is using the rebase command with the -i option.
- If you include this option, git will open up a UI to show you which commits are about to be copied below the target of the rebase. It also shows their commit hashes and messages, which is great for getting a bearing on what's what.
- In interactive rebase you can do many more things like picking commits, dropping commits, squashing (combining) commits, amending commit messages, and even editing the commits themselves.

		git rebase -i HEAD~4

		*** this will provide opportunity to edit last 4 commits


## Git Remote Branches

- The first thing you may have noticed is that after cloning a remote branch appeared in our local repository called `<remote name>/<branch name>`. This type of branch is called a remote branch; remote branches have special properties because they serve a unique purpose.
- Remote branches reflect the state of remote repositories (since you last talked to those remote repositories). They help you understand the difference between your local work and what work is public -- a critical step to take before sharing your work with others.
- Remote branches have the special property that when you check them out, you are put into detached HEAD mode. Git does this on purpose because you can't work on these branches directly; you have to work elsewhere and then share your work with the remote (after which your remote branches will be updated).
- To be clear: Remote branches are on your local repository, not on the remote repository.
- Most developers actually name their main remote origin
- This is because origin/branch_name will only update when the remote updates.


## Git Fetch
- fetch data from a remote repository

		git fetch

- only remote branches will update to reflect that new representation.

<img src="./static_res/fetch_place.png" alt="before_fetch" />


### Before fetch
<img src="./static_res/before_fetch.png" alt="before_fetch" style="height: 350px; width:750px;"/>

### After fetch
<img src="./static_res/after_fetch.png" alt="before_fetch" style="height: 350px; width:750px;"/>

### What fetch does
git fetch performs two main steps, and two main steps only. It:

- downloads the commits that the remote has but are missing from our local repository, and...
updates where our remote branches point (for instance, o/main)
- git fetch essentially brings our local representation of the remote repository into synchronization with what the actual remote repository looks like (right now).

- If you remember from the previous lesson, we said that remote branches reflect the state of the remote repositories since you last talked to those remotes. git fetch is the way you talk to these remotes! Hopefully the connection between remote branches and git fetch is apparent now.

- git fetch usually talks to the remote repository through the Internet (via a protocol like http:// or git://).

### What fetch doesn't do

- git fetch, however, does not change anything about your local state. It will not update your main branch or change anything about how your file system looks right now.

- This is important to understand because a lot of developers think that running git fetch will make their local work reflect the state of the remote. It may download all the necessary data to do that, but it does not actually change any of your local files. We will learn commands in later lessons to do just that :D

- So at the end of the day, you can think of running git fetch as a download step.


## Git Pull
There are actually many ways to do this -- once you have new commits available locally, you can incorporate them as if they were just normal commits on other branches. This means you could execute commands like:

	git cherry-pick o/main
	git rebase o/main
	git merge o/main
	etc., etc.
In fact, the workflow of fetching remote changes and then merging them is so common that git actually provides a command that does both at once! That command is `git pull`.
So, `git pull` is equivqlent to `git fetch; git merge`

## Git push
In order to specify both the source and the destination in push command, simply join the two together with a colon:

		git push origin <source>:<destination>

This is commonly referred to as a colon refspec. Refspec is just a fancy name for a location that git can figure out (like the branch foo or even just HEAD~1).

Once you are specifying both the source and destination independently, you can get quite fancy and precise with remote commands. Let's see a demo!

### Before push
<img src="./static_res/push_with_args_before.png" alt="before_push" style="height: 350px; width:750px;"/>

### After push
<img src="./static_res/push_with_args_after.png" alt="after_push" style="height: 350px; width:750px;"/>

- #### if the destination you want to push doesn't exist, git will create the branch on the remote.


## Other Commands
- **git merge commit-id**
> will take the branch forward to a specific commit by moving the pointer forward using the fast-forward merge process
- **git rm -r --cached myFolder**
> Remove directory from Git but NOT local


