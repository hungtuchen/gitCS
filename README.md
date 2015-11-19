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

git log
--------------

`$ git log`

`$ git log --pretty=oneline`

// (SHA hash) (commit_message)

`$ git log --pretty=format:”%h %ad- %s [%an]”`

// %ad = author date % an = author name

// %h = SHA hash %s = subject %d = ref names

`$ git log --oneline -p`

// -p for patch output (detail change)

// --stat insertion and deletion

// --graph visualize the merging

`$ git log --until=1.minute.ago`

// --since=1.day(hour) ago

// --since=1.month.ago --until=2.weeks.ago

// --since=2015-01-01 --until= 2015-04-01

git clone
--------------

`git clone <url> <new_repo_name>`

`git clone <repo_to_be_cloned> <new_repo_name>`

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

// Deletes all deleted branches on `<remote_name>` but still referenced under local(`remotes/<remote_name>`) 

// options: --dry-run, report what branches will be pruned, but do not actually prune them.

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

`$ git branch -m <newname>`

// rename current branch

`$ git branch <new_branch_name> <hash>`

// create new branch point to <hash>

// <hash> can be replaced with reflog shortname

*Recover from deleted branch*

`$ git reflog`  // and find the SHA1 for the commit at the tip of your deleted branch, then

`$ git checkout [sha]`

`git checkout -b [branchname]` //  to recreate the branch from there.

git checkout
--------------

`$ git checkout -- <file>… `

// to discard changes in working directory
// blow away all changes since last commit

`$ git checkout -b <branch_name>`
// as if `$ git branch <branch_name>` were called and then checked out

`$ git checkout <tag>`

git reset
--------------

`$ git reset HEAD <file> `

// to unstage

`$ git reset --soft HEAD^`

// undo last commit, put changes into staging

`$ git reset --hard HEAD^`

// undo last commit and all changes

`$ git reset --hard HEAD^^`

// undo last 2 commits and all changes

`$ git reset --hard <SHAhash>`

`$ git reset --hard HEAD@{[number]}`

git reflog
--------------

// git update reflog whenever HEAD moves

// only exists locally

`$ git reflog`

// list all the reflogs

`$ git log --walk-reflogs`

// to see reflog info in log format

git tag
--------------

`$ git tag`

// list all tags

`$ git tag -a <tag_name> -m <message>`

// to add a new tag and make it annotated

`$ git tag -d <tag_name>`

// delete tag

`$ git push origin :refs/tags/<tag_name>`

// to delete a remote tag

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

git cherry-pick
--------------

`$ git checkout <branch_to_put_cherry-pick>`

`$ git cherry-pick <SHAhash>`

*options:*
  --edit // to add new commit message
  --no-commit <SHAhash…> // pull (multiple) commit and stages them
  -x : add source SHA to commit message
  --sign : track who did the cherry-picking

git diff
--------------

`$ git diff`

// show unstaged differences since last commit

`$ git diff --staged`

// view staged differences

`$ git diff HEAD~5`

// five commits ago

`$ git diff HEAD^..HEAD`

// second most recent commit vs. most recent

`$ git diff <hash1>..<hash2>`

// also (branch1)..(branch2)

// time range as in [git log](README.md#git-log)

git push
--------------

`$ git push <remote> <branch>`

`$ git push -u <remote> <branch>`

// link local `<branch>` to remote `<branch>` (tracking)

`$ git push <remote> <local_branch>:<remote_branch>`

// link up <local_branch> to <remote_branch> (useful for ex: heroku)

`$ git push <remote> :<branch>`

// delete remote branch

`$ git push --tags`

// push changes and new tags

`$ git push origin :refs/tags/<tag_name>`

// to delete a remote tag

`$ git push --recurse-submodules=check`

// abort push if haven’t pushed submodule

// can run when pushing from parent

`$ git push —recurse-submodules=on-demand`

// push all submodules automatically

git apply
--------------

`$ git apply <patch_file>`

// read the supplied patch file and applies it to files (generated from [git format-patch](README.md#git-format-patch))

// this command applies the patch but does not create a commit

git format-patch
--------------

`$ git format-patch origin`

// Extract all commits which are in the current branch but not in the origin branch

`$ git format-patch --root origin`

// Extract all commits that lead to origin since the inception of the project

`$ git format-patch -3`

// Extract three topmost commits from the current branch

git stash
--------------

`$ git stash (save) <message>`

// save modified files and restore last commit

`$ git stash save --keep-index`

// keep staging area not to be stashed

// other options: --include-untracked

// normally git stash only tracked files

`$ git stash apply stash@{[number]}`

// bring stashed files back

// by default: stash@{0}, use `$ git stash list` to check

`$ git stash list (--stat)`

// list all stashes, any argument as git log

`$ git stash show stash@{[number]}`

// show particular stash,  by default: stash@{0}, any argument as git log

`$ git stash drop stash@{[number]}`

// drop stash after applied, by default: stash@{0}

`$ git stash pop`

// $ git stash apply; git stash drop

// need to drop manually if conflict exists

`$ git stash branch <branch_name> stash@{[number]}`

// checkout a new branch, apply the stash you specify and drop automatically

`$ git stash show -p stash@{0} | git apply -R`

// sometimes you wanna un-apply stash, thought there is no command for that

`$ git config --global alias.stash-unapply '!git stash show -p | git apply -R'`

// to use `$ git stash-unapply`

`$ git stash clear`

// clear all stashes

git filter-branch
--------------

`$ git filter-branch --tree-filter <shell_command> -- --all`

// check out each commit to run `<shell_command>` and recommit

ex: --tree-filter `‘rm -f password.txt’`

--all   // on all branches

HEAD    // filter only current branch

`$ git filter-branch --index-filter <shell_command>`

// `<shell_command>` ‘must’ operate on staging area

ex: --index-filter `‘git rm --cached --ignore-unmatch password.txt’`

-f    // if we wanna run filter-branch again, which overwrite the backup

--prune-empty     // drop commit not modifying any file

.gitignore
--------------

ex: logs/*.log

git rm
--------------

`$ git rm <file>; git commit -m <message>`

// stop tracking
// ex: you do `rm <file>` then do above, it would stage the file’s removal and commit
// <file> will be gone and no longer tracked

`$ git rm —cached`

// keep the file on your hard drive but not have Git track it anymore

git clean
--------------

`$ git clean -f`

// delete untracked local files from your current branch

option:
`-fd`: also remove directories
`-fX`: remove only ignored files
`-fx`: remove ignored as well as non-ignored files

`$ git clean -n`

// no going back for `$ git clean -f`, so use this to preview first

git blame
--------------

`$ git blame <file> --date short`

git submodule
--------------

`$ git submodule add <repo_address>`

// create `.gitmodules` and `<new_module_name>` (actually a directory)

**TO MODIFY SUBMODULES**

`$ cd <new_module_name>`
`$ git checkout master`

// by default, don’t have branch

// after modifying, add, commit, push as usual but also ‘need to back to parent module and do it again’

`$ git submodule init`

// to init a repo containing submodules first, adding entry to `.git/config`

`$ git submodule update`

// pull down the repo and new changes

// notice: after update, it would be on no branch

# Credit
Most of the content are based on what I learned from [CodeSchool](https://www.codeschool.com/paths/git)


![git logo image](https://github.com/transedward/gitCS/blob/master/Git-Logo-2Color.png)
