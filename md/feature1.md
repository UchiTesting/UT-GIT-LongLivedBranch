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

As you can see in the snippet bellow it worked well. On commit *0ffb62c *
we can see the branches names align. However, it did checkout
to feature1-v3 branch. Not ideal but that's not a big deal.

```bash
$ git log --oneline -3
0ffb62c (HEAD -> feature1-v3, origin/feature1-wip, origin/feature1-v3, feature1-wip) Add descriptive text about version 3
44bdc63 Create version 3 header
210091a (origin/feature1-dev, feature1-dev) Merge pull request #3 from UchiTesting/feature1-v2

```

We can use the occasion to push the update befor checking back to the *feature1-wip* branch.