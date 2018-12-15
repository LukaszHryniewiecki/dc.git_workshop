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
3. `C:\stuff\new_repo>git init` - initialize a new empty git repositry in current directory
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
6. `C:\stuff\new_repo>git add a.txt` - stage file `a.txt` for commit
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
Untill now our repositry exists only locally. To create/add a remote counterpart for our repository we will need to create a github account and create a new empty repository on github. After creating a new repository on git hub we can tell our local repository that is has a remote counterpart.
1. `C:\stuff\new_repo>git remote add origin https://github.com/inwenis/new_repo` - tell our local repository that is has a remote repository under the URL `https://github.com/inwenis/new_repo`. The remote repository will be named `origin`
   * we can name our remote repository anything - using `potato` insted of `origin` will work. It is however a convetion to name the `main` remote repository `origin`
   * we can add multiple remote repositories `git remote add my_secret_remote https://github.com/inwenis/my_secret_remote`, however this is used rarley.
2. `C:\stuff\new_repo>git remote` - make sure our remote repositry was added. Git should print a list of remote repositores, this list should contains only `origin`.
3. `C:\stuff\new_repo>git remote show origin` - make sure `origin` has correct URLs.
```
* remote origin
  Fetch URL: https://github.com/inwenis/new_repo.git
  Push  URL: https://github.com/inwenis/new_repo.git
  HEAD branch: (unknown)
```
At this point our local repository has a remote `origin` repository but no branches are yet connected between our local repository and `origin`
4. `C:\stuff\new_repo>git push -u origin master` - push commits from `master` branch to `origin`. Bind our local `master` banch to `origin`'s `master` branch.
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
   * git tells us the `master` branch was created in `origin`
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
   * if we would like the repo to be cloned to another folder we can find the appropriate option in `git clone --help`
6. add some changes in the cloned repository, commit and push them. Note that this time we can just use `git push` without `-u origin master` since when cloning everything is already setup.
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
   * in this case everything should go smooth an git should tell us the merge is a `fast-forward`
   * we can use the command `git pull` which is equivalent to `git fetch` + `git merge`

What would happen if before fetching you would introduce changes in `C:\sutff\new_repo` to the same as which `joe_doe` modifies?

You can replay the exercise and try to do it - you should get a merge confilict which is a often problem if multiple people modify the same file in the same places.
