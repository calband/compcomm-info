# Git and Github

Many of you will never have used [git](http://git-scm.com/) or Github before, so please read this carefully.

## Introduction to git

Git is a version control system. The problem that git solves is this: say you have about 10 people working on a project (like we will), and you divide up tasks between people, which makes sense. Let's call two of them person A and person B. Suppose person A needs person B's code.

How does person B give his code to person A? He could email it, but then person A has to download and copy and paste the new code every time, and as soon as person B does more work, he has to email his new code to person A again. That's no good.

Person A and person B could use Dropbox (or something similar), but then sometimes person A's files would get automatically updated with person B's new code, causing person A to lose his work. That's no good either. Not to mention, none of the other people on the team have any idea what person A and person B are doing!

This is where git comes in. When person B completes the code that he's working on, he can "push" the code to a "repository" (in this case, our space on [Github](http://github.com/calband/)), and person A can "pull" the new code from the repository. Then, when person A is done, he can push his code to the repository too. Now everyone on the project has access to everything, easily.

### Github

The most efficient way for everyone to have access to our code is of course to store it in the cloud. We can do this with Github. Github is one of many version control sites which use git to communicate with your local computer, such as Bitbucket. If you look at any of our Github repositories, like [Members Only](https://github.com/calband/members-only), you will be able to see all the files for that project as well as all the times that we've pushed.

## Git Tutorial

### Installing git

If you have a Mac with [homebrew](http://mxcl.github.io/homebrew/) installed, you can simply run `brew install git` from the command line and everything should work. You can also download a non-command line client [here](http://git-scm.com/downloads).

If you're on Windows, [read the instructions](http://git-scm.com/downloads) on the git website. You will be able to download a shell program called **Git Bash** which will let you run all the commands that I'm going to reference here (if you're on Mac/Linux, you'll be able to run the commands from the terminal). Please don't run any git commands from the Windows command prompt - though this is possible, it's just bound to create more setup errors, so use Git Bash instead.

### Quick Reference

If you need a cheat sheet, [this](http://www.git-tower.com/blog/git-cheat-sheet/) is a pretty good reference. Listed below are some of the most common commands you'll need:

- `git clone <repository URL>` - this will copy files from a repository to your local computer. See the _Cloning_ section.
- `git status` - this will display the branch you're on, the files you've changed, and any files staged for a commit. See the _Committing changes_ section.
- `git add [-A] [<file>, <file>]` - this will add the given file(s) to the list of files to commit. The `-A` flag adds all the files. See the _Committing changes_ section.
- `git commit -m "<message>"` - this will commit all files that have been staged with the `git add` command, attaching the given message to this commit. See the _Committing changes_ section.
- `git push origin <branch>` - this will push your commits on the given branch to Github. See the _Committing changes_ section.
- `git pull origin <branch>` - this will pull commits from Github to your local computer. See the _Committing changes_ section.
- `git branch <name>` - this will create a new branch with the given name. See the _Branches_ section.
- `git checkout <branch>` - this will change the branch you're currently working on. See the _Branches_ section.
- `git merge <branch>` - this will merge the given branch into the branch you're currently in. See the _Branches_ section.

### Cloning

In order to copy all the files from Github to your computer for the first time, you'll need to "clone" our repository. After you get the files on your computer, you can start making changes to the project. The repository should have all the files necessary to make the project work, so just follow the set up directions in the README file and you'll be good to go!

To clone the repo, get to whatever folder you'd like to put the files into via [command line](http://lifehacker.com/5633909/who-needs-a-mouse-learn-to-use-the-command-line-for-almost-anything) or Git Shell. Then run `git clone <repository URL>` (if you're on Mac, you should do this from Terminal. If you're on Windows, you should do this from Git Shell). The repository URL can be found on the repository page, something along the lines of `https://github.com/calband/members-only.git`. This command will copy all of the files in the repository into a new folder with the same name as the repository.

For example, if you store Comp-Comm projects in the directory `programming/calband/`, running `git clone https://github.com/calband/members-only.git` in that directory will put all the files into `programming/calband/members-only/`.

You can also set up git to work over [ssh](http://en.wikipedia.org/wiki/Secure_Shell) rather than HTTPS. Check out the instructions on [setting up git](https://help.github.com/articles/set-up-git) for more information - this is totally optional but recommended since you won't have to enter your Github username and password each time.

### Committing changes

After you've changed the files that you need to, you'll need to "commit" them so that the changes will be logged and so you can push them to the repository. A commit is basically a snapshot of how your files look and what kind of changes you've made. Having commits is good because you can look through all of your commit history and revert back to any past commit if you need to. In general, it's good to make small commits - make a small edit, commit. Implement a new feature, commit. This helps you, and everyone else, see where and why any file got changed.

After you've made changes and tested that your code works, run `git status`. This will show you the name of the branch you're on (more on branches later) and a list of changes that you've made so far. Make sure that everything looks okay. You can also run `git diff` to see an output of all the changes you've made that will be saved in the next commit.

If all the changes look okay, run `git add -A`. This will add all the changes you've made to all the files to a commit (basically, this tells git what changes you've made and saves them so that you can restore them later if you need to). You'll notice that if you run `git status` again, the files will have a different label next to them.

Now you're ready to finish the commit. Run `git commit -m "this is what i did and why i did it"` to add a message and finalize the commit (replace the message in quotes with a short description of whatever you were working on - this will show up on Github). After committing, you should see a message like this one:

    [master d673c80] this is what i did and why i did it
    1 file changed, 2 insertions(+), 2 deletions(-)

Now you're ready to push your changes to the remote repository on Github so that everyone else will be able to see it. Before pushing, you should make sure you have the most current versions of all the other files in the repo. To do this, run `git pull origin master` (or replace master with whatever branch you're on; again, more on this later). Hopefully, there are no error messages (more on how to fix merge errors later). If not, run `git push origin master` (again, more on the master branch later) to push all your changes to Github. The push command should give you an output like this:

    Delta compression using up to 4 threads.
    Compressing objects: 100% (24/24), done.
    Writing objects: 100% (24/24), 9.61 KiB, done.
    Total 24 (delta 18), reused 0 (delta 0)
    To git@github.com:calband/members-only.git
        f4d7d40..d673c80  master -> master
        
Again, here's a list of what commands you should run when you're ready to push code to Github:

```
git status
<make sure branch/files are right>
git add -A
git commit -m "<message>"
git pull origin <branch>
git push origin <branch>
```

### Branches

Often times, when we have a few people working on one thing and a few people working on another, it gets to be a hassle to have to pull and merge every time someone wants to commit code.

For example, say I'm working on a fix to make the homepage look better. I'll probably have a lot of edits, but someone else might be editing the same files as me! This means that we might change the same line, and if this happens, then git has to figure out whose edits to actually put in. This is frustrating to do every time anyone edits the same files as you!

For this reason, we can create "branches" of our edit history, edit them to our hearts content, and merge them back together later.

Every git repo starts out with a `master` branch, and our goal at the end is to have one `master` branch with everything in it done and working. In the mean time, we might have branches such as `homepage_fix` for working on the home page of Members Only, or `custom-tools` for development work about adding custom tools. Each of these branches would be a little different than `master`, but they will have edit history in common with `master` - in fact, they will have "branched off" somewhere in the edit history of `master`.

- To make a new branch: `git branch noah__my_first_branch` (this will create a new branch called `noah__my_first_branch`)
- To list all branches: `git branch`
- To switch to a branch: `git checkout noah__my_first_branch`
- To merge another branch into this branch: `git merge other_branch`

For more information, read [this](http://git-scm.com/book/en/Git-Branching-Basic-Branching-and-Merging), [this](http://git-scm.com/book/en/Git-Branching-Branch-Management), [this](http://git-scm.com/book/en/Git-Branching-Branching-Workflows), and [this](http://git-scm.com/book/en/Git-Branching-Remote-Branches) about branching.

Now, say you have been totally rewriting the trip signup pages, and you're collaborating with a few other people on it. You might have a branch on Github called `trip-signup-master` that would always have the most up to date (though not yet complete) trip signup code. After fixing a bug in your implementation you'd run `git push origin trip-signup-master` when you're done. **Be careful** not to push to `master` when you mean to push to another branch - it is not the end of the world, but it might create a lot of merge errors which will give us a headache.

Check out the Workflow.md file for more information on how we use branches to develop on Comp-Comm stuff.

#### Merge conflicts

Say someone's made changes in another branch that you'd like to have in your branch so you can continue editing on their changes. You'd use `git merge` to merge their changes, but what happens if they changed the same file you've changed? Maybe there was a file that said `Last edited by Bob`, and in their branch, the other person changed it to `Last edited by Oski`, while in your branch, you changed it to `Last edited by Me`. Git won't know which edit to keep; maybe you like the reference to Oski, so you'll want that change, or maybe you want all the recognition so you want to keep your change. Because of this, git will throw a "merge conflict".

After you merge another branch into yours, if there is a merge conflict, you'll get an error like:

    Auto-merging public/assets/manifest.yml
    CONFLICT (add/add): Merge conflict in public/assets/manifest.yml
    Auto-merging public/assets/application.js.gz
    CONFLICT (add/add): Merge conflict in public/assets/application.js.gz
    Auto-merging public/assets/application.js
    CONFLICT (add/add): Merge conflict in public/assets/application.js
    Auto-merging public/assets/application.css.gz
    CONFLICT (add/add): Merge conflict in public/assets/application.css.gz
    Auto-merging public/assets/application.css
    Automatic merge failed; fix conflicts and then commit the result.
    
Don't be scared, all you have to do is take a look at each file that git lists a `CONFLICT` for. In those files, you'll see something like this:

    >>>>>>>>>>>>>>>>> HEAD
    Last edited by Me
    =================
    Last edited by Oski
    <<<<<<<<<<<<<<<<< 8e637d62b1
    
The HEAD section represents the changes you've made; the section below represents the changes someone else made on the other branch. First, erase the =,<,> signs. Then change the file so that everything is _how it should be_ and commit everything again. Note that _how it should be_ does not just mean that you should erase everything you or the other person changed - instead, you should look at what the affected code does and make sure you know that you're not undoing someone else's work before you're done.

Sometimes, you'll see a vim console on a successful merge. See the Vim section for more details.

If you need to know who committed some lines in order to ask them about it, check out [git blame](http://alblue.bandlem.com/2011/07/git-tip-of-week-assigning-blame.html).

There are also programs that allow you to merge easily using a pretty interface. More about these [here](http://www.gitguys.com/topics/merging-with-a-gui/).

### Vim

Sometimes, git uses vim (or emacs sometimes) for text input. There are tons of guides [online](https://blog.interlinked.org/tutorials/vim_tutorial.html), but the main things I do on vim can be done with the following commands:

- `:q` quits the screen (saves the commit if something's written)
- `:wq` saves and quits the screen
- `i` allows you to edit the page
- `<Esc>` gets you out of editing the page

## Github Tutorial

Github provides different tools that allow us to easily collaborate on a project. The two main tools we use are the Issues page and Pull Requests.

In a given repository, there is an issues page that can be accessed via the sidebar/tab bar. This page lists all of the things that need to be done for a given project. You can add a new issue, look at old issues, and assign yourself to issues you'd like to work on.

Going back to the _Branches_ section, say you branch off from `master` and you've made some changes. Now, you'd like to merge the changes back into `master`. What you should do is go on the Github website, go to the Pull Requests page (also found in the sidebar/tab bar) and create a new Pull Request, setting the base to `master` and comparing with the branch you've made. Once someone's reviewed your changes and made comments on your edits, the branch will eventually be merged to master via this pull request.

See the Workflow.md file for more information on how we as Comp-Comm use Github for our projects.
