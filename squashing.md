# Git squashing - cleaning up your history

Working with git can create quite the commit history.  
If you want to clean up some of the history (mostly the `woops, typo` and `another commit` messages that are of no use), you might want to look into squashing your commits.

You can do this in one of 2 ways:

1. Squashing in your current branch
1. Squashing on a merge into a new branch

## Why would you choose one over another?  

**Squashing in your current branch** allows you to clean up your current branch without having to merge with another branch.

This can change your commit history from this:  
![Commit history before squash](images/squash_before.png)

To this:

![Commit history after squash](images/squash_after.png)


When using the **Squashing on a merge option**, a completely merged branch (with potentially dozens of commits) will look as if it was simply a single commit on the branch you're merging on.  
So for example you want to merge `feature1` onto `main`, the merge will look like a commit on `main`, not actually branching out to/from `feature1`.

![Squash merge looks like a commit](images/squash_merge_commit.png)

## Squashing in your current branch

Squashing in your current branch can be done through the use of the `git rebase` command.  
Now **don't immediately start ramming your keyboard** and executing this, there's some nuance to this, as [rebase](https://git-scm.com/docs/git-rebase) is a rather powerfull (and destructive) command if you use it incorrectly.

The rebase command rewrites/deletes history through a new commit and removing previous commits on the way.  
How to use it is as follows:

`git rebase -i <commit to look back at>`

for example

`git rebase -i HEAD~3`  
which means HEAD (current location) + 2 commits back (the last 3 commits)

or

`git rebase -i c2d0fd3`  
which means all the commits from now (HEAD) untill **c2d0fd3**.

Tip: you can find your commits by using `git log --oneline`

![git log --oneline](images/squash_git_log.png)

### Example of squashing in your current branch

Let's take `git rebase -i c2d0fd3` as an example

This will start the **rebase** in [**interactive**](https://git-scm.com/docs/git-rebase#Documentation/git-rebase.txt---interactive) mode and takes the last commits since **c2d0fd3** and will let you define what to do with them.

It will open your favourite editor with a `/.git/rebase-merge/git-rebase-todo` file which you need to manually edit and say what you want to squash (or take other actions on).  

![Example squash todo](images/squash_example_before.png)

It includes more information on what the options are, but we'll narrow it down to what is needed for the squash: `squash` or `s`.

Leave the commit you want latest on `pick` (take into account that this means the files, not the commit message, you can change this later).

Set all the commits which you want to squash to `squash`, leave the rest of the commits as they are (`pick`) and **save and close** the file.

![Example squash changed](images/squash_example_after.png)

It will then open your favourite editor with a `/.git/COMMIT_EDITMSG` file in which you need to define what commit messages you want to include on your latest commit.  
Do note that you by default it will leave all commit history messages available in your latest commit, but you can edit it here to either include all messages, parts or nothing at all.  

![Example commit message history before](images/squash_commit_before.png)

The easiest thing to do is to comment everything out that you don't want with a `#` and leave what you want to be the commit message uncommented.

![Example commit message history after](images/squash_commit_after.png)

**Save and close** this file and presto chango, git will rebase with your input and history has been rewritten!

![Final squash result](images/squash_git_log_after.png)


Because you've re-written history, you can't simply push the current changes to your online git repository, as it will think you are behind (since according to online you're missing certain commits).  
![Error pushing to repository](images/squash_error_push.png)

You will have to force push your changes to online to update the future using  
`git push origin <branch> -f`  
![Force push to repository](images/squash_push.png)


## Squashing on a merge into a new branch

Now this is the "easiest" of the 2 options and will be the most commonly used if everything is done right.  
Most of the time you will have a `main` branch which will be locked/protected from merging, thus requiring a `Pull Request` before changes onto it can be merged.  
Once you want to Complete the Pull Request, you can choose what kind of merge you want to apply.

In this situation you want to look at the Squash Merge option.  

### Azure DevOps

In Azure DevOps this can be easily done through the "Complete pull request" wizard, [selecting the correct Merge type](https://learn.microsoft.com/en-us/azure/devops/repos/git/merging-with-squash?view=azure-devops#complete-pull-requests-with-squash-merge)

![Complete Merge Azure DevOps](images/squash_devops1.png)
![Select Merge type Squash commit Azure DevOps](images/squash_devops2.png)


### GitHub

In GitHub this can be done by selecting the dropdown option on `Merge pull request` and selecting `Squash and merge` when you're ready to merge your Pull Request.
![Squash and Merge GitHub](images/squash_github.png)

Simply Click `Squash and merge`, fill in the new commit message and `Confirm squash and merge`.
![Squash and Merge Github commit](images/squash_github2.png)

If you don't have the option directly available in GitHub, this might be restricted by the repository owner. You can configure the option as described [here](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/configuring-commit-squashing-for-pull-requests).
