---
title: Troubleshooting how Universal Links are registered
description: Finding out the hard way why under some circumstances Universal Links might not be registered with iOS immediately after installing an app.
---

<!--more-->

I recently faced a problem related to [Universal Links](https://developer.apple.com/ios/universal-links/) in a mobile app I was working on. Our team had configured [deep linking](https://en.wikipedia.org/wiki/Deep_linking) for a new feature that would allow third-party apps to return to our app after users had completed a task on them.

## Brief overview of Universal Links
Without going into much detail, Universal Links (and their Android counterpart, [App Links](https://developer.android.com/training/app-links)) are a mechanism that enables advanced deep linking in mobile apps. The advanced behaviour comes from the fact that the OS can take an alternative action if the target application cannot be reached.

For example, if you tap a link from a mobile phone and the target app is not installed, the OS can take users to an app store so that they can install the app. Or it can open a web browser for users to use the equivalent web application.

The registration process is conceptually simple: when an app is installed, the OS goes to a designated website where the specification for the links is stored. The specification is then processed, and the links for the app are enabled accordingly[^1].

## The problem
But after releasing an app version containing this new feature we had developed, we noticed that some users were not being brought back to our app from third-party ones. Instead, they were being redirected to the App Store.

Our first reaction was to verify that all components were correctly configured. Maybe we had missed an edge case in which some third-party apps would open the link in some weird way. After looking at it carefully, everything seemed fine.

Then we went through a [technical note](https://developer.apple.com/documentation/technotes/tn3155-debugging-universal-links) published by Apple with guidelines for debugging the behaviour of Universal Links. This allowed us to further confirm that the problem was definitely not in the configuration. There were, however, two sections that pointed us in the right direction.

The first one was understanding [Apple's CDN role](https://developer.apple.com/documentation/technotes/tn3155-debugging-universal-links#Understand-Apples-CDN) in enabling Universal Links. We used that to ask friendly users to reinstall the app, in hope that it would trigger the registration mechanism again and thus narrow down the root cause.

The other one was learning through the [use of `swcutil` and `sysdiagnose`](https://developer.apple.com/documentation/technotes/tn3155-debugging-universal-links#Debug-through-sysdiagnose) that the registration phase of Universal Links is seemingly controlled by the `swcd` daemon. We tried with several tests devices until we found one where we could reproduce the problem. The logs showed a potential explanation: for some reason, the registration phase was either not being triggered right after installing the app or taking a while to complete.

Equipped with this knowledge, we opened a technical support request with Apple to understand if our hunch was right and see if they could provide a workaround.

In our conversation with them, we also discovered that using a deprecated format in the `apple-app-site-association` specification might have been playing a role too. In theory, this format should still be supported because it's [used by iOS 12](https://github.com/firebase/firebase-ios-sdk/issues/4914#issuecomment-592656035). But if an app doesn't support iOS 12 any more, it's apparently best if it adopts [the new format](https://developer.apple.com/documentation/bundleresources/applinks/details/components?changes=latest_major).

## Lessons learned
All in all, what's clear to us now is that solely relying on Universal Links might not be enough to guarantee a correct behaviour for a feature.

If a Universal Link is only meant to open an app without any subsequent side effect, being redirected to the App Store is clearly a suboptimal user experience, but still somewhat acceptable.

But the feature we had developed depended on deep linking to allow users to complete a multistep workflow. So we had to go back to the drawing board and design an alternative solution in which opening the link only served to further improve the user experience, but wasn't a critical step any more.

[^1]: The process is described more in detail in [Supporting associated domains](https://developer.apple.com/documentation/xcode/supporting-associated-domains)
