# Git

## Create new branch and sync to remote

```
export BRANCH=newbranch
git checkout -b $BRANCH
git push origin $BRANCH
git branch --set-upstream-to=origin/$BRANCH $BRANCH
git pull
```

Bash script:

```
#!/bin/bash
  
set -e

export BRANCH=$1
if [ -z "$BRANCH" ]
then
    echo "Must provide a branch name"
    exit 1
fi

echo New Branch=$BRANCH

git checkout master
git pull
git checkout -b $BRANCH
git push origin $BRANCH
git branch --set-upstream-to=origin/$BRANCH $BRANCH
git pull
git status
```

## Squash Commits

If needed - use git log to see how many commits you wish to squash on the current branch.

    git log

If you want to squash the last 4 commits:

    git rebase -i HEAD~4

Then change the history in the interactive window to:

```
pick ...
s ...
s ...
s ...
```

Then write that and on the next prompt update the commit message (pick and update a single commit message and delete the intermediate messages.

If branch was already pushed to the remote:

    git push -f

## Cherry pick

* run ```git pull``` on both the source branch and target branch of the cherry pick action.

```
git checkout <SOURCE_BRANCH>
git pull
git checkout <TARGET_BRANCH>
git pull
git cherry-pick <DESIRED_COMMIT_SHA>

# Assuming there are no merge conflicts to resolve:
git status
git push
```

## Clone private repo

```
git clone https://username@github.com/orgname/reponame.git
```

Where username is the github user with access to the repo.

## Drop local repo changes and reset to remote state

```
git fetch origin
git reset --hard origin/master
```

## Add existing code to a newly created repo

* Create a new repo on github, then

```
export USERNAME=foo
export PROJECTNAME=bar
echo "# $PROJECTNAME" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/${USERNAME}/${PROJECTNAME}.git
git push -u origin master
git add .
git commit
git push
```

## Show remotes

```
git remote -v
```

## Change remote on existing repo

```
git remote -v
git remote set-url origin https://github.com/USERNAME/NEW_REPO_NAME.git
git push
```

## Update local branch after forced update

If someone else forced an update to a branch, say "develop" and you want to get back in sync with remote:

```
export BRANCH=develop
git checkout $BRANCH
git fetch
git reset origin/$BRANCH --hard
```

## Remove a commit that isn't at HEAD

If you want to remove a commit with sha "SHA" from a branch that doesn't happen to be the last commit, try:

```
git rebase -p --onto SHA^ SHA
```

* You may need to fix conflicts. If so then use `git status` to see what needs fixing, fix it, then do `git rebase --continue`
* If the branch is pushed remote, then it will be diverged now, so you'll have to do `git push -f` to force 
  the overwriting the remote (do this with caution of course!).
