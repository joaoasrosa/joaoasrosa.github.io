---
title: 'Diverge and converge to create a Context Map'
date: 2020-10-23 11:22:51.000000000 +02:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
permalink: "/2020/10/23/diverge-and-converge-to-create-a-context-map/"
comments: true
categories:
- Collaborative modelling
tags:
- Domain-Driven Design
- Context Map
- Software Architecture
excerpt: My experiences of applying some Design Thinking techniques to my Context Mapping workshops
---

Context Map was the first visualisation for the Bounded Context pattern from Domain-Driven Design. In a nutshell, it is a map of the different Bounded Contexts and their relationships. I tend to create a Context Map during or after a Big Picture EventStorming. Changing perspectives can be helpful, to challenge assumptions and get the best of different techniques.

However, sometimes it is hard to reach a consensus on the Context Map. I often operate in brownfield projects, with large organisations. Although people agree with the different bounded contexts, it is a process that takes time, and most significant energy. Which can lead to fatigue towards the method, and at the same time raises exciting patterns in the behaviours. But this blog post is not about emergent behaviour. :)

To tackle it, and inspired by the [Divergence and Convergence cycles](https://www.seanvantyne.com/2017/02/19/design-thinking-divergence-convergence-cycles/) from Design Thinking, I start to apply the same pattern to my Context Mapping workshops. After a Big Picture EventStorming, I give the theory about Bounded Contexts and Context Mapping. You can find useful resources from the [DDD Crew](https://github.com/ddd-crew/context-mapping). 

I split the group into small groups of 3 to 4 people. Each group needs to create a Context Map for their domain, using the output of the EventStorming. As they generate insights, they challenge the EventStorming, documenting it. We can have several rounds, timeboxed (the wonders of timeboxing). After that, each group do a show and tell about their reasoning and thought process. People can ask questions, challenging their model. As the process goes, we collect these questions and ideas. This is what I call the diverge phase. Each group creates their own version of the Context Map, but because the discussion is in small groups, it can be more effective. 

The next phase is to start to converge. I ask one person to volunteer and to get all the bounded contexts from the different groups that are the *same*. In this case, we can get 50% to 80% of the Context Map done, with the advantage that is the part that people agree with each other. It avoids the fatigue of rehashing discussions. The next step in this phase is to start to decide on the "leftovers", each needs more time to discuss. From my experience, this step is the most interesting one, because people have their own mental models about the bounded contexts. Focusing the energy to discuss the differences and trade-offs of the boundaries leads to a better outcome, and I can guide people over the discussion on the boundaries of the more complicated and complex problems. This last step can take a few hours, or a few sessions over time, depending on the size of the domain. As a rule of thumbs, I tend to split over multiple sessions, to allow people to think about it. Some of the best ideas happen in the shower!

You may ask if it is useful both physically and remotely. And the answer is yes. Physically you need more modelling space, where groups can discuss but not bias each other. Online you need tools that allow people to be isolated in their own room. In the end, it will produce the same output.

I'm wondering about your experiences. How do you get consensus over a Context Map?