# git-good
Some Git commads that DigitKoodit-developers have found useful


#Resources 
[Git basics](https://try.github.io/) - good 15 minutes training

[Atlassian Git](https://www.atlassian.com/git) - documentation from basics to more advanced stuff

[Git workflow](http://nvie.com/posts/a-successful-git-branching-model/) - awesome workflow how to use Git in larger projects by yourself or collaboratively as well 
  
## Common 
	- HEAD 		: current state
	- HEAD^		: latest commit
	- HEAD^^	: parent of latest
	- HEAD~5	: 5th commit
	- HEAD@{i} 	: where i is index is history shown in reflog

	git status	: display current stage of your files. Are files staged, edited, deleted etc
	git show	: display more information about the current state

	git config --global color.ui true	: enable colors
	gid config --list					: list values which can be set through config
	git config --get-regexp [value]

### EASE TO LINE ENDINGS	
	git config --global core.autocrlf input 	: enable CR/LF to LF on commit on Linux
	git config --global core.autocrlf true		: change LF to CR/LF on checkout
	git config --global core.autocrlf false 	: For only Windows teams
	git update-index --assume-unchanged [file-name] 	: 
 
## Logging
	git log --oneline -p	 	: patch commit. Show changes etch 
	git log --oneline --stat	: statistics of removed and added
	git log --since=1.hour/minute.ago --until=1.day/month.ago	: multiple changes 

## Changes between comments
	gid diff HEAD^ 		: parent of latest commit
	git diff HEAD^^		: grandparent of latest commit
	git diff HEAD~5		: five commits ago
	git diff HEAD^..HEAD	: second most recent commit vs most recent
	gid diff SHA		: differencews between certain commit
	git diff --stat [branch] [branch2] 	: files different between branches
  
## Diffs 
	git stash						: save current work for later use
	git stash save "message"		: save current work for later use with custom message 
	git stash apply					: rerun changes and 
	git stash apply stash@{index}	: rerun changes of selected stash and it's index
	git stash drop					: remove stash from stash stack
	git stash drop					: remove stash from stash stack
	git stash pop					: stash apply -> stash drop
	git stash save --keep-index		: onlu unstaged files will be stashed
	git stash save --include-untracked	: onlu unstaged files will be stashed
	git stash list --stat 			: any log flags and commands
	git stash show 		 			: more info about latest stash
	git stash clear 		 		: more info about latest stash

## Cherry-pick
	git cherry-pick [SHA]			: copy single commit to other branch
	git cherry-pick --edit [SHA]	: edit message of selected commit
	git cherry-pick --no-commit [SHA1] [SHA1]	: 
	git cherry-pick -x [SHA]		: copy multiple commits into one commit
	git cherry-pick --signoff [SHA]	: Set the name of the cherry-picker

## Bug hunt
	git blame index.html --date short 	: show who, what, when
	git bisect [start|good|bad]	: "binary search" find out when your changes broke the code

## Aliases
	git config --global alias.name  "[command]"
	git config --global alias.lol  "log --graph --decorate --pretty=oneline --abbrev-commit --all"
	git config --global alias.plog 
  
## Calculate commits 
	git shortlog -s 

## Display git history tree
	git log --oneline --decorate --all --graph

## Create alias "tree" to display history tree
	git config --global alias.tree "log --oneline --decorate --all --graph"

## Remote 
	git remote -a						: show tracked remote and local branches
	git remote -r						: show only tracked remote files
	git remote show origin				: show information about origin
	git ls-remote						: show all remote branches
	git push origin :branch_name		: remove branch "branch_name" from remote
	git push origin --delete branch_name	: remove branch "branch_name" from remote
	git remote prune remote_name 		: remove all information about deleted branches 

## Modifying history 
	git filter-branch --tree-filter "some bash script" 	: some dark magic
					  --index-filter

## Tagging 
	git tag -a vTAG -m "message" 
	git push remote_name --tags 	: push all tags to remote 
	git push remote_name v1 		: push certain tag to remote 
	git checkout tag

## Resettings
	git reset --soft HEAD~1 / HEAD^ 		: remove latest changes 
	git reset --hard HEAD~1 / HEAD^ 		: remove latest commit and add every information about it
	git reset --hard [SHA] / HEAD@{INDEX} 	: Can reset a reset. HEAD-section comes from the reflog

	- Getting deleted branch back
	git log --walk-reflogs				: display more information about latest commits/changes/resets/etc
	git branch [branch_name] [SHA]		: create new branch based on the SHA
		or
	git branch [branch_name] HEAD@{index}
  
## Submodules  
	- .gitmodules-file is created
	- submodules does not come with any particular branch so remember to call 'git checkout master'!!!
	- cloning repository with submodules
		- module folder is empty by default
		- it needs to be intialized with:
			git submodule init
			git submodule update 	: clones submodules to the parent project
	- CHANGES IN SUBMODULE HAS TO BE ADDED TO A BRANCH AND PUSHED! NEXT MOVE TO THE PARENT PROJECT, STAGE SUBMODULE FOLDER AND PUSH!

	git branch [submod_branch_name] [SHA]		: create new branch for the submods commit SHA
	git submodule add git@example.com:css.git	: clone submodule called css
	git push --recurse-submodules=check 		: check that all submodules are pushed to the server
	git push --recurse-submodules=on-demand 	: push submodules as well as the parent

