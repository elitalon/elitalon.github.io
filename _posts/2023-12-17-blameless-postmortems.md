---
title: Blameless postmortems
description: Some thoughts about why blameless postmortems can be problematic
---

<!--more-->

On his reflections about the risks of looking back too much when something goes wrong in your company, [Jason Fried wrote](https://world.hey.com/jason/look-back-less-848e9db0) the following:

> _…so many failed projects subject to retrospectives are searching for reasons where there are only humans to be found._

Funnily enough, a couple of days before Jason published that I was talking with a friend about blameless postmortems. I posited that the "blameless" aspect is wishful thinking. More often than not someone truly made a mistake and a postmortem is only going to make that evident.

As far as I know blameless postmortems were [first described by Etsy](https://www.etsy.com/codeascraft/blameless-postmortems/) in 2012[^1] and made even more popular around 2017 when [Google included them](https://sre.google/sre-book/postmortem-culture/) in their Software Reliability Engineering book. The intention is to focus on how incidents are triggered, instead of who caused them, and balance safety and accountability.

But J. Paul Reed [had pointed out the problems](https://www.youtube.com/watch?v=Udmx3qfGYic) with that approach as early as 2014. He argued that the blameless postmortem is a myth because the tendency to blame is hardwired through millions of years of evolutionary neurobiology. Ignoring this tendency and their [associated biases](https://fractio.nl/2015/10/30/blame-language-sharing/) is incredibly difficult, so it's more practical to be [blame-aware](https://techbeacon.com/app-dev-testing/blameless-postmortems-dont-work-heres-what-does) than trying to be blameless.

My own experience definitely matches J. Paul's observations[^2] and has led me to believe that these biases and the ingrained tendency to blame actually work both ways.

I once worked in a team where a developer dropped a database table in production. A whole table. In production. There's no way we could have written a blameless postmortem. That poor soul literally dropped the damn table!

Sure, we could have focused on the actions that led them do that. Maybe a confirmation dialog was missing. Maybe they shouldn't have had write permissions to the database in the first place. But in every step of the discussion, everyone had that developer in their minds.

In my career I have also made mistakes that ended up in a postmortem. I remember having published new versions of a mobile app that signed out all users that upgraded to them. Or preventing users from signing up because the logic to accept some legal clause had a subtle bug.

In these two cases no one needed to blame me because I did so myself. And here comes the twist: regardless of whether others actually blame you or not, sometimes you can't help but thinking that someone will. I agree it's just how our brains are wired.

This is not to say that postmortems aren't useful at all and we shouldn't be doing them[^3]. My point is rather to avoid fooling ourselves with the idea that they can be blameless.

Being aware of their problems can help us evaluate if they are the right tool for our team or a specific incident. We could ask ourselves questions like:

- Do their benefits compensate the damage we might be inflicting to the psychological safety in the team?
- Is it worth worth making them publicly available to the whole company or a whole department?
- Is there any other tool we could use instead, like lightweight informal retrospectives?

If postmortems work for you, then great. But make sure you don't adopt them just because if they do for someone else, they should for you too.

[^1]: Later in 2016 Etsy also wrote [guidelines for facilitating postmortems](https://www.etsy.com/codeascraft/debriefing-facilitation-guide/).
[^2]: Yes, I'm aware this is anecdotical and I might have just been extremely unlucky in my career.
[^3]: Though I would definitely consider using less [macabre terminology](https://github.com/etsy/morgue).
