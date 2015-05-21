# gitCS
a git cheet sheet arranged by command and short discription

Usage
--------------
Sometimes You know some keyword for key command but can't memorize it.
This cheat sheet is I creat for this need, just use command(ctrl) + F to quickly find what you need.

// for short discription

git config
--------------
config: --local --global --system

`$ git config --global user.name  [name]`
`$ git config --global user.email [email]`

`$ git config user.email <email>`

// only for current repo

`$ git config --global color.ui true`

`$ git config --global core.editor <editor>`

`$ git config --global merge.tool opendiff`

`$ git config (--global) --list`

// list all the config

// edit config directly in ~/.gitconfig

#### common pattern for log
```
$ git config --global alias.mylog \
"log --pretty=format:'%h %s [%an]' --graph"

$ git config --global alias.lol \
"log --graph --decorate --pretty=oneline --abbrev-commit --all"

$ git config --global alias.hist \
“log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short”
```

`$ git config --global core.autocrlf input`

// auto carriage return

`$ git config --global pull.rebase true`

// default to $ git fetch; git rebase rather than $ git pull = git fetch; git merge

`$ git config --global rerere.enabled true`

// records all fixes to merge conflict, automatically fix later ones if the same

git remote
--------------

`$ git remote add origin <repo URL>`

`$ git remote -v`

// show remote repositories

`$ git remote add <name> <URL>`

// to add new remotes

`$ git remote rm <name>`

// to remove remotes

`$ git remote show <remote_name>`

// all the branch information between <remote_name> and local

`$ git remote prune <remote_name>`

// to clean up deleted remote branches

git branch
--------------

`$ git branch -d <branch_name>`

// delete branch

`$ git branch -D <branch_name>`

// force delete branch

`$ git push <remote> :<branch>`

// delete remote branch

`$ git branch -r`

// list all remote branch

`$ git branch -a`

// view all of the branches, including remote

`$ git branch -m <oldname> <newname>`

// rename branch

`$ git branch <new_branch_name> <hash>`

// create new branch point to <hash>

// <hash> can be replaced with reflog shortname

git merge
--------------

`$ git merge <branch_name>`

// fast-foward condition:

// (assume on master) nothing new

// <branch_name> something new

// recursive condition:

// both branches have changed

`$ git merge —no-ff <branch>`

git commit
--------------

`$ git commit -am <message>`

// add changes from all tracked files, doesn’t add new (untracked) files

// add and commit in 1 step

`$ git commit --amend -m <new_message>`

// whatever has been staged is added to last commit

git fetch, rebase
--------------

// when local and remote both commit

`$ git fetch; git rebase`

// (if not to merge automatically)

// instead of recursive merge (local)

`$ git checkout <feature>`
`$ git rebase master`

// (assumed we want <feature> merged into master), this command will add the commits of master into feature

`$ git checkout master`
`$ git merge <feature>`

// then it would be fast-forward

// when rebase comes into conflict

`$ git rebase --continue`

// problem has resolved

`$ git rebase --skip`

//skip this patch

`$ git rebase --abort`

//check out the original branch and stop rebasing

`$ git rebase -i  HEAD~3`

// interactive rebase after HEAD~3

# Credit
Most of the content are based on what I learned from [CodeSchool](https://www.codeschool.com/paths/git)
