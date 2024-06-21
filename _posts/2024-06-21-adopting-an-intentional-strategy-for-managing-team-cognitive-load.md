---
title: "Adopting an Intentional Strategy for Managing Team Cognitive Load"
date: 2024-06-21 09:52:45.306409 +02:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
permalink: "/2022/12/20/my-observations-on-the-effects-of-CAPEX-and-OPEX-on-organisational-behaviour/"
comments: true
categories:
- Team Cognitive Load
tags:
- Online course
- Domain-Driven Design
- Team Topologies
- Digital Transformation
excerpt: I recently created an online cohort-based course, [Effectively Manage Team Cognitive Load](https://joaorosa.consulting/effectively-manage-team-cognitive-load). Since the release of [Team Topologies book](https://teamtopologies.com/book), I have adopted its language and principles in my consultancy practice, supporting organizations in their [digital transformation journey](https://joaorosa.consulting/services/digital-transformation). I've noticed in the field that more people are aware of the effects of unmanaged Team Cognitive Load in their teams and organizations, using the concept presented in the Team Topologies book to drive changes in their organizations.
---

I recently created an online cohort-based course, [Effectively Manage Team Cognitive Load](https://joaorosa.consulting/effectively-manage-team-cognitive-load). Since the release of [Team Topologies book](https://teamtopologies.com/book), I have adopted its language and principles in my consultancy practice, supporting organizations in their [digital transformation journey](https://joaorosa.consulting/services/digital-transformation). I've noticed in the field that more people are aware of the effects of unmanaged Team Cognitive Load in their teams and organizations, using the concept presented in the Team Topologies book to drive changes in their organizations.

By creating a learning environment where people are interested in deepening their knowledge about Team Cognitive Load and, at the same time, reflecting on their own context through the lens of Team Cognitive Load, we can find leverage points to create a humane and effective working environment. I always learn from my colleagues when I join cohort-based courses as an attendee. I'm always fascinated by the nuances in different contexts, and it is my goal to have a course that exposes those so we can learn from each other.

## One example from the field
Consider this example from an organization in the utilities sector undergoing a digital transformation. They are transitioning from a data center-centric to a cloud-native-centric approach, a shift that requires significant changes in their development and business operations teams. This short example, among many others, demonstrates the relevance of the sharp focus on managing cognitive load:
- They move from a Dev and Ops world to DevOps
- The primary mode of communication between services and applications will be events, which means that the go-to architecture pattern is an event-driven architecture
- Development teams will be responsible for their designs within the enterprise guidelines
- Business operation teams are heavily involved in the design process, increasing the business agility
- The release cycle goes down from a couple of months to a couple of hours

Those paradigm changes led the organization to adopt Domain-Driven Design principles and practices to shape its software services landscape and support its business ambitions. Using the Cognitive Load lens, the goal of having a [Ubiquitous Language (page 3)](https://www.domainlanguage.com/wp-content/uploads/2016/05/DDD_Reference_2015-03.pdf) is to lower the cognitive load of everyone involved with that particular service. At the same time, defining proper [Bounded Contexts (page 2)](https://www.domainlanguage.com/wp-content/uploads/2016/05/DDD_Reference_2015-03.pdf), allows the organization to strategically invest on the areas that will enable them to realize their ambitions.

Bringing everything together, you can see that development teams will experience an increase in intrinsic cognitive load since they need to learn new technology and patterns to support their architectural changes. However, by using Domain-Driven Design principles and practices, the shift will move to germane cognitive load, where they focus on the purpose of their domain.

One of the teams went through all of these phases, where they invested in creating a space where they could model, together with the business, their language, and the essential aspects of the model. Once they concisely and crisply defined their model, they discovered it was not reflected in the code! This factor influences Team Cognitive Load, where people need to constantly make connections between a domain concept and a code concept. The solution for the team to manage their cognitive load was to refactor both the code and the underlying cloud infrastructure to match the Ubiquitous Language. Refactoring the code was easy since they used the power of the IDE; however, changing the names in the infrastructure took more time and a well-crafted plan since they couldn't afford production outages. They do all of this because they want to protect their own well-being. Imagine that you are on call, and the service is down. By having the infrastructure name match the domain concepts, they can easily navigate what is going on, and under stress (yes, we all been there) at 3:00 in the morning when we should be resting.

## What to do next?
The course will cover a range of tools and patterns that can help you better understand and manage Team Cognitive Load. We will discuss tools for mapping the landscape of a team and organization, identifying potential sources of cognitive load, and patterns for team cognitive load management. Additionally, the course encourages participants to bring their own examples and share the nuances of their context, fostering a collaborative learning environment where we can collectively address blind spots and challenges.

Will I see you there?