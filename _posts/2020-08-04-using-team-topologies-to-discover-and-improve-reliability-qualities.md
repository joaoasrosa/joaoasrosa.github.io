---
title: 'Using Team Topologies to discover and improve reliability qualities'
date: 2020-08-04 11:22:51.000000000 +02:00
type: post
parent_id: '0'
published: false
password: ''
status: draft
permalink: "/2020/08/04/using-team-topologies-to-discover-and-improve-reliability-qualities/"
comments: true
---

[Team Topologies](https://teamtopologies.com/) is the work of [Matthew Skelton](https://twitter.com/matthewpskelton) and [Manuel Pais](https://twitter.com/manupaisable), and I use it as part of my job. From a sociotechnical perspective, a team-first approach is paramount for any organisation and helps to decrease the accidental complexity. As such, I'm often asked "How can we operate in DevOps?" or "How can I have a reliable service to deliver value to my customer?".

#### Service reliability qualities
There are different reliability qualities, and we have literature about it. Think about the [SRE](https://landing.google.com/sre/) books from Google or [Building Evolutionary Architectures](https://www.thoughtworks.com/books/building-evolutionary-architectures) from [Neal Ford](https://twitter.com/neal4d), [Rebecca Parsons](https://twitter.com/rebeccaparsons) and [Patrick Kua](https://twitter.com/patkua). They describe different qualities for digital services and different approaches to it. But before getting those concepts into action, *How does it affect the team(s)?*

#### Sociotechnical thinking into action
To answer to that question, I use Context Mapping and Team Topologies in a workshop mode (lately in a remote mode; I will share my experiences in a later post) to visualise the (1) domains, bounded contexts and their interactions, and (2) the teams and how they interact. Following this path it allows the people involved to see the complexity of their landscape and how the teams are organised to create solutions for the problem space.

Having these insights, both from a social and technical perspective, it enables people to reason about their design choices. By design choices, I mean the organisation of teams and individuals (organisational design) and the technical design (solution/software architecture). Hence, the **sociotechnical** thinking, where the concept of a team is not an after-thought.

#### Right, nice introduction. How about my service reliability qualities?
Yes, I know the title of the post. :) I'm about to get there, but first I want to write about another important concept. *Complexity*, namely on software land. [Frederick P. Brooks Jr.](https://en.wikipedia.org/wiki/Fred_Brooks) wrote the paper [No Silver Bullet - Essence and Accident in Software Engineering](http://worrydream.com/refs/Brooks-NoSilverBullet.pdf) back in 1986, where he describes two types of complexity: **essential complexity** and **accidental complexity**. Complexity is inherent to a distributed system (as a thought exercise you can think about the stack to connect *one web server* to *one database server*), and we build complex solutions from complex problems. More often than we expect, the solutions grow organically (using [Kent Beck](https://twitter.com/KentBeck) punch line, we don't know any other type of growth), but unfortunately it almost by accident; the complexity of the solution outgrows the complexity of the problem.

Back to service reliability qualities: I witness people demanding more *availability* (or any other *-ility*) for service X. And again, teams keep adding components to *try* achieve it, adding more cognitive overhead. Aware of it (I'm guilty because I had the same behaviour in the past), I started to look to the problem from another angle: what if the answer is in the way that teams interact, rather than throw more technology at it?

Using the insights from the Context Map and the Team Topologies, we can reason about the organisational design to achieve the desired service reliability qualities. Usually, I have a few questions, such as:
* Does the flow of value crosses multiple teams? If so, what are those team types? A mix of platform and stream-align?
* Do they belong to the same department or different departments?
* Do they have the same managers?
* Are the teams co-located, or are they in different timezones?
* Are we sharing models across different bounded contexts?
* Do we need to revise our SLA/SLO/SLI?
* Should we adopt living documentation?
* How many handovers do we have?

In my experience, taking a look at how the teams interact and how we layout our solutions is a great start to discover and improve service reliability qualities, before changing the technical aspects. As an organisation grows, the complexity increases, and it is important to make design decisions to cope with the complexity. The essential one!

#### A readers note
I mainly operate in complex environments, highly regulated, with hundreds of teams. If you have a smaller context, take my experience with a pinch of salt!