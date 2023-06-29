# Commits For Confidence

## Introduction

Git has a "bag of tricks" that we can use for "development without fear".

Lets look at

> * Confidence for making design decision
>
> * Disaster recovery from a poor design decision
>
> * Disaster recovery from a rebase attempt
>
> * Disaster recovery from a completed rebase/ broken local build

## Commits As "Checkpoints"

> git commit -m "Implemented some successful design"

Sometimes when developing code you'll hit a fork in the road where you are unsure as to what design direction to take from here on in.

When you hit a situation like this especially if you have been commiting work regularly you can commit the current work you have like a "checkpoint" in a video game.

If you find the design direction you were unsure about isn't fit for purpose you can "load" the old "save" with

> git reset --hard

If the design however is fit for purpose and maybe needs some optimisation.

> git commit -m "A design that worked for the thing I was working on"

## Git Push As A Remote Disaster Recovery

So you've developed a piece of work that you are really happy with and you push it but it comes back with "merge conflicts"...

Isn't that one frustrating so you try to fix the merge conflict completing it but the branch you now have doesn't work, you only got 5 hours sleep because of the neighbours cat and you did some other things (but NOT git push --force) to your branch and now you are in a total mess and completely paniced and don't know how to proceed...

Relax...

> git reset --hard origin/your_branch --force

## Git Rebase --abort As A Merge Conflict Disaster Recovery

Lets say you started a rebase or merge and you made some mistakes and you're no longer confident that the changes you made by merging your branch with develop work but you are still in the middle of the rebase somewhere.

> git rebase --abort
>
> git merge --abort

This will put your branches back to before you tried to rebase. Give someone a call who can help you and proceed from there.

## Git Pull Is Not Git Pull --rebase

When pulling the latest branch we want to ensure we are doing it in a safe reversable way.

> git config --global pull.rebase true

Ensure this setting is set and never make the mistake with git pull accidently merging the latest over rebasing your branch to the latest ever again.

### Note

There may be additional settings for git frontends that you'll need to check

## Final Thoughts

Quick "disaster recovery" is one of the key strengths of version control and knowing these helpful tips will ensure you can proceed with confidence as a developer.
