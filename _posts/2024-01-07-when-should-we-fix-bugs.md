---
title: When should we fix bugs?
description: More often than we think, the best moment to fix a bug is now.
---

<!--more-->

I worked once in a team that struggled to fix bugs in the mobile apps we were developing. Unless defects were blatantly obvious and had a serious impact for users, for example if they prevented signing up, so-called product work was always prioritised over fixing them.

The most immediate consequence, from an organisational perspective, was that the list of bugs kept growing as users and stakeholders continued filing them. This had an impact on the morale of the team because we thought we would never be able to catch up.

I also had the impression that a sense of disinterest on the part of some employees and stakeholders had set in. As if they were thinking "if they're not going to be fixed, why bother reporting them?". That's completely understandable, but it meant that there might be bugs we didn't know about.

But what was probably worse is that deferring working on these issues would eventually damage the brand and bring the satisfaction of users down. This effect, described more in detail in [Death by a Thousand Papercuts](https://engineering.instawork.com/death-by-a-thousand-papercuts-and-how-to-avoid-it-d2f05070b339), is actually difficult to detect and measure because it only develops over time and it's not easy to attribute to a single cause.

## Enter the defect policy matrix
Faced with this problem, I proposed the team two changes in our processes to try and improve the situation.

The first one was committing to work on at least two bugs on every iteration[^1]. The idea was not so much that we would decrease the list of bugs, but rather to get everyone used to a steady rhythm of fixing defects.

The second was using a [defect policy matrix](https://www.mountaingoatsoftware.com/blog/defect-management-by-policy-a-fast-easy-approach-to-prioritizing-bug-fixes) to triage bugs as they were coming into our backlog. We would assign a severity level to each bug based on the number of occurrences and the number of users affected. Then we would prioritise bugs according to their severity, addressing the ones with the highest value first.

This approach worked pretty well for a while. We were able to fix many bugs and reduce the backlog significantly. And more importantly, everyone was confident now that we were actively working on them. If we were not doing more was due to either capacity constraints or competing priorities, i.e. keeping a balance on every iteration between addressing bugs and product features.

However, many "paper cuts" remained there because those with a higher severity assessment were routinely planned to be worked on first. The most important problems got fixed sooner, which was good, but small nuisances kept bothering users.

## Dealing with papercuts
Some time later, inspired by [Death by a Thousand Papercuts](https://engineering.instawork.com/death-by-a-thousand-papercuts-and-how-to-avoid-it-d2f05070b339), our Product Owner proposed scheduling some fixed time on a regular basis to work only on paper cuts. Something like one day every two months or so.

This was the perfect complement because now we had an opportunity to trim the backlog "from the bottom". We even found ourselves prioritising paper cuts by our own perceived level of annoyance. At the end of the day we were also users of our apps, so we more or less knew.

But even with all these improvements, some bugs still lived in a kind of limbo. They were not planned in our regular iterations because of their low severity assessment. And they almost never made it into our "paper cuts sessions" either because they were not annoying enough. Moreover, they had been reported so long ago that fixing them often took longer than usual, just because we needed to remember the context in which they occurred.

## The best moment to fix a bug might be now
One day I was doing exploratory testing in our apps to verify the behaviour of a component. I noticed three subtle bugs related to it in different parts of the system, but as I was filing them I quickly realised they were not going to be fixed any time soon.

Then I had a thought. I knew the context, I knew how to reproduce the issues and I also had a relatively good idea of where the problem was in the code. What if I took the time to address them now? So I [made a bet](/2023/09/02/always-be-gardening/#making-a-bet), started working on them immediately and, lo and behold, I had them fixed in approximately three hours.

That reminded me of an [article from Allen Holub](https://holub.com/bugs/) in which he suggested a kinda provocative idea: when you discover a bug, either fix it as soon as possible or don't add it to the backlog. The main reason is to avoid waste and focus on quality. It often happens that when you discover a bug is when you have the best context and knowledge; the more you delay working on it, the more you need to spend later fixing it. So you keep the list of bugs small by preventing them enter the system in the first place.

I think that this approach works pretty well when bugs are discovered soon after a change is made to the system. My recent experience, when I was able to fix three bugs in a short time because I had the knowledge fresh in my head, had just shown it.

For features that have been developed a long time ago, I would argue that bugs still deserve going through some sort of prioritisation and living in the backlog for a while to give them a chance.

But if I had to choose one of the two approaches, all these years working on different teams and products have led me to believe that fixing bugs the moment we discover them is probably more effective. We might have to pay the price of slightly delaying work that had already been planned. But on the upside it will help keep the product in a consistently good quality, if not improved, over time.

[^1]: We were working within a Scrum setup, with two-week sprints. But a similar approach would have worked with any other methodology.