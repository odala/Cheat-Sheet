# Git for Dummies

VIEW STATUS OF REPOSITORY

    git status

ADD TO STAGING AREA

    git add <file>

COMMIT

    git commit -m "<write what the commit of the staged files do>"
    
DISCARD ALL LOCAL CHANGES

    git reset --hard

PUSHING TO A REMOTE

    git push origin master		# REMOTENAME = origin, BRANCHNAME = master

PULLING FROM A REMOTE
    git pull origin master
 
INITIALIZE A DIRECTORY AS A REPOSITORY

    git init
    git add			# adds the files in the local repository and stages them for commit
    git commit -m 'First commit.'
    git remote add origin <remote repository URL>	# sets the new remote
    git remote -v		# verifies he new remote URL
    git push origin master	# pushes the changes in your local repository up to the remote repository

DELETE A FILE FROM THE REPO AND / OR THE LOCAL FILE SYSTEM

    git rm file.txt			# remove the file from the repo AND delete it from the local file system (doesn't mind if the file is already deleted manually)
    git rm --cached file.txt	# remove the file from the repo, DO NOT delete it from the local file system 
    git rm $(git ls-files --deleted)# removes all deleted files from the repo

CREATE A .gitignore

    touch .gitignore	# creates a local .gitignore file in the repo
    git config --global core.exludefile ~/.gitignore_global	# creates a global .gitignore_global file for ignoring files in every git repo on your computer
    
NEW BRANCH

    git checkout -b iss53

the same as

    git branch iss53
    git checkout iss53
    
BRANCHING

    git checkout <name of branch>
    git pull origin <name of branch>
    git push origin <name of branch>
    
LIST ALL BRANCHES (-a gives also those not local to your workspace)

    git branch -a
    
MERGE BRANCH WITH MASTER

    git checkout master
    git pull origin master
    git merge <branch name>
    git push origin master
    
REMOVE BRANCH LOCALLY
    
    git branch -d <branch name>
    
REMOVE BRANCH REMOTE

    git push origin --delete <branch name>
    
STASHING

    git stash
    git stash list
    git stash apply
    git stash apply stash@{2}
    git stash drop stash@{2}
