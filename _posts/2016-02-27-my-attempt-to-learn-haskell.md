---
title: My attempt to learn Haskell
description: An unpleasant journey towards learning functional programming through Haskell
---
A lot of attention was brought into functional programming when Swift [was announced in WWDC 2014](https://developer.apple.com/videos/play/wwdc2014/101/). That wasn't really new. Bringing these concepts to your day-to-day programming has been a trend in general. But within the Apple ecosystem in particular, Swift made everyone take it more seriously.

<!--more-->

I was hesitant at first to refresh my knowledge of functional programming. I remembered enough from my university years to understand the main concepts, so I focused more on transitioning from Objective-C to Swift. After all, having a deep knowledge of functional programming is not really a requirement for being proficient in Swift. It only gives you more options to design a solution.

Several months passed and I was comfortable writing code in Swift. But I also kept reading articles about how to leverage its functional features. I thought that maybe it was the moment to take a step back, refresh my functional programming knowledge and grow my toolkit.

## Functional programming redux
I decided to start by learning a new language that followed the functional paradigm. Like I said, I remembered the overall theory so all I needed was to put it into practice again. Inspired by [Chris Eidhof](http://www.twitter.com/chriseidhof/) and [Natasha The Robot](https://twitter.com/NatashaTheRobot), I chose [Haskell](https://www.haskell.org).

Haskell is a general-purpose, purely functional programming language with strong static typing, type inference and lazy evaluation. Its weird syntax is definitely not what you are used to see with imperative languages. However, it's not [Lisp](https://en.wikipedia.org/wiki/Lisp_(programming_language)) either. From all the resources available, I went with these three:

* [Real World Haskell](http://book.realworldhaskell.org)
* [Haskell for Mac](http://learn.hfm.io)
* [Learn You a Haskell for Great Good](http://learnyouahaskell.com)

"Real Word Haskell" had a promising start, but the narrative becomes tedious and I think it fails to explain concepts with more clarity. The examples are a bit complex too, because they require knowledge about the problem domain and that adds noise to the exposition.

"Haskell for Mac" was a nice surprise. It was easy to follow, the examples suited better the concepts explained and the pace made the learning curve less steep. However, it didn't cover everything as they are apparently still working on it.

Finally, I went ahead with "Learn You a Haskell for Great Good". This one is a good compromise between the other two. It covered most of the things you need to know about Haskell, while keeping a good balance between the complexity of the examples and the overall narrative.


## A disappointing journey
I must admit that this journey wasn't really as fun as I had expected (with the exception of "Haskell for Mac", maybe).

I have a better understanding of the language now. I have learned the concepts, completed many exercises and revisited the theory to consolidate my knowledge. It also helped me understand functional programming concepts in Swift, and how Haskell, [Scala](http://www.scala-lang.org) and other functional languages might have served as inspiration.

But I cannot say that I'm able to write something meaningful and have the feeling that I have wasted my time.

And I don't think the problem here is the language itself. Haskell isn't a particularly beautiful language, but a lot of thought has been put into its design. The affordances it provides are smart and elegant (maybe too smart sometimes). If I had to criticise something, I would say that the syntax is more suited for writing, instead of reading, and that too many things happen behind the scenes.

Maybe the problem is that it needs better communication or marketing. The available resources for learning are not great, most of the examples are based on mathematical trivia and there is a big gap between them and real life problems.

## Next steps
Honestly I don't see myself writing software in Haskell in the near future. But at least it got me interested in learning more about functional programming.

I'm going to take a different approach next time, though. Learning [Erlang](http://www.erlang.org) and the applications of [OTP](https://en.wikipedia.org/wiki/Open_Telecom_Platform) have always been in my radar. And I think [Elixir](http://elixir-lang.org) is worth exploring too, if only for the sake of reading a more familiar syntax.
