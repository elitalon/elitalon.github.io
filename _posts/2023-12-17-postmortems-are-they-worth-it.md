---
title: "Postmortems: are they worth it?"
description: Some thoughts about why postmortems can be problematic
---

<!--more-->

Reflecting about the risks of looking back too much when something goes wrong in your company, [Jason Fried wrote](https://world.hey.com/jason/look-back-less-848e9db0) the following:

> _…so many failed projects subject to retrospectives are searching for reasons where there are only humans to be found._

Coincidentally, I was talking with a friend about blameless postmortems a couple of days before Jason published that. I posited that the "blameless" aspect is wishful thinking. More often than not someone truly made a mistake and a postmortem is only going to make that evident.

As far as I know blameless postmortems were [first described by Etsy](https://www.etsy.com/codeascraft/blameless-postmortems/) in 2012[^1] and made even more popular around 2017 when [Google included them](https://sre.google/sre-book/postmortem-culture/) in their Software Reliability Engineering book. The idea is to focus on how incidents were triggered, instead of who caused them, and balance safety and accountability.

But J. Paul Reed [had pointed out the problems](https://www.youtube.com/watch?v=Udmx3qfGYic) with that approach as early as 2014. He argued that the blameless postmortem is a myth because the tendency to blame is hardwired through millions of years of evolutionary neurobiology. Ignoring this tendency and their [associated biases](https://fractio.nl/2015/10/30/blame-language-sharing/) is incredibly difficult, so it's more practical to be [blame-aware](https://web.archive.org/web/20240414140552/https://techbeacon.com/app-dev-testing/blameless-postmortems-dont-work-heres-what-does) than trying to be blameless.

My own experience definitely matches J. Paul's observations[^2] and has led me to believe that these biases and the ingrained tendency to blame actually work both ways.

I once worked in a team where a developer dropped a database table in production. A whole table. In production. There's no way we could have written a blameless postmortem. That poor soul literally dropped the damn table!

Sure, we could have focused on the actions that led them do that. Maybe a confirmation dialog was missing. Maybe they shouldn't have had write permissions to the database in the first place. But in every step of the process everyone had that developer in their minds.

In my career I have also made mistakes that ended up in a postmortem. I remember having published a new version of a mobile app that signed out all users that upgraded to it. Or preventing users from signing up because the logic to accept some legal clause had a subtle bug.

In these two cases no one needed to blame me because I did so myself. And here comes the twist: regardless of whether others actually blame you or not, sometimes you can't help but thinking that they will. I agree it's just how our brains are wired.

Another thing I've seen often is teams spending too much time trying to get to the heart of what went wrong, sometimes for days, when the lessons learned barely compensated the effort. Digging deep into logs, going back to chat conversations, coming up with a thorough timeline of events, cross-referencing pull requests with deployments,… It seems to me like pointless paperwork that will rarely be looked at again, if ever.

This is not to say that postmortems aren't useful at all and we shouldn't be doing them[^3]. I understand they can have a place, perhaps in highly regulated industries or when incident reporting is actually an integral part of the business. My point is rather to avoid fooling ourselves with the idea that they can be blameless and think carefully about the real value they bring.

Being aware of their problems and cost can help us evaluate if they are the right tool for our team or a specific incident. We could ask ourselves questions like:

- Do their benefits compensate the damage we might be inflicting to the psychological safety in the team?
- Is it worth or even necessary making them publicly available to the whole company or a whole department?
- What would be the opportunity cost if we chose not to do them? Is there any other tool we could use instead, like lightweight or more informal retrospectives?

If postmortems work for you, then great! But make sure you don't adopt them just because if they work for someone else, they should for you too.

[^1]: Later in 2016 Etsy also wrote [guidelines for facilitating postmortems](https://www.etsy.com/codeascraft/debriefing-facilitation-guide/).
[^2]: Yes, I'm aware this is anecdotical and I might have just been extremely unlucky in my career.
[^3]: Though I would definitely consider using less [macabre terminology](https://github.com/etsy/morgue).
