---
layout: post
title:  "Microservices Vs. Monoliths, Part XXLVII"
date:   2023-07-20 15:10:33 +0800
categories: basics opinion
---
When I decided to start this blog I tried to think of what the most useful tip, advice or explanation I could give to fellow engineers and architects. What I ended up settling on is something that is actually not very technical, but that speaks to what is probably the most common mistake I see people making on a day to day basis.

The advice is this: before you try to solve a problem, make sure you actually know what the problem is.
Seems pretty obvious, no? The kind of thing you almost feel silly for saying. And yet, we in the field (yeah, including me) constantly fail to do this, and it leads to so much wasted effort.

From what I have observed, there are a few main reasons that lead us to this mistake.

### The Monolith/Microservice Continuum
The problem we can observe is often not the root problem, so if you don't stop and try to look deeper, you can end up throwing resources at the wrong thing.

One obvious example: you notice a specific service is taking long to respond when concurrent use increases, so you try to solve that by increasing the server size, or by distributing the service among more servers. However, the problem turns out to be something downstream (an expensive query is overwhelming the database, the service is calling a second service that is the actual bottleneck, etc).

### Remembering What Microservices Are For

If the article is not a particulary strong case against microservices, why did it, or at least it's title, seem to resonate with so many people?

Some of it is just wanting to be a contrarian, for sure. But I believe some of it has to do with a thing I have experienced myself in my work, which is the microservice as cargo cult mindset. Some people, especially for some younger engineers and archiechts, think micro services are good and monoliths are bad. So if any service gets a little bigger, starts to remind people even a little bit of a monolith, it must be broken into smaller services. Because microservices are good, and the monolith must be destroyed.

This kind of mindset is unmoored from the reasons behind the introduction of microservices, and thus fail to actually consider if they are a solution to the current problem. In fact, it doesan't even consider if there is a problem.

Being very high level, microservices were introduced as a solution to a few problems:

Mostly, *microservices are a technical solution to an organizational problem*. 

Different from what some people seem to believe, turning a monilth into microservices almost always *increases* the complexity of the system (making a system more distributed almost always makes things more complex). However, when done well, it`s a more complex system with parts that can evolve separetly, allowing us to distribute the work better between teams and allowing each team to deal with a lower cognitive load, since they don't actually need to know the whole system. 

Sometimes those things are really important and more than make up for the added complexity. Sometimes they don't.

### So, When Should I Use (Or Not) Microservices?

Or more especifically, when should you break a service in two (or more)? 

The article actually gives a good example of a case where you shoudln't. In it there are two services that are *very* tighly coupled. One service is always executed after the other, and the output of the first service is the input of the second service. Also, it seems like the second service is the only one that consumes that output. This is a case where there are clear gains by keeping the services together (you can share memory and communicate that way, orchestration becomes simple) and the advantages of splitting the services is much less clear.

You want your microservices to be more loosely coupled. That is why microservices and event driven architechtures go together well like chocolate sprinkles and butter.

The specifics of your company also should help to decide how much to split. A strong DevOps plataform, mature observability tooling and well understood company wide best pratices all help to mitigate the complexity introduced by microservices. A big and growing workforce will be more likely to reap benefits from more splitting of services. 

If the company is not that big yet, or the plataform, tooling and best pratices aren't that mature for now, consider developing bigger services and being more parciminious with the splitting. And remember, a bigger service can still be developed in a modular manner, you don't need to actually split the service to split the code into logically separated parts.

### No Silver Bullets

When it comes to software architectures, almost no approach is inherently good or bad. It’s very tempting to just apply whatever the newest pattern or approach is blindly (another technique to diminish cognitive load!), but the sad truth is we have to understand the reason for each architectural style to know if it applies in our specific case.

*On white bread. No, really, it's good.