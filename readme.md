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
* [Make a local change](#Make-a-local-change)
* [Revert a local change](#Revert-a-local-change)
* [Create a local copy of a repository to your local machine (clone)](#Create-a-local-copy-of-a-repository-to-your-local-machine-(clone))
* [View current status of the local copy](#View-current-status-of-the-local-copy)
* [View the remote repositories your local copy is connected to](#View-the-remote-repositories-your-local-copy-is-connected-to)
* [Make a local change available on the GitHub repository (push)](#Make-a-local-change-available-on-the-GitHub-repository-(push))
* [Make a remote change available on your local copy (pull)](#Make-a-remote-change-available-on-your-local-copy-(pull))

### More advanced tasks for if you're comfortable the above tasks

* [Working with branches](#Working-with-branches)
* [Forking a repository (collaborating)](#Forking-a-repository-[collaborating])
* [Making a local change available on the original repository (pull request)](#Making-a-local-change-available-on-the-original-repository-[pull-request])
* [Merging pull requests](#Merging-pull-requests)

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

Click the <kbd>+</kbd> icon and select New Repository, or click on the New Repository icon on your GitHub account page to create a new repository.

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
```

Will create `C:\Git\GittingStarted`, containing the content of the GitHub repository

## View current status of the local copy

As the description says, you can see if there are changes available for Git to work with using the following command:

`git status`

This can tell you if there are changes available which require action, or no changes at all:

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

As the status mentions, you can add the changes to commit by using the `git add` coimmand, where you either specify exactly which file you want to commit (`git add readme.md`), or you can also specify folders or everything (`git add .`).

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

Now that you have staged your changes 

## Revert a local change

## View the remote repositories your local copy is connected to

```git
git remote -v
```

## Make a local change available on the GitHub repository (push)

```git
git push <remote> <branch>
```

By default your remote will be called `origin` and your branch will be called `master`.
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

## Make a remote change available on your local copy (pull)

## Working with branches

## Working with GitHub Issues

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

[GitLogo]: https://git-scm.com/images/logo@2x.png
[GitDocs]:https://git-scm.com/doc
[GitMoL]:https://www.manning.com/books/learn-git-in-a-month-of-lunches
[WhatIsGit]:https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F
[GitHub]:https://github.com/join
[GitClient]:https://git-scm.com/downloads
[GitConfig]:https://git-scm.com/docs/git-config
[GitStatus]:https://git-scm.com/docs/git-status
[CommitWorkflow]:https://git-scm.com/book/en/v2/images/areas.png
[GitCommit]:https://git-scm.com/docs/git-commit
[GitRemote]:https://git-scm.com/docs/git-remote
[GitPull]:https://git-scm.com/docs/git-pull
[GitPush]:https://git-scm.com/docs/git-push
[dahlbyk Twitter]:https://twitter.com/dahlbyk
[Posh-Git GitHub]:https://github.com/dahlbyk/posh-git
[PowerShell Profile]:https://gist.github.com/powershellpr0mpt/e03a2809db23c890d58d1a889961cbc9
[prompt-def-long]: https://github.com/dahlbyk/posh-git/wiki/images/PromptDefaultLong.png   "~\GitHub\posh-git [master ≡ +0 ~1 -0 | +0 ~1 -0 !]> "
