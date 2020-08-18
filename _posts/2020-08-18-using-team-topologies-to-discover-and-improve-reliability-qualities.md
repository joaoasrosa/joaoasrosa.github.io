---
title: 'Using Team Topologies to discover and improve reliability qualities'
date: 2020-08-18 11:22:51.000000000 +02:00
type: post
parent_id: '0'
published: false
password: ''
status: publish
permalink: "/2020/08/18/using-team-topologies-to-discover-and-improve-reliability-qualities/"
comments: true
---

[Team Topologies](https://teamtopologies.com/) is the work of [Matthew Skelton](https://twitter.com/matthewpskelton) and [Manuel Pais](https://twitter.com/manupaisable), and I use it as part of my job. From a sociotechnical perspective, a team-first approach is paramount for any organisation and helps to decrease the accidental complexity. As such, I'm often asked "How can we operate in DevOps?" or "How can I have a reliable service to deliver value to my customer?".

#### TL;DR
Combining Team Topologies from the DevOps movement, with Context Mapping form the Domain-Driven Design community, can give insights about the *potential* friction contact points between software engineering teams. Below you can find how it can be combined and how to generate ideas to drive your organisations to new performance levels, creating a safe and healthy working environment.

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

#### Let's visualise one example
Using a fictional case, where a company provides a SaaS solution to analyse sales leads (I don't have an idea is this exists or not, maybe a business idea). Analysing the Team Gold, responsible to over the service that qualifies a lead, we can have the following Team Topologies:
![Team Topologies for Team Gold](/images/assets/2020-08-04-using-team-topologies-to-discover-and-improve-reliability-qualities-teamtopologies.png)

As you can see, I placed the Team Gold in the middle of the diagram. Also, the rest of the teams have names related to their purpose, and I will let your imagination to fill the technology details. Now, in this fictional case, Team Gold is asked to improve the *cycle time* of features to production, since they are losing their differentiative features to the competition. Based on Team Topologies, we can see that there are different interaction modes with various teams that **might** affect the feature cycle time.

Although we can see some room for improvement there, using a Context Map also can indicate what the level of flexibility on the relationships between bounded contexts is, and by extension, the teams who own those:
![A Context Map with the relevant bounded contexts](/images/assets/2020-08-04-using-team-topologies-to-discover-and-improve-reliability-qualities-contextmap.png)

For this exercise, let's say that the Team ERP owns the bounded context Lead Information, the Team CRM owns the bounded contexts Customer Information and Customer Analytics, and the Team Gold owns the bounded contexts Qualified Leads and Leads Analytics. Doing a quick analysis, we can spot that although the relationships between the Team Gold and Team ERP is X-as-a-Service, in reality, the Qualified Leads is conformist to Lead Information. If the Team ERP decides to make changes to their bounded context, it will have cascading failures for the Team Gold. On the opposite direction, the relationship between Lead Analytics and Lead Information is customer-supplier, where Team Gold has influence over the decisions made by Team ERP. Last but not least, we have a team to manage documents; however, none of the bounded contexts is related to it. In this example, mismatches like this can be a potential cause of friction between teams, since the functional needs are not aligned with the sociotechnical needs, e.g., team boundaries and technological decisions. 

In this naïve example, we can see the potential to improve on the alignment of teams to the functional needs. From my experience, it was the first step to discover and improve reliability qualities. If the responsibilities of the teams are aligned with the bounded contexts, and the teams work towards the most beneficial interaction modes, it improves the system reliability. For organisations that are adopting different collaboration patterns, it is a great starting point to discover the boundaries from a product level; what are the teams and bounded contexts that are involved, and what might/should change to achieve the desired reliability. Designing organisations with that in mind (in other words, the essential complexity) can lead to better collaboration between teams, while maintaining their autonomy.

#### Heuristics
A small list of heuristics that can be used to generate insights:
* Team interactions match context relationships
* Invest on the team environment, then on the technology
* Improve reliability by improving team interactions

#### A readers note
I mainly operate in complex environments, highly regulated, with hundreds of teams. Your context is different, take my experience with a pinch of salt!