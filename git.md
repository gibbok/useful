# Git commands

## Compare changes from branch XXX against master

```shell
git reset $(git merge-base master XXX)
```

## Create a fake commit and trigger the new build

```shell
git commit -a --amend --no-edit --no-verify; git push --force-with-lease
```

## Create an empty commit
```shell
git commit --allow-empty -m "My empty commit with a message"
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

## List all branches except master and the current branch, and delete them

```shell
git branch | grep -v "master\|$(git branch --show-current)" | xargs git branch -d
```

or delete all branch except master and develop:

```shell
git branch | grep -v "develop\|master\|$(git branch --show-current)" | xargs git branch -D
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

## Remove all untracked files

To see which files will be deleted:

```shell
git clean -n
```

To remove all files:
```shell
git clean -f
```

## Revert latest commit which was pushed

Create a new commit that undoes the changes of a previous commit.

```shell
git revert HEAD
```

## Create a path file

```shell
git diff > my_patch.patch
```

## Apply a path file

```shell
 git apply my_patch.patch
```

# Resources

[Deep Dive into Git - Edward Thomson](https://www.youtube.com/watch?v=fBP18-taaNw)

## Removing the last commit pushed

```shell
git reset --hard HEAD^
git push origin -f
```

or

```shell
git reset --hard HEAD~1
git push origin -f
```

## Conflicts with Merge or Rebase

Rebase:

When rebasing a feature branch on top of the base branch:

- **Current changes:**  
  Your changes from the feature branch (usually the changes you are working on).
- **Incoming changes:**  
  Changes from the base branch.

Merge:

Merging combines the changes from two branches (the feature branch and the base branch) into a single commit. 

- **Current changes:**  
  Your changes from the feature branch (usually the changes you are working on).
- **Incoming changes:**  
  Changes in the base branch.

### Prevent a local file to be commit locally

Prevent a file from being committed locally (event after it is included in a `.gitignore` file). It can be insalled as git hook for instance after a checkout `post-checkout`.

```shell
git update-index --assume-unchanged path-to-file.json
```

This differs from using a `.gitignore file`, as it applies to tracked files that you want Git to temporarily ignore. Files already tracked by Git are not affected by `.gitignore` settings.

## Commit case-sensitive only filename changes

```shell
git mv FileName.ts filename.ts
```

## Go back in time and check out at that point in time

```shell
git checkout HEAD@{1.week.ago}
```

## Switches you to your previous branch

It switches you to your previous branch. Instead of typing it all out, you can just say "-"

```shell
git checkout -
```

works also with:

```shell
`git merge -`
```







