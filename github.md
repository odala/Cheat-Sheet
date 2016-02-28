# GitHub for dummies

VIEW STATUS OF REPOSITORY

    git status

ADD TO STAGING AREA

    git add <file>

COMMIT

    git commit -m "<write what the commit of the staged files do>"

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