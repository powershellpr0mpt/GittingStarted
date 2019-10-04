# Getting used to working with Git - Real life examples and instructions

This guide is made to provide a tutorial on how to work with Git using my personal experience and hopefully will help others learn from my mistakes/teachings.
While it can definitely be handy to learn more about the inner workings of Git by using the official Git documentation [https://git-scm.com/doc] or books such as Learn Git in a Month of Lunches [https://www.manning.com/books/learn-git-in-a-month-of-lunches], 
I've noticed that actually playing with Git and DOING the basics will get you started so much quicker and will make the documentation so much easier to grasp.

The guide will try and provide you instructions on how to do the following tasks:

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

Excercises to practice

* Create repository
* Clone a repository
* Make local change available remote
* Creating a branch
* Fork a repository
* Creating a pull request for a repository not owned by you

## Prerequisites

* A GitHub account [https://github.com]
* Git installed locally [https://git-scm.com/downloads]

## Creating a local copy [Clone] of the repository on your local machine

On GitHub, go to the repository you want to work on.
Click on the Clone or Download button to obtain the link to your repository

On the Client
Go to a folder in which you want to have the files for this repository.
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

Will create C:\Git\GittingStarted, containing the content of the GitHub repository
