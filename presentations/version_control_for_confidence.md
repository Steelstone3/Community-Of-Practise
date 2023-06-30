# Version Control For Confidence

## Introduction

Git has a "bag of tricks" that we can use for "development without fear".

Lets look at

> * Confidence For Making Design Decisions
>
> * Disaster Recovery From Poor Design
>
> * Disaster Recovery From Fixing Merge Conflicts
>
> * Disaster Recovery From A Broken Local Branch

## Commits As "Checkpoints" - Confidence For Making Design Decisions

> git commit -m "Implemented some successful design"

Sometimes when developing code you'll hit a fork in the road where you are unsure as to what design direction to take from here on in.

When you hit a situation like this especially if you have been commiting work regularly you can commit the current work you have like a "checkpoint" in a video game.

If you find the design direction you were unsure about isn't fit for purpose you can "load" the old "save" with

> git reset --hard

If the design however is fit for purpose and you want to proceed you can "save your progress" with a commit.

> git commit -m "A design that worked for the thing I was working on"

## Git Branch new_branch 35d34ad2dd015d70904c91dedd4cfdcf4a51f168 As Disaster Recovery From Poor Design

Sometimes when we design code we wish we could go branch off two or three commits ago and just try something else.

Well you can!

To switch to a specific commit use git log to find the commit hash that you wish to switch to.

For example:

> * git log

```md
commit f80ad9d432dbd3f302865534b35b7425602ac763
Author: Trip Tucker <triptucker@gmail.com>
Date:   Sun Mar 5 18:34:28 2023 +0000

    MVP V1.5

commit f1df51ffd31cb833e2948437967067268213fa29
Author: Trip Tucker <triptucker@gmail.com>
Date:   Sun Mar 5 17:57:32 2023 +0000

    MVP V1.4
```

Then use...

> git branch new_branch f1df51ffd31cb833e2948437967067268213fa29
>
> git checkout new_branch

To create a new branch from a specific commit then checkout to that new branch.

or to do it all in one step

> git checkout -b new_branch f1df51ffd31cb833e2948437967067268213fa29

Alternatively we can use this command

> git branch branch_name HEAD~3

To create a new branch from N commits back from the HEAD of the current local branch

### HEAD~N Example

If the latest commits looked like this on the original branch

> commit Version 5 (HEAD)
>
> commit Version 4
>
> commit Version 3
>
> commit Version 2
>
> commit Version 1

and you then run this

> git branch new_design_idea HEAD~3

The branch will start at commit "Version 2"

### Conclusion

Just one more reason to commit incrementally and often.

From the new branch carry on from a better starting point.

## Git Push As Disaster Recovery From A Broken Local Branch

So you've developed a piece of work that you are really happy with and you push it but it comes back with "merge conflicts"...

> git push origin your_branch

You finishing fixing the merge conflicts and are testing the changes before you are about to push them to remote... but disaster the build doesn't work in your local branch.

Relax...

> git reset --hard origin/your_branch

will reset the not working local branch with the original remote branch with the work you were happy with.

## Git Rebase --abort As Disaster Recovery From Fixing Merge Conflicts

Lets say you pushed your branch and find that it has merge conflicts so have now started to rebase your branch

> git pull --rebase

You find your branch has merge conflicts and when in the process of resolving the merge conflicts you get confused and make some mistakes...

You feel that if you proceed fixing merge conflicts you'll only make further mistakes that will break the build. What can you do?

In this case git offers the following

> git rebase --abort

This will put your branches back to before you tried to rebase. Give someone a call who can help with resolving the merge conflicts and proceed from there.

## Git Pull Is Not Git Pull --rebase

When pulling the latest branch we want to ensure we are doing it in a safe reversable way.

> git config --global pull.rebase true

Ensure this setting is set and never make the mistake with git pull accidently merging the latest over rebasing your branch to the latest ever again.

### Note

There may be additional settings for git frontends that you'll need to check

## Final Thoughts

Quick "disaster recovery" is one of the key strengths of version control and knowing these helpful tips will ensure you can proceed with confidence as a developer.
