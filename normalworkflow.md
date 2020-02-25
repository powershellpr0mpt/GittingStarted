# Normal branching workflow - step by step

## On Local machine

Create a new branch

```git
git checkout -b <newbranch>
```

Add changes to new branch

```git
git add .
```

Commit changes to new branch

```git
git commit -m "message"
```

Push new branch and its changes to remote

```git
git push origin <newbranch>
```

## On GitHub

Go on GitHub and create a Pull request based on the new branch

`github -> compare & pull request`

`github -> base master -> compare <newbranch> -> create pull request`

Merge the pull request into the master branch once the pull request has been approved

`github -> merge pull request`

Delete the new branch from GitHub once the merge has completed

`github -> delete <newbranch>`

## On Local machine

Change working branch to master

```git
git checkout master
```

Get the changes from GitHub and merge in local master branch

```git
git pull origin master
```

Delete the new branch from the local machine

```git
git branch -d <newbranch>
```

Delete the new branch from the remote branch view

```git
git branch -a
git fetch -p
git branch -a
```
