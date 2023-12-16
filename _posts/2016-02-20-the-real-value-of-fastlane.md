---
title: The real value of fastlane
description: Fastlane really shines when composing actions for more complex deployment pipelines
---
I was not particularly excited when [fastlane](https://fastlane.tools) started to get attention from the community. I agreed it was a cool project, but it was not solving any actual problem I had.

<!--more-->

We already had [nomad](https://github.com/nomad), [xctool](https://github.com/facebook/xctool), `xcrun` and an improved `xcodebuild`. I just didn't see the need of another tool to deal with workflows that any seasoned iOS developer should be familiar with.

But I got involved recently in a relatively big project and decided to try fastlane.

## Simplifying Makefiles
I usually include a [Makefile](https://www.gnu.org/software/make/manual/make.html#Introduction) with the iOS projects I work on, where [_rules_](https://www.gnu.org/software/make/manual/html_node/Rule-Introduction.html) act as shortcuts to perform different workflows. A _target_ in a rule is the entry point for performing one or more _recipes_ that eventually completes a given workflow.

For example, a `deploy` target would have three recipes: running all tests, creating an [IPA](https://en.wikipedia.org/wiki/.ipa_(file_extension)) and sending artefacts somewhere via `scp`, `sftp` or a similar tool.

My first step in adopting fastlane was to use its [tools](https://github.com/fastlane/fastlane/blob/7aeb29aea2eb437f8c6bd79f9c657528f160a3d0/README.md#fastlane-toolchain) to replace some of the recipes. Like fastlane, I often use [xcpretty](https://github.com/supermarin/xcpretty) to make `xcodebuild`'s output more developer-friendly, so it was something we could get rid of too.

All in all we were able to simplify the initial Makefile a bit, but it still felt like we were only replacing one set of tools with another. With the downside that this new set of tools was a third party dependency we didn't control.

## Dealing with complex workflows
Shortly afterwards we had to add new configurations and workflows for the pipelines in the [CI service](https://en.wikipedia.org/wiki/Continuous_integration).

The changes needed were complex. Depending on the pipeline we had to switch branches, check out previous releases, notify the team on Slack, increment bundle versions, submit builds to external services, etc. As a result, adapting the Makefile made it grow out of control.

We turned to fastlane's documentation, hoping to find an alternative solution. And we indeed found that, besides the default toolchain, fastlane also offered [actions](https://github.com/fastlane/fastlane/blob/master/docs/Actions.md): additional utilities that covered practically every single requirement we had. So we kept refactoring the Makefile, transforming most of the original rules into lanes in a [Fastfile](https://github.com/fastlane/fastlane/blob/7aeb29aea2eb437f8c6bd79f9c657528f160a3d0/docs/README.md#fastfile) that reduced the amount of code required for each workflow.

## The real value of fastlane
At that point I had to admit that my initial thought about fastlane was an oversimplification.

I still think that using some of the tools in isolation, like [gym](https://github.com/fastlane/gym) or [scan](https://github.com/fastlane/scan), do not present a significant advantage over mastering `xcodebuild`. And others like [snapshot](https://github.com/fastlane/snapshot) are simply nice-to-have. But the ability to combine these tools and actions together in complex workflows is what makes fastlane really shine (as if it had been inspired by the [Unix philosophy](https://en.wikipedia.org/wiki/Unix_philosophy)).

On top of that, a whole ecosystem around fastlane is growing because it also offers a way to integrate external actions. This makes it a kind of framework that allows developers add their own functionality when something is missing from the built-in toolchain.

The only downside I still see is that now iOS projects have yet another dependency with a third party tool, which is always a risk. I'll keep a copy of my good old Makefile, just in case.
