---
title: When experience turns into frustration
description: Having experience appears to be a double-edged sword. On one hand, you have the ability to see things from different angles. But on the other, it's frustrating to see people falling into the same traps again and again.
---

<!--more-->

I've reached a point in my career in which I struggle to understand if I'm doing things wrong, others are doing things wrong, we're all doing things wrong, or there's no right nor wrong answer and everything is contextual.

Let me explain.

I spend a decent part of my leisure time improving my craft as a software developer. This comes in many forms, but my preferred one is reading books, followed by articles from a curated collection of RSS feeds and watching conference talks[^1].

I've never cared too much about cutting-edge technology because I'm wary of hype cycles. Instead, and perhaps because I like history, I've focused on the foundations of the field. I'm definitely not an expert in everything that I've read or learned. But I believe I know enough to have developed a minimum of critical thinking.

So part of my problem begins when someone says that a practice they do is called X, or part of methodology Y, but I know that this isn't entirely accurate, if not plain wrong. Or when a team insists on doing things in a particular way because "it's a best practice", but I know being "best" actually depends on different factors, starting with the context.

I see an increasing number of teams with a seemingly hardwired set of practices and ideas that are incredibly difficult to steer in a different direction. Programmers that claim to write "clean code", without having read [the book](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882), teams convinced of doing SCRUM, without having read [the guide](https://scrumguides.org/scrum-guide.html)[^2], or believing they "do" agile[^3] without having even heard about its [12 principles](https://agilemanifesto.org/principles.html).

This would be fine if some developers didn't try to stick to their personal preferences (or, worse, hubris) or weren't guided by politics or a [cargo cult](https://en.wikipedia.org/wiki/Cargo_cult_programming) when an opportunity for debate presented.

Instead, what I find sometimes is that challenging a concept or practice is met with upfront opposition, even if arguments are supported by research or respected sources. It feels as though none of my previous experience and knowledge mattered.

Ironically, the other part of my struggle has to do with the fact that, as I've been working in the industry for nearly two decades, trying[^4] to put all this accumulated knowledge into practice, I've developed a certain ability to see more and more nuances and fewer absolutes.

One implication of this is that my engineering skills have evolved to be less opinionated about platform conventions and more concerned about how technology has to serve the problem domain and the business, and not the other way around.

This has led me to find myself in situations where I often have to justify every little change, simply because it deviates from the established norm[^5], regardless of whether that norm might actually be detrimental to the code, the project or the team.

In those moments, when every step is a struggle, when every decision I take is questioned in the name of a supposedly best practice or convention, I sometimes wonder why I should go on. Is this what having experience in software engineering was supposed to be?

More importantly, how are we supposed to evolve our practices, where is the space to question the status quo and experiment with alternatives, if we repeatedly prefer "the way we do things here"? And sometimes it's not even about coming up with new ideas. But rather, just going back to basics and simplifying.

Please don't get me wrong. I believe in the power of consistency and the benefits of conventions. It helps us focus on what matters and not be distracted with irrelevant details. But it's also beneficial to be open to see the world through a different lens, specially when it may offer an opportunity for improvement. Or realising that some of these details were not so irrelevant after all.

So what I've been practicing lately is learning to let go. When I see a debate entering an endless exchange of arguments and going in circles, I tend to take a step back and let others prevail. Firstly, because they could be right and there's something new for me to learn. And secondly because letting others learn from their own ~~mistakes~~ choices is sometimes more effective.

A recent example is from an iOS app that I've been helping develop for years. I was always hesitant to introduce the [Combine framework](https://developer.apple.com/documentation/combine/) because I feared it would transform the app into a Frankenstein of imperative and [reactive code](https://en.wikipedia.org/wiki/Reactive_programming), opening the door to a new class of bugs.

One day, a colleague proposed introducing a [publisher](https://developer.apple.com/documentation/combine/publisher) because it could simplify the implementation of a new feature. I was not convinced because in that context I didn't see any real benefit beyond syntactic sugar. But after some back and forth I said, "alright, let's try it".

We ended up with roughly the same amount of code, albeit a little more complex, as if we had followed one of the existing patterns. And when we published the app, we found that we had introduced a couple of bugs. But while my initial gut feeling was right, and I still think there was no need to design that feature that way, the incident left me better equipped to understand where and how that approach would fit better.

So having experience appears to be a double-edged sword. On one hand, you have more tools at your disposal and the ability to see things from different angles. But on the other, it's frustrating to see people falling into the same traps and dismissing your advice. And deep down, I can't help but ask myself if I'm not just getting old and tired.

[^1]: The list of authors is long: [Martin Fowler](https://martinfowler.com/), [Kent Beck](https://kentbeck.com/), [Robert C. Martin](http://cleancoder.com/), [Kathy Sierra](https://en.wikipedia.org/wiki/Kathy_Sierra), [Kevlin Henney](https://www.kevlin.tel/), [Allen Holub](https://holub.com/), [Scott Meyers](https://www.aristeia.com/), [Dave Thomas](https://pragdave.me/), [Andy Hunt](https://toolshed.com/), [Sandi Metz](https://sandimetz.com/), [Ron Jeffries](https://ronjeffries.com/), [Nicole Forsgren](https://nicolefv.com/), [Dave Farley](https://www.davefarley.net/), [Jez Humble](https://continuousdelivery.com/about/), [Michael C. Feathers](https://www.r7krecon.com/michael-feathers-bio), [Michael Lopp](https://randsinrepose.com/), [Tim Ottinger](https://agileotter.blogspot.com/), [Jason Fried](https://world.hey.com/jason), [David Heinemeier-Hansson](https://dhh.dk/), [Donella Meadows](https://en.wikipedia.org/wiki/Donella_Meadows), [Tom DeMarco](https://en.wikipedia.org/wiki/Tom_DeMarco), [Tim Lister](https://en.wikipedia.org/wiki/Tim_Lister), [Eric Evans](https://www.domainlanguage.com/),…

[^2]: A recurring plot twist here is teams that have actually read the SCRUM guide, ignored or forgotten most of it, and still say they follow it.

[^3]: You don't do agile, you _are_ agile. The mere use of the word agile as something you could do tells you already how misguided part of the industry is.

[^4]: I say trying because sadly many companies don't really give you the space to experiment and do things differently. Some pretend they do. But when it comes to actual change, the status quo wins because, it turns out, change is surprisingly hard. Most people, myself included, prefer to keep doing things the way we always have, even though it's not necessarily the best, simply because it's more comfortable or we're used to it.

[^5]: A pet peeve of mine is listening to developers justifying doing something because "it's what big companies do". I'm sorry, but your team of 10 developers is nowhere near the category of problems that the likes of Google is having.
