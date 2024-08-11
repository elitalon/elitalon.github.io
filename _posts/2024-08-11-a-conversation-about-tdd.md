---
title: A conversation about Test-Driven Development
description: While discussing the use of AI assistants, a friend and I digressed briefly to talk about Test-Driven Development.
---

<!--more-->

What follows is an edited transcription of a conversation I had on [Signal](https://signal.org) with a friend about [Test-Driven Development](https://en.wikipedia.org/wiki/Test-driven_development) (TDD). We were discussing the use of AI assistants for writing code and we digressed briefly.

My friend and I are both native Spanish speakers and, naturally, we talked in Spanish. But I've done my best to keep the original meaning and nuances in the translation to English.

---

**Me:** That said, I think it's mostly hype right now. I spend most of my time reading and thinking about the design, not actually writing code. And even more so since I started to discipline myself in the use of TDD.

**Friend:** And how is it going? I've heard it mentioned in so many interviews, and nobody uses it 😂

**Friend:** The truth is that I'd like to use it to experiment with using tests as a contract between clients, managers and devs. Everybody could easily understand this. But it's just a wild idea that I haven't seen anyone talk about, and I don't know if it would have a future in practice.

**Friend:** I use an AI assistant to generate tests and it works well. I give it the code and it does the rest.

**Me:** Well, I like TDD a lot, to be honest. The learning curve was a bit painful because after years writing tests differently, changing my routine was hard. But the truth is that I enjoy it now.

**Me:** But I don't use it to generate an interface contract. For me, the biggest advantage is that I notice that I tend to write less code and come up with simpler designs. Because once a test passes, that's it.

**Me:** It's true that in some rare cases the resulting design is not the simplest. But I think it's a trade-off worth making when you consider all other benefits.

**Me:** I'm not dogmatic either. There are times when I write tests after the fact. My guess is that nowadays I write 80% of my code using TDD and the rest ‘the old way’

**Friend:** You tend to write less code?! Break it down.

**Me:** Writing a test first forces me to design the interface first. So, I only declare the types and methods that are strictly necessary for the test to compile. With the interfaces declared, I only need to write the minimum implementation necessary to pass the test.

**Me:** An interesting side effect I've observed is that some colleagues tend to use design patterns out of inertia, almost without considering if they're really needed. Whereas I use patterns and coding techniques in a more incremental, deliberate way.

**Friend:** I had guessed something like that, but I'm a bit surprised because then you tend not to think about design[^1].

**Me:** This is a criticism I often hear about TDD, and partly rightly so. It's also true that it often comes from people who haven't given TDD a serious try 🤷🏻‍♂️

**Me:** That's what I meant before when I said that in some cases the resulting design is not the most optimal. But generally speaking, in my experience it's quite the opposite. Writing tests first forces you to think about design because you also want to keep your tests well-designed.

**Me:** The difference is that the design is incremental, it emerges as you write more and more tests, communicating components with each other.

**Me:** The problem I see is that we developers are mostly used to doing all the design upfront. And the notion of "one little bit of design at a time" feels odd.

**Me:** This is based on my experience, anyway. I use TDD at my convenience, just as another tool. I don't care much about "pure TDD" 😅

**Me:** To give you an analogy, TDD would be like using an [MVP](https://en.wikipedia.org/wiki/Minimum_viable_product) to validate a business idea with a group of users.

**Me:** It helps me develop the minimum necessary code to "launch" a functionality to the market. And users (for example, me the next week) validate whether the design was right or not, using the ease of changing the code for a new requirement as a metric.

**Friend:** I think it's a good idea. The only problem I see is that it requires continuous refactoring, and that's a bit dangerous.

**Me:** Why would it be? You have tests precisely for that.

[^1]: I think my friend was referring here more broadly to the architecture of a sofware system.
