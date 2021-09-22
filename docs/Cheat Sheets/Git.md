# Git

> Git commands and tidbits of info I have found useful.

Tip: Always make a backup branch if you are unsure of what you're doing.

## First Time Setup Config

Setup name and email guide:
https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup

## Most Common Commands

### Change branch name

#### One method

To change the local/remote name of a branch:

1. `git branch -m new-name` # rename local branch, while on that branch
2. `git push origin :old-name new-name` # delete old-name remote branch, push new-name local branch
3. `git push origin -u new-name` # switch to new branch, reset upstream branch for new-name local branch

#### Another method

1. While on branch to be renamed, `git checkout -b new-branch-name`
2. Re-push it with `git push -u origin new-branch-name`

### Merge one branch into another

Can be easy to forget, especially if new to this. Just think, "merge name-of-incoming-branch INTO current branch".

`git merge incoming-branch` # while on current branch

### Replay your changes on top of latest from main branch

`git pull --rebase`

### Edit a non-pushed commit

1. If doing more than just fixing a commit message, make whatever code changes needed.
1. `git commit --amend`

### Remove most recent pushed commit(s) from history

Works for removing any number of commits as long as they are all the most recent ones or single most recent one.

1. `git reset [SHA]` where the SHA is the most recent commit in the history that you want to keep (and will remove anything in the future from this point). This will unstage the changes but now they are in the working directory.
1. `git reset --hard` this removes the working directory changes. Now it's as if you are on whatever SHA you reset to, and have not made any changes since then.
1. `git push -f` erase the future commits that were removed and update remote repo.

## Other Commands

### Delete a branch

`git branch -D branch-name` - delete locally

`git push origin:branch-name` - delete on remote

### Squash commits periodically

#### One Way of Doing It

1. `git log` // view history of commits (count these correctly for the next step)
1. `git rebase -i HEAD~[# of commits]`
1. Change top commit from Pick to e
1. Change rest from Pick to f
1. First commit will have summary of project as description when updated
1. Press y, hit enter, to save changes locally
1. `git commit --amend` // change commit message
1. Exit editor
1. `git rebase --continue`
1. `git push origin branch-name --force`

Tip: To get multi-line cursor, do CTRL+ALT+arrow keys

Tip: To just replace pick with squash, do:
`:%s/pick/s/g`

#### Another Way of Doing It

1. Go to commits history (on GitHub or from terminal)
1. Copy the sha of the most recent commit that you want to actually save and not have it be erased. “This is the commit that I want to keep, everything ahead of it I want to delete.” This is likely the sha of the commit that you branched off from (it existed from the master branch and you branched off of it).
1. Go to your feature branch and type `git rebase -i [SHA]`
1. After rebase, do `git push -f`. Now you have 1 commit for this branch.

### Stage all deleted files

Add all of the already-deleted files to staging.

`git status -s | grep -E '^ D' | cut -d ' ' -f3 | xargs git add --all`

## RGB Colors in Git Bash

- Black 0;30 Dark Gray 1;30
- Blue 0;34 Light Blue 1;34
- Green 0;32 Light Green 1;32
- Cyan 0;36 Light Cyan 1;36
- Red 0;31 Light Red 1;31
- Purple 0;35 Light Purple 1;35
- Brown 0;33 Yellow 1;33
- Light Gray 0;37 White 1;37

Example of this being used can be found on my awesome-git-hooks repo:
CompSciLauren/awesome-git-hooks
