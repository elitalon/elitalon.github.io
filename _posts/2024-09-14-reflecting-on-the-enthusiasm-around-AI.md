---
title: Reflecting on the enthusiasm around "AI"
description: Some thoughts about what's going on the "AI" front in 2024, based on what I've learned from other people and my own experience.
---

<!--more-->

I've tried to consolidate my thoughts on the current fad around "AI" for weeks already, hoping to write something constructive or at least something that didn’t sound too pessimistic. But regardless of the angle I took, I always ended up somewhat demoralised.

So I'm just going to share the current issues I see with "AI" without any further rumination. If you want to read something more thoughtful, I highly recommend [Molly White's take](https://www.citationneeded.news/ai-isnt-useless/).

By the way, I write "AI" in quotes because what's been sold as artificial intelligence so far is pure marketing nonsense. [Generative AI](https://en.wikipedia.org/wiki/Generative_artificial_intelligence) (its actual name) belongs to the research field of [deep learning](https://en.wikipedia.org/wiki/Deep_learning), is not anywhere near actual AI[^1], and would be better called [statistical autocompletion](https://mastodon.social/@thomasfuchs@hachyderm.io/113125426967682488).

## Intellectual property
Products like [ChatGPT](https://chatgpt.com) use [Large Language Models](https://en.wikipedia.org/wiki/Large_language_model) (LLMs), which need a vast amount of data for their training. And where does the data come from? It turns out, they [scrap](https://en.wikipedia.org/wiki/Web_scraping) as much content as they can from the public Internet, often without permission of rights holders[^2].

One can argue that there are other products that benefit from similar techniques. [Search engines](https://en.wikipedia.org/wiki/Search_engine_(computing)), for example, crawl websites to build their page indexes and ranks. The difference is that their results link to the original source. Even if you pay for a search engine like [Kagi](https://kagi.com/), you will be paying for the indexing functionality, not for the content itself.

Similarly, people can share copyrighted media on platforms like YouTube or SoundCloud. But these platforms usually go to great lengths to make sure that all content is published according to existing laws.

The problem with some "AI" companies is that they take someone else's content and turn it into a commercial product, often without giving anything back to the original creators.

[Sam Altman](https://en.wikipedia.org/wiki/Sam_Altman), the president of [OpenAI](http://openai.com), wrote in a [submission](https://committees.parliament.uk/writtenevidence/126981/pdf/) to the House of Lords in December 2023 that

> _[b]ecause copyright today covers virtually every sort of human expression– including blog posts, photographs, forum posts, scraps of software code, and government documents–it would be impossible to train today’s leading AI models without using copyrighted materials._

And more interestingly

> _[…] although we believe that legally copyright law does not forbid training, we also recognize that there is still work to be done to support and empower creators. We have been industry leaders in allowing creators to express their preferences with respect to the use of their works for AI training._

That's basically turning the rules around. OpenAI is proposing that they should be granted free access to any copyrighted content, and it's up to creators to say "hey, just don't steal from me, pretty please?".

## Environmental impact
Then there's also the question of how much these "AI" products cost in terms of environmental impact.

Training a single LLM [takes a lot of energy](https://www.scientificamerican.com/article/the-ai-boom-could-use-a-shocking-amount-of-electricity/) and emits hundreds of tons of carbon. It also needs a decent amount of fresh water to cool down data centres. These requirements continue to increase as models become more and more advanced, as reported by [Kate Crawford in Nature](https://www.nature.com/articles/d41586-024-00478-x):

> _A lawsuit by local residents revealed that in July 2022, the month before OpenAI finished training the model, the cluster used about 6% of the district’s water. As Google and Microsoft prepared their Bard and Bing large language models, both had major spikes in water use — increases of 20% and 34%, respectively, in one year, according to the companies’ environmental reports_

Note that these figures come from companies working on these products, not from an outside observer.

As if we didn't face enough challenges to put climate change measures in place, from ineffective and/or slow politics to companies [greenwashing](https://en.wikipedia.org/wiki/Greenwashing) their image, now there's another contender trying to derail our efforts.

I remember a time when [cryptocurrencies](https://en.wikipedia.org/wiki/Cryptocurrency), or [blockchains](https://en.wikipedia.org/wiki/Blockchain) in general, were heavily criticised for their impact on the environment. Could it be that LLMs don't get the same scrutiny because cryptocurrencies were mostly driven by outsiders, whereas "AI" is benefitting the ruling class?

## Ethical implications
Another aspect that often goes unexamined in the race to adopt "AI" is the ethical implications that comes along with them.

On one hand, there's the incessant data collection, not just for training LLMs but also as part of users interacting with them.

When you ask one of these tools to solve something, you have to provide some input. This could be something as asking the colours of a flower. But in more complex tasks, users who aren't careful or experienced could disclose private or sensitive information that shouldn't reach these companies' servers.

So a lot of information is being fed to the likes of OpenAI, Google, Microsoft, Meta and Apple, by millions and millions of users, one prompt at a time. What could they do with that in the future, should they have a need?

On the other hand, there's also the false sense of accuracy, correctness or quality that many people attribute to this technology. But if you [spend enough time playing with them](/2024/06/01/quick-notes-on-using-github-copilot-with-xcode/), you'll soon realise that they hallucinate a lot.

Deep learning in general has many valid use cases. A neural network _specifically trained_ to perform a _very concrete_ task, like cancer detection in medical imaging, often works well and can serve as a tool to support human experts (note the emphasis I used).

However, the current claim is that "AI" can be broadly applied as long as we [get the prompt right](https://en.wikipedia.org/wiki/Prompt_engineering), even when a correct outcome is _never_ guaranteed. In some instances, the same wrong results are returned over and over, simply because the misinformation and biases around the public Internet have also been used to train these models. Garbage in, garbage out.

I believe that having these tools giving inaccurate or outright false information to users, regardless of their experience in a given domain, and then being applied to decision-making tasks is a huge liability.

## What about software development?
I'd like to finish with some ideas about the impact of "AI" in software development, specifically on the use of coding assistants.

First these insights from Kevlin Henney in a [recent interview](https://www.youtube.com/watch?v=B7Mbpbk_lnw), slightly edited for clarity, when he was asked about how software engineering would look like in 2034[^3]:

> _You’re going to need to get good at testing. Because if you’re just going to take the first thing that is generated, and you don’t know what it’s supposed to do, you'll end up being a maintenance programmer._
>
> _[…]_
>
> _We've seen how programmers use the tools they're given. There is no evidence to suggest AI assistants are going to be for the better. The majority of developers will create legacy code. They will just do it faster. And they will be dealing with code that somebody else wrote._
>
> _[…]_
>
> _Developers that go all in on generative AI to create their own code are going to discover that they've taken all the joy out of their job._

The second one comes from a [thorough analysis from Ian Cooper](https://ian-cooper.writeas.com/is-ai-a-silver-bullet), in which he discusses whether AI is the silver bullet we've been searching for decades:

> _Optimizing for authorship is usually a poor trade-off in the long run, as we spend more time on maintenance and modification than on creation._

If you agree that code is written once and read many times, it doesn't seem unreasonable to think that current "AI" assistants are a false economy. They try to help with the part of programming that takes less time, while potentially introducing subtle bugs and less readable code for the part that takes more time.

[^1]: There's a _significant_ difference between using an AI technique in a very specific field and achieving [artificial general intelligence](https://en.wikipedia.org/wiki/Artificial_general_intelligence) or [artificial superintelligence](https://en.wikipedia.org/wiki/Superintelligence#Feasibility_of_artificial_superintelligence).
[^2]: There are some exceptions in which some part of training data is actually licensed.
[^3]: In the same interview, Kevlin also mentions a [study from BitClear](https://www.gitclear.com/coding_on_copilot_data_shows_ais_downward_pressure_on_code_quality) about changes in code quality with the adoption of AI coding assistants.
