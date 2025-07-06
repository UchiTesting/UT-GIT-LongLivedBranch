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
- then we push that branch
- and create a PR/MR from it.
- When we merge it, we update the feature dev branch *feature1-dev*
  the command is `git fetch origin feature1-dev:feature1-dev`
- at this point both the *feature1-dev* and the *feature-wip* branches
  are at the same point. However we also created easy to identify branches
  that can be deleted in the MR/PR. The *wip* branch will remain 
  and continue using it until the feature is complete.
