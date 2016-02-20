---
layout: post
title: The real value of fastlane
published: true
---
When [fastlane](https://fastlane.tools) started to get attention by the community, I was not particularly excited about it. I thought it was certainly a cool project, but it was not solving any real problem.

<!--more-->

We already had [nomad](https://github.com/nomad), a set of command line utilities by [@mattt](https://twitter.com/mattt). And with the aid of [xctool](https://github.com/facebook/xctool), `xcrun` and the improved `xcodebuild`, I did not see the need of yet another tool to handle a workflow that any seasoned iOS developer should be able to manage. However, I started recently a relatively big project and decided to give fastlane a go.


## Cleaning a Makefile
I usually put a [Makefile](https://www.gnu.org/software/make/manual/make.html#Introduction) in my iOS projects with *targets* to perform different tasks. Each target contains one or more *recipes* in order to complete it. For example, a `deploy` target runs the tests and creates an [IPA](https://en.wikipedia.org/wiki/.ipa_(file_extension)). When setting up a CI service, those targets can be easily triggered by invoking `make deploy`.

We started replacing the recipes with the tools provided by fastlane. I often use [xcpretty](https://github.com/supermarin/xcpretty) to filter the output too, so we were able to clean up the initial Makefile a lot. But still, it felt like we were simply replacing one set of tools with another.


## Adding more requirements
Later on we had to customise some of the phases of our CI service, and also adding new ones. The changes needed were complex and adding more stuff to the Makefile made it grow out of control. Both the number of recipes per target and the variables to avoid repeating program arguments increased significantly.

Depending on the specific deployment pipeline, we needed to switch branches, go back to a previous release, notify the team on Slack, temporarily increment the bundle version, deploy to an external service,…

So we dug into fastlane's documentation and found a potential solution to our painful Makefile: the [actions](https://github.com/fastlane/fastlane/blob/master/docs/Actions.md). Besides the actions for the fastlane tools, there is more than a hundred additional actions that cover almost every single requirement we had. We started then to clean up the Makefile again and moved most of the targets into dedicated lanes in the [Fastfile](https://github.com/fastlane/fastlane/tree/master/docs), reducing the code needed to accomplish every deployment pipeline.

I suddenly realised that my initial thought about fastlane was due to an oversimplification. I still think that some of the tools (e.g. [gym](https://github.com/fastlane/gym), [scan](https://github.com/fastlane/scan)) do not present any real advantage over mastering `xcodebuild`. And some others are just a nice-to-have (e.g. [snapshot](https://github.com/fastlane/snapshot), [match](https://github.com/fastlane/match) or [pem](https://github.com/fastlane/pem)). But I also think that the ability to combine these tools with the rest of default actions is what makes fastlane stand out of the rest of the previous solutions.


## Conclusion
For beginners, fastlane's tools provides an easy way of automating different development tasks (building, testing, creating IPAs,…). Setting up a continuous integration and deployment service becomes then more manageable, although you should know what is happening behind the scenes.

However, for me the real value of fastlane lies in the ecosystem surrounding it. By offering a way to integrate additional [actions](https://github.com/fastlane/fastlane/blob/master/docs/Actions.md), fastlane has rather become a framework that allows developers to implement really complex pipelines beyond the scope of the default tools.
