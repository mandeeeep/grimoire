# GIT Basics

**First of all, what is Git?**
> Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.
 
> Git is software for tracking changes in any set of files, usually used for coordinating work among programmers collaboratively developing source code during software development. 

So Git, is just a software that allows us to manage code changes. It's usecase isn't only for software code though, we can just about use it in any kind of domain like creative art works, document management and versioning and more; that has digital footprint. Simply put, its a system that provides **indefinite and manageable Ctrl-Z Ctrl-Y** capabilities and "**a bit more /s**".

## Concepts

First we will cover the basic concepts of Git.

For lack of a git fiddle, this here is a very good interactive [tutorial](https://learngitbranching.js.org/).

### Branch
Branches are just a reference to a snapshot of your code modifications. To put it simply, branch allows one to store all code commits/changes on a certain codebase or project and encapsulate/protect those changes without affecting the original piece of code.

### Tag
Tags are basically just references to specific commits in git history. Tags are mostly used to provide snapshots for a particular point in history of the codebase; or just call it **versions**. It is effectively an immutable branch that stores changes and history upto a particular point in time of the codebase's timeline. Unlike branches, new commits aren't accepted. 

### States 
Files that are part of a git ecosystem have following states:

**1. Untracked / Ignored**

These are files that will not be tracked by git, which essentially means they don't exist in the repo. Concepts like `.gitignore` are used.

**2. Tracked**

These are files that wil be tracked by git.

**3. Modified**

Tracked files, if updated or changed will be stated as modified. When we say modified, we meant updated the codebase using any kind of editors and saving them. The file hasn't still been saved to git repo yet.

**4. Staged**

Changes or updates that are final and should be saved are set to staged state.

~~~
git add MyClass.java //The file MyClass.java is now staged/ready for saving/commiting to the git ecosystem.
~~~

**5. Commited**

Finalized changes or updates that needs to be saved are then commited.

~~~
git commit -m "Added MyClass required for ......" //The staged file MyClass.java now has been saved in the git ecosystem
~~~

### Repositories
A repository in git is the collection of files of various different versions of a given project. It's actually the `.git` folder inside a project. This folder contains all the information about how the files have changed, all commit histories, versions, tags and branch details; basically everything.

#### Local
Local git repo is just the repo currently existing in your local computer. When you need to share your codebase and provide a more distributed access to the code base, we **add remote** like Github, Gitlab, Bitbucket or any self hosted VCS nodes.

#### Remote
Remote git repositories are more of a mirror of your current/local git repo existing on another computation node (server). Services like Github, Gitlab, Bitbucket or any self-hosted VCS allow us to mirror our local git repo to a cloud based node or any other external computational node. 

### Merge
Git merge is a utility that allows you to merge branches in Git.

~~~
//Switched to registration-impl task branch
git checkout feature/GL-12-reg-code-impl 

//Create -> write -> saved
nano RegImplementation.java 

//Staged 
git add RegImplementation.java 

//Commited
git commit -m "Added Registration implementation" 

//Pushed to remote
git push origin feature/GL-12-reg-code-impl

//Switched to current development branch
git checkout develop 

//Merged regsistration based implementation to development branch or codebase
git merge feature/GL-12-reg-code-impl 

//Pushed to remote
git push origin develop
~~~

### Rebase
Git rebase is a git utility that allows developers to integrate changes from one branch to another.

### Merge vs Rebase
Below is a very clear and concise explanation of the difference between Rebase and Merge, taken from reddit post [here](https://www.reddit.com/r/learnprogramming/comments/4ykgu4/eli5_what_is_git_rebase_and_common_use_cases_for/)

If you only ever commit to your master branch, your [DAG](https://en.wikipedia.org/wiki/Directed_acyclic_graph) will look like this:
~~~
A ---> B ---> C ---> D [master]
~~~

...where A, B, C, and D are commits, and commit D is labeled as the "master" branch.

Git supports something called "branching", where you can do something like this:
~~~
A ---> B ---> C ---> D [master]
       \
        +----> X ---> Y ---> Z [experiment-1] 
~~~

Here, what's happened is that after commit B, we made a branch called "experiment-1". In this branch, we added commits X, Y, and Z which are completely independent from the commits that were added to the master branch.

(Perhaps we wanted to play around with an experimental and potentially risky feature without breaking any working code in the master branch? So that we, if experiment-1 is broken, we don't piss off our coworkers who would prefer to work with non-broken code).

What rebasing lets us do is take the graph that looks like the above, and make it look something like this:

~~~
A ---> B ---> C ---> D [master]
                      \
                       +----> X ---> Y ---> Z [experiment-1] 
~~~

Basically say something like "you know how in order to get to experiment 1, I need to apply the diffs inside commits A, B, X, Y, Z in that order? Yeah, I changed my mind -- I want to split off of a different commit so that now in order to get to experiment 1, you need to apply diffs A, B, C, D, X, Y, and Z, in that exact order".

There are many potential applications to this (since git is a data structure, you can do arbitrarily complex/creative/nasty things to the underlying DAG), but the two usual use cases are when Somebody commits something really nice to the master branch (like a bug fix!) and you'd really like to have that in your work-in-progress. You're happy with the results of your experiment, and want to add it to master, but don't want to do a merge, since that could look messy/you like having master be a straight line without splits.

More specifically, if you start from here:
~~~
A ---> B ---> C ---> D [master]
        \
         +----> X ---> Y ---> Z [experiment-1] 
~~~

...and merge experiment-1 into master and update the master branch, you'll end up with your DAG looking like this:

~~~
A ---> B ---> C ---> D -------> M [master]
        \                      /
         +----> X ---> Y ---> Z [experiment-1] 
~~~
...where M is a new commit representing what happens when you combine diffs X, Y, and Z.

In contrast, if you rebase experiment-1 into master and update the master branch, you'll end up with your DAG looking like this:
~~~
A ---> B ---> C ---> D
                      \
                       +----> X ---> Y ---> Z [experiment-1, master]
~~~

...which is exactly identical to this:
~~~
A ---> B ---> C ---> D ---> X ---> Y ---> Z [experiment-1, master]
~~~

So, if you'd prefer keeping an exact historical record, you might go with merges, but if you prefer keeping an idealized and clean historical record, you might go with rebasing.

To summarize use case of Rebase and Merge:

**Use Rebase:**
1. If you are the only person working with the repository. So, when on team and public repos if you really need to rebase, just make sure you fully understand how rebase works
2. Need a more streamlined git history.
3. You feel merge commits are unnecessary details that disturbs understanding of the git log.

**Use Merge:**
1. If working on public repos and teams.
2. If you are confused about which one to use, it might be safe to stick with merge for now.
3. For a more simpler and safer approach to integrating codebase.
4. Git history needs to provide a more chronologically ordered log of commits.
