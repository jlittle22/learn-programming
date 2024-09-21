# Introduction

I would bet that one of the reasons why software has (at least historically) grown more capable at an exponential rate is because software engineers often develop software whose purpose is to make it easier to develop other ([or even the same](<https://en.wikipedia.org/wiki/Bootstrapping_(compilers)>)) software.

![thanos_meme](https://i.imgflip.com/93s0kl.jpg)

Git is a great example of this. It's a [version control system](https://en.wikipedia.org/wiki/Version_control) released in 2005 by Linus Torvalds to support the development of the Linux operating system kernel. Today, it is likely one of the most widely used tool in software engineering.

## Learning Philosophy

There are at least 2 ways you could go about becoming a git expert.

1. **The command-focused approach**. Git (as you interface with it) is just a command-line program, and like most command-line programs, it comes with a manual. You can read this manual by running `man git` in your shell. The manual lists all the various options and flags that git supports, which you could memorize, and upon doing so you would become a git expert.
2. **The implementation-focused approach**. Git is just a program, and programs are just code. Git's source code is [open source](https://en.wikipedia.org/wiki/Open_source), so you could [read it](https://github.com/git/git) and understand exactly how the program works if you _really_ wanted to. Doing this would definitely make you a git expert.

Fortunately, the goal of this guide is not to make you a git expert. Instead of defining git commands in isolation or doing a deep dive into how git works, I want to focus on _the practical things you can actually do with git_. That is, my goal is to take an _action-focused_ approach. I will teach you the workflows that I believe are important and comprise the core functionality provided by the software. The important thing is for you to know that these workflows exist, understand what they achieve, when to use them, and why the are necessary. Of course I will give you the commands, but at the end of the day, remembering them isn't really what I hope you gain from this guide. After all, you can always find them again here, look them up in the man page, Google them, or even ask an LLM if that's your style.

Lesson 0 of software engineering, which is especially relevant in the case of git, is that looking things up is never shameful (although copying things without understanding them is).

With that in mind, this guide will consist of a sequence of exercises that will teach you the important parts of git.

Now also seems like a good time to pass on some advice from [Prof. Mark Sheldon](https://engineering.tufts.edu/cs/people/faculty/mark-sheldon) who taught my intro to computer science class: "Copy and paste is evil". Or, if pithy phrases aren't your thing: "for the sake of learning, you should physically type out each of the commands below instead of copy-and-pasting them, because the typing helps your brain absorb the information better in the same way that writing things down does".

## Core Problems That Git Solves

To help you understand the more complex tasks you can achieve with what you learn in the admittedly contrived exercises below, I want to start with a list of some of the core problems that git solves:

- I'm working on task A, but need to switch to task B. I want to do this without losing my work on A.
- I'm working on task A and my co-worker is working on task B. We want to be able to make changes to the code independently, without affecting each other's workspace. When the changes are done, we want to combine them in a way that doesn't break things.
- I'm working on a new feature that isn't ready for our client to use yet. I'll need to make lots of changes to implement this feature, but I don't want to make any changes to the codebase our client uses until the entire feature is complete.
- I make some changes that break everything. Sirens are going off. Global famine is imminent. There is no time to debug and figure out what's wrong-- how do I revert the code to a previous state that I know works?

# The Basics

Start by making a directory somewhere in your file system:

```Bash
mkdir learn-git
cd learn-git
```

## Create a Git Repository

A git **repository** is a collection of files managed by git. You can create one in your current directory like so:

```Bash
git init
```

It might seem like nothing has happened, but if you list the contents of the directory including hidden files (while they sound super mysterious, hidden files are just regular files whose name starts with the `.` character)...

```Bash
ls -a
```

...you will see that a new directory called `.git` has been created. The contents of _this_ directory are not important, although you are free to look inside if you are interested. What you should know is that it is where git keeps track of the state of the repository.

## Make Some Changes

Within a repository, git knows about every change you make. Start by creating a new file and putting some text into it:

```Bash
echo "Chicken" > grocery_list
```

> [!NOTE]
> There's a lot going on in this command. The `echo` command puts the string we give it into the [_standard output stream_](https://en.wikipedia.org/wiki/Standard_streams), which by default is connected to your terminal. The `>` operator redirects this stream to the file we specify, creating it if necessary.

Now, ask git for the status of the repository:

```Bash
git status
```

You'll see something like:

> Untracked files:
>
> (use "git add <file>..." to include in what will be committed)
>
> grocery_list

Untracked here means that git hasn't saved any of the changes you've made to the file. Git helpfully tells us that if we want it to track it, we need to use the `git add` command. Let's do that.

```Bash
git add grocery_list
```

Git has now saved a snapshot of the file. If you check the status again, you'll see:

> Changes to be committed:
>
> (use "git rm --cached <file>..." to unstage)
>
> new file: grocery_list

In git terminology, the file is **staged for commit**. You'll learn what a commit is soon.

Let's make another change. Open `grocery_list` in your favorite editor and add some new items, so that it looks like this:

```
Chicken
Noodles
Broth
```

Again, check the status. Exactly as you might expect, you'll see that `grocery_list` is still staged for commit as before, but there are some additional modifications to the file that are not yet staged. You can ask git to show you all unstaged changes with the following command:

```Bash
git diff
```

The output is shown in a standard format called [diff](https://en.wikipedia.org/wiki/Diff), so called because it shows how a file differs from another. In this case, git is showing you how the current version of your file differs from the version you staged earlier. Notice how the lines you _added_ are prefixed with a `+` symbol.

Lastly, run `git add grocery_list` again to stage your new changes.

## Committing Your Changes

You're done with your changes, so you are now ready to **commit** them. To do that, we type the following:

```Bash
git commit -m "Add list of groceries"
```

The string after the `-m` flag is your _commit message_. It's purpose is to succinctly document what changes you made so that other developers (and future you) will have an easier time understanding them. If you omit the `-m` flag and the message, git will open a terminal-based editor where you can write multi-line message more easily. [Here](https://cbea.ms/git-commit/) is a good guide on writing commit messages.

If you check the status again, you'll see that it's empty. What happened to your change? Now that it's committed, it's recorded in the **log**:

```Bash
git log
```

You will see your commit, including its author, date, and message.

## Branches

A **branch** is a name that labels a specific commit. In computer science terminology, we say that a branch _points to_ or _references_ a commit. You can get a list of your branches as follows:

```Bash
git branch
```

You will see that git has created a default branch for you. In my version of git, this branch is called `master`, although this name has fallen out of style. It's common now for default branches to be called `main`. You can rename yours using this command:

```Bash
git branch -m master main
```

Take another look at the log. Notice that your commit is annotated with a long string of characters followed by `HEAD` and `main`.

- The string of characters is called the **commit hash** and it uniquely identifies the commit.
- You now know that `main` is a branch. Git is telling us that the `main` branch points to the commit we made earlier.
- `HEAD` is a special branch that always points to the commit that's currently active (or, in git terminology, **checked out**) in the repository.

Let's create a new branch called `optional-items`:

```Bash
git branch optional-items
```

List your branches and look at the log to convince yourself that it worked. Notice that `optional-items` points to the same commit as `main`, but it's not checked out. We can check it out with the following command:

```Bash
git checkout optional-items
```

> [!NOTE]
> You can create _and_ check out a git branch with a single command: `git checkout <branch-name>`.

Check the status, and you will see:

> On branch optional-items

That is, `HEAD` now points to `optional-items`. Great.

Now add a new item to your list. Perhaps some carrots? Your diff should look like this:

```Diff
--- a/grocery_list
+++ b/grocery_list
@@ -1,3 +1,4 @@
 Chicken
 Noodles
 Broth
+Carrots
```

Stage and commit the change:

```Bash
git add grocery_list
git commit -m "Add carrots to grocery list"
```

Check the log. You will see that there are now two commits, with the most recent at the top. `optional-items` points to the commit you just made, while `main` still points to the original one. Because you were on branch `optional-items` when you made the commit, git updated `optional-items` to point to it. `main`, on the other hand, was unchanged.

Print the contents of the file:

```Bash
cat grocery_list
```

You will see exactly what you expect-- that the carrots we added are there. But, if you check out `main` and run the command again...

```Bash
git checkout main
cat grocery_list
```

...you will see that carrots are missing! This is because `main` _still points to the previous commit_, where you hadn't added them yet!

## Merging

Make sure you are on `main`, then make a new file called `soup_recipe` with the following contents:

```
Ingredients:
TODO
```

Stage and commit your changes, then look at the log. Just like before, `main` was updated to point to the new commit. Now check out `optional-items`, look at the log, and convince yourself that it remains unchanged.

The state of your repository is represented by the diagram below, where each square is a commit.

```
       Add carrots to grocery list
                  (optional-items)
                                 │
                                 ▼
                               ┌───┐
Add list of groceries      ┌───┤   │
                    │      │   └───┘
                    ▼      │
                  ┌───┐    │   ┌───┐
                  │   │◄───┴───┤   │
                  └───┘        └───┘
                                 ▲
                                 │
                            (main)
               Add recipe for soup
```

Now you see why they are called _branches_. Notice how `main` and `optional-items` have **diverged**-- that is-- they each contain separate changes. Lets say you decide that the optional items aren't so optional and you want to include them in your main list. In git terminology, you want to **merge** `optional-items` into `main`. You can do this like so:

```Bash
git checkout main
git merge optional-items
```

Git will open a terminal-based text editor with a prompt to write a commit message. Save and quit to confirm the merge.

> [!NOTE]
> If your editor is `nano`, press `<CTRL>x` to quit. If your editor is `vim`, type `<ESC>:wq`.

Check the log and notice that all the commits we've made, even the one on the `optional-items` branch, are here. Git took all the commits in `optional-items` starting from the point where it diverged from `main` (in this case there was only 1 such commit), put them on `main`, then made a new commit that includes the changes necessary to join the branches. Note that `optional-items` remains exactly the same as it was before the merge.

If you list the files in the repo and print their contents...

```Bash
ls
cat grocery_list
cat soup_recipe
```

...you will see the recipe is there _and_ carrots are on your grocery list! The changes from `optional-items` have indeed been merged into `main`.

To really understand what's going on, look at the diff between each successive pair of commits with this command:

```Bash
git diff <earlier-commit-hash> <later-commit-hash>
```

Notice a few things:

- The first (bottom) commit is the initial commit we made.
- The next commit is from `optional-items`. There should be nothing unexpected here-- you added "Carrots" to your grocery list.
- The commit directly after `optional-items` is where things get interesting because the diff tells us that "Carrots" existed in the commit before, but is missing from this one. This is because this commit came from `main`, which did not have "Carrots"! When we did the merge, git simply stacked all the diverging commits from `main` on top of the commits from `optional-items`. None of the individual commits were (or, more generally, ever will be) changed by this process.
- The last (top) commit is the one that git made when you did the merge. This is where git fixes the inconsistencies it caused by doing the commit stacking: notice how "Carrots" is added back again. Git figured out for you exactly what changes needed to be made to `main` to get your grocery list to look like the one in `optional-items`.

Sometimes git isn't smart enough to do this last step automatically, in which case you will have **merge conflicts** that you must resolve manually in order to complete the merge. [Here](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line) is a good guide on merge conflicts.

Git also offers an alternative strategy for joining branches called **rebasing**. For now, just focus on understanding merges, but if you are curious, you can read the relevant [git documentation](https://git-scm.com/book/en/v2/Git-Branching-Rebasing).

# Remote Git

Up until now, everything you have done with git has been _local_, meaning "on your own computer". Much of git's power, however, comes from the fact that that it is **[distributed](https://en.wikipedia.org/wiki/Distributed_computing)**. Other computers run git too, and you can interact with them.

## Remote Repositories

A **remote repository** is a git repository hosted on a server which is accessible over a network.

The file you are reading right now is stored in a remote git repository hosted on [GitHub](https://github.com/). GitHub is a service owned by Microsoft that makes it easy to set up and host git repositories. It also has collaboration features.

A remote repository doesn't _have_ to be hosted on GitHub-- all you need to host a remote repository yourself is a computer running a git server. For example:

- [Here](https://gitlab.com/wireshark/wireshark) is the remote repository that stores [Wireshark](https://en.wikipedia.org/wiki/Wireshark), a network traffic analyzer. It's hosted on a different service called GitLab.
- [Here](https://android.googlesource.com/platform/packages/modules/Uwb/) is the remote repository that stores the Android operating system's software for [Ultra-wideband](https://en.wikipedia.org/wiki/Ultra-wideband). This one is hosted from a Google data center.

## Uploading Your Local Repository

Make sure you are in the `learn-git` repository you created in [The Basics](#The-Basics). We're going to upload this repository to GitHub so that you have a place to experiment.

Make a new repository on GitHub by signing in and visiting [github.com/new](https://github.com/new), or clicking the green "New" button on the left sidebar. Give your repository a name-- `learn-git`, then click "Create repository" at the bottom.

Git will give your repository a URL that should look something like `git@github.com:<your-github-username>/learn-git.git`.

Now, back in your your local repository, we need to associate it with the remote one:

```Bash
git remote add origin git@github.com:<your-github-username>/learn-git.git
```

This command registers the remote repository as a version of your local one with the name `origin`. `origin` is the name git uses for the remote repository that a local repository was originally downloaded (in git terminology: **cloned**) from.

Then upload branch `main` to remote `origin`:

```Bash
git push -u origin main
```

Go the remote repository on GitHub (or reload the page, if you already had it open), and see that your `grocery_list` and `soup_recipe` are there! Take a few minutes to familiarize yourself with the GitHub user interface and understand how it represents some of the same information you saw when using git. A few things to notice:

- Your commit log is recorded in the remote repository.
- There is 1 branch-- `main`. This is because you haven't uploaded `optional-items` yet. It's still a local branch-- more on this [later](#Remote-Branches).

## Downloading a Local Copy

Now pretend that you're another developer who wants to collaborate on the grocery list. Start by navigating up a directory so that you're no longer in the `learn-git` repository:

```Bash
cd ..
```

The first step to collaborating is to make a local copy of the remote repository, which you can do by **cloning** it:

```Bash
git clone https://github.com/<your-github-username>/learn-git.git another-devs-clone-of-learn-git
```

> [!NOTE]
> The second argument to `clone` here ("another-devs-clone-of-learn-git") is the name that git should use for the directory that contains your repository. This argument is usually not necessary-- when it's omitted, git will give the directory the same name as the repository. In this case, we need to provide it because a directory with the name of the repository ("learn-git") already exists.

This will create a new directory called `another-devs-clone-of-learn-git` containing a clone of the `learn-git` repository that you uploaded. `cd` into the directory and run `git log` to convince yourself that it is really a clone.

## Making Changes

Still role-playing as another developer, you can make changes to the local clone just as before. Add "Potatoes" to `grocery_list`:

```Diff
--- a/grocery_list
+++ b/grocery_list
@@ -2,3 +2,4 @@ Chicken
 Noodles
 Broth
 Carrots
+Potatoes
```

Stage and commit your changes:

```Bash
git add grocery_list
git commit -m "Add potatoes to grocery list"
```

You now have a commit in your local repository that doesn't exist in the remote one. To upload, (git terminology: **push**) in git terminology, your local changes to the remote repository:

```Bash
git push
```

Look at your remote repository on GitHub and verify that the new commit has been pushed.

## Updating Your Local Repository

Now, go back to being yourself. `cd` into the original repository (you should be able to get there by doing `cd ../learn-git`).

Take a look at the log and your grocery list. You'll see that the commit to add "Potatoes" made by the other developer isn't there! This is because, while the commit was pushed to the remote repository, your local repository was not updated. You need to explicitly tell git when you want to update your local repository with all new changes made to the remote:

```Bash
git pull
```

Now check the log and your grocery list. All should be well.

## Remote Branches

Lastly, we'll cover remote branches.

Check out the `optional-items` branch that you created earlier (`git checkout optional-items`). This branch hasn't been pushed to the remote repository yet, so its still a **local branch**. You can make it a **remote branch** by using the same command you used to upload `main` when you first created the remote repository:

```Bash
git push -u origin optional-items
```

Now, use the following command to view _all_ your branches, both local and remote:

```Bash
git branch --all
```

Notice that you actually have 4 branches in this repository: your local `main` and `optional-items`, plus their remote counterparts `origin/main` and `origin/optional-items`.

Check out `main` and view the log. You can see that your local branches all point to the same commit as their remote counterparts. This is expected, because you just ran `git pull` to sync your repository with the remote.

Check out `optional-items` again and make a new commit, but do not push it to the remote repository yet!

```Diff
--- a/grocery_list
+++ b/grocery_list
@@ -2,3 +2,4 @@ Chicken
 Noodles
 Broth
 Carrots
+Cake
```

View the log. Notice how your local `optional-items` has been updated to point to the new commit, but `origin/optional-items` is still where it was before! If you check the status, you'll see that git makes this very clear:

> Your branch is ahead of 'origin/optional-items' by 1 commit.

You already know how to update the remote branch with your new change:

```Bash
git push
```
