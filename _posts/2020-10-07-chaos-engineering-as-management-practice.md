---
title: 'Chaos Engineering as management practice'
date: 2020-10-07 11:22:51.000000000 +02:00
type: post
parent_id: '0'
published: false
password: ''
status: draft
permalink: "/2020/10/07/chaos-engineering-as-management-practice/"
comments: true
---
Chaos Engineering is a practice that has its roots at Netflix. It born from the challenges of moving their workloads from the data centre to the cloud; the transient nature of the cloud affected the way that they build and operate a system at scale. The initial project was call [Chaos Monkey](https://netflixtechblog.com/the-netflix-simian-army-16e57fbab116), and it has almost 10 years.

Since then the community grow, fueled by Netflix practitioners. Today there are commercial and open-source tools, and we can see more initiatives in different t communities. The technical practices had matured, and the knowledge started to spread in the IT world. 

However, it is deemed perceived as a technical practice. Can we leverage Chaos Engineering as a management practice?

#### Role of a manager in today's world

The role of a manager has changed. From a prescriptive approach, where the manager is leading the activities of people (managing and sometimes micromanaging), towards a supportive and transformational role. Today a manager needs to give structure and create a safe space for people and teams to excel in their fields.

Organisations require managers that take a leadership role in creating *safety* for both individuals and teams.

But what are practices a manager should embrace?

#### Dynamic Safety Model

The *Dynamic Safety Model* was described by Jens Rasmussen in his paper titled [Risk management in a dynamic society: a modelling problem](https://www.sciencedirect.com/science/article/pii/S0925753597000520). It can be illustrated by the following picture:
![Ilustration of the Dynamic Safety Model](/images/assets/2020-09-04-chaos-engineering-as-management-practice-dynamic-safety-model.png)

[Casey Rosenthal](https://twitter.com/caseyrosenthal) and [Nora Jones](https://twitter.com/nora_js) in the book [Chaos Engineering, System Resiliency in Practice](https://www.oreilly.com/library/view/chaos-engineering/9781492043850/) summarises the *Dynamic Safety Model* in Economics, Workload and Safety, where software engineers areec good into understand the limits and trade-offs with economics and workload. Still, we often miss theh limits and trade-offs in safety. I agree with the analysis, and I learned in my career the same. Sometimes I underestimate my decisions towards safety, and another I overestimate. Which made me retrospect based on the learnings of the past decade.

#### My retrospective

As a software engineer, I often focus on solving the problem at hand, and as a manager trying to optimise for maximising the value delivering. And as interim CTO and consultant, I help organisations to change their operating models to accommodate a fast-changing world. As part of my retrospective, I discover that we try to induced change into organisation, even when we take into [consideration human aspects](https://www.joaorosa.io/2020/08/18/using-team-topologies-to-discover-and-improve-reliability-qualities/), when a stressful event happens in the new model, people (and teams) usually fall back to the old behaviour. As a trivial example, I observed and worked together with organisations that moved from a siloed environment to end-to-end responsible teams. Where the responsibilities of creating and operating software are in different teams and/or departments, to end-to-end responsibly teams (we can call them DevOps), where they need to design, build, release and operate the software in production. However, in an outage scenario, the teams have problems to react and fix the issue, due to the fact they are not used to operate in the new context. Hero culture often arises, where individual contributors are the ones solving the problems. In the long run, it is not sufficient and can lead to a dysfunctional and toxic culture.

I believe that managers can create safety, and coach and mentor engineers to improve their decision-making process regarding the safety limits. At the same time, having a positive effect on the organisation culture towards an open and trustworthy culture. 

#### Declare your intents

As system thinker, declared intention in a system is crucial. Together with colleagues, we are exploring a concept called Intent Oriented Architecture, wherefrom social and technical angles we are explicit about the intentions of a team and the solution (often software). I'm not trying to predict behaviour, but rather be explicit about my intentions, and the software that I produce. It is valid at all layers of the organisation. It is also the base of any operating model. But base on my experience declares intent is not enough. We need to verify and test our assumptions, namely on the safety limits of the system (you can read my definition of a system [here](https://www.joaorosa.io/2020/06/25/what-does-mean-system-in-the-socio-technical-land/)). 

Based on the role of a manager in today's world, how can we help individuals and teams to test the safety of the system (people, processes and technology)?

#### Chaos Engineering and management

Well, we get back to the title of this blog post. Chaos Engineering! Not only as technical practice for the resilience of the software but more critical to the ability of a organisation to by truly adaptative, e.g., anti-fragile. As I mentioned before, a system is the intersection of people, processes and technology, and a manager was a tool to induce controlled experiments into the system to teams and individuals practice their ability to cope with that event. Not only if the software has the right measures in place, but if the process is adequate for the context of the organisation. It is very similar to the way of working of first responders, namely firefighters: 80% of their time is practising, and 20% are in action. 

We can adopt Chaos Engineering as a management practice to lead the organisation to an anti-fragile state, creating a safe environment for people and teams to excel. As some organisations demonstrate, when the environment is safe, people unleash their superpowers.

How do you create a safe environment? 