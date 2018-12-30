# Workshop 1 - introduciton to git from console

Commands we have used:
* `git init`
* `git clone`
* `git status`
* `git add`
* `git commit`
* `git log`
* `gitk`
* `git branch`
* `git remote`
* `git fetch`
* `git pull`
* `git push`
* `git merge`

#### Local repository
1. `C:\stuff>mkdir new_repo` - create a new folder for your new repository
2. `C:\stuff>cd new_repo` - change directory to `new_repo`
3. `C:\stuff\new_repo>git init` - initialize a new empty git repository in current directory
   * all git commands work in the currect directory
   * this command will create a `.git` directory in which git stores everything about the repository
4. `C:\stuff\new_repo>echo 'some text' > a.txt` - create file `a.txt` and write some content to it
5. `C:\stuff\new_repo>git status` - show what is going on
```
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        a.txt

nothing added to commit but untracked files present (use "git add" to track)
```
   * tells you what branch you are current on - `On branch master` - by defualt it will be `master`
   * tells us we don't yet have any commits in our repository - `No commits yet`
   * tells us that git sees an untracked file - `a.txt` - an untracked file is a file which git sees but the file has not yet been commited to our repository
6. `C:\stuff\new_repo>git add a.txt` - stage file `a.txt` for commiting
   * in git before a file is commited it first must be staged. Staging is just tellig git: "hey, we want to commit this file in a moment". When staging git will mark the file as "by next commit this file will be included in the commit"
   * if we don't want to stage every file separately we can stage all files by `git add .`
7. `C:\stuff\new_repo>git status` - make sure our file is staged
```
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   a.txt

```
   * our file is in `Changes to be commited:` which is what we wanted
8. `C:\stuff\new_repo>git commit -m "initial commit"` - commit `a.txt` to the first commit in our repositry
   * to get help on `commit` command use `git commit --help`, this work for all git commands - `git **** --help`
   * most git commands follow the convetion of a abbreviated form `git commit -m "here goes the message"` and full name `git commit --message="here goes the message"`
9. `C:\stuff\new_repo>git status` - make sure everything is commited
```
On branch master
nothing to commit, working tree clean
```
   * git tells us there is `nothing to commit` so we have commited our file succesfully
10. We can now add some more text into `a.txt`. This time after modifying the file and running `git status` git should tell us that the file is `modified` - it is alredy tracked, and it has chages which were not yet commited.
11. Add some more commits to your repository.
12. `C:\stuff\new_repo>git log` - show all commits
```
commit 2ca0ca6f3e645a7282750f4fb1e97080c723c86a (HEAD -> master)
Author: Filip Kucharczyk <fku-ext@danskecommodities.com>
Date:   Sat Dec 15 23:00:29 2018 +0100

    adding b.txt

commit 05e978bf0058beac0ac8fa0a7a3eac430a5b51af
Author: Filip Kucharczyk <fku-ext@danskecommodities.com>
Date:   Sat Dec 15 22:39:23 2018 +0100

    initial commit
```
13. `C:\stuff\new_repo>gitk` - show commits tree in a visual form

#### Remote repository
Untill now our repositry exists only locally. To create/add a remote counterpart for our repository we will need to create a github account and create a new empty repository on github. After creating a new repository on github we can tell our local repository that is has a remote counterpart.
1. `C:\stuff\new_repo>git remote add origin https://github.com/inwenis/new_repo` - tell our local repository that is has a remote repository under the URL `https://github.com/inwenis/new_repo`. The remote repository will be named `origin`
   * we can name our remote repository anything - using `potato` insted of `origin` will work. It is however a convetion to name the main remote repository `origin`
   * we can add multiple remote repositories `git remote add my_secret_remote https://github.com/inwenis/my_secret_remote`, however this is used rarley.
2. `C:\stuff\new_repo>git remote` - make sure our remote repositry was added. Git should print a list of remote repositores, this list should inclusd only `origin`.
3. `C:\stuff\new_repo>git remote show origin` - make sure `origin` has correct URLs.
```
* remote origin
  Fetch URL: https://github.com/inwenis/new_repo.git
  Push  URL: https://github.com/inwenis/new_repo.git
  HEAD branch: (unknown)
```
At this point our local repository has a remote `origin` repository but no branches are yet connected between our local repository and `origin`

4. `C:\stuff\new_repo>git push -u origin master` - push commits from `master` branch to `origin`. Bind our local `master` branch to `origin`'s `master` branch.
```
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (7/7), 504 bytes | 126.00 KiB/s, done.
Total 7 (delta 0), reused 0 (delta 0)
To https://github.com/inwenis/new_repo.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```
   * git tells us the `master` branch was created in `origin` - `* [new branch]      master -> master`
   * `Branch 'master' set up to track remote branch 'master' from 'origin'.` - git tells us our local `master` it bound to `origin`'s `master`
   * we will only need to write `-u origin master` only the first time. It tells git to "bind" our local `master` to `origin`'s `master`
   * we can now see our commits on github

#### Collaborating on remote repositories
1. `C:\stuff\new_repo>cd ../..` - move up two directoires
2. `C:\>mkdir joe_doe` - pretent we are `joe_doe` and would like to contribute to our new repository
3. `C:\>cd joe_doe` - change direcotry to `joe_doe`
4. `C:\joe_doe>git clone https://github.com/inwenis/new_repo` - clone the remote repository into a local one
```
Cloning into 'new_repo'...
remote: Enumerating objects: 7, done.
remote: Counting objects: 100% (7/7), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 7 (delta 0), reused 7 (delta 0), pack-reused 0
Unpacking objects: 100% (7/7), done.
```
   * by default cloning will create a `new_repo` folder (named after the URL) with the repository
   * the local clone has `origin` already setup to `https://github.com/inwenis/new_repo`
   * `master` is already "bound" to `origin`'s `master`
   * if we would like the repository to be cloned to a folder name firrerently we can find the appropriate option in `git clone --help`
6. Add some changes in the cloned repository, commit and push them. Note that this time we can just use `git push` without `-u origin master` since when cloning everything is already setup.
7. `C:\joe_doe\new_repo>cd ..\..\sutff\new_repo` - go back to our original repository
8. `C:\sutff\new_repo>git fetch` - download new commits from `origin`
```
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/inwenis/new_repo
   2ca0ca6..e930175  master     -> origin/master
```
   * git tells us there are new commits in `master` branch - `2ca0ca6..e930175  master     -> origin/master`
9. `C:\sutff\new_repo>gitk --all` - see what is going on in `origin`
   * we can see the the branch `remotes/origin/master` is ahead of `master`. It has commits commited while we were `joe_doe`
   * `origin/master` is a branch used by our local repository to track `origin`'s `master` branch
10. `C:\sutff\new_repo>git merge origin/master` - merge commits present in `origin/master` to our current branch - ie. `master`
   * in this case everything should go smooth and git should tell us the merge is a `fast-forward`
   * we can use the command `git pull` which is equivalent to `git fetch` + `git merge`

What would happen if before fetching you would work on the same file as `joe_doe` did?

You can replay the exercise and try to do it - you should get a merge confilict which is a popular problem if multiple people modify the same file in the same places.

# Workshop 2 - introduciton to branches

New commands we have used:
* `git branch`
* `git checkout`
* we have resused a lot of commands from Workshop 1

#### Collaborating on remote repositories on your own branch
1. `C:\stuff>git clone https://github.com/inwenis/dc.git.workshop1` - clone the remote repository into a local one
2. `C:\stuff>cd dc.git.workshop1` - change the working directory to `dc.git.workshop1`
3. `C:\stuff\dc.git.workshop1>git status` - make sure we are in a git repository.
   * if you see `fatal: not a git repository (or any of the parent directories): .git` it means you have a problem and you're not in a git repository. 
4. `C:\stuff\dc.git.workshop1>git branch my_very_own_branch_123` - create a new branch `my_very_own_branch_123` in the current repository.
   * you can use almost any name for a branch. If the name will not be valid git will tell you.
   * teams often agree on some naming convention for their branches. For example branches which you use to code features are named: `feature/DCT-123` and branches used to code hotfixes are named: `hotfix/DCT-124`.
      * git considers the `feature/DCT-123` branch names just a name, the `/` or `feature` has no special meaning for git
      * `DCT` might be the teams acronim or name of jira board
      * `123`/`124` can be the task names from jira
      * using this naming convention will allow jira to automatically assosiate tasks with git branches
5. `C:\stuff\dc.git.workshop1>git branch` - list all branches
```
* master
  my_very_own_branch_123
```
   * git tell us there are 2 branches in this repository and the current branch is `* master` (marked by a `*`)
6. `C:\stuff\dc.git.workshop1>git checkout my_very_own_branch_123` - change the current branch to `my_very_own_branch_123`
```
Switched to branch 'my_very_own'
```
   * creating a new branch and checking it out is a very common activity. You can do it with a single command - `git checkout -b new_branch_name`
7. make same changes to existing files, add new ones, commit a few commts on your branch.
8. `C:\stuff\dc.git.workshop1>gitk` - see how the commits tree looks like after adding new commits
9. `C:\stuff\dc.git.workshop1>git push -u origin my_very_own_branch_123` - push your `my_very_own_branch_123` branch to the remote repository.
```
Total 0 (delta 0), reused 0 (delta 0)
remote:
remote: Create a pull request for 'my_very_own_branch_123' on GitHub by visiting:
remote:      https://github.com/inwenis/dc.git.workshop1/pull/new/my_very_own
remote:
To https://github.com/inwenis/dc.git.workshop1
 * [new branch]      my_very_own_branch_123 -> my_very_own_branch_123
Branch 'my_very_own_branch_123' set up to track remote branch 'my_very_own_branch_123' from 'origin'.
```
   * untill now the branch `my_very_own_branch_123` was present only in your local clone of the repository `dc.git.workshop1`.
   * after pushing `dc.git.workshop1` to `origin` others can now see your branch.
10. `C:\stuff\dc.git.workshop1>git checkout master` - change the current branch to `master`
11. `C:\stuff\dc.git.workshop1>git merge my_very_own_branch_123` - merge branch `my_very_own_branch_123` into the current branch (into `master`)
```
Updating 6c56d1c..be86211
Fast-forward
 b.txt | Bin 0 -> 14 bytes
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 b.txt
```
12. `C:\stuff\dc.git.workshop1>gitk` - see how the commits tree looks like.
13. `C:\stuff\dc.git.workshop1>git push` - push new commits on current branch `master` to the remote repository

Using branches helps to better organize your work. You can work on multiple tasks at the same time having a separate branch for every task.

If you would like to share work in progress with someone you can push your branch to remote repository and send the branch name to your coworkers. They will be able the do a `git fetch` and then `git checkout ...` and admire the genius of your work!