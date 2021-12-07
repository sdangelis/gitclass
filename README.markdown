A quick introduction to Git/Github, delivered as part of the BCI bioinformatics Cafe

# Overview

The goal is to learn the basic Git commands and understand how it can help you write better software.

This class is split into two parts. In the first section, I'll quickly introduce Git and Github. In the second section, we'll work through some examples.

Rather than work on a program, we've decided to go with a more artistic, esoteric approach - combining lines of Shakespeare with contemporary Rap and Hip-Hop lyrics to create something new.

Indeed, Git powers extend beyond traditional programming and as long as your files are text files git is a pretty good way to track them.

A notable exception is tabular data, while git can store it, it will not be extremely effective at doing so. And remember Office files and pdfs are not technically text files.

# Resources and other options

There are many ways to get help, and many great tutorials out there

* [https://try.github.io/](https://try.github.io/) - Probably the best one out there.
* [https://guides.github.com/activities/hello-world/](https://guides.github.com/activities/hello-world/) - A little simple and github focused
* [http://gitreal.codeschool.com/](http://gitreal.codeschool.com/) - Another tutorial.
* [Git Flight rules](https://github.com/k88hudson/git-flight-rules) **We all** get stuck with so Git at some point, so this is a collection of
  quick guides to solve specific git issues. **Highly recommended**
* [https://explainshell.com/](https://explainshell.com/) While we'll print some help information with `--help` the help pages of command line tools can quickly get overwhelming. Explainshell
attempts to explain only the options (aka flags) you're currently using.

## git scm book

This deserves it's own section, as the material is excellent. I refer to this page often. There is a paperback book with a PDF version also, if you prefer that sort of thing.

* [https://git-scm.com/doc](https://git-scm.com/doc)
* [https://git-scm.com/book/en/v2](https://git-scm.com/book/en/v2)

# Set Up

Make sure you have a good text editor available, if you don't have a preference [VS Code](code) is free and a solid choice  that works on Windows, Macs and Linux

You should also create a [http://github.com](github.com) account if you don't have one.

You should also install git on your machine, see [here] for a guide.

**NOTE**: git is the command line version control tool, Github is both a server where you can store git repositories and web interface on top of git.  
This means that you have a copy of every modification you made to your repository both on your machine and online, so it can be easily shared with others.

**Another note**, while GitHub is arguably the most popular git hosting service GitHub is not the only website to do so.

# Anatomy of git

In git terminology a repository is a directory containing all the text to keep track of
The central idea of git is that changes are organized according to a tree, with the root being the beginning of your repository history and a series of branches extending from it.
However, unlike a real tree branches can fuse back with the trunk or change the point at which they diverge.

Sounds too complicated? Git has been designed to keep track of large scale open source projects and often has many ways to do similar but slightly different changes. In reality you can get a lot out of it from using a small subset of its features in your projects.

# Part 1: The basics

## git clone

The first thing to do is to clone the repository. Open git, and navigate to a place in your home directory and run the command:

    git clone https://github.com/sdangelis/gitclass

You should see a directory appear called gitclass that has all the files you need to get started

## git pull 

Cloning the repository downloads the entire content to your computer. We 
only need to do this once.

To update our copy we run the command:

    git pull 

This only gets the new changes (and automatically checks if we have conflicting changes - see Part2)

## git status

Run the following command from inside the gitclass directory:

    git status

Git should print out the status of all the files in the current directory - whether they are being tracked, if they've been modified and other useful information.

This command is very useful when you are making changes and you want to see what needs to be saved and what doesn't

## Create a new file

Now, we can start with our new lyrical masterpiece, be it a song, poem or just something that sounds funny. Using a , create a file named something like *myfirstpoem.txt* or similar. Take a look at the two files, *shakespeare_corpus.txt* and *rap_lyrics_corpus.txt*. Select a few lines from each (say 5 to 10) and come up with something new.

## Staging

By default git status keeps an eye on the current modifications for all files in your repository but does not keep an history for them. 
To add a file to git's history you must manually add files to the so-called staging area.
Think of the staging process as calling actors to the wings of the theatre. they are ready to go but are not on stage yet.

## git add

Now we can add your new file to the staging area. You can, if you like, run `git status` to see the status of your new file. We should add this file, so it is `tracked`  or `staged` within the git system. Run the command

    git add <MYFILENAME>

**Note**: replace `<MYFILENAME>` with the actual filename. In general when you see `<VALUE>` in coding documentation you should replace it with the appropriate value, without `<>`.  
i.e `hello <NAME>` becomes `hello Simone`

Run `git status` again and you should see that it is now tracking the new file.

## Committing

Once we are done adding files to the staging area we can commit our changes. This creates a snapshot of the repository, a note in the history of your project about the content of the staged files at that timepoint.

Before we can commit however, we need to create our own copy of this repository on github.com because while have read access to the public repository we cannot automatically write to it - but we can copy it and write our own copy, and then ask the original author to merge it.

### Fork the repository on github

We now have a clone of the master repository, but it's time to create your own copy on github.com. Login to github.com and navigate to [https://github.com/sdangelis/gitclass](https://github.com/sdangelis/gitclass). At the top right of the page you should see a button labelled *fork*. Press this and fork your own repository.

## git remote

The command *git remote* shows you the various remote repositories linked to this one. These repositories can be anywhere, not just on github.com but for now, that's the place we'll use. 

If you have created a git repository from scratch i.e with `git init`, you can link to a remote repository with

    git remote add origin <address>

You will need to replace `<address>` with the github.com address of the new repository.
In our case, we are changing the remote so we need to use  

  git remote set-url origin <address>

The address is the link to your fork of the class repository we created in the previous step. You can find this out by navigating to your forked repository and taking a look at the `https` text box at the top of the page. It will look something like this:

    https://github.com:MYUSERNAME/gitclass.git 

If you make a mistake, run the command:

    git remote --help

This will show you the commands needed to remove the remote and start again.

## git commit

Possibly one of the most useful and often used commands as it creates a commit.

    git commit --help 

 For the most part however, we will use the following:

    git commit -a -m "<MY MESSAGE>"

The `-a` flag is quite special.  
It is effectively a shorthand to stage all tracked files and commit in one go.

### before the commit can take place

When you first commit something, you may be asked to setup a name and email address with git. This is so commits can be tied to a particular user. Git will warn you about this and offer the following solution

    git config --global user.email "<YOUR EMAIL>"
    git config --global user.name "<YOUR NAME>"

The quotes are important. Simply follow the onscreen instructions and then re-try the commit.

### commit messages

Before we actually commit, we should take a short time to talk about commit messages. Take a look at this: [https://xkcd.com/1296/](https://xkcd.com/1296/). This sums up what developers often do when the commit to repositories. Please don't do this sort of thing. Commit message are quite useful and although you don't want to be too long winded, do please try and write useful comments. make your comments meaningful!

### commit messages and Vim

So far we have provided git commit messages from the command line. This is fine for short comments.  we can ask git to open a text editor by simply omitting the `-m "<message>"`  part

    git commit

On many systems this will open vi/vim. Vim is an amazing text editor but has a steep learning curve.

to save you some time:
vim uses `h`, `j`, `k`, `l` to move left, down, up and right.  
You can often get away with using the arrow keys instead.  
You press `i` to insert text, and `esc` to quit the inserting mode.  
To quit vim type `:q` if you made no changes, `:x` if you made some changes you'd like to save and `:q!` if you made changes but you'd like to quit **without** saving.  

#### verbose git commits  

Sometimes we might forget what changes we have committed,
we can ask git to add a list of all modifications with the `-v` flag.

    git commit -v 

**NOTE**: the modifications will appear at the bottom of the code editor window but **will not actually be part of the commit message**. Git tracks changes anyway and there is not need to specify them all in the commit message

## Performing the  commit

We are ready to perform our commit. Run the command:

    git commit -a -m "<MY MESSAGE>"

You will see some output that reflects the changes you have made to the repository. If all has gone well, you will a success message. If it does not, it's probably because you have a conflict or similar.

## git push

We are ready to send our changes somewhere other than our local machine. Run the command:

    git push 

If all goes well, you should see a success message. Navigate to your github.com page and you should see your file has appeared with the commit message you set.

try running the diff command again 

    git diff 

# Part 2: More git

Excellent! You've managed to commit things and send things to other places. This means you know how to backup your code and keep track of the changes you've made. This is one of the most powerful and useful features of git.

## git log 

Lets take a quick look at what we've done so far. Run the command:

    git log

You should see a list of commits, with their unique ID numbers and the messages you have written. Press `q` to quit.

## git rm

Let us suppose you are not a fan of the prose you have just written. Let's delete it. Run the command:

    git rm <YOURFILENAME>

replacing `<YOURFILENAME>` with the name of your file.

git will now delete the file in the next commit, removing it for future commits. Run the command

    git commit -a -m "Deleted our file"

You have now made a new commit with the file removed

## pointers

We should talk about pointers, in particular the *HEAD* pointer. This pointer is sort-of-like the default location. You can typically think of this as 'which commit am I working on right now'. We will need this in our next example.

## git reset

The command `git reset` has many uses, but as it's name suggests, it resets various things in git to their previous state. Let's pretend we really did want that file we deleted after-all. How can we undo what we just did?

We can use the following command:

    git reset --hard HEAD~1

**WARNING** this command will trash data and delete things potentially, so use it lightly!

Lets break that command down a little bit. The `--hard` flag means *really set everything back. delete, rename, do what you have to*. This means if you just created a new file it will be deleted when we *roll-back* so be careful.

The `HEAD~1` statement means *one commit before this one*. You can, if you prefer, replace this with the actual commit id instead, which you can find with `git log`.

Run the command and see what happens. Your file should now have appeared and we have effectively, gone back in time, wiping out that commit we just made.

Another use case for reset might look like this. Say, you are working on a commit and you make a terrible mistake and you want to go back to where you started. You can use:

    git reset --hard HEAD

We are resetting to the beginning of the current commit we are working on. This is a destructive but useful command if you want to just forgot the mistakes you may have made. Combined with the `branch` feature, this is an excellent way to test and try-out new features.

Reset will change all the files in the repository. Arguably more useful is the ability to reset specific files to an earlier version. Git

Git checkout can do that.

    git checkout HEAD -- <YOURFILE> 

The rules around the HEAD pointer are the same as before, so this command is equivalent of

    git reset --hard HEAD 

for your file.
Try changing a file and use checkout to revert to `head~1`

    git checkout HEAD~1 -- <YOURFILE> 

## git branch

It's time to introduce one of the most used, and most powerful features of git, branching. Branching does exactly what it sounds like. If you imagine your commit history as a totally linear narrative, you'd get a straight line, each commit pointing to the last. A branch creates a fork in that line, splitting into two different paths.

Run the following command:

    git branch morespeare

This creates a new branch that forks at the current *HEAD* pointer. If you type the following command

    git branch

you should see that the branch has been added but you are still on the `master` branch.  
**NOTE**: the term `master` is not very inclusive so the term `main` is now the default term for the main branch in a repository.

### git checkout (branches)

Checkout is a somewhat cryptic but it also moves you to a new branch or working tree. So lets do that:

    git checkout morespeare

Try running

    git branch

You should see that you are now on the *morespeare branch* - your next commit will appear on this branch, and your *HEAD* pointer will be pointing to it as well.

### Add some more shakespeare

For arguments sake, lets alter the Shakespeare corpus and add some more extracts to our list. Navigate to [Project Gutenberg](https://archive.org/details/gutenberg?and[]=shakespeare) and take a look at all the text files they have. Pick one of them  and add the text you like to the *shakespeare_corpus.txt* file.

Lets commit out changes. Run a command like this one:

    git commit -a -m "Added more shakespeare to use"

We can make whatever changes we like on this branch, without affecting the master branch.

## git merge

Lets switch back to our master branch.

    git checkout master

We are back to where we were before. Let us suppose we are happy with the changes we made in the morespeare branch. Lets merge these and clean up.

    git merge morespeare

You should see a message saying the *shakespeare_corpus.txt* file was updated. This will cause a new commit to be created.

## conflicts

This is the real heart of version control. What to do when things don't match up. Our above case is very simple, but sometimes you might see this:

    Auto-merging shakespeare_corpus.txt
    CONFLICT (content): Merge conflict in shakespeare_corpus.txt
    Automatic merge failed; fix conflicts and then commit the result.

If this happens, the file in question will contain portions of *both* sides and you'll need to decide which of the changes you want to keep. If you look at the file, typically, you'll see something like this:

    <<<<<<< HEAD:index.html
    <div id="footer">contact : email.support@github.com</div>
    =======
    <div id="footer">
    please contact us at support@github.com
    </div>
    >>>>>>> iss53:index.html

This example is taken from [https://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging](https://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging) and is unrelated to this project. However, it illustrates the point.  

There are two versions of the same set of lines in the file `index.html`. The current `HEAD` pointer is given first, and another commit from another branch called `iss53` is also shown.

In such a case you must remove all the <, > and = signs and leave just the code you want. For example, if I wanted to accept the iss53 change I'd end up with this:

    <div id="footer">
    please contact us at support@github.com
    </div>

Once we've made resolved this conflict we can use:

    git add <FILENAME>

to stage the file for commiting and

    git commit -m "merging branch <BRANCH>" 

to  commit it.

# Part 3: More complex histories

In this optional section we'll deal with two more commands that can be very useful for more complex histories. We likely won't have time to do this in the session.

## Rebasing

Suppose we switch back to the master branch with

    git checkout master

and add a further modification to our files. Our `morespace` branch is now behind the main branch by 1 commit. If we keep doing this eventually our branch will increasingly out of sync with the main branch.

We can use git rebase to change the origin point of our branch and incorporate changes from the specified branch with.

    git rebase head <morespace>

Rebasing erases part of your repository history and there is no undo. Another alternative is to merge the changes from the  main branch into your second branch with

    git checkout <morespace> 
    git merge main

Whether rebasing is more appropriate than merging is debeable and controversial see  [this Stack overflow thread](https://stackoverflow.com/questions/457927/git-workflow-and-rebase-vs-merge-questions)

## git stash

Sometimes merging and pulling will result in conflicting changes to modified but not committed files. 
By default git will gives a warning and refuse to override our changes.
We have already seen we can use reset/checkout to discard all  modifications or commit to force a merge with conflicts we can resolve.

But what if we don't want to commit to changes or get rid of them? git can `stash` them for later use. Stashed files don't get pushed.

we can ask git to stash all staged and unstaged files with

    git stash 

we can see what we have in the stash with

     git stash list

The stash is saved as a stack. (i.e the last item added is the first in the list). We can access it in two ways

### Pop

pop will remove the change from the stash and apply to the current files

    git stash pop stash@{1}

**NOTE**: `@` is a shorthand for `HEAD`

### Apply

apply will apply the changes without removing them

    git stash apply stash@{1}

### clearing the stash

unless we popped all the items, we manually need to clean the stash, to do so we do:

    git stash clear

# Lets review  

We've looked at a lot of things. It's normal to feel somewhat overwhelmed at this point. So far we've covered:

* Creating and cloning repositories
* Staging files
* Committing changes
* Pushing and pulling from remotes
* Undoing changes
* Logs
* Conflicts
* Branching
* Rebasing
* Stashing

You might have noticed we have not looked much at github.com.
It is comparatively easier to learn how to make the most of GitHub with a foundation of git
than the other way around

There are also many more ways of using git, please see the tutorials linked to hear more.

# Credits

Inspired by [http://poly-graph.co/vocabulary.html](http://poly-graph.co/vocabulary.html).

All Shakespeare snippets are taken from Project Gutenberg. All rap lyrics 
are taken from Rap Genius.

As the git history shows, this material is directly forked and adapted from a series of exercises developed for the 2016 QMUL CIS Software Workshop,
like its source material, this version is released under the GPL-3.0 license.
