# Git commands

## Compare changes from branch XXX against master

```shell
git reset $(git merge-base master XXX)
```

## Create a fake commit and trigger the new build

```shell
git commit -a --amend --no-edit --no-verify; git push --force-with-lease
```

## Rename git branch locally and remotely

```shell
git branch -m old_branch new_branch         # Rename branch locally    
git push origin :old_branch                 # Delete the old branch    
git push --set-upstream origin new_branch   # Push the new branch, set local branch to track the new remote
```

### Takes a patch (e.g. the output of git diff ) and applies it to the working directory

```shell
git apply << EOF
... some diff here
EOF
```

### Attaches a pull request for the current branch to the existing issue number x using hub

```shell
hub pull-request -i x
```

## Remove all your local git branches but keep master

```shell
git branch | grep -v "master" | xargs git branch -D
```

## Pull multiple projects automatically

```shell
find . -mindepth 1 -maxdepth 1 -type d -print -exec git -C {} pull \;
```

## Remove all files which are not tracked by git

```shell
git clean -fxd
```

## Move branches around 

Reassign a branch to a commit with the -f option. It moves (by force) the main branch to three parents behind HEAD.

```shell
git branch -f main HEAD~3
```

## Shorthand for a fetch and a rebase

```shell
git pull --rebase
```

## Show any action performed in git

```shell
git reflog
```

## Print the SHA1 hashes given a revision

```shell
git rev-parse
```

## Remove all branches matching a pattern

```shell
git branch | grep "<pattern>" | xargs git branch -D
```

## Check all differences between two branches and apply to a new branch

```shell
git checkout master
git diff master..your-branch > mypatch.patch
git checkout -b new-branch
git apply mypatch.patch
```

# Resources

[Deep Dive into Git - Edward Thomson](https://www.youtube.com/watch?v=fBP18-taaNw)
