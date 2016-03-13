---
title: My failed attempt to learn Haskell
description: An unpleasant journey towards learning functional programming through Haskell
---
A lot of attention was brought into [functional programming]() when Swift [was announced in WWDC 2014](https://developer.apple.com/videos/play/wwdc2014/101/). That was not anything new: applying such techniques to modern software development has been a trend in general. But within the Apple development ecosystem in particular, Swift really made everyone to take it more seriously.

<!--more-->

At first I was hesitant to refresh my knowledge of functional programming. I remembered enough to understand the main concepts, so I tried to focus more on transitioning from Objective-C to Swift. After all, having a deep knowledge of functional programming is not really a requirement for being proficient in Swift. It just gives you more options to design a solution.

Several months passed and I was comfortable writing a good amount of code in Swift without having to check a number of resources. But I also kept reading articles about how to leverage the functional features of Swift. So maybe that was the right moment to take a step back, study some functional programming and improve my Swift toolkit.


## Functional programming revival

I decided to start by learning a new language that followed the functional paradigm. Like I mentioned above, I remembered the overall theory; I just needed to put that into practice again. So inspired by [Chris Eidhof](http://www.twitter.com/chriseidhof/) and [Natasha The Robot](https://www.natashatherobot.com/reading-functional-programming/), I chose [Haskell](https://www.haskell.org).

Haskell is a general-purpose, purely functional programming language with strong static typing, type inference and lazy evaluation. Its weird syntax is definitely not what you are used to see with imperative languages. However, it is not [Lisp](https://en.wikipedia.org/wiki/Lisp_(programming_language)) either. From all the resources available, I went with these three:

* [Real World Haskell](http://book.realworldhaskell.org)
* [Haskell for Mac](http://learn.hfm.io)
* [Learn You a Haskell for Great Good](http://learnyouahaskell.com)

I started with "Real Word Haskell". The beginning is promising, but the narrative becomes tedious and I think it fails to explain the concepts with more clarity. The examples are a bit complex too, because they require knowledge about the problem domain and that adds noise to the exposition.

"Haskell for Mac" was a nice surprise. It is easier to follow, the examples suit better the concepts explained and the pace makes the learning curve less steep. However, the resources do not cover everything as they are apparently still working on it.

Finally, I went ahead with "Learn You a Haskell for Great Good". This one is a good compromise between the other two. It covers most of the things you need to know about Haskell, while keeping a good balance between the complexity of the examples and the overall narrative.


## The problem with Haskell... is not Haskell

I must admit that this journey was not fun at all (with the exception of "Haskell for Mac", maybe). I definitely have a deeper understanding of the language now. I learnt the concepts behind it, I did a lot of exercises and I revisited the theory to consolidate the knowledge. However, I cannot say I'm able to write something meaningful in Haskell. I have the feeling that I have failed miserably.

But I do not think the problem here is the language itself. While I think Haskell is not a beautiful language, a lot of thought has been put into its design. The techniques that it provides are really smart and elegant, maybe too smart sometimes. If I had to criticise something, I would say that:

* The syntax is horrible.
* Implicit things happen, and they are difficult to follow.

The problem with Haskell is that it needs better communication and marketing. The resources for learning are not good, most of the examples are based on math stuff and there is a big gap between those examples and real-life problems.

## But I am not done yet

Despite my failed attempt to learn, I want to leave you with a positive note.

Haskell helped me understand better how Swift is designed and how Haskell, [Scala](http://www.scala-lang.org) and some other functional languages had an impact on it. When the Swift compiler makes something implicit, I can see why and where that comes from.

I do not see myself writing software in Haskell, but it got me interested in learning more about functional programming. I will take a different approach this time, though. I intend to learn [Erlang](http://www.erlang.org) and the applications of [OTP](https://en.wikipedia.org/wiki/Open_Telecom_Platform). But first I am going to start with [Elixir](http://elixir-lang.org), just for the sake of using a familiar syntax for once.
