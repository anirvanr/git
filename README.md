## Setup

See where Git is located:
`which git`

Get the version of Git:
`git --version`

To see the current configuration:
`git config --list`

Configure user information for all local repositories:

`git config --global user.name "[name]"`

`git config --global user.email "[email_address]"`

Create an alias (shortcut) for git status:
`git config --global alias.st status`


Help:

`git help`

`git help diff`

Get a list of contributors and the number of commits by them:
`git shortlog -sn`

## General

> Git provisions 3 different areas that are the core of the repository. The first one is the `working directory` which is the root of your Git project, here the files go through any change that the user performs. The `staging area` (also called the `index`, `stage`, or `cache`) is where changes are built up, in this area all files are converted to tracked files by git. And the last one called as the `commit area` or `local repository` that safely stores all files already committed. There’s another area called Remote Repository, that represents the remote location of the origin repository.

> With three sections, there are three main states that a file can be in at any given time: modified, committed, or staged. You modify a file any time you make changes to it in your working directory. Next, it's staged when you move it to the staging area. Finally, it's committed after a commit.

> Git maintains a reference variable called HEAD. HEAD always points to the tip of the current branch in our repository.
>The Caret (`^`) is the parent of the Commit. The tilde (`~`) is a shorthand character for a row of several characters (^). The equivalence of HEAD~2 to HEAD^^. And, in the same way, the equivalence of HEAD~3 to HEAD^^^. The default used is 1, if no number is mentioned, so HEAD~ or HEAD~1 is equal to HEAD^

Initialize Git:
`git init`

Add or edit gitignore:
`nano .gitignore`

Track empty dir:
`touch dir/.gitkeep`

Get everything ready to commit:
`git add .`

Get custom file ready to commit:
`git add [filename]`

Commit changes:
`git commit -m "Message"`

Commit changes with title and description:
`git commit -m "Title" -m "Description..."`

Add and commit in one step:
`git commit -am "Message"`

Commit only exists in your local repository and has not been pushed to upstream repository:

`git add .`

`git commit --amend`

`git push`

Commit already pushed to upstream repository:

`git add .`

`git commit --amend`

`git push --force-with-lease`

> `force` overwrites a remote branch with your local branch and it is strongly discouraged as it can destroy other commits already pushed to a shared repository.

> `force-with-lease` is a safer option that will not overwrite any work on the remote branch if more commits were added to the remote branch (by another team member or coworker or what have you). It ensures you do not overwrite someone elses work by force pushing.

To specify the commit message inline:
`git commit --amend -m "New commit message"`

To use the previous commit message without changing it:
`git commit --amend --no-edit`

Remove files from Git:
`git rm [filename]`

Add files which are currently tracked ("update"):
`git add -u`

Remove file but do not track anymore:
`git rm --cached [filename]`

Move or rename files:
`git mv [filename] [new_filename]`

Undo modifications (restore files from latest commited version):
`git checkout -- [filename]`

Number of commits in a branch:
`git rev-list --count [branch-name]`

## Compare

Compare the working directory with index (staged but not yet commited): 
`git diff [filename]`

Compare the working directory with local repository:
`git diff HEAD [filename]`

Compare the staging with local repository:
`git diff --cached [filename]`

Compare modified files within the staging area:
`git diff --staged`

Compare branches:
`git diff master..[branchname]`

Compare commits:
`git --diff [old_commit] [new_commit]`

Useful comparings:
`git diff --stat --summary [commit_id]..HEAD`

Compare commits of file:
`git diff [commit_id 1]..[commit_id 2] [filename]`

## Branch
Show branches:
`git branch`

Create branch:
`git branch [branchname]`

Change to branch:
`git checkout [branchname]`

Create and change to new branch:
`git checkout -b [branchname]`

Rename the branch you have checked out:
`git branch -m [new_branchname]`

Rename another branch:
`git branch -m [branchname] [new_branchname]`

Show all completely merged branches with current branch:
`git branch --merged`

Delete merged branch (only possible if not HEAD):
`git branch -d [branchname]`

Delete not merged branch:
`git branch -D [branchname]`

List all branches:
`git branch -a`

List remote branches:
`git branch -r`

To verify which remote branches your local branches are tracking:
`git branch -vv`

Switch to the previous branch
`git checkout -`

Delete remote branch
`git push origin --delete [remote_branchname]`

Push branch to remote:
`git push -u [remotename] [branchname]`

> By default, git pushes the local branch to a remote branch with the same name. For example, if 
you have a local called _new-feature_, if you push the local branch it will create a remote branch _new-feature_ as well.
If you want to use a different name for the remote branch, append the remote 
name after the local branch name, separated by : `git push [remotename] [local_branchname]:[remore_branchname]`

Track upstream branch:
`git branch -u origin/[branchname]`

List local branches that contain a specific commit:
`git branch --contains [commit_id]`

## Log
Show commits:
`git log`

Show oneline-summary of commits:
`git log --oneline`

Show oneline-summary of commits with full SHA-1:
`git log --format=oneline`

Show oneline-summary of the last three commits:
`git log --oneline -3`

Show only custom commits:

`git log --author="Sven"`

`git log --grep="Message"`

Show only custom data of commit:

`git log --format=short`

`git log --format=full`

`git log --format=fuller`

`git log --format=email`

`git log --format=raw`

Show changes:
`git log -p`

Show every commit since special commit for custom file only:
`git log [commit_id].. [filename]`

Show changes of every commit since special commit for custom file only:
`git log -p [commit_id].. [filename]`

Show stats and summary of commits:
`git log --stat --summary`

Show history of commits as graph:
`git log --graph`

Show history of commits as graph-summary:
`git log --oneline --graph --all --decorate`

Colorize Logs:
`git log --graph --pretty=format:'%Cred%h%Creset %C(yellow)%an%d%Creset %s [%N] %Cgreen(%ar)%Creset' --date=relative`

Log between two branches:
`git log [branchname_1]..[branchname_2]`
> It will show the commits that are on _[branchname_2]_ and not on _[branchname_1]_.


## Collaborate

Show remote:
`git remote`

Show remote details:
`git remote -v`

Add remote upstream from GitHub project:
`git remote add upstream https://github.com/user/project.git`

Add remote upstream from existing empty project on server:
`git remote add upstream ssh://root@123.123.123.123/path/to/repository/.git`

Fetch:
`git fetch upstream`

>The command `git fetch [remotename]` can then be used to create and update remote-tracking branches [remotename]/[branchname].

Fetch a custom branch:
`git fetch upstream [branchname]:[local_branchname]`

Merge fetched commits:
`git merge upstream/master`

Change your remote url:
`git remote set-url origin https://localserver/develop/myrepo.git`

Remove origin:
`git remote rm origin`

Create and checkout branch from a remote branch:
`git checkout -b [local_branchname] upstream/[remote_branchname]`

Compare:
`git diff origin/master..master`

Push (set default with `-u`):
`git push -u origin master`

Push:
`git push origin master`

Force-Push:
`git push origin master --force`

Pull:
`git pull`

Pull specific branch:
`git pull origin [branchname]`

Clone to localhost folder:
`git clone https://github.com/user/project.git ~/dir/folder`

Clone specific branch to localhost:
`git clone -b [branchname] https://github.com/user/project.git`

Delete remote branch (push nothing):
`git push origin --delete [branchname]`


## Reset

>This usage of git reset is a simple way to undo changes that haven’t been shared with anyone else.

Unstage a file if not commited:

>If you moved a file into the staging area with git add, but no longer want it to be part of a commit, you can use git reset to unstage that file:

`git reset helloworld.txt`

>The changes you made will still be in the file, this command just removes that file from your staging area.

`git reset --soft`

> This git command will only move the HEAD. And, your staging area and working directory will not be affected.

`git reset --mixed` or `git reset`

> This git command will move the HEAD and also update the staging area. So this command will undo content added by git add and by git commit.

`git reset --hard`

> Dangerous! Use the following for resetting the staging area and the working directory to correspond to the last commit. It will unstage changes overwriting all changes in the working directory, too.

Undo last commit:

`git reset HEAD~`

....edit

`git add .`

`git commit -c ORIG_HEAD`

>commit with `-c ORIG_HEAD` will open an editor, which initially contains the log message from the old commit and allows you to edit it. If you do not need to edit the message, you could use the `-C` option.


## Clean
> Remove untracked files from the working tree

Print out the list of files which will be removed (dry run)
`git clean -n`

Forcefully remove untracked files:
`git clean -f`

Forcefully remove untracked directories in addition to untracked files: 
`git clean -fd`


## Revert

Undo a commit by creating a new commit:

`git revert [commit_id]`

Undo a commit which was pushed to a remote repository:

>If you committed and pushed your code to the remote repository, it is HIGHLY ADVISED that you DO NOT use git reset which rewrites history.

>This command creates a new commit that undoes the changes from a previous commit. This command adds new history to the project (it doesn't modify existing history).

First thing you should do is getting the list of commits that have been done so far by `git log` and identifying the commits that need to be reverted. In my case, the commit I want to revert would be ‘4dfebd1b’.

`git checkout 4dfebd1b`

`git revert 4dfebd1b`

This command will create a new commit with the “Revert” word in the beginning of the message, as you can see above. Copy the new commit hash. In my case, it would be ‘8002f5c4’. Then, push the new commit hash to a new branch in local (I created a local branch called ‘test-revert’) and push the branch to remote using commands:

`git branch test-revert 8002f5c4`

`git push origin test-revert`

You’ve got a new branch with the reverted commit changes.

Revert a series of commits:
`git revert [commit_id 1]..[commit_id 2]`

[commit_id 1] should be older than [commit_id 2].

## Merge

This example shows creating the test branch from the master branch:

`git checkout -b test master`

Before merging the two branches, you can take a look at what has changed between the branches by using `git diff test master`. Test is your source branch and master is your target branch. To perform the merge, you will have to move back to the master branch and then use the merge function like this:

`git checkout master`

`git pull origin master`

`git merge test`

Last, pushes the branch contents to the remote repository

`git push origin master`

> While you are working on your branch, other developers may update the master branch with their branch. This action means your branch is now out of date of the main branch and missing content. You can merge the master branch into your branch by checking out your branch and using the same git merge command `git checkout test && git merge master`

Git performs merges two ways: `fast-forward` and `three-way`

If master has diverged since the feature branch was created, the merging the feature branch into master will create a merge commit. If master has not diverged, instead of creating a new commit, git will then simply point master to the latest commit of the feature branch. This is a `fast forward`.

<img width="489" alt="Screenshot_01" src="https://user-images.githubusercontent.com/13599486/128633888-80a54861-75ee-45a9-bc17-cf0839257aa0.png">




