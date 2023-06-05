---
layout: post
title:  "Before Anything, Make Sure You Know What The Problem IS"
date:   2023-06-04 15:10:33 +0800
categories: basics opinion
---
When I decided to start this blog I tried to think of what the most useful tip, advice or explanation I could give to fellow engineers and architects. What I ended up settling on is something that is actually not very technical, but that speaks to what is probably the most common mistake I see people making on a day to day basis.

The advice is this: before you try to solve a problem, make sure you actually know what the problem is.
Seems pretty obvious, no? The kind of thing you almost feel silly for saying. And yet, we in the field (yeah, including me) constantly fail to do this, and it leads to so much wasted effort.

From what I have observed, there are a few main reasons that lead us to this mistake.

### Confusing The Symptom For the Disease
The problem we can observe is often not the root problem, so if you don't stop and try to look deeper, you can end up throwing resources at the wrong thing.

One obvious example: you notice a specific service is taking long to respond when concurrent use increases, so you try to solve that by increasing the server size, or by distributing the service among more servers. However, the problem turns out to be something downstream (an expensive query is overwhelming the database, the service is calling a second service that is the actual bottleneck, etc).

### The "I Have Seen This Before" Syndrome

Pattern matching is at the core of human intelligence, and a big part of what we get from experience is more patterns to match to. But pattern matching can sometimes deceive us.

When we find a problem that looks just like a problem we have solved before, it's good to take a minute to make sure the problem really is the same, and that the same solution will apply.

### Falling In Love With The Hammer

We in tech are especially prone to making this mistake, and it's close cousin "look at this new shiny hammer I found, let's use it!".

We like cool tech, be it hardware, an AWS service, a library or an architectural pattern. We especially like cool tech we have just learned about. And it can be very tempting to believe that the problem we are having is exactly the kind of problem that tech solves. 

Unfortunately, a lot of problems require very dull, not that technically interesting solutions. So before just applying the cool solution to everything (*cough* microservices *cough*)  make sure the problem you have is the same problem the solution was created to address.

### Assuming The Customer Thinks Just Like You

An especially common mistake when working with frontends, although it crops up a lot when creating APIs that will be consumed by others too. 

There have been books written about this, but at the core we have to be willing to spend some time actually looking at how the customer is using the product and finding out what their expectations are. If we assume they are going to use it just like we would, we might have a lot of trouble to even reproduce the error, much less to actually find out what is causing it.

Relatedly, just assuming the user's description of what they are doing and what they are seeing is accurate can be quite dangerous too. Better to get some evidence, some traces or even better, to watch them use the system.

### Confusing Organizational Problems With Tech Problems

This is a tough one. 

People like me, with a technical background, are often very comfortable with solving things with a technical solution, and way less comfortable in finding social and organizational solutions. But when working in organizations that include a lot of other human beings (those messy, complicated things) we will run into problems that just don't have a technical fix.

A while back there was a team in a company I was working with where the technical leader was constantly proposing refactorings to a particular product. Those refactorings were meant to increase the productivity of the team, since there were a lot of complaints about the speed of delivery. But the refactorings didn't seem to be making a difference, so they asked me to take a look at it.

After talking with the team, analysing the architecture and observing their day to day for a while, it became clear that there was nothing wrong with the code or architecture (I mean, those things can always be improved, but nothing too wrong). However, there was a lot of confusion about the product definition, and even some disagreement between the Product Owner and the higher ups about what the product should actually do. That confusion was leading to a lot of wasted work, and to a mismatch between what the team was working on and what some stakeholders expected. All the refactoring in the world wasn't going to solve that.
The solution in that case turned out to be a lot of meetings to get everyone on the same page and get the definition straightened out. 

Obviously, meetings are not going to be our preferred solution to anything. Be every once in a while that is what the problem demands.

***

Ultimately, there is no silver bullet to avoid this mistake. But keeping those common pitfalls in mind, taking a minute to question yourself about how sure you are about what the problem is, and putting some effort into deeper investigations, can end up saving you a lot of time and grief.

