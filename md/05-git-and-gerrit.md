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
[source](https://git-scm.com/book/en/v2/Getting-Started-A-Short-History-of-Git)

Linux kernel development is done as a large virtual global team

  * highly distributed


## Git basics
Nearly all operations are local


## Let's create a repository

```
$ mkdir awesome_project
$ cd awesome_project
$ git init
```

    Initialized empty Git repository in /home/gbraad/awesome_project/.git/


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
```

    [master (root-commit) ea80784] Add hello file
     1 file changed, 1 insertion(+)
     create mode 100644 hello


## What happened this time?
We stored our first change

```
$ git log
```

    commit ea8078459e0c569b0d055cc7d580a40ef36f5337
    Author: Gerard Braad — 吉拉德 <me@gbraad.nl>
    Date:   Tue Apr 19 07:47:56 2016 +0000
    
        Add hello file

Note: (root-commit)


## In more detail
Let's prepare a new commit.

```
$ echo "Goodbye, CVS!" >> hello
```

```
$ git status
```

    On branch master
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)
    
            modified:   hello

Git tells you that there is a change that has not been staged yet.


## Verify changes
Always verify the changes you are going to commit

```
$ git diff
```

    diff --git a/hello b/hello
    index 670a245..4be5eec 100644
    --- a/hello
    +++ b/hello
    @@ -1 +1,2 @@
     Hello, Git!
    +Goodbye, CVS!


## Staging
Git has a convenient staging area, which allows you to prepare a commit from
changes you have.

```
$ git add hello
```


## Staged

```
$ git status
```
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)
    
            modified:   hello


## Now make more changes

```
$ echo "Hello, Git! You rule!" > hello
```


## Now verify the changes

```
$ git status
```
    On branch master
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)
    
            modified:   hello
    
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)
    
            modified:   hello


## The diff compares staging and work directory

```
$ git diff
```
    diff --git a/hello b/hello
    index 4be5eec..d198fd6 100644
    --- a/hello
    +++ b/hello
    @@ -1,2 +1 @@
    -Hello, Git!
    -Goodbye, CVS!
    +Hello, Git! You rule!


## Choices

  1. I perform `git commit -m "Say goodbye to cvs"`
  2. I perform `git add hello; git commit -m "I declare my preference"`
  3. Perform two commits
  4. I undo my changes


## Choice 1

```
$ git commit -m "Say goodbye to cvs"
```

    [master bf5d3d8] Say goodbye to cvs
     1 file changed, 1 insertion(+)

```
$ git log
```

    commit bf5d3d87f4b354851ef5f41ec4bfba3673c326fa
    Author: Gerard Braad — 吉拉德 <me@gbraad.nl>
    Date:   Wed Apr 20 02:55:00 2016 +0000
    
        Say goodbye to cvs


## What happened

```
$ cat hello
```

    Hello, Git! You rule!

```
$ git show
```

    commit bf5d3d87f4b354851ef5f41ec4bfba3673c326fa
    Author: Gerard Braad — 吉拉德 <me@gbraad.nl>
    Date:   Wed Apr 20 02:55:00 2016 +0000
    
        Say goodbye to cvs
    
    diff --git a/hello b/hello
    index 670a245..4be5eec 100644
    --- a/hello
    +++ b/hello
    @@ -1 +1,2 @@
     Hello, Git!
    +Goodbye, CVS!


The last can be done manually  with `git diff master`


## Choice 2
```
$ git commit -m "I declare my preference"
```

    [master b8586e3] I declare my preference
     1 file changed, 1 insertion(+), 1 deletion(-)

```
$ git log
```

    commit b8586e361918fe8343b906706a1aa579badec64f
    Author: Gerard Braad — 吉拉德 <me@gbraad.nl>
    Date:   Wed Apr 20 03:01:37 2016 +0000
    
        I declare my preference
    

## What happened
```
$ git show
```
    commit b8586e361918fe8343b906706a1aa579badec64f
    Author: Gerard Braad — 吉拉德 <me@gbraad.nl>
    Date:   Wed Apr 20 03:01:37 2016 +0000
    
        I declare my preference
    
    diff --git a/hello b/hello
    index 670a245..d198fd6 100644
    --- a/hello
    +++ b/hello
    @@ -1 +1 @@
    -Hello, Git!
    +Hello, Git! You rule!


## Choice 3

```
$ git commit -m "Say goodbye to cvs"
```

    [master bf5d3d8] Say goodbye to cvs
     1 file changed, 1 insertion(+)

```
$ git add hello
$ git commit -m "I declare my preference"
```

    [master 89486a6] I declare my preference
     1 file changed, 1 insertion(+), 2 deletions(-)


## What happened
Both changes are commited. Use staging to your advantage to 'stage' partial changes.

```
$ git log
```

    commit 89486a636f60477d04637306ff75f382e0bac166
    Author: Gerard Braad — 吉拉德 <me@gbraad.nl>
    Date:   Wed Apr 20 03:05:57 2016 +0000
    
        I declare my preference
    
    commit bf5d3d87f4b354851ef5f41ec4bfba3673c326fa
    Author: Gerard Braad — 吉拉德 <me@gbraad.nl>
    Date:   Wed Apr 20 02:55:00 2016 +0000
    
        Say goodbye to cvs


## Move between commits

```
$ git checkout bf5d3d8   # or `git checkout master~1`
```

    Note: checking out 'bf5d3d8'.
    
    You are in 'detached HEAD' state. You can look around, make experimental
    changes and commit them, and you can discard any commits you make in this
    state without impacting any branches by performing another checkout.
    
    If you want to create a new branch to retain commits you create, you may
    do so (now or later) by using -b with the checkout command again. Example:
    
      git checkout -b new_branch_name
    
    HEAD is now at bf5d3d8... Say goodbye to cvs

```
$ cat hello
```

    Hello, Git!
    Goodbye, CVS!


## Back to master

```
$ git checkout master
```

    Previous HEAD position was bf5d3d8... Say goodbye to cvs
    Switched to branch 'master'


## What is master / are branches
Master is the name given to a branch. Branch names are pointers
to a change inside the git repository.

Branching in Git is a very cheap operation and initially exist
locally.


## Create a branch
To create a branch from the current checkout you can

```
$ git branch cool-feature
$ git checkout cool-feature
```

    Switched to branch 'cool-feature'

or

```
$ git checkout -b cool-feature
```


## What just happened

```
$ git branch
```

    * cool-feature
      master


## Graph

```
$ git log --graph --all

```
    * commit 5ce4316680f4ece250f91d3157d552d2399b7150
    | Author: Gerard Braad — 吉拉德 <me@gbraad.nl>
    | Date:   Wed Apr 20 07:16:43 2016 +0000
    | 
    |     I declare my preference
    |  
    * commit a4e6e0433c2863959d0613e233ed968a87da3516
    | Author: Gerard Braad — 吉拉德 <me@gbraad.nl>
    | Date:   Wed Apr 20 07:15:41 2016 +0000
    | 
    |     Say goodbye to cvs
    |  
    * commit e52304db8b885a1217db2bcf0e2a2245959f61ee
      Author: Gerard Braad — 吉拉德 <me@gbraad.nl>
      Date:   Wed Apr 20 07:15:03 2016 +0000
      
          Add hello file


## Add some code

```
$ echo > hello << EOF
> #include<stdio.h>
> 
> int main(void) {
>     printf("Hello, World\n");
>     return 0;
> }
> EOF
$ mv hello hello.c
```


## What happened

```
$ git status
```

    On branch cool-feature
    Changes not staged for commit:
      (use "git add/rm <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)
    
            deleted:    hello
    
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
    
            hello.c
    
    no changes added to commit (use "git add" and/or "git commit -a")


## I need to add and remove

```
$ git rm hello
$ git add hello.c
```


```
$ git rm hello
```

    rm 'hello'

```
$ git add hello.c
```


## Result

```
$ git status
```

    On branch cool-feature
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)
    
            deleted:    hello
            new file:   hello.c

Note: the files are so different that no comparing can be done


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
