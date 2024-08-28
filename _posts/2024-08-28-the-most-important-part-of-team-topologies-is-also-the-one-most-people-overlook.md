---
title: "The most important part of Team Topologies is also the one most people overlook"
date: 2024-08-28 13:29:20.705487 +02:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
permalink: "/2024/08/28/the-most-important-part-of-team-topologies-is-also-the-one-most-people-overlook/"
comments: true
categories:
- Team Topologies
tags:
- Team Interaction Modeling
- Organization Design
excerpt: We sometimes hear criticism that the Team Topologies approach is incomplete, as it doesn't allow people to map the whole organizational chart. People like to create maps and charts, and there will probably always be ideas and approaches trying to map the entire universe of an enterprise. Team Topologies is not one of those.
---

Last year, during [FastFlowConf](https://www.youtube.com/watch?v=qHBQm1vKKXQ), Matthew Skelton answered questions about what had changed/evolved since the Team Topologies book was published. In his own words, they (both authors) should have emphasized the team interactions and the evolution of the topologies over time as central themes for achieving a fast flow of value.

We sometimes hear criticism that the Team Topologies approach is incomplete, as it doesn't allow people to map the whole organizational chart. People like to create maps and charts, and there will probably always be ideas and approaches trying to map the entire universe of an enterprise. Team Topologies is not one of those.

People should look at Team Topologies as a way of thinking or a pattern language. Team Topologies aims to help leaders design for a fast flow of value. It allows you to design a team-of-teams organization, which, combined with a relevant decoupled architecture of products and the appropriate processes (think Continuous Delivery as one example), allows even big organizations to achieve fast flow of value. Unlike organizational charts, the resulting diagrams are just a starting point and must continuously evolve as the organization grows and changes along with the environment in which it operates. This is why we often tell people to consider Team Topologies more like Design Thinking, i.e., an iterative and continuous process that helps you understand complex challenges and find optimal solutions.

The [Team Topologies](https://teamtopologies.com/book) book was released in 2019, and the approach has continued to evolve. The community is creating new techniques and practices to help practitioners looking to adapt their organizations for fast flow. Those new techniques typically combine the Team Topologies approach with other methods and ideas, e.g., Wardley Mapping or Domain-Driven Design. The common denominator of all is the focus on accelerating the flow of value at scale. If you take a closer look at one of the new techniques of the Team Topologies approach, [Team Interaction Modeling](https://teamtopologies.com/key-concepts-content/team-interaction-modeling-with-team-topologies), you can see how central the “Flow of value” is. This is one of the evolutions pointed out by Matthew at FastFlowConf, where the flow of value in the book’s diagrams is implicit. Team Interaction Modeling makes the flow of value explicit by having a dedicated shape, the “Flow of value” arrow.

## So, what is the new idea here, João?
As a Team Topologies practitioner since the book's release, I frequently use the Team Topologies approach as a pattern language to discuss organization evolution with customers. Based on the customers' strategic ambitions, we explore the options to evolve the organization so that the teams can achieve these ambitions and simultaneously have a humane organization. As [Team Topologies is hitting the “Slope of Enlightenment”](https://www.linkedin.com/feed/update/urn:li:activity:7211313895955668992/) in one of the Gartner Hype Cycles, I see more and more organizations asking to be a “Team Topologies organization”. Well, I think the goal is not to be a “Team Topologies organization” but rather leverage the patterns and principles of Team Topologies (and other fitting pattern languages, approaches, and techniques) ***to safely evolve the organization***!

When you work in a smaller organization, a startup, or just focus on a structure with a couple of teams building a product, things are obvious and intuitive. The challenges emerge once you try to model organizations with dozens or hundreds of teams. Trying to map all of those teams in one diagram is not feasible, and it is also not useful for the purpose of the Team Topologies approach, as mentioned earlier. It gets messy fast as there are multiple flows of value to consider since a bigger organization would often have multiple value streams, business units, customer segments, and whatnot.

![A messy Team Interactions Modeling diagram, which doesn't follow the rules, and tries to represent the full enterprise](/images/blog/2024-08-28-the-most-important-part-of-team-topologies-is-also-the-one-most-people-overlook-diagram-1.JPEG)

*Figure 1 - Trying to represent a big chunk of an imaginary organization. A bit of a messy representation, and it can be even messier for modern enterprises with even more lines of business…*

I want to address this challenge in this article: **how do we make the flows of value visible in bigger organizations that have multiple lines of business and value streams?** 

The solution starts with *being explicit about the flow of value* that we are mapping. By writing the use case within the “Flow of value” arrow, we can focus the group's attention on mapping one particular line of business or a value stream inside a business line, with all the nuances involved. In my experience, as many big enterprises are well-integrated across lines of business, other related use cases will emerge in the mapping process, and we note those to analyze later separately. What happens in bigger organizations with multiple services, products, and value streams is that, ultimately, we will have *multiple maps* focused on different flows of value. And this is the essence of Team Topologies that is often overlooked: the focus on the flow of value rather than hierarchical relationships between people and managers. Organizations that prioritize *how they deliver value* over who reports to whom can create a generative working environment that is not only enjoyable but also makes the company more successful than its competitors.  

There is nothing better than a deep dive into examples that I hope most of us can relate to. This was the subject of a discussion with [Matthew Skelton](https://www.linkedin.com/in/matthewskelton/) in March this year (2024) in Cork, Ireland.

## How to overcome the challenge of mapping multiple flows of value
This year at [FlowCon](https://joaorosa.consulting/speaking/flowcon-intentional-architecture) in Paris, I presented how organizations deliver value (as networks - a topic for a whole separate post) and how we can be explicit when discussing use cases. For the purpose of illustration, let's use an example of the common functions inside an organization - Human Resources (HR) and Internal Information Technology (IT), which can each be platforms on their own.

Let's explore the first use case, where the Internal IT platform supports HR and other teams within the company.

![A Team Interactions Modeling diagram where the Internal IT platforms offers services to the HR platform](/images/blog/2024-08-28-the-most-important-part-of-team-topologies-is-also-the-one-most-people-overlook-diagram-2.JPEG)

*Figure 2 - Diagram of the interaction mode of the Internal IT platform when others can use the software from the enterprise catalog*

Enterprises have software catalogs that different people use. Those catalogs are a way to avoid compliance and security issues. Imagine if someone uses software that is not properly licensed or verified for security flaws. It puts the organization at several compliance and security risks. The central catalogs also allow for economies of scale as organizations can get better deals for non-differentiator software, such as the productivity suite, accounting and finance suite, etc.

In this case, this organization has an Internal IT platform with several stream-aligned teams. One of those teams is responsible for the internal software catalog, streamlining the process for the rest of the staff to use it. Using the Team Topologies patterns, the internal platform offers its services as X-as-a-Service, where others can self-serve it.

## But what if a team needs software that isn't part of the catalog (yet)?
![A Team Interactions modeling diagram, that has a new scope of value: discover the needs for the new Learning Management System](/images/blog/2024-08-28-the-most-important-part-of-team-topologies-is-also-the-one-most-people-overlook-diagram-3.JPEG)

*Figure 3 - Diagram for the teams collaborating across the platforms to discover the needs for the new Learning Management System*

As you can see in Figure 3, a team in the Internal IT platform collaborates with multiple teams in the HR platform for this specific use case: the organization requires a new Learning Management System to better support staff self-paced learning paths.  

Those teams Collaborate for a fixed period of time, during which they clarify the requirements, risks, costs, and migration path between the different Learning Management Systems. After the new system is live and the stabilization period is over, the Collaboration ends, and they return to the previous (Figure 2) Team Topologies' interaction mode.

## How about the services offered by HR?
![A Team Interactions Modeling diagram, where the HR platform offers the recruiting staff service for everyone](/images/blog/2024-08-28-the-most-important-part-of-team-topologies-is-also-the-one-most-people-overlook-diagram-4.JPEG)

*Figure 4 - HR typically offers recruitment services, where they streamline processes and connections to recruitment agencies and recruitment platforms*

This diagram represents a different use case: recruiting staff. It shows the HR platform at the bottom, since it offers services for everyone in the company. Remember the rules of Team Interaction Modeling: platforms provide their services “up” for others to consume. You can imagine the typical services offered by HR, such as a streamlined recruitment process, where they manage the different commercial relationships with recruitment agencies, recruitment platforms, and such.

## What if the Internal IT platform needs different content from the Learning Management System?
![A Team Interactions Modeling diagram, where the HR platform collaborates with a different team to discover what content is needed in the Learning Management System](/images/blog/2024-08-28-the-most-important-part-of-team-topologies-is-also-the-one-most-people-overlook-diagram-5.JPEG)

*Figure 5 - Team Interactions Modeling diagram when the Internal IT platform needs new learning content*

Well, the answer is the same. The teams collaborate for a fixed period of time to discover the user's needs. Imagine that the folks from the Internal IT platform have different needs, such as managing Large Language Model (LLM) tools at an enterprise level. They need to identify the best way to discover and acquire the content to be present in the Learning Management System. That content could be helpful for other teams in the organization; who knows. This is also a positive side effect of considering platforms as boundaries for groups of services and treating your platforms as products.

# Sum it up
As you can see, what I'm proposing to improve within Team Interaction Modeling is to be explicit about the use case within the “Flow of value” arrow. By starting to agree on what we are modeling, we can have a visual anchor that allows us to contextualize and frame the discussion. Other important bits and pieces can emerge from the use case, and they should. I've been testing this approach for more than a while now, and it helps groups to focus on the challenge at hand and, at the same time, capture eventual scenarios to be modeled later.

Remember that Team Interaction Modeling diagrams are not only **bounded in time** but also **bounded in scope**!
