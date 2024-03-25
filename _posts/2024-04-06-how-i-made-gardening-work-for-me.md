---
title: How I made gardening work for me
description: Additional ideas to adopt gardening on a day to day basis.
---

<!--more-->

For some time now my colleagues have known me for using "gardening" to describe an essential element of my programming style. So much so that I wrote [a whole post](/2023/09/02/always-be-gardening/) explaining why I think it's an important practice. The executive summary would be this:

> _Making small and continuous improvements over time is one of the most effective ways to keep a codebase in a healthy state._

None of what I wrote was really new, but rather a compilation of ideas well known in the software industry. Almost every programmer with a minimum of experience would agree that concepts like DRY or YAGNI, refactoring or having a good test harness bring mostly benefits.

But it often happens that we only think about them when we are knee-deep in problems, maybe even constrained by an impending deadline. Spending time improving the code in that context will surely delay work. So we are faced with a dilemma: do we continue in the current state or take a step back and risk an agreed delivery?

## Why don't we do the right thing?
To avoid this situation it seems reasonable to conclude that we should apply the aforementioned practices from the very beginning of a project. Otherwise we won't reap the benefits later.

But then I wonder what makes us give them up and at what point it happens. Is it inexperience? Lack of knowledge or tools? Lack of discipline? External pressure from an executive team? An imbalance of power with other roles in a team? The inability to explain why these practices are important for the business and not just for our comfort?

I don't have a definitive answer to these questions. Or at least not one that could explain a majority of cases. Software development is a creative and social activity, in which many of the dynamics in a team arise organically and are specific to that particular group of people. And while research like the one presented in [Accelerate](https://itrevolution.com/book/accelerate/) helps understand some factors, a subsequent [study on the so-called Developer Experience](https://dl.acm.org/doi/10.1145/3639443) (DevEx) pointed out that the reality is usually more complex:

> _[DevEx] is a complex process that happens over time and with processes that are mutually reinforcing. Future work should investigate longitudinal relationships between and among DevEx constructs and their outcomes._

So when a colleague asked me how I make gardening work for me when others apparently seem to struggle, I thought I might share some additional insights.

Note that, as hinted above, I may only find them useful because of my personality, my career path, the influence of colleagues and other factors that have shaped my skills over the years.

In fact, writing these lines has been a difficult exercise because most of the micro-decisions I make are driven by intuition and experience. But there are certain patterns that I have been able to identify.

## Building a habit
First of all, I think the key is not so much the concrete practices of "gardening" but the concept of "always". When I write code it's as if I had a background thread constantly on the lookout for improvements. It doesn't matter if it's a prototype, an actual feature or a unit test.

In fact, I believe I do this with everything I write, not just code: chat messages, emails, documentation,… I often read again and hit the "Edit" button to change a sentence, use a different term or delete a paragraph that doesn't provide relevant information.

So if you want to build the habit of gardening, doing something every day, however small, is probably more important than the impact of any improvement in itself.

## Breaking problems down
Another contributing factor is to trust in the effectiveness of small changes accumulated over time. Simple actions like renaming a variable or splitting a function are relatively contained and cheap to do. More importantly, they are easy to understand and have immediate impact.

Complex changes are trickier because they usually have a larger scope. When there's too much unmanaged technical debt or an overall design that prevents making changes easily, it's tempting to stop planned work and spend time on solving that before continuing. And while there are cases where this is unfortunately the way to go, in my experience it's rarely a good idea, let alone feasible. Such big changes are _not_ gardening.

Instead, we can split them into small steps and execute them incrementally as part of regular work. I know this is not easy. Nobody likes to work on a suboptimal codebase for a long time. But patience is a virtue: with a strategy in place and a bit of discipline, they will bring us closer to the state we want.

## Picking your battles
Even when we aim to routinely improve the code as we work in features, being able to assess the impact of candidate improvements is equally important.

For example, given a feature request and a candidate refactoring, I estimate how much it takes to refactor and how much it takes to develop the feature with and without it. It doesn't need to be particularly accurate, I'm only trying to sense the opportunity cost. Because what I need to decide is if now it's the best moment to [make the change easy](https://twitter.com/kentbeck/status/250733358307500032) or if I should wait and not compromise planned work[^1].

Unfortunately, I cannot give you a general rule of thumb for how to make these assessments. I do them almost always with respect to my previous experience implementing similar changes. That's why I believe it's helpful for junior developers to work closely with someone more experienced, so that they can exchange ideas and understand the nuances of programming.

## Reducing frictions
Something that's also overlooked is how a needlessly complex development life cycle reduces the incentives to make small improvements.

Changing one line of code and seeing it live in production should be as quick and straightforward as possible. So it's completely understandable to feel discouraged when it comprises multiple steps that take hours, if not days.

That's probably one of the reasons why teams relying on pull requests have little or no incentive to keep them small. The associated cost of opening a pull request, writing a meaningful description, waiting for a review and addressing any comments leads naturally to accumulating many changes in one large pull request.

If you work with an issue tracking system, having every single change perfectly described, planned and tracked can be another source of complexity. Sure, some level of coordination and traceability is needed. But taken to an extreme it becomes useless paperwork that barely helps anyone.

So I would recommend to keep an eye on your processes and reduce or eliminate any frictions that discourage you from making small changes. It could be something as simple as mastering a tool to automate routine work.

## Back to the roots
We programmers are generally attracted to the latest shiny new thing. This is good for the most part because it helps us keep a curious mind and be more exposed to innovative ideas.

But on the other hand it can also make us forget the foundational elements that define the practice of programming, which are rarely altered by the latest technology.

So my final piece of advice, perhaps one of the most underrated, is to go back to the roots and rediscover and practice these fundamentals until they become second nature. I believe this will allow you to see the bigger picture and develop a better sense for gardening.

[^1]: This is a good example of being tactical in a [strategy vs. tactics](https://fs.blog/strategy-vs-tactics/) context.