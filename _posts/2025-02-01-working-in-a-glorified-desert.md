---
title: We work in glorified deserts
description: \"The Forest and the Desert\" metaphor led me to think about my current frustration with the software industry.
---

<!--more-->

Martin Fowler writes this in [his summary](https://martinfowler.com/bliki/ForestAndDesert.html) of Beth Anders-Beck and Kent Beck's metaphor of [The Forest and The Desert](https://tidyfirst.substack.com/p/forest-and-desert)[^1]:

> _It is possible to change Desert into Forest, but it's difficult - often requiring people to do things that are both hard and counter-intuitive. (It seems sadly easier for The Forest to submit to desertification.)_

I've told my wife lately that part of my frustration with the current state of the software industry comes from a similar observation.

Software engineers want to work on a healthy codebase, with a clean architecture that's easy to change, has a good test coverage and a low number of bugs. Most of us would also agree that [agile development](https://agilemanifesto.org/principles.html) is the ideal way to work, collaborating closer with stakeholders, delivering change in incremental steps, listening to users and avoiding rework. All driven by technical excellence.

But when I reflect on my last 15 years in the IT industry, I can't help but think that in reality we are essentially doing things in the same way.

Yes, we have made a few improvements. We have increased the frequency of deliveries, put more emphasis on automated testing and shortened the feedback loop with colleagues and stakeholders a little.

And yet, I must admit that there hasn't been any profound change. We keep tweaking the same processes that we often complain about, or switching from one methodology to another and reshuffling teams and organisations. But almost always within the same paradigm.

Going back to Martin Fowler's quote above, I believe this happens because we seem to prefer ineffective ways of working, which are suboptimal but are also familiar and somewhat comfortable, over more effective ones that take significant time and effort to achieve.

For example, implementing [Continuous Integration](https://martinfowler.com/articles/continuousIntegration.html) (CI) requires that changes made by developers to their local copies of a codebase must be integrated with the main codebase _at least once a day_. This means rethinking many practices in a team, from how you slice and plan tasks to the use of [pull requests](https://en.wikipedia.org/wiki/Distributed_version_control#Pull_requests). You might even need to reconsider your hiring strategy and look for a different set of skills.

That's difficult to do, it seems counter-intuitive and takes time. Instead, we configure a CI server that runs some automated tests when a change arrives to the main codebase. Meanwhile, developers continue doing the same: picking a task from the backlog, working on it more or less in isolation[^2] and asking for a review some days later. And thus, we end up with the illusion of improvement.

Interestingly, this seems to happen in other industries too. My wife has worked in the education and retail sectors, and now in the public administration. The first time I shared my thoughts on this, she said she had observed a similar behaviour in pretty much all of her jobs too.

So maybe all of this is just a human trait and all I need to do is adjust my expectations of the software industry.

[^1]: They [introduced](https://www.youtube.com/watch?v=nt6m8qtRbz0) this metaphor at the Øredev conference.
[^2]: It's called "having focus" these days, because we are doing very important work all the time.
