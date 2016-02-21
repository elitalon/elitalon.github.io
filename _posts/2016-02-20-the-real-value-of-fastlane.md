---
layout: post
title: The real value of fastlane
published: true
---
When [fastlane](https://fastlane.tools) started to get attention by the community, I was not particularly excited about it. I thought it was certainly a cool project, but it was not solving any real problem.

<!--more-->

We already had [nomad](https://github.com/nomad), a set of command line utilities by [@mattt](https://twitter.com/mattt). And with the aid of [xctool](https://github.com/facebook/xctool), `xcrun` and the improved `xcodebuild`, I did not see the need of yet another tool to handle a workflow that any seasoned iOS developer should be able to manage. But I recently got involved in a relatively big project and decided to give fastlane a go.


## Cleaning a Makefile
I usually include a [Makefile](https://www.gnu.org/software/make/manual/make.html#Introduction) with my iOS projects, where the *targets* are simply shortcuts to perform different tasks. Each target contains one or more *recipes* in order to complete it. For example, a *"deploy"* target may run the tests, create an [IPA](https://en.wikipedia.org/wiki/.ipa_(file_extension)) and send it somewhere via `curl`. When setting up a CI service, those targets can be easily triggered with `make deploy`.

I started replacing the recipes with the [iOS toolchain](https://github.com/fastlane/fastlane/blob/7aeb29aea2eb437f8c6bd79f9c657528f160a3d0/README.md#fastlane-toolchain) provided by fastlane. I often use [xcpretty](https://github.com/supermarin/xcpretty) to filter the output too, so I was able to clean up the initial Makefile a little bit. But still, it felt like I was simply replacing one set of tools with another.


## Dealing with complex pipelines
Later on I had to customise some of the configurations of the CI service, and also adding new ones. The changes needed were complex and adding more stuff to the Makefile made it grow out of control. Both the number of recipes per target and the variables to reuse program arguments increased significantly.

Depending on the specific deployment pipeline I needed to switch branches, go back to a previous release, notify the team on Slack, temporarily increment the bundle version, submit the builds to external services,…

So I dug into fastlane's documentation and found a potential solution: the [actions](https://github.com/fastlane/fastlane/blob/master/docs/Actions.md). Besides the default toolchain, fastlane also offers more than a hundred additional actions that cover almost every single requirement I had. I started then cleaning up the Makefile again and moved most of the targets into dedicated lanes in the [Fastfile](https://github.com/fastlane/fastlane/tree/master/docs), thus reducing the code needed to accomplish every deployment pipeline.

I suddenly realised that my initial thought about fastlane was due to an oversimplification. I still think that some of the tools (e.g. [gym](https://github.com/fastlane/gym), [scan](https://github.com/fastlane/scan)) do not present any real advantage over mastering `xcodebuild`. And some others are just a nice-to-have (e.g. [snapshot](https://github.com/fastlane/snapshot), [match](https://github.com/fastlane/match) or [pem](https://github.com/fastlane/pem)). But I also think that the ability to combine these tools with the rest of default actions is what makes fastlane really stand out of other alternatives.

The only downside is that now the project has (another) dependency with a third-party tool, which is something I do not like. I will keep a copy of my good old Makefile, just in case.

## What fastlane really means
For beginners, fastlane's toolchain provides an easy way of automating different development tasks (building, testing, creating IPAs,…). Setting up a continuous integration and deployment service becomes then more manageable, although every iOS developer should know what is happening behind the scenes.

However, for me the real value of fastlane lies in the ecosystem surrounding it. By offering a way to integrate additional actions, fastlane has rather become a framework that allows developers to implement really complex pipelines beyond the scope of the default tools.
