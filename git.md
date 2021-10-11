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

## pull multiple projects automatically

```shell
find . -mindepth 1 -maxdepth 1 -type d -print -exec git -C {} pull \;
```

## remove all files which are not tracked by git

```shell
git clean -fxd
```

## To move branches around, reassign a branch to a commit with the -f option. It moves (by force) the main branch to three parents behind HEAD.

```shell
git branch -f main HEAD~3
```

## shorthand for a fetch and a rebase

```shell
git pull --rebase
```

## show any action performed in git

```shell
git reflog
```

## print the SHA1 hashes given a revision

```shell
git rev-parse
```
