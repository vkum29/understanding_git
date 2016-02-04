Git understanding

//WHY GIT
  VCS
  CVCS
  DVCS

PS:GIT is DVCS


//SETUP
 	//Install 
  	http://git-scm.com/download/<os> //linux  or mac or win for installer and setup


  	//GIT config: values stored in .gitconfig file in repo or user directory(global)
		//set or view user email
		git config [--global] user.email [value]

		//Set or view username
		git config [--global] user.name [value]

		//SET default Message editor
		git config [--global] core.editor <application>

		//SET diff tool to view file differences
		git config --global diff.tool <toolapp>
		to use configure difftool use command: git difftool

		//SET merge tool to view file differences and merge files
		git config --global merge.tool <toolapp>
		to use configure mergetool use command: git mergetool

		//Reference: 
		https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup
		http://stackoverflow.com/questions/1881594/use-winmerge-inside-of-git-to-file-diff

		PS: With value the command works as setter and without it behaves as getter also --global sets the value for all git projects untill unless overridden by local configuration


 //Commands
 	//SET GIT REPO
 		git init //intializes an empty directory as git repo

 	//Get an existing repo from github to local system
		git clone <repo url> //clones url with its last name as dir
			eg: git clone git://DI/XX/repo.git will create repo under a folder repo
		git clone <repo url> <[path/]foldername> //to clone to a specific empty folder or new folder use 

	//Setup a branch or feature branch to add your changes
		git branch <branch-name> //will create a branch from the current branch you are in
		git branch -d  <branch-name> //to delete a branch 
		git branch -D <branch-name> //to delete a branch which has files in 1,3,4 state( please see git status below for state details). 

		PS: you can't delete if you are in that branch, checkout to some other branch and then delete it.


 	//ADD files/folder/changes in repo
 		git add . or git add --all //moves all changes into the stage state
 		git add -u //adds any modified files into the stage 

 	//MARK changes as retrivable changes
 		git commit //  moves staged changes as a history and ensures the changes will not be lost only after you successfully enter the commit message in opened prompt.
 		git commit -m <msg> //is one lline command to confirm your staged changes with specifc commit message qnd stores it for retrival 
 		git commit --amend // to be used only for un pushed changes and modify last commit to include any missed changes or update commit message

 	//View the state of changes/files/folder after any action performed on files/folder
	 	git status //shows the state of files and folders in the repo it can be any of following
		 	1. Untracked files - new files/changes which were earlier not tracked by git
		 	2. unmodified files - files/changes which were commited into git repo
		 	3. modified files - tracked files/changes which are changed and not commited in repo
		 	4. staged files - files after performing git add these are snapshot entries ready to saved as retrivable content
		git status -s or git status --short //retruns one liner status for all files in state 1,3 or 4 in format  
			XY file path
			where X and Y represent state of file with respect to stage and unstage respectively values could be untracked(?) or Added(A) or Modified (M)
	
	//Get logs to retrive the action taken by various people or files changed in a commit
		git log //retrives information realted to commits in branch
		git log -<n> // will log details only on last n commits
		git log -p // will show you difference or changes made in that commit is useful for review

	//View difference between two files
		git diff [file-name] // will show the stage vs unstaged difference between metioned file
		PS: not specifying file-name will loop thorugh all modified files.
		git diff --cached [commit] <file-name> // will show the difference in modified (specified) file with respsect to head or specified commit


	//RESET : will only mark the changes to modified and unstage so that a commit will not save those files
		git reset HEAD <file-name> // to unstage a change (changes which are ready for commit i.e changes on which you used git add and are awaiting git commit).


	//CHECKOUT : 
		git checkout [--] <file-name> //When used on a modified files removes any cahnges made in that file if cahnges were unstaged.
		git checkout -b <branch-name> //to create a feature branch from current branch and navigate to same.
		git checkout <branch-name> // to switch to an existing branch

	//REMOTE:
		git remote //lists only the remote tracked in your local repo
		git remote -v //list remotes with url you have configred for tracking on local branch
		git remote add <remote-name> <url> //will add a new remote to track files
		git remote show <remote-name> // will show more details on remote and how/which branches it is tracked against
		git remote rename <remote-old-name> <remote-new-name> // to change name reference used for a remote branch
		git remote rm <remote-name> // to untrack a remote repo 
		git remote set-url <remote-name> <remote-url> // to edit existing or to create a new remote tracking for local repo.

	//FETCH:
		git fetch [-p] <remote-name> //brings down the references for all branches in remote repo
		//use of -p will delete a branch refrence from remote if they are not avialble at remote
		PS: this doesnot mean a branch will be deleted from local repo.

	//PUSH:
		git push [remote-name] [branch-name] //to send commits to specified remote in specified branch 
	
	//PULL:
		git pull [remote-name] [branch-name] //to get content from specified remote of specified branch into current branch
		git pull --rebase [remote-name] [branch-name] //to apply remote branch changes first and on top apply your changes

	//REBASE
		git rebase <branch-name> [target-branch]//will rebase current or target branch(if specified) on top of specified branch
		git rebase --continue // after resolving conflicts to continue with ongoing rebase
		git rebase --abort // incase you don't want to perform rebase and rollback to before git rebase command state.

	//MERGE
		git merge <branch-name> [target-branch]//will merge the specified branch changes into current branch
		git merge --continue // after resolving conflicts to continue with ongoing merge
		git merge --abort // incase you don't want to perform merge and rollback to before git merge command state.

	//STASH
		git stash // create a dump of unstaged modifications onto a seprate buffer space
		git stash list // list all stash branch
		git stash apply @satsh{n} //

	//delete a file in git
		git rm [--cached] [file-name] // deletes specified file from tracking in git also deltes from system if --cached is not given

	//rename a file
		git mv <old-file-name> <new-file-name>


	ABOUT FORK WAY OF WORKING

Reference:
	https://git-scm.com/docs
	https://git-scm.com/book/en/v2
