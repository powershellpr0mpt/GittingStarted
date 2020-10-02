# Working with ![Git][GitLogo]

This guide is made to provide a tutorial on how to work with Git using my personal experience and hopefully will help others learn from my mistakes/teachings.

While it can definitely be handy to learn more about the inner workings of Git by using [the official Git documentation][GitDocs] or books such as [Learn Git in a Month of Lunches][GitMoL].

I've noticed that actually playing with Git and DOING the basics will get you started so much quicker and will make the documentation so much easier to grasp.

## What is Git

For some people, you might know what Git is and just need to get familiar with the actual usage of the product.

For people that are completely new to Git, I would suggest reading the [official What is Git documentation][WhatIsGit].  
One snippet from this that really helped me grasp Git a bit better is the following:

> The major difference between Git and any other Version Control Systems (VCS) is the way Git thinks about its data.  
> Conceptually, most other systems store information as a list of file-based changes.
> Git doesn’t think of or store its data this way.  
> Instead, Git thinks of its data more like a series of snapshots of a miniature filesystem.  
> With Git, every time you commit, or save the state of your project, Git basically takes a picture of what all your files look like at that moment and stores a reference to that snapshot.

So instead of your versioning system being updated every time you Save a file, Git gets updated everytime you commit a change.

This means that while working on a file, you might be able to save/change it 20 times, but if you only commit it once, this is the new state (snapshot) of your file.

---

## Prerequisites

* A [GitHub][GitHub] account
* The [Git Client][GitClient] installed locally.  
A simple **Next** -> **Next** -> **Finish** installation will suffice

---

## Tasks explained in this guide

* [Set a required minimal default configuration for git on your local machine](#Set-a-required-minimal-default-configuration-for-git-on-your-local-machine)
* [Create a repository on GitHub](#Create-a-repository-on-GitHub)
* [Create a local copy of a repository to your local machine (clone)](#Create-a-local-copy-of-a-repository-to-your-local-machine-(clone))
* [View current status of the local copy](#View-current-status-of-the-local-copy)
* [Make a local change](#Make-a-local-change)
* [Revert a local change](#Revert-a-local-change)
* [Make a remote change](#Make-a-remote-change)
* [View the remote repositories your local copy is connected to](#View-the-remote-repositories-your-local-copy-is-connected-to)
* [Make a local change available on the GitHub repository (push)](#Make-a-local-change-available-on-the-GitHub-repository-(push))
* [Make a remote change available on your local copy (pull)](#Make-a-remote-change-available-on-your-local-copy-(pull))

### More advanced tasks for if you're comfortable the above tasks

* [Working with branches](#Working-with-branches)
* [Forking a repository (collaborating)](#Forking-a-repository-[collaborating])
* [Making a local change available on the original repository (pull request)](#Making-a-local-change-available-on-the-original-repository-[pull-request])
* [Merging pull requests](#Merging-pull-requests)

### Repeatable excercises

* [Start a new project](#Start-a-new-project)
* [Revert to your original project state](#Revert-to-your-original-project-state)
* []

---

## Set a required minimal default configuration for git on your local machine

Once you have the [Git Client][GitClient] installed on your local machine, you need to define a username and email address to which your commits will be attributed to.

You can [configure][GitConfig] this easily by running the following command either using Git Bash or your favourite commandline application if you have Git added to your PATH. In my case, using PowerShell works just fine.

```git
git config --global user.email "you@example.com"
git config --global user.name "your name"
```

Any time you make a commit (change), it will add these details so you can track who made changes to your repository.

## Create a repository on GitHub

Click on the New Repository icon ![New Repo][GitNewRepo1] on your GitHub account page or click the <kbd>+</kbd> icon in the top-right of the site and select `New Repository` ![New Repo][GitNewRepo]  
to create a new repository.

Choose a repository name that's representative and select if you want the contents of the repository to be seen publicly or privately only. You can change all of these settings later if needed.

There's no need to add a README file, .gitignore file or even a license for now.  
Once you get more comfortable with Git, you'll know exactly which you want to add, where and why.

## Create a local copy of a repository to your local machine (clone)

On GitHub, go to the repository you want to work on.
Click on the `Clone or Download` button to obtain the link to your repository

On the Client, go to a folder in which you want to have the files for this repository.  
Do note, it will make a subfolder with the name of the repository in there for you, so you don't have to pre-create a subfolder for this.
Enter the following command:

```git
git clone <url>
```

for example

```git
cd C:\Git
git clone https://github.com/powershellpr0mpt/GittingStarted.git

Cloning into 'GittingStarted'...
remote: Enumerating objects: 50, done.
remote: Counting objects: 100% (50/50), done.
remote: Compressing objects: 100% (28/28), done.
remote: Total 50 (delta 12), reused 41 (delta 10), pack-reused 0
Unpacking objects: 100% (50/50), done.
```

Will create `C:\Git\GittingStarted`, containing the content of the GitHub repository

For more details on the command usage and all options visit [here][GitClone].

## View current status of the local copy

As the description says, you can see if there are changes available for Git to work with using the following command:

`git status`

As expected, this command will do nothing else but tell you what the current status of your repository is compared to its last commit.  
IT can tell you if there are changes available which require action, no changes at all or perhaps a mix of staged and unstaged changes (you'll learn more about the types of changes [later](#Make-a-local-change)):

```git
git status

On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
```

or perhaps

```git
git status

On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   readme.md
```

For more details on the command usage and all options visit [here][GitStatus].

## Make a local change

Git will automatically try to track all changes within the local copy directory structure (the *Working directory*).  
You will have to tell Git which files you actually want to have in your versioning and you need to add them to a so-called *Staging area* before you can commit them to your local repository.

![change areas][CommitWorkflow]

Git will inform you about new files which are not yet staged by using the previously learnt `git status` command:

```git
git status

On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   readme.md

no changes added to commit (use "git add" and/or "git commit -a")
```

As the status mentions, you can add the changes to commit by using the `git add` coimmand, where you either specify exactly which file you want to commit (`git add readme.md`), or you can also specify folders to add or simplt add everything (`git add .`).

Using `git status` will then tell you the updated status:

```git
git add readme.md

git status

On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   readme.md
```

By specifying single files you can also stage changes in separate commits (in case you've been editing multiple files, but a change has a separate 'goal').

For more details on the command usage and all options visit [here][GitAdd].

Now that you have staged your changes, you want to commit the changes to your local repository:

```git
git commit -m "<message with info what happens when you apply the commit>"
```

so for example you've updated the readme.md file (the file you're actually reading now), you'll say something like this:

```git
git commit -m "Add information on how to make a local change with Git"
```

Once you have commited the change, your repository is "updated" with these changes.  
Consider it as if you've just created a new snapshot of your repository with the latest changes.

For more details on the command usage and all options visit [here][GitCommit].

## Revert a local change

### Revert before you added and tracked the change
In case you've made a change to a file in the Working Directory but not yet added the file to the Staging Area, you can easily revert back to the previous version using the `restore` command.

For example if you've made a change to *Hello.html* which you shouldn't have, first check the status of your repo using `git status` as usual:

```git
$ git status
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git restore <file>..." to discard changes in working directory)
#
#   modified:   hello.html
#
no changes added to commit (use "git add" and/or "git commit -a")
```

The file is marked as modified, but not yet staged.  
You can go back to the "previous" state of the file using the `git restore` command (you CAN also use `git checkout -- <file>`, however this has been changed in [GitCL][git v2.23.0] in favour of `git restore`).

```git
git restore Hello.html

```

For more details on the command usage and all options visit [here][GitRestore].

### Revert after you've added/tracked the change, but not yet committed

In case you've made a change to a file in the Working Directory and you've added the file to the Staging Area, you can revert back to the previous state using the `git restore` command as well, but using different switches.

Again, first check the status of your repo using `git status`:

```git
git status

On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   Hello.html
```

The file is marked as tracked in the Staging Area and ready to be committed

```git
git restore --staged Hello.html
```

removes the file from the Staging Area, but still marks it as Modified.  
You can now follow the [RemoveBeforeTrack][instructions under the previous section] to also restore the file to its previous state.

## Make a remote change

In this example we're going to generate a remote change through the GitHub webinterface, but a remote change can be innitiated from another device or another user in a similar manner as we will explain

## View the remote repositories your local copy is connected to

If you followed the steps above correctly and cloned your repository from your GitHub account to your local machine, your repository will always have a "remote link" to the GitHub repository, allowing you to add your changes ([push](#Make-a-local-change-available-on-the-GitHub-repository-(push))) to the remote repository as well as getting changes ([fetch/pull](#Make-a-remote-change-available-on-your-local-copy-(pull))) from the remote repository.

But in order to do this, you need to know how Git has configured them, if at all!  
This is where the following command comes in handy:

```git
git remote -v

origin  https://github.com/powershellpr0mpt/GittingStarted.git (fetch)
origin  https://github.com/powershellpr0mpt/GittingStarted.git (push)
```

This shows you remote connections in the following format:

```git
<remote name> <remote url> <purpose>
```

For future use, the most important thing to get from this is the `remote name`, so mostly *origin*.

You can add/remove remote connections as you see fit, thus allowing you to rename them if you want to.
By default, the remote repository where you cloned data from will be called `origin`.

For more details on the command usage and all options visit [here][GitRemote].

## Make a local change available on the GitHub repository (push)

So you've made a change, but you want the change to be visible and accessible on GitHub.  
This means you will need to send (push) your changes to the remote repository.

You can do this by using the following command:

```git
git push <remote name> <branch>
```

As we found in [our previous excercise](#View-the-remote-repositories-your-local-copy-is-connected-to), by default your remote will be called `origin` and your branch will be called `master`.
So "normally" it should look like this:

```git
git push origin master

Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 332 bytes | 166.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/powershellpr0mpt/GittingStarted.git
   246e29d..ae5b3b1  master -> master
```

This works fine unless the remote location has an update you don't yet have locally.  
In this case you'll see something like this:

```git
git push origin master

To https://github.com/powershellpr0mpt/GittingStarted.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/powershellpr0mpt/GittingStarted.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

If this happens you will first need to retreive the update from the remote location before you can update it.  
How to do this can be found in the next section.

For more details on the command usage and all options visit [here][GitPush].

## Make a remote change available on your local copy (pull)

Similar to pushing changes to a remote repository, you can pull changes from a remote repository using the following format:

```git
git push <remote> <branch>
```

As we found in [our previous excercise](#View-the-remote-repositories-your-local-copy-is-connected-to), by default your remote will be called `origin` and your branch will be called `master`.
So "normally" it should look like this:

```git
git pull origin master

From https://github.com/powershellpr0mpt/GittingStarted
 * branch            master     -> FETCH_HEAD
Updating 2342d9c..2413c4b
Fast-forward
 readme.md | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
 ```

This will update your local repository to have at least the same changes as the remote repository.  
In case you have more updates locally, this will now allow you to [push](#Make-a-local-change-available-on-the-GitHub-repository-(push)) your most recent changes to the remote repository.

 For more details on the command usage and all options visit [here][GitPull].

## Working with branches

## Forking a repository [collaborating]

## Making a local change available on the original repository [pull request]

## Merging pull requests

---

## Recommended configuration settings

### Git configuration

For when you start doing more advanced things in Git [branch related work], you might want to add the following configuration to your Git installation:

```git
git config --global alias.lol "log --graph --decorate --pretty=oneline --all --abbrev-commit" 
```

This will allow you to run `git lol` which does the same as running `git log --graph --decorate --pretty=oneline --all --abbrev-commit` .  
Basically giving you a nice somewhat graphical overview of all your commits, including brances etc. from within your command line experience.

### PowerShell configuration

#### Posh-Git module

Seeing that I'm a PowerShell user, that's my command line experience of choice.  
For me this means I'd love to see the status of my local Git copy.

Luckily a user by the name of [Keith Dahlby][dahlbyk Twitter] created the PowerShell module [Posh-Git][Posh-Git Github].

As per it's GitHub page, this module does the following:

> posh-git is a PowerShell module that integrates Git and PowerShell by providing Git status summary information that
> can be displayed in the PowerShell prompt, e.g.:
>
> ![C:\Users\Keith\GitHub\posh-git [master ≡ +0 ~1 -0 | +0 ~1 -0 !]> ][prompt-def-long]
>
> posh-git also provides tab completion support for common git commands, branch names, paths and more.
> For example, with posh-git, PowerShell can tab complete git commands like `checkout` by typing `git ch` and pressing
> the <kbd>tab</kbd> key. That will tab complete to `git checkout` and if you keep pressing <kbd>tab</kbd>, it will
> cycle through other command matches such as `cherry` and `cherry-pick`. You can also tab complete remote names and
> branch names e.g.: `git pull or<tab> ma<tab>` tab completes to `git pull origin master`.

It's a great module to have around when you're working with PowerShell, but you do have to account that it only "triggers" or "shows up" when you're working in a folder that actually is initiated by Git [had a .git folder].

You can install this module by running the following command in PowerShell:

```powershell
Find-Module -Name Posh-Git -Repository PSGallery | Install-Module
```

##### Posh-Git in your PowerShell profile

Since you'll be wanting to use Git as much as possible [if you're not already, hopefully you will want to after this guide], you might want to have the functionality of the Posh-Git module available whenever you're working in PowerShell.

In order to do this, you can add the following code to your PowerShell profile:

```powershell
notepad $profile.CurrentUserAllHosts
```

and adding the following code:

```powershell
Import-Module -Name Posh-Git
```

To see what else you could do in your profile, you might want to see [my example profile here][PowerShell Profile].

[GitLogo]: https://github.com/powershellpr0mpt/GittingStarted/blob/master/images/git_logo.png
[GitDocs]:https://git-scm.com/doc
[GitMoL]:https://www.manning.com/books/learn-git-in-a-month-of-lunches
[WhatIsGit]:https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F
[GitHub]:https://github.com/join
[GitClient]:https://git-scm.com/downloads
[GitConfig]:https://git-scm.com/docs/git-config
[GitNewRepo]:https://github.com/powershellpr0mpt/GittingStarted/blob/master/images/github_newrepo.png
[GitNewRepo1]:https://github.com/powershellpr0mpt/GittingStarted/blob/master/images/github_newrepo1.png
[GitClone]:https://git-scm.com/docs/git-clone
[GitStatus]:https://git-scm.com/docs/git-status
[CommitWorkflow]:https://github.com/powershellpr0mpt/GittingStarted/blob/master/images/git_commitworkflow.png
[GitAdd]:https://git-scm.com/docs/git-add
[GitCommit]:https://git-scm.com/docs/git-commit
[GitRemote]:https://git-scm.com/docs/git-remote
[GitPull]:https://git-scm.com/docs/git-pull
[GitPush]:https://git-scm.com/docs/git-push
[GitRestore]:https://git-scm.com/docs/git-restore
[RemoveBeforeTrack]:(#revert-before-you-added-and-tracked-the-change)
[GitCL]: https://github.com/git/git/blob/306ee63a703ad67c54ba1209dc11dd9ea500dc1f/Documentation/RelNotes/2.23.0.txt#L61
[dahlbyk Twitter]:https://twitter.com/dahlbyk
[Posh-Git GitHub]:https://github.com/dahlbyk/posh-git
[PowerShell Profile]:https://gist.github.com/powershellpr0mpt/e03a2809db23c890d58d1a889961cbc9
[prompt-def-long]: https://github.com/powershellpr0mpt/GittingStarted/blob/master/images/posh-git.png  "~\GitHub\posh-git [master ≡ +0 ~1 -0 | +0 ~1 -0 !]> "
