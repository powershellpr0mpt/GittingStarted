# Getting used to working with Git - Real life examples and instructions

This guide is made to provide a tutorial on how to work with Git using my personal experience and hopefully will help others learn from my mistakes/teachings.

While it can definitely be handy to learn more about the inner workings of Git by using [the official Git documentation][GitDocs] or books such as [Learn Git in a Month of Lunches][GitMoL].

I've noticed that actually playing with Git and DOING the basics will get you started so much quicker and will make the documentation so much easier to grasp.

## Tasks explained in this guide

1. Set a required minimal default configuration for git on your local machine
1. Create a local copy [clone] of a repository to your local machine
1. View current status of the local copy 
1. View the remote repositories your local copy is connected to
1. Make a local change available on the GitHub repository [push]
1. Make a remote change available on your local copy
1. Revert a local change
1. Working with branches
1. Working with GitHub Issues
1. Forking a repository
1. Making a local change available on the original repository [pull request]
1. Merging pull requests

## Repeatable excercises to practice

* Create repository
* Clone a repository
* Make local change available remote
* Creating a branch
* Fork a repository
* Creating a pull request for a repository not owned by you

---

## Prerequisites

* A [GitHub][GitHub] account
* [Git Client][GitClient] installed locally

---

## Set a required minimal default configuration for git on your local machine

Once you have the [Git Client][GitClient] installed on your local machine, you need to define a username and email address to which your commits will be attributed to.

You can configure this easily by running the following command either using Git Bash or your favourite commandline application if you have Git added to your PATH. In my case, using PowerShell works just fine.

```git
git config --global user.email "you@example.com"
git config --global user.name "your name"
```

Any time you make a commit [change], it will add these details so you can track who made changes to your repository.

### Recommended configuration settings

#### Git configuration

For when you start doing more advanced things in Git [branch related work], you might want to add the following configuration to your Git installation:

```git
git config --global alias.lol "log --graph --decorate --pretty=oneline --all --abbrev-commit" 
```

This will allow you to run `git lol` which does the same as running `git log --graph --decorate --pretty=oneline --all --abbrev-commit` .  
Basically giving you a nice somewhat graphical overview of all your commits, including brances etc. from within your command line experience.

#### PowerShell configuration

##### Posh-Git module

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

###### Posh-Git in your PowerShell profile

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

## Create a local copy [clone] of a repository to your local machine

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
C:\Git
git clone https://github.com/powershellpr0mpt/GittingStarted.git
```

Will create `C:\Git\GittingStarted`, containing the content of the GitHub repository

## View current status of the local copy

## View the remote repositories your local copy is connected to

## Make a local change available on the GitHub repository [push]

## Make a remote change available on your local copy

## Revert a local change

## Working with branches

## Working with GitHub Issues

## Forking a repository

## Making a local change available on the original repository [pull request]

## Merging pull requests

[GitDocs]:https://git-scm.com/doc
[GitMoL]:https://www.manning.com/books/learn-git-in-a-month-of-lunches
[GitHub]:https://github.com
[GitClient]:https://git-scm.com/downloads
[dahlbyk Twitter]:https://twitter.com/dahlbyk
[Posh-Git GitHub]:https://github.com/dahlbyk/posh-git
[PowerShell Profile]:https://gist.github.com/powershellpr0mpt/e03a2809db23c890d58d1a889961cbc9
