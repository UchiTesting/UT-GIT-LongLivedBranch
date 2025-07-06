Feature 1
=========


This is the the first feature document in this demo project.

## Version 1

This is some text to simulate working on a 1st verison of a feature.
So far, we won't worry about team-work. 
This is about a single developer working on a feature.

## Version 2

This is some text about version 2. Nothing too special here.
The point is basically I did not even switch branches, 
I just kept working on the same branch.

## Version 3

This is some text about version 3. Nothing too special here neither.

So far the process is 
- working from *feature-wip* branch.
- then when we believe it it relevant for a PR/MR 
  we create a branch called *feature1-v{n}*
  where `n` is the version of the branche.  
  `git branch feature-v1` for instance.
- then we push that branch  
  `git push -u origin feature-v1`
- and create a PR/MR from it.
- When we merge it, we update the feature dev branch *feature1-dev*
  the command is `git fetch origin feature1-dev:feature1-dev`
- at this point both the *feature1-dev* and the *feature-wip* branches
  are at the same point. However we also created easy to identify branches
  that can be deleted in the MR/PR. The *wip* branch will remain 
  and continue using it until the feature is complete.

In the context of PR/MR 3 we had to make changes to validate it.
We worked from feature1-wip branch.
We now need to update out feature1-v3 branch to include those changes.
There are several ways to get to that result but we prefer any method  
that would avoid checking out the other branch.

`git rebase feature1-wip feature1-v3`

As you can see in the snippet bellow it worked well. On commit *0ffb62c *
we can see the branches names align. However, it did checkout
to feature1-v3 branch. Not ideal but that's not a big deal.

```bash
$ git log --oneline -5
74d0322 (HEAD -> feature1-v3, feature1-wip) Add additional CLI details to v3 description
0ffb62c (origin/feature1-wip, origin/feature1-v3) Add descriptive text about version 3
44bdc63 Create version 3 header
210091a (origin/feature1-dev, feature1-dev) Merge pull request #3 from UchiTesting/feature1-v2
64be63d (feature1-v2) Create version 2 header and small descriptive text.
```

We can use the occasion to push the update before checking back to the *feature1-wip* branch.

> Bonus:
> 
> We likely will delete version branches that got merged.  
> This is done from the PR/MR interface.
> However, if we want to delete the branch from the command line we can use:
> `git remote prune origin` or `git fetch --prune origin`
> The output differs but the result is the same.
>
> ```bash
> $ git remote prune origin
> Pruning origin
> URL: https://github.com/UchiTesting/UT-GIT-LongLivedBranch.git
>  * [pruned] origin/feature1-v1
>  * [pruned] origin/feature1-v2
> ```
>
> ```bash
> $ git fetch --prune origin
> From https://github.com/UchiTesting/UT-GIT-LongLivedBranch
>  - [deleted]         (none)     -> origin/feature1-v3
> ```
>
> This is a good practice to keep the remote repository clean 
> and avoid confusion with old branches that are no longer relevant.
> It helps to keep the repository tidy and makes it easier for team members
> to read the graph. It also tells about how much is a WIP at current time.
>
> After the branches got pruned, it only removes references to remote branches.
> The local branches remain intact.
> To clean it we shall use this one-liner:
>
> `git branch -vv --merged | grep ': gone]' | awk '{print $1}' | xargs git branch -d`
>
> You can dry-run by removing the content from the last pipe (|) i.e. :
> `git branch -vv --merged | grep ': gone]' | awk '{print $1}'`
>
> ```bash
> $ git branch -vv --merged | grep ': gone]' | awk '{print $1}'
> feature1-v1
> feature1-v2
> feature1-v3
> ```
> 
> ```bash
> $ git branch -vv --merged | grep ': gone]' | awk '{print $1}' | xargs git branch -d
> Deleted branch feature1-v1 (was fc02764).
> Deleted branch feature1-v2 (was 64be63d).
> Deleted branch feature1-v3 (was d34627f).
> ```
