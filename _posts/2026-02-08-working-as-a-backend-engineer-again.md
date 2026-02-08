---
title: Working (again) as a backend engineer
---

<!--more-->

In 2025, after 13 years working as an iOS engineer, I changed career paths and started working as a backend engineer again. As I'm writing this, I'm involved in building and maintaining services that use [Spring Boot](https://spring.io/projects/spring-boot), [MongoDB](https://www.mongodb.com/), [Kafka](https://kafka.apache.org/) and [RabbitMQ](https://www.rabbitmq.com/).

I had already worked on the backend at the beginning of my career, mostly on [CakePHP](https://cakephp.org/) applications. So even though the field was not entirely new to me, a lot has changed in a decade.

For example, I was used to deploying applications on [VMware](https://en.wikipedia.org/wiki/VMware) virtual machines running on [Debian](https://www.debian.org/) servers. And deploying meant pulling changes from a VCS, sometimes even uploading files through [SFTP](https://en.wikipedia.org/wiki/SSH_File_Transfer_Protocol), and restarting an [Apache](https://httpd.apache.org/) server. Those were the days.

A friend asked me how I was doing after being a while in my new role. So I thought it would be a good opportunity to write down some thoughts for posterity's sake.

The first thing that surprised me was that the programming language (Java) was not an issue. If you've been exposed to multiple programming languages over your career, it's not too hard to learning the basics of another one. And I suppose mastering it will be just a matter of time and practice.

Learning new technologies or paradigms, like Kafka, can be slightly more challenging if one is new to the problems they solve. But reading documentation, playing around and asking more experienced developers has made the learning curve more approachable.

The real challenge, but also the real fun, has been having to think about different problems compared to mobile app development. Or rather, looking at similar problems from a different perspective.

For example, users are not any more people interacting with a gesture-based UI. They are now other engineers or applications using the APIs I'm designing.

Also, a mobile app normally deals with one user at a time, so availability is not the first concern when thinking about performance. But a backend application might receive hundreds, thousands, or millions of requests. This requires thinking about how it's going to cope with different workloads.

At the crossroads between consistency and availability, I don't necessarily have to worry about concurrency or performing tasks asynchronously at the OS level, which is quite common when developing mobile apps[^1].

However, I do need to pay attention to a different type of asynchronicity at the service level. One example is when a payment is sent multiple times and a load balancer forwards them to different instances of the same application.

When it comes to data storage, mobile apps that persist data on the device can make local optimisations about how these data is arranged. But now sometimes I have to work on a monolithic backend service that requires reconciling different concerns when designing the [schema](https://en.wikipedia.org/wiki/Database_schema).

Finally, releasing a mobile app through an official app store can take from half a day to multiple days. This was always a challenge in situations where I needed to address a serious issue. But deploying a backend application can be a matter of minutes if you have a decent [continuous delivery](https://en.wikipedia.org/wiki/Continuous_delivery) setup, which is great.

These are just some examples of the differences that stood up quite early on. And that’s without mentioning how much more enjoyable my development experience is now compared to using Xcode and Swift.

Working with [IntelliJ IDEA](https://www.jetbrains.com/idea/), an IDE that is consistently reliable and gives you powerful refactoring features, and a stable and mature language like Java, is a blessing. [Boring technology](https://boringtechnology.club/) works!

[^1]: Mobile apps have a main thread dedicated to rendering UIs on screen only, while non-UI tasks can be run concurrently on background threads. Some tasks are also commonly run asynchronously to avoid leaving the UI unresponsive. The typical example is apps waiting for responses to HTTP requests.
