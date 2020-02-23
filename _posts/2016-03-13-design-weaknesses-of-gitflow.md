---
title: Design weaknesses of GitFlow
description: Some thoughts about the weaknesses of GitFlow after four years using it
---
I started using GitFlow more or less two years after [Vincent Driessen](https://twitter.com/nvie) introduced [his proposal](http://nvie.com/posts/a-successful-git-branching-model/) in 2010. Since then, there has been several occasions when either me or one of my fellow developers have faced some issues with it.

<!--more-->

The company I was working for had recently moved from Subversion to Git. We were struggling with defining the best approach for collaborative development, since not everyone was familiar with Git. More often than not, experienced Git users had to help other teammates to understand what was going on. With GitFlow everyone in the team welcomed the idea of having a consistent way of working with our repositories.

Four years has passed and every company I have worked with seems to have embraced GitFlow as the default approach. But as with any other tool or methodology, one has to carefully _examine whether it fits the purpose of a project or the way a team works_. I have the impression that little thought has been put into choosing GitFlow as *de facto* model. I'd like to share with you what I consider two of its weaknesses.


## Redundant branches
> *The `master` branch at origin should be familiar to every Git user. Parallel to the `master` branch, another branch exists called `develop`.*

> *When the source code in the `develop` branch reaches a stable point and is ready to be released, all of the changes should be merged back into `master` somehow and then tagged with a release number.*

I always wondered if nobody noticed that the `master` branch is completely useless in this model. If every release must be tagged, why do we need the separation between `master` and `develop` at all? Can't we just live with a single *main* branch and go back to any release using its tag?

Not even the need for `hotfix` branches seems to justify this redundancy. It's perfectly possible to create a branch from a tag, apply the patch for the existing bug in production and merge back to the main branch.


## A polluted commit history
> *The --no-ff flag causes the merge to always create a new commit object, even if the merge could be performed with a fast-forward. This avoids losing information about the historical existence of a feature branch and groups together all commits that together added the feature.*

> *Reverting a whole feature (i.e. a group of commits), is a true headache (...) whereas it is easily done if the --no-ff flag was used.*

By avoiding [fast-forward merges](http://git-scm.com/docs/git-merge#_fast_forward_merge) the commit history of the repository is polluted with merge commits. This situation is even worse when you realise that both [GitHub](https://help.github.com/articles/merging-a-pull-request/) and [Bitbucket](https://bitbucket.org/site/master/issues/6106/forced-non-fast-forward-merge-of-pull) merge pull requests using that flag. But to be honest, I haven't found a situation yet where those commits have been proven useful. Let me address these apparent benefits.


### Historical reference
There are other ways of keeping historical reference of _when_ a feature was merged. If you have an issue-tracking system, you can prefix commit messages with the related feature ID. You can also provide [better commit messages](http://chris.beams.io/posts/git-commit/) or maintain a [CHANGELOG](https://keepachangelog.com/en/1.0.0/), something I definitely recommend.

In any case, the fact that some branch was merged at some point in time does not tell me anything about the lifetime of a feature.


### Reverting a feature
The existence of merge commits are in theory useful to revert a feature. This is a highly unlikely scenario when you work in a team, where

- Several developers work together in one or more features
- One or more features are developed concurrently

As a result, multiple branches coexist. They are created and merged so that everyone in the team can benefit from everyone's work. Go through that a few times and there is no easy way of reverting a whole feature anymore.

This is because *software development is inherently an organic process*. An scenario where a feature starts and gets merged later without being affected by changes in other branches is rare to happen. And when it does it's probably because the change was so small that making a subsequent change on top has roughly the same cost as reverting a previous one. That would actually reflect the reality of the project more accuralety: we introduced a change and for some reason we adjusted it later.

If you really want to revert a feature, you [design it in a way that you can do that with the software itself](http://martinfowler.com/articles/feature-toggles.html), not by messing with the commit history.


## Ready to try something else?
Git is a difficult tool to master and users can do whatever they want with it. Making mistakes is easy and it takes a while to develop good practices and learn how to avoid or solve [some pitfalls](http://stackoverflow.com/q/9264314/592454). So it's easy to understand why people have embraced a complex workflow of limiting but well-defined rules.

It's also difficult to change things when almost every developer is familiar with it. Conventions are powerful. And the fact that major repository hosting services don't offer a way to fast-forward merges doesn't help either.

I'm certainly not the first one that saw all the issues stated above. [Scott Chacon](https://twitter.com/chacon) himself [wrote about it](http://scottchacon.com/2011/08/31/github-flow.html) in 2011 and proposed the GitHub approach as a simpler alternative. If you are willing to escape from GitFlow, I would start there.
