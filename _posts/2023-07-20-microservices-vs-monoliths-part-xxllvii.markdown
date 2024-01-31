---
layout: post
title: "Microservices Vs. Monoliths, Part XXLVII"
date: 2023-07-20 15:10:33 +0800
categories: basics opinion
---
So,zI got sent this article several times, by several people:

[Scaling up the Prime Video audio/video monitoring service and reducing costs by 90%
The **move from a distributed microservices architecture to a monolith application** helped achieve higher scale, resilience, and reduce costs.](https://www.primevideotech.com/video-streaming/scaling-up-the-prime-video-audio-video-monitoring-service-and-reducing-costs-by-90).

If any of them asked, my opinion was always the same: although the underlying experience and refactor the article is based on is quite interesting, the article itself is bad. And the microservice to monolith framing is especially confused. 

I`ll let Adrian Cockcroft [speak for me](https://adrianco.medium.com/so-many-bad-takes-what-is-there-to-learn-from-the-prime-video-microservices-to-monolith-story-4bd0970423d4):

> The problem is that they called this refactoring a microservice to monolith transition, when it’s clearly a microservice refactoring step,

The same Adrian Cockcroft, [talking to NewStack](https://thenewstack.io/amazon-prime-videos-microservices-move-doesnt-lead-to-a-monolith-after-all/):

> This definitely isn’t a microservices-to-monolith story,It’s a Step Functions-to-microservices story.

Reading the article it becomes clear that the main performance issue was the use of AWS Step Function for something they weren't ready for. Removing Step Functions was the main reason for the gains (as an aside, that is great for me, a long time Step Functions skeptic).

They also joined two microservices into one. Maybe a little more monolithic, but a far cry from making the whole system a monolith.

### The Monolith/Microservice Continuum
The truth is that any modern, cloud based, system is unlikely to be totally a monolith. If you think about it, even the simplest realistic architecture is going to include two services: a web server and a database.

The question is always going to be when to break something into multiple services, and how small the services are going to be. Although there are tons of microservices best practices that give some guidance, there is always going to be a lot of subjectivity. And each team is going to have to decide where to place their system in the continuum between a single service and a multitude of very tiny services.

The article is, in part, about a slight adjustment in where they place the Prime Video system in that continuum.

### Remembering What Microservices Are For

If the article is not a strong case against microservices, why did it, or at least its framing, seem to resonate with so many people?

Some of it is just wanting to be a contrarian, for sure. An especially juicy proposition if you can say "wow, even Amazon is leaving microservices".

But I believe some of it has to do with a thing I have experienced myself in my work, which is the microservice as cargo cult mindset. Some people, especially younger engineers and architects, think micro services are good and monoliths are bad. So if any service gets a little bigger, starts to remind people even a little bit of a monolith, it must be broken into smaller services. Because microservices are good, and the monolith must be destroyed.

This kind of mindset is unmoored from the reasons behind the introduction of microservices, and thus fail to actually consider if they are a solution to the current problem. In fact, it doesn't even consider if there is a problem.

Being very high level, microservices were introduced as a solution to a few problems:

- The need to rebuild and redeploy the whole system everytime anything changes.
- Overhead of having to scale the whole application when you only need to improve performance in a specific part that is the bottleneck.
- The need for everyone to use one technology stack, even though different teams might have different expertises and different technologies being more adequate for different parts of the system.
- Difficulty of coordinating changes when different teams are working on the same large application.
- Need for every team to have knowledge of the whole codebase (related to the last one).

Each of these problems are real, but in theory there are other ways to mitigate them that don't involve breaking things into microservices.

In practice though, as teams get larger and larger, a lot of other solutions fail as it starts to get harder and harder to keep everybody on the same page and following the same best practices. 

That is why, after years of working with and studying microservices, I come to the conclusion that, mostly, *microservices are a technical solution to an organizational problem*.

Different from what some people seem to believe, turning a monolith into microservices almost always [*increases* the complexity of the system](https://martinfowler.com/articles/microservice-trade-offs.html) (making a system more distributed pretty much guarantees things get more complex). However, when done well, it`s a more complex system with parts that can evolve separately, allowing us to distribute the work better between teams and allowing each team to deal with a lower cognitive load, since they don't actually need to know the whole system.

Sometimes those things are really important and more than make up for the added complexity. Sometimes they don't.

### So, When Should I Use (Or Not) Microservices?

Or more specifically, when should you break a service in two (or more)?

The article actually gives a good example of a case where you shouldn't. In it there are two services that are *very* tightly coupled. One service is always executed after the other, and the output of the first service is the input of the second service. Also, it seems like the second service is the only one that consumes that output. This is a case where there are clear gains by keeping the services together (you can share memory and communicate that way, orchestration becomes simple) and the advantages of splitting the services is much less clear.

You want your microservices to be more loosely coupled. That is why microservices and event driven architectures go together well like chocolate sprinkles and butter[^1].

The specifics of your company also should help to decide how much to split. A strong DevOps platform, mature observability tooling and well understood, company wide, best practices all help to mitigate the complexity introduced by microservices. A big and growing workforce will be more likely to reap benefits from more splitting of services.

If the company is not that big yet, or the platform, tooling and best practices aren't that mature for now, consider developing bigger services and being more parsimonious with the splitting. And remember, a bigger service can still be developed in a modular manner, you don't need to actually split the service to split the code into logically separated parts.

### No Silver Bullets

When it comes to software architectures, almost no approach is inherently good or bad. It`s very tempting to just apply whatever the newest pattern or approach is, blindly (another technique to diminish cognitive load!) but the sad truth is we have to understand the reason for each architectural style to know if it applies in our specific case.

[^1]:On white bread. No, really, it's good.