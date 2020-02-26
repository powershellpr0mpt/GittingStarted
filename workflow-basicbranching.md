# Normal branching workflow - step by step

So you have a Repository on GitHub that works fine, but you want to fix some issues.  

In this case, you might want to leave the `master` branch untouched while working and only push the changes to the `master` branch when everything works as intended.  
In this case, you might want to create a new branch and allow yourself to work on issues [be it features, enhancements or bugfixes] without it directly affecting the `master` branch.

This workflow describes the steps/actions required to do so in a very basic manner.

**Side note:**  
This assumes a basic workflow for a common scenario, where the user is working with an already cloned Repository from GitHub.
There are of course exceptions to this scenario, but this workflow only describes the common steps required.

## On Local machine

Starting point is a single `master` branch with a single commit.  
![Repo1][Repo1]

Create a new branch

```git
git checkout -b <newbranch>
```

Your local repository will now look like this:  
![Repo2][Repo2]  

Add changes to new branch

```git
git add .
```

Commit changes to new branch

```git
git commit -m "message"
```

Your local repository will now look like this:  
![Repo3][Repo3]  
However your remote GitHub repository will remain unchanged.

Push new branch and its changes to remote (GitHub)

```git
git push origin <newbranch>
```

## On GitHub

Go on GitHub and create a Pull request based on the new branch

`github -> compare & pull request`

`github -> base master -> compare <newbranch> -> create pull request`

Merge the pull request into the `master` branch once the pull request has been approved

`github -> merge pull request`

Your remote GitHub repository will now look like this:
![Repo4][Repo4]  

Delete the new branch from GitHub once the merge has completed

`github -> delete <newbranch>`

## Back on Local machine

Your local repository has not yet merged the branches and still looks like  
![Repo3][Repo3]

Change working branch to `master`

```git
git checkout master
```

Get the changes from GitHub and merge in local `master` branch

```git
git pull origin master
```

![Repo4][Repo4]  
Now your local repository is in the desired state and all that's left is some clean-up work!

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

[Repo1]: https://github.com/powershellpr0mpt/GittingStarted/blob/master/images/Repo1.png
[Repo2]: https://github.com/powershellpr0mpt/GittingStarted/blob/master/images/Repo2.png
[Repo3]: https://github.com/powershellpr0mpt/GittingStarted/blob/master/images/Repo3.png
[Repo4]: https://github.com/powershellpr0mpt/GittingStarted/blob/master/images/Repo4.png
