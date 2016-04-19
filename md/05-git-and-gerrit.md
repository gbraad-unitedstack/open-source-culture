# Open Source Culture

### Git and Gerrit


## Why we use these tools

  * To encourage collaboration
  * To get improvements to users faster
    * Without sacrificing quality


## Overview
You will learn the basic usage of git as a source management tool.

  * branching
  * merging
  * rebasing
  * squashing

And the usage of Gerrit for the review process.


## What is version control
also known as Source Control Management

"The undo functionality for a developer"


## Available Open Source tools

  * CVS
  * Subversion
  * Mercurial
  * Bazaar
  * Git


## Git history
"As with many great things in life, Git began with a bit of creative destruction
and fiery controversy." -
[Source](https://git-scm.com/book/en/v2/Getting-Started-A-Short-History-of-Git)

Linux kernel development is done as a large virtual global team

  * highly distributed


## Git basics
Nearly all operations are local


## Let's create a repository

```
$ mkdir awesome_project
$ cd awesome_project
$ git init
Initialized empty Git repository in /home/gbraad/awesome_project/.git/
```


## What did just happen?
The command `git init` created a `.git` folder which represent the state of
your work directory and contains a local repository.


## The three states

  * Working directory
  * Staging area or index
  * Local repository (.git)


## Let's create our first change

```
$ echo "Hello, Git!" > hello
$ git add hello
$ git commit -m "Add hello file"
[master (root-commit) ea80784] Add hello file
 1 file changed, 1 insertion(+)
 create mode 100644 hello
```


## What happened this time?
We stored our first change

```
$ git log
commit ea8078459e0c569b0d055cc7d580a40ef36f5337
Author: Gerard Braad — 吉拉德 <me@gbraad.nl>
Date:   Tue Apr 19 07:47:56 2016 +0000

    Add hello file
```

Note: (root-commit)


## Make changes to review

  * [...]
  * git add [file]
  * git commit --amend
  * git review


## Don't

```
git push --force
```


## Reference

  * https://www.mediawiki.org/wiki/Gerrit/Tutorial
  * https://git-scm.com/book/en/v2
  * http://gitref.org/basic/
