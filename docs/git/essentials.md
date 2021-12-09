# Git basics to get up and running

Inside a new project directory initialize a new git project with the command:

`Note:` enable "show hidden files and folders"
```
git init
```

Show the status (untracked files and other informations):
```
git status
```

Create and edit a new file of your choice (or just use the untracked files) and
after done, save it and send it to the stage area. Type:
```
git add myfile (ie: git add index.html)

git add . // the dot will select all the 'red' files and folders in git status
```

To remove a file from the stage area. Type:
```
git restore --staged myFileOrFolderInStageArea
```

To commit files that are in the stage area use:
```
git commit -m "this is a message to describe our commit, write something clear and meaningful, Initial commit"
```

Different way to make a git commit. After type git commit, press enter and a file
called COMMIT_EDITMSG will open in your editor. Write a message and close the file to save:
```
// and press enter, it will open a file, when done, close the file to save and exit
git commit
```

To check the commit history use:
```
git log

git log --oneline // shorter version of git log
```

Head is like a pointer and is associed with the current branch (probaly the default
branch called master) it points to the last commit, but you can traverse to the
desired one like in a linked list data structure. To show this behaviour and see
relevant information type:
```
git show HEAD

// We can use this to log information about commits, just pass the commit index
// (an interger, HEAD~1 for example), but a thing to know is that HEAD
// access the elements by like an array, so it starts at zero index: [0, 1, 2, 3]
// the length is 4, but the last element is three
git show HEAD~commitIndex
```

To undo the modification of a file, use the checkout command, the file will go back
to the last snapshot:
```
git checkout myModifiedFileName

git checkout . // apply the command on all modified files

git checkout * // similar to the dot
```

The checkout command has other use cases and it's safe cause it's read only:

Go back at a specific stage of the project based on a commit, it will make HEAD
point to that commit (notice that every modification and new files will be deleted):
```
// Set the project to the exactly point of the given commit, we can also use
// HEAD~index instead of commitID
git checkout commitID

git checkout master // Go back to the state before the first checkout and make HEAD point to the last commit again
```

There are other commands that change the timeline of the project, but permanently:

To undo the changes to the project commits history use the revert command, the effect
will be applyied only in the given commit:
``` 
// it will open the COMMIT_EDITMSG, close the file and all the changes will be undone
// and a new commit will be added to the timeline
git revert commitID
```

The Reset command is dangerous, because it can permanently delete content. It has three flags:

* --mixed
* --soft
* --hard

IMPORTANT: the command takes the ID of the ```PREVIOUS```, that is one commit before
the one you want to start deleting.

mixed flag:
The mixed flag is the dafault one, so "git reset commitID" is the same as git reset --mixed commitID

``` 
// removes the commits after the given commitID from the project history and removes
// them from the staging area
git reset commitID

git checkout . // removes the files completaly
```

soft flag:
The difference is that the soft flag does not remove the files from the stage area.
``` 
// it will open the COMMIT_EDITMSG, close the file and all the changes will be
// undone and a new commit will be added to the timeline
git reset --soft commitID

git reset . // remove the files from the stage area

git checkout . // delete the files permanently
```

hard flag:
Removes the commits from the history and delete the files

``` 
// it will open the COMMIT_EDITMSG, close the file and all the changes will be
// undone and a new commit will be added to the timeline
git reset --hard commitID
```

To ignore files and folders from tracking we can use a .gitignore file:
create a new .gitignore file and inside it write the path of files and folders you
don't want that git tracks. Use asterisks (*) to select and ignore all files from
the current path or folder, using * we can ignore files by extension too:
``` 
folderName/*.exe
otherfolder/*
/security/key.pem
```

`Note:` if the gitignore file is created, but there are already files that has been
modified, then our gitignore won't work, we need to clean the history cache:
``` 
git rm -r cached . // clean the history cache
```

To compare the changes of files in history use the diff command:

`Note:` you need to make chenges on files and save first obviously. if there is no
changes it will return nothing.
```
git diff // it will show a lot of information about not staged file versions

git diff --staged // show the diff info of staged files
```

We can compare our current state with any previous state in history by using the
commit hashes or the HEAD pointer.
```
git diff hasheOfTheCommit

git diff HEAD~int
```

To restore a state from the history we can use the restore command:

`Note:` you need to make a change first. it will restore the file to the last known
version on history.
```
git restore fileName
```

We can go back to a specific state on history useing the restore command:

`Note:` we can use the commit hash or the HEAD pointer
```
git restore --source commitHashOfFile fileName
```
