# ForgeGitHubFlow
Practice Repo for Forge Team's GitHub flow.  You can make changes to the HelloGitHub.html file to practice using the Git commands for the workflow.
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
## Workflow 3. Write some code!
Now you're ready to start coding.  If a story takes you more than one day to complete, you should remember to do a fetch and rebase each morning.  It's also a good idea to rebase anytime someone else's code is merged into the team repo.

```bash
git fetch team
git rebase team/master
```
If you've already made code changes but haven't committed them yet, you might see a message like this after you run the rebase command:

```bash
stuller@MN-STULLER-L MINGW64 /C/Users/dev/projects/ForgeGitHubFlow (JIRA-123-fix-css-on-menu)
$ git rebase team/master
Cannot rebase: You have unstaged changes.
Please commit or stash them.
```
You'll need to commit those changes before you can rebase. First, you'll probably want to run this command to see which files have changed:

```bash
git status
```
There are a few commands you can use to add files to a commit.
This one will add all changes to the commit:

```bash
git add .
```

This one will add a specific file to the commit:

```bash
git add path/to/the/file/you/want/to/commit.html
```

This one will add all the files in an entire directory to the commit (in this case, the "file" directory)

```bash
git add path/to/the/file
```

After you've added the files, you still need to commit them. The commit command also includes a commit message (the words that follow -m).  The commit message should be a brief sentence about what you changed in the commit.

```bash
git commit -m "Added css to prevent overlapping text on menu"
```

## Workflow 4.  I'm done writing code, now what?

1. Make sure you've tested your code!
2. Run the add and commit commands
3. Fetch and rebase - this is important to avoid merge conflicts on your pull request.
4. If rebasing merged in fresh changes from the team repo, test your code again!! You want to make sure what you did still works after the updates from the team repo.
5. Push the code to your personal fork (origin)

This command will push your commit to your personal fork on GitHub.  This command means "push the committed changes in this branch (JIRA-123-fix-css-on-menu) to origin (my personal fork)":

```bash
git push origin JIRA-123-fix-css-on-menu
```
You should see a response that shows your changes getting pushed up:

```bash
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 303 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/stuller/ForgeGitHubFlow.git
   74d2f7d..3a21d23  JIRA-123-fix-css-on-menu -> JIRA-123-fix-css-on-menu
```

## Workflow 5. Making a Pull Request
So now you've completed your code work and you've made sure you have the latest team changes merged with it, and it's been pushed up to your personal fork (origin).  The next step is making a pull request so that another team member can review your code and merge it into the team repo.  To do that, view your personal fork on the GitHub website. Above the list of files in the repo, you'll see a Branch dropdown and a New Pull request button.  Make sure that the Branch dropdown is displaying the name of the branch that you want to do a pull request for, and then click the New pull request button.

On the Open a pull request page, you will see some dropdowns for team repo and branch, as well as dropdowns for your repo and branch. These should be set correctly by default.  We almost always merge to master on the team repo, unless we are working on a long running change, in which case we might use a different branch.  The majority of the time you will not need to change these.

Below that you'll see an area where you can modify the text of the message you used on your commit, and also an area for comments. The comments area can be used to provide more info about your commit, or to leave a message for team members who might review and merge your code.  It's a good idea here to leave a message like "Ready for merge" or "HOLD for code review, do not merge" if you plan on holding a code review meeting before the code should be merged. 

Below this area, you can also see diffs of your code changes.  It's a good idea to review these before making the pull request.

Once you've finished writing your message, go ahead and click the Create pull request button.  Now a pull request has been created, and team members will be notified on Slack through our GitHub integration that your code is ready for them to review and merge.

## Workflow 6. Reviewing and merging a team member's code
If you're committing code to a team repo, you'll probably also be reviewing and merging pull requests for your team members as well. The only rule is that you should never merge your own pull requests! To review someone else's code, you can go to the team repo and click on the pull requests tab.  Select the pull request you want to review from the list.  You'll be able to see the comments for the pull request and by clicking on the Files changed tab you'll be able to see diffs of the code changes.  You can add comments at specific lines by clicking the little plus button near the line numbers. You should always take a look at the diffs before merging.

Back on the Conversation tab, there will be an area that will let you know if the pull request can be merged without conflicts.  If you think the code changes are good ones, and there are no merge conflicts, you can click the green button to merge the pull request.  In the rare occasion that this space indicates that there will be merge conflicts, you should not merge. Let the submitter know that there are conflicts.  Usually this is because someone forgot to fetch and rebase.  They will be responsible for fixing their code to make sure there are no conflicts, and then they will resubmit their pull request.

## After the merge
After your code has been merged into the team repo, you should do another fetch and rebase from your local master branch to get the merged code back into your local master.
After you've done that, you can clean up locally by deleting the branch you used for your code change.  This command will delete a branch:

```bash
git branch -d branchName
```




