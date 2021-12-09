# Github

First create an account in [Github](https://www.github.com) website

Create a new repository

`Note:` If you want to import a local project don't mark any of the checkboxes in the
Github page (do not mark: create README, gitignore...) cause it can create different
commit histories when pushing the local project, resulting in many problems.

To push a local project to a github repository we can use:

First, we need to connect the repo with our local project. Type:

``` 
// the remoteName is usually called 'origin'. The unique link is provided by github
git remote add remoteName githubRepositoryUniqueLink
```

`Note:` changes made in origin (the remote repository on github) needs to be pulled
to local project and changes made on local project needs to be pushed to the remote
envirnoment, always remember this.

Push locally commited files to github:
``` 
git push origin branchName
```

We can create commits from Github website, but our local code doesn't receive the
change, so we need to pull it using:
```
git pull origin main
```

Origin refers to the remote github repository and main is the default branch that
refers to our local project.

We can create remote branches on Github. It is pretty straigthfword and intuitive.

To create a local branch and track the remote one type:
```
git checkout --track remote/branchName
```
