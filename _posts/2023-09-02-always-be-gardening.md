---
title: Always be gardening
description: Edited repost of "Always be gardening", an article I wrote in FAIRTIQ's blog.
---
For posterity's sake I'm reposting a slightly edited version of [an article](https://fairtiq.com/en/tech/always-be-gardening) I published on FAIRTIQ's [Tech Blog](https://fairtiq.com/en/tech) in May 2023.

<!--more-->
---

As a software engineer I've always been interested in learning effective development techniques. But it was only recently that I started describing my experience as having an "always be gardening" mindset.

## What is gardening?
The [Oxford Dictionary of English](https://www.oed.com/) defines gardening as:

> _The activity of tending and cultivating a garden, especially as a pastime._

The use of "tending" and "pastime" is particularly interesting in that definition. It somehow implies that looking after a garden not only requires dedicated attention, but it's also something one does regularly, rather than occasionally.

Bringing that to the context of software development, "always be gardening" is simply an expression I use to refer to the practice of slowly and continuously improving the code we work on[^1].

It's something that we do slowly, in small steps, because it's a never ending activity. We remove weeds today, cut some branches tomorrow and almost without noticing it the garden keeps improving.

It's also a continuous activity because it has little value if we remove weeds one day and then do nothing for the next three months. When we go check again, weeds will probably be back in the garden, maybe together with other unexpected guests.

The central idea is that making small and continuous improvements over time is one of the most effective ways to keep a codebase in a healthy state.

## Why is gardening important?
Gardening is important because software is meant to be changed. And if software is meant to be changed, code complexity, in any of its forms, is our number one enemy.

I think we can all agree that the complexity of a piece of code is inversely correlated with the ease of changing it to meet the desired functionality and quality. The more complex and messy the code, the less capable we are to handle it with ease.

To make things worse, complexity has a rippling effect. Dealing with complex code is something developers don't like. But the impact spreads beyond the context of programming and affects the business as well:

1. It hinders the ability to adapt to changing requirements – complex code is more difficult to change
2. It increases the cost of producing code – code is an asset but also an expense[^2]
3. It increases the vulnerability of the system – complex code is more difficult to protect, partially because it requires a higher cognitive load to understand all its ramifications
4. It damages the brand – complex code is more prone to have bugs and more difficult to optimise

The irony here is that complexity is inevitable.

We cannot get rid of essential complexity, which is intrinsic to the problem domain and has nothing to do with the quality of the code. If we are solving a complex problem there will be some complexity that we cannot avoid. Sometimes things are hard because they are hard.

But there's also accidental complexity, which results from the choices we make in our solutions: the programming language, the architecture, unmanaged technical debt, the lack of a test harness, the naming of types and functions, etc.

Our goal shouldn’t be to eliminate complexity entirely. I don’t think that's realistic. But we should aim to reduce it to the bare minimum, so that we can manage the code with comfort and confidence.

## OK, but is it _really_ that important?
If you need another reason why gardening is important, let me tell you my experience at FAIRTIQ as an iOS developer.

Historically we've had more Android than iOS developers in the company. This is common in many teams, because external factors specific to Android as a platform (e.g. the variety of vendors) sometimes require having more capacity. But after restructuring the Tech Team in 2019, I ended up in a squad where that imbalance was higher.

At that moment, while we waited for new hires to fill the gap, my reasoning went like this:

- If iOS has to keep up with Android, despite having less capacity, I need to work smarter, not harder
- If I can keep the code easy to understand and change, I don't have to fight it to implement whatever is required
- If I have a good test harness, I can make progress with confidence because tests will tell if I break something
- With everything combined, I can develop faster, avoid rework and increase my effectiveness

So gardening for me has also become a survival mechanism in situations like this. And as a result, our iOS apps have benefitted from:

1. Feature parity with Android, without sacrificing quality, until the previous balance in capacity was restored
2. A number of bugs consistently kept below 10 over time, if not less
3. Only four outages in four years strictly caused by defects in the apps
4. Being able to carefully and intentionally choose when to incur in new technical debt, while continuously paying the existing one

## How can we actually do gardening?
All of this sounds good in theory, but how can we actually do gardening in practice? In my experience I've found that these three aspects are essential:

1. Practice – detecting complexity and choosing the right treatment requires trying, learning from your mistakes and getting help from more experienced developers
2. Perseverance – oftentimes the improvements we make today only have an effect later; it's easy to feel frustrated if we don't see immediate results
3. Prudence – we need to understand the cost of an improvement and the impact on the project and the team; do we have enough knowledge to make a decision now?

With that in mind I would like to share some practical things I do:

1. Don't ask for permission
2. Keep your own list of pain points
3. Have a strategy
4. Testing is your friend
5. Code is an expense

This is first and foremost my personal experience. It's what I’ve found to work for me and the projects I’ve worked on. But I believe it can be beneficial for you too.

### Don't ask for permission
I consider gardening part of my day to day work, the same way I push commits to a repository or fix a failing build in our CI service.

I don't wait for Product Owners, Project Leaders or any other stakeholder to tell me when to clean the code. Gardening is our responsibility as engineers and we should be the ones leading this aspect of product development. Fortunately, this is the case at FAIRTIQ, because our culture encourages engineers to do that. And in my particular experience, no stakeholder has had a major issue with it so far[^3].

I don't create separate tasks for what I need to do either. If I can anticipate that a large refactoring is needed I will mention it during planning and account for it when estimating. Only exceptionally, if I think I need to allocate extra time to deal with a delicate part of our apps, I create a task to give visibility to it.

Remember that gardening is all about small steps done continuously over time. If a change is small enough, the overhead of creating a task, discussing it during planning and convincing the Project Leader or the Product Owner that it needs to be done, probably takes more time than the change itself.

### Keep your own list of pain points
Another thing that I do is keep my own list of pain points: parts of the code that I find difficult to work with and are candidates for improving.

I do this because gardening requires an [act of balance](#finding-a-balance). Our work as engineers is subject to deadlines and expectations from stakeholders and our own team. We have to consider the context to understand the impact of doing gardening at a given moment.

So when I see a piece of code that’s cumbersome to work with, I stop and assess the situation:

<img src="{{ site.url }}/files/abg_figure-01-decision-flow-to-assess-a-potential-gardening.png" alt="" width="100%" />

If the required treatment is sufficiently small, I do it regardless of whether the code is related to the task at hand or not.

If the required gardening is not small, but the code is related to the task at hand, I first try to create one or more [preparatory changes](https://martinfowler.com/articles/preparatory-refactoring-example.html) and then continue afterwards. Gardening should be focused on improving the structure of the code, not the behaviour. If the two are mixed in the same batch of changes, they are more difficult to understand and review.

If the required gardening is not small and the code is not related to the task at hand, I add it to the list of pain points and move on.

I revisit my list of pain points often to see when and how we can deal with them. Sometimes I just leave them there for future reference; it turns out that sooner or later they will be addressed as part of upcoming work (e.g. when adding a new feature). But if I think we should tackle them I follow different strategies, as I describe next.

### Have a strategy
Small improvements are ideal to execute during an ongoing task and go a long way over time, even when it's something as simple as renaming a variable or a method.

But what happens with medium or big changes? I use different approaches depending on the context.

#### Making a bet
When the end of an iteration (a.k.a. sprint or cycle) is approaching, it's tempting to take shortcuts and avoid gardening. But I know that spending time today to get something right will prevent rework tomorrow.

So I take a step back, go over the options and assess if gardening will put the goal at risk. Then I make a bet. Sometimes I win, meaning that I could do the gardening and achieve the goal. But sometimes I lose, meaning that I could do the gardening but didn't have time to finish all planned work. In this last case I take responsibility and consider it as part of my learning process as an engineer.

#### Using spare time
If I think I won't have enough time and decide to skip gardening, I wait until I have finished all planned work. If the iteration is still open and I don't have anything else to do, I use that spare time instead of picking something else from the backlog.

But be careful with deadlines! Sometimes the right thing to do is to actually pick the next thing from the backlog.

#### Planning for large improvements
For large improvements I usually draft a plan. I decompose it in small steps that ideally can be executed in isolation. I tell the team if the code is intended to be in a half-way state until we finish. I leave comments in the code explaining why something is not optimal but it's OK because it's intentional and temporary.

Beware though that no plan survives first contact with the enemy. The steps that make sense today might not make sense in a month because the code keeps evolving. That's why I find it best to state the plan in terms of the general problem I want to solve and keep implementation details to a minimum.

### Testing is your friend
When I decide to proceed with gardening, testing is fundamental for me. Nowadays roughly 2/3 of the code I write, if not more, is guided by tests. I don't want to convince you to adopt [TDD](https://en.wikipedia.org/wiki/Test-driven_development). It works for me, but there are other ways to write well designed and testable code.

Regardless of the actual approach, the underlying idea is still the same: we need to have tests before refactoring. Because, again, when we refactor we are not changing the behaviour of the code, only the structure.

### Code is an expense
When it comes to deciding a concrete treatment during gardening, I like to think about code as an expense. In practical terms this means that less code is good code and no code is the best code.

I'm not going to go over refactoring techniques nor design principles because there's plenty of literature about it. If you want to start somewhere, I think Martin Fowler's [Refactoring](https://www.goodreads.com/book/show/35135772-refactoring) should be mandatory reading. Not because of the refactoring recipes themselves, which are great. For me the greatest value comes from the analysis of coding smells in the first part of the book.

Another reason why I don't want to talk about concrete refactoring techniques or architectural choices is because I think there are no silver bullets. A lot of so-called "best” or “modern” practices are actually contextual and not broadly applicable. The perfect architecture does not exist. Even when some architecture fits a problem better than others, at the end of the day it's all about trade-offs.

That said, I would like to share two general guidelines that influence how I design and refactor code today.

#### Duplication is better than the wrong abstraction
I'm fine with duplicated code to a certain extent. Sometimes it's crystal clear that a piece of logic will be useful in other parts of the code. But sometimes a solution is quite specific to a context and it's difficult to tell what the right abstraction is. Here the [rule of three](https://en.wikipedia.org/wiki/Rule_of_three_(computer_programming)) is helpful.

#### YAGNI, SOLID, DRY, in that order
[YAGNI](https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it), the [SOLID](https://en.wikipedia.org/wiki/SOLID) ~~principles~~[^4] guidelines and DRY are helpful but sometimes they conflict with each other. For example, following the SOLID principles may lead us to create more classes than we really need to solve a simple problem.

That's why I follow a kind of priority list:

1. YAGNI
2. SOLID
3. DRY

This means that some duplication can be fine (hence DRY comes last) and the SOLID principles are great to guide the overall design of software. But above all, we should implement things only when we actually need them. I try to resist visionary solutions for imaginary problems I don't have today.

And that's also why sometimes I don’t apply design patterns by the book if they don't fit the problem exactly as they are meant for. This happens in our iOS apps in some cases, especially when the design of surrounding components is not ready to support a pattern as intended.

## Finding a balance
You might be thinking that some of the things I’ve said contradict each other. That’s entirely possible. But it’s at these “friction” points where experience comes into play. After years of practice I still make mistakes and continue learning when I need to go in one direction or another. It turns out, finding the right balance is hard.

Part of finding that balance is accepting that today I know less than tomorrow. I don't try to find the perfect architecture, choose the perfect variable name or apply the perfect abstraction. I work with the knowledge about a problem I have today and stay pragmatic.

For example, I don't think renaming a method that I had already renamed last week is a waste of time if today I have a better understanding of the domain. It was probably the right call back then, because it reflected the knowledge I had. And it's probably the right call now too, because I know more.

I hope I've been able to inspire you to integrate this mindset as part of your work. This is something that might not be news for you, but it’s helpful to have a reminder from time to time.

And if you disagree with something, that's fine! As [Ron Jeffries wrote](https://ronjeffries.com/articles/-z022/0222ff/terms/):

> _People and the way they work together is more important than any particular practices or tools. Practices and tools make a difference, but people working well together can transcend any flaws in their tools and improve their practices. And people working poorly together can screw things up no matter what practices and tools are used._

---

What follows is a section excluded from [the original article](https://fairtiq.com/en/tech/always-be-gardening) for brevity, but I think it's only fair to give credit where its due.

## Where did I learn all this?
I didn't come up with all this knowledge myself. Over the last years I have become quite interested in effective coding techniques. I have studied and learned from many different authors.

This is a selection of the many resources I have used, which are mostly books and talks, in no particular order:

- [The Pragmatic Programmer](https://www.goodreads.com/book/show/4099.The_Pragmatic_Programmer), by David Thomas and Andy Hunt
- [Getting Real](https://basecamp.com/gettingreal), by Jason Fried and David Heinemeier-Hansson
- [Refactoring: Improving the Design of Existing Code](https://www.goodreads.com/book/show/35135772-refactoring), by Martin Fowler
- [Clean Code](https://www.goodreads.com/book/show/3735293-clean-code) and [The Clean Coder](https://www.goodreads.com/book/show/10284614-the-clean-coder), by Robert C. Martin
- [Working Effectively with Legacy Code](https://www.goodreads.com/book/show/44919.Working_Effectively_with_Legacy_Code), by Michael Feathers
- [Smalltalk Best Practice Patterns](https://www.goodreads.com/book/show/781561.Smalltalk_Best_Practice_Patterns), by Kent Beck
- [Head First Design Patterns](https://www.goodreads.com/book/show/58128.Head_First_Design_Patterns), by Eric Freeman and Elisabeth Robson
- [99 Bottles of OOP](https://www.goodreads.com/book/show/54500642-99-bottles-of-oop), by Sandy Metz
- [Seven Ineffective Coding Habits](https://www.youtube.com/watch?v=SUIUZ09mnwM) and [Code as Risk](https://www.youtube.com/watch?v=YyhfK-aBo-Y), by Kevlin Henney
- [How to not build legacy systems that everyone hates](https://www.youtube.com/watch?v=Kwtit8ZEK7U), by Chris James

[^1]: The expression has its origins in “Mobile Gardening”, a name that [Seán Labastille](https://twitter.com/flufffel) coined for a weekly meeting that mobile developers used to have at FAIRTIQ. I liked it when I heard it the first time and started drawing on this idea of treating a codebase as a garden. I could have used "always be refactoring", but I don't think refactoring alone conveys the same meaning.
[^2]: You might have heard an alternative take: "functionality is an asset, code is a liability".
[^3]: At the time of writing I have been in the company for more than four years.
[^4]: I prefer [Kevlin's Henney reframing](https://www.youtube.com/watch?v=tMW08JkFrBA) of SOLID as guidelines, rather than principles.