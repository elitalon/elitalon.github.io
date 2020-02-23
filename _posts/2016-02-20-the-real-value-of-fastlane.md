---
title: The real value of fastlane
description: Discovering where fastlane really shines when going beyond the default tools for more complex deployment pipelines
---
When [fastlane](https://fastlane.tools) started to get attention from the community, I was not particularly excited about it. I thought it was certainly a cool project, but it was not solving any real problem.

<!--more-->

We already had [nomad](https://github.com/nomad) and [xctool](https://github.com/facebook/xctool), plus `xcrun` and the improved `xcodebuild`. I just didn't see the need of another tool to deal with workflows that any seasoned iOS developer should be able to manage. However, I got involved recently in a relatively big project and decided to give fastlane a go.


## Cleaning a Makefile
I usually include a [Makefile](https://www.gnu.org/software/make/manual/make.html#Introduction) with my iOS projects, where the *targets* are simply shortcuts to perform different tasks. Each target contains one or more *recipes* in order to complete a given task. For example, a *"deploy"* target may run the tests, create an [IPA](https://en.wikipedia.org/wiki/.ipa_(file_extension)) and send it somewhere via `curl`. Those targets can be easily triggered in a CI service.

So I started replacing the recipes with the [iOS toolchain](https://github.com/fastlane/fastlane/blob/7aeb29aea2eb437f8c6bd79f9c657528f160a3d0/README.md#fastlane-toolchain) that fastlane provides. I often use [xcpretty](https://github.com/supermarin/xcpretty) to filter the output too, so I was able to clean up the initial Makefile a little bit. But still, it felt like I was simply replacing one set of tools with another.


## Dealing with complex pipelines
Later on I had to customise some of the build configurations of the CI service and add new ones. The changes needed were complex and adding more stuff to the Makefile made it grow out of control. Both the number of recipes per target and the variables to reuse program arguments increased significantly.

Depending on the specific pipeline I needed to switch branches, go back to a previous release, notify the team on Slack, temporarily increment the bundle version, submit the builds to external services,…

So I dug into fastlane's documentation and found a potential solution: the [actions](https://github.com/fastlane/fastlane/blob/master/docs/Actions.md). Besides the default toolchain, fastlane also offers more than a hundred additional actions that covered almost every single requirement I had. I kept cleaning up the Makefile and moved most of the original targets into dedicated lanes in the [Fastfile](https://github.com/fastlane/fastlane/tree/master/docs), thus reducing the code needed to execute them.

I suddenly realised that my initial thought about fastlane was due to an oversimplification. I still think that some of the tools (e.g. [gym](https://github.com/fastlane/gym) or [scan](https://github.com/fastlane/scan)) do not present any real advantage over mastering `xcodebuild`, while some others are just a nice-to-have (e.g. [snapshot](https://github.com/fastlane/snapshot), [match](https://github.com/fastlane/match) or [pem](https://github.com/fastlane/pem)). But the ability to combine these tools with the rest of default actions is what makes fastlane really stand out of other alternatives.


## What fastlane really means
For beginners, fastlane's toolchain provides an easy way of automating different development tasks (building, testing, creating IPAs,…). Setting up a continuous integration and deployment service becomes then more manageable, although every iOS developer should know what is happening behind the scenes.

However, for me the real value of fastlane lies in the ecosystem surrounding it. By offering a way to integrate additional actions, fastlane has rather become a framework that allows developers to implement really complex pipelines beyond the scope of the default tools.

The only downside is that now iOS projects have (another) dependency with a third-party tool, which is something I do not like. I'll keep a copy of my good old Makefile, just in case.
