---
title: Quick notes on using Xcode with GitHub Copilot
description: Quick notes after using Xcode with GitHub Copilot for one month
---

<!--more-->

I've been using Xcode together with [GitHub Copilot](https://github.com/features/copilot) almost daily for about two months now, and I thought I'd share some notes about my experience so far.

I'm integrating Copilot through the [Copilot For Xcode](https://github.com/intitni/CopilotForXcode) extension, which does a decent job despite being a bit fiddly to configure. It also offers integrations with other similar services as well, like [ChatGPT](https://chatgpt.com).

And at the risk of stating the obvious, this is my usual cycle when programming with Copilot enabled:

1. Start typing
2. See what Copilot suggests
3. Decide whether to accept the suggestion or not
4. If I agree, make sure it does what I intended and make changes if necessary
5. Continue

So with the above in mind, these have been my observations:

- I would classify the suggestions I get into two broad categories: "one-liners" and "code chunks" of up to 10–15 lines. I haven't figured out yet the criteria Copilot uses to go with one or the other, but I would like to know

- Suggestions tend to get in the way of Xcode's autocompletion. This is particularly annoying for one-liners, as autocompletion is fast and accurate enough to make Copilot redundant, if not useless

- One-liners don't seem to save me time or offer a useful alternative to what I was going to write anyway. In fact, I'd argue that pausing briefly to look at the suggestion makes me spend more time than I would otherwise

- Code chunks, on the other hand, are valuable in terms of throughput, even if they are not entirely correct. Yes, I still have to spend time reviewing, but that's often faster than writing them from scratch

- However, code chunks are only marginally valuable in terms of impact or effectiveness. Like with one-liners, they often contain what I already wanted to type. Somehow, I expected Copilot to offer alternatives to an "obvious" solution

- [Hallucinations](https://en.wikipedia.org/wiki/Hallucination_(artificial_intelligence)) are surprisingly common, at least for Swift. And this happens with multiple tabs open and plenty of surrounding code. Unit tests are probably the only context where suggestions are consistently more accurate

- I wonder if relying too much on AI-based suggestions might make developers less likely to think out of the box. Programming languages, especially modern ones, allow us to solve problems in different ways. And while I try to avoid clever code, we shouldn't give up our ability to explore alternatives

Overall, I think it's fair to say that my experience has been relatively disappointing.

I can see how using Copilot could help save time when producing many lines of code at once. But is it a game changer? I'm not sure. Maybe this applies to Swift only and the benefits are greater in other languages. It also seems clear that thinking, the most critical aspect of software development, will remain with the programmer for now.

I will continue to use Copilot and see if it improves over time, or if I learn new uses that bring additional benefits.
