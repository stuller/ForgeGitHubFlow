# ForgeGitHubFlow
Practice Repo for Forge Team's GitHub flow

# Getting Set Up

## Step 1 - Getting Set Up: Fork the repo
Fork this repo.  You can do that by clicking on the Fork button in the upper right area of this page.  Forking basically makes a copy of this repo in your own space.  It's just a copy though, just a snapshot in time.  So updates to this repo won't automatically show up in the forked repo in your own space.

## Step 2 - Getting Set Up: Clone your fork
Go to your fork of the repo, which you can find at ```github.com/<your username>/ForgeGitHubFlow```.  There will be a green button there that says "Clone/Download".  When you click on it, it will expand a little area that has a url in a field and a clipboard icon.  Click on the clipboard icon to copy the url to your clipboard.

Now go to your git bash or terminal window.  Use cd to navigate to the directory you want to download the repo into on your computer.  For Forge repos, this will always be:
```bash
cd /C/Users/dev/projects
```

Once you're in the directory shown above, type in ```git clone ``` and paste in the url you just copied to your clipboard, and then hit enter. 

```bash
git clone <paste url from clipboard here>
```

You may be asked to enter your credentials.  Once you've provided those (if asked) you'll see it downloading the repo.  Once the download has finished, you'll want to change directory (cd) into the new repo directory.  

```bash
cd ForgeGitHubFlow
```

## Step 3 - Getting Set Up: Set up your remotes
The code that you just downloaded is your local.  In our flow, you'll start by downloading the latest code updates from our team repo, then you'll be making code changes to your local, and then uploading those to your personal fork (which is called origin).  Then, you'll be making a pull request from your fork to the team repo, where it will be reviewed by a team member and merged.

If you type in ```git remote -v``` into your terminal right now, you should see the path to your personal fork is already called "origin".

What we want to do is add a remote that will allow you to connect to the team repo so that you can always get the latest code.  We'll call that remote "team".  We need the url for the team repo to do that.  So go back to the team repo on GitHub, look for that Clone/Download button and copy the url, just like you did before on your personal fork.  Now go back to your terminal and type in:

```bash
git remote add team <paste the team repo url here>
```
If you don't have your terminal set up to paste on right-click, you can 

Now if you type in ```git remote -v``` you should see that "origin" points to your personal fork, and "team" points to your team's shared repo. 

# Workflow

## Workflow 1. Before you start making code changes - Fetching and Rebasing
Before you get started on any code change, you should fetch the latest changes from the team repo to make sure you're starting with code that is already up to date.  To do that, type in ```git fetch team```.  If there are changes, you'll see something like this:

```bash
$ git fetch team
remote: Counting objects: 9, done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 9 (delta 3), reused 9 (delta 3), pack-reused 0
Unpacking objects: 100% (9/9), done.
From https://github.com/stuller/ForgeGitHubFlow
 * [new branch]      master     -> team/master
```
Right now your machine has fetched those changes, but it hasn't updated your local with them yet - it's kind of put them off to the side.  To do that, we're going to rebase - which will merge any changes from the team repo into your local.   (you won't need to rebase if fetching didn't count, compress or unpack anything - that means you are already up to date) At this point, you're probably still in your master branch, since we're just getting started.  You should be able to see that from the terminal line - it'll be in parenthesis.  We want to make sure that your master branch gets updated to the team master branch, so to do that, we'll type in 

```bash
git rebase team/master
```

You'll see a message that looks something like:

```bash
First, rewinding head to replay your work on top of it...
Fast-forwarded master to team/master
```
Fetching and rebasing is something you should do often.  Specifically - at the beginning of each day, or any time you know someone else's code has been merged into the team repo.  You'll also do it again before you push any of your own code.  Fetching and rebasing often will help prevent merge conflicts.

## Workflow 2. Creating a new branch for your task
Any time you start working on a new story, you'll want to create a new git branch for it.  That will help you keep work on different stories separate.  Preferably, the branch name should include the JIRA story id to help with tracking later.  To create a new branch, you'll use this command, where you'll replace JIRA-123... with whatever you want to name your branch:

```bash
git checkout -b JIRA-123-fix-css-on-menu
```

This command is a bit of shorthand - it creates the branch AND checks it out for you, so afterwards you'll notice that you've already been put in that new branch.  You can see from the response that you were on the master branch when you started, and now you've been moved into the new branch:

```bash
stuller@MN-STULLER-L MINGW64 /C/Users/dev/projects/ForgeGitHubFlow (master)
$ git checkout -b JIRA-123-fix-css-on-menu
Switched to a new branch 'JIRA-123-fix-css-on-menu'

stuller@MN-STULLER-L MINGW64 /C/Users/dev/projects/ForgeGitHubFlow (JIRA-123-fix-css-on-menu)
$
```
