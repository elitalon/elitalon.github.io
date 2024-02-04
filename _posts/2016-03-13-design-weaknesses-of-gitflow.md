---
title: Design weaknesses of GitFlow
description: Weaknesses I have found in GitFlow after four years using it
---
I started using GitFlow more or less two years after [Vincent Driessen](https://twitter.com/nvie) introduced [his proposal](http://nvie.com/posts/a-successful-git-branching-model) in 2010. Since then, there has been many times in which either me or another fellow developer has faced some issues with it.

<!--more-->

The company I was working for in 2012 had recently moved from [Subversion](https://subversion.apache.org) to [Git](https://git-scm.com). We were struggling with defining the best approach for collaborative development, since not everyone was familiar with Git. Experienced Git users often had to help other teammates understand what was going on. With GitFlow, everyone in the team welcomed the idea of having a consistent and well defined way of working with our repositories.

Four years has passed and practically every team I have worked with seems to have embraced GitFlow. But as with any other tool or methodology, one has to carefully examine whether it really fits a project or helps a team work more effectively. My impression is that little thought has been put into choosing GitFlow as a *de facto* model. I'd like to share two weaknesses that I find annoying.

## Redundant branches
My first problem comes with the use of the ["main branches"](https://nvie.com/posts/a-successful-git-branching-model/#the-main-branches):

> _The `master` branch at `origin` should be familiar to every Git user. Parallel to the `master` branch, another branch exists called `develop`._

> _When the source code in the `develop` branch reaches a stable point and is ready to be released, all of the changes should be merged back into `master` somehow and then tagged with a release number._

I always wondered if nobody noticed that the `master` branch is completely useless in this model. If every release must be tagged, why do we need the separation between `master` and `develop` at all? Can't we just live with a single _main_ branch and go back to any release using its tag?

Not even the need for `hotfix` branches seems to justify this redundancy. It's perfectly possible to create a branch from a tag, apply a patch for the existing bug in production and merge back to the main branch.

## A polluted commit history
The second problem is a consequence of using [feature branches](https://nvie.com/posts/a-successful-git-branching-model/#feature-branches):

> _The ``--no-ff`` flag causes the merge to always create a new commit object, even if the merge could be performed with a fast-forward. This avoids losing information about the historical existence of a feature branch and groups together all commits that together added the feature._

> _Reverting a whole feature (i.e. a group of commits), is a true headache […], whereas it is easily done if the `--no-ff` flag was used._

By avoiding [fast-forward merges](http://git-scm.com/docs/git-merge#_fast_forward_merge) the commit history of the repository is polluted with merge commits. This situation gets worse when you realise that prominent version control cloud services, like [GitHub](https://help.github.com/articles/merging-a-pull-request/) or [Bitbucket](https://bitbucket.org/site/master/issues/6106/forced-non-fast-forward-merge-of-pull), merge pull requests using that flag. But to be honest, I haven't found a situation yet where those commits have been proven useful. Let me address these apparent benefits.

### Keeping historical reference
There are other ways of keeping historical reference of _when_ a feature was merged.

For example, if your teams uses an issue-tracking system you can include the issue ID in commit messages. Or more generally, you can take the time to write [better commit messages](http://chris.beams.io/posts/git-commit/). Another option is to maintain a [CHANGELOG](https://keepachangelog.com/en/1.0.0/), something I strongly recommend because it can also be useful for other stakeholders, not just the development team.

I'd argue that the fact that a feature branch was merged at some point in time says little about the actual lifetime of a feature.

### Reverting a feature
The existence of merge commits are in theory useful to revert a feature easily. But in my experience this scenario is not very likely.

When you work in a team, you typically (ideally?) have more than one developer working together on the same feature. Moreover, sufficiently large teams usually work on more than one feature in parallel. Thus, multiple feature branches coexist and get merged, with everyone integrating each other's work into their branches.

Go through this process a few times, look at the commit history and you will realise that, predictably, there is no easy way of reverting a whole feature from these merge commits alone.

This is because software development is inherently an organic process. A scenario where a feature starts and gets merged without being affected by changes in other branches is rare. When that happens, it's probably because changes were so small that making subsequent ones is more effective than reverting the original set of commits. And this reflects the true nature of incremental software development: make a change, inspect the result and adapt the solution from what you learned.

In general, if you really want to be able to revert a feature, you design and implement it in a way that [the software itself allows you to do it](http://martinfowler.com/articles/feature-toggles.html), instead of messing with the commit history.

## What are the alternatives?
Git is a difficult tool to master. Making mistakes is easy and it takes a while to adopt good practices and learn how to avoid or solve [some pitfalls](http://stackoverflow.com/q/9264314/592454). It's understandable why people have embraced a complex workflow with limiting but well-defined rules.

It's also difficult to change established processes in a team when every member is familiar with them. Conventions are powerful. And the fact that major version control cloud services don't offer a way to do fast-forward merges doesn't help either.

But I'm not the first one that have seen issues like the ones I described above. [Scott Chacon](https://twitter.com/chacon) proposed in 2011 [the GitHub flow](https://scottchacon.com/2011/08/31/github-flow/) as a simpler alternative. If you are willing to escape from GitFlow, I would start there.
