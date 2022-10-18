---
title: "Mental models: a reflection on AWS outage"
date: 2021-01-11 12:00:00.000000000 +02:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
permalink: "/2021/01/11/mental-models-a-reflection-on-aws-outage/"
comments: true
categories:
- Sociotechnical systems
tags:
- Autonomy
- Agency
- Team
- Chaos Engineering
- Management
- Complexity theory
- Cynefin
- Wardley Maps
excerpt: My reflection on the recent AWS outage (November 2020). Rather than focus on the technical aspects, and how technical dependencies can be managed, I will deep dive into social aspects; namely the mental models, and how they play in a sociotechnical system under stress. I will share my experiences in how to escape from the reliability trap
---

In November 2020 AWS had a major outage, which started with their Kinesis service, having a cascading failure over some services. Several articles and analyses of the outage, including the [official note](https://aws.amazon.com/message/11201/) from AWS. This blog post reflects the outage, but rather focus on the technical aspects, I will deep dive into the social ones, namely mental models.

### Pre-reflection, what is a mental model?

I will borrow two definitions for the mental models; the first one from Kenneth Craik:

> If the organism carries a "small-scale model" of external reality and of its own possible actions within its head, it is able to try out various alternatives, conclude which is the best of them, react to future situations before they arise, utilise the knowledge of past events in dealing with the present and future, and in every way to react in a much fuller, safer, and more competent manner to the emergencies which face it.

And the second one from Jay Wright Forrester, where he defines general mental models:

> The image of the world around us, which we carry in our head, is just a model. Nobody in his head imagines all the world, government or country. He has only selected concepts, and relationships between them, and uses those to represent the real system.

I can say that a *mental model* is a representation of concepts and their relationships, which help us to reason about a problem/challenge/whatever needs mental capacity. It is influenced by our bias, past experiences, knowledge and information. We use these models to try to anticipate future events, and it shapes our behaviour. Our mental models are not static, they evolve, although we are not aware of it most of the time. Note that I'm not a specialist in behavioural or cognitive science, and there is more behind it, but we can stick with these definitions and my own spin for now.

### My reflection

On the [AWS official note](https://aws.amazon.com/message/11201/), towards the end of the message, it states:

> Outside of the service issues, we experienced some delays in communicating service status to customers during the early part of this event. We have two ways of communicating during operational events – the Service Health Dashboard, which is our public dashboard to alert all customers of broad operational issues, and the Personal Health Dashboard, which we use to communicate directly with impacted customers. With an event such as this one, we typically post to the Service Health Dashboard. During the early part of this event, we were unable to update the Service Health Dashboard because the tool we use to post these updates itself uses Cognito, which was impacted by this event. We have a back-up means of updating the Service Health Dashboard that has minimal service dependencies. While this worked as expected, we encountered several delays during the earlier part of the event in posting to the Service Health Dashboard with this tool, as it is a more manual and less familiar tool for our support operators. To ensure customers were getting timely updates, the support team used the Personal Health Dashboard to notify impacted customers if they were impacted by the service issues. We also posted a global banner summary on the Service Health Dashboard to ensure customers had broad visibility into the event. During the remainder of the event, we continued using a combination of the Service Health Dashboard, both with global banner summaries and service-specific details, while also continuing to update impacted customers via Personal Health Dashboard. Going forward, we have changed our support training to ensure that our support engineers are regularly trained on the backup tool for posting to the Service Health Dashboard.

I was drawn to this paragraph, and it is the reason for this blog post; mental models and the ripple effects on a sociotechnical system. As stated in the paragraph, AWS service operators have a backup procedure to update the Service Health Dashboard. I notice the delays, where the publicly available information was reporting that everything was fine, but services running on top of the AWS cloud where down. And the well known [DownDetector](https://downdetector.com/) was reporting the outage.

I assume that AWS services are stable (actual top of the line, a *fact*), and people got used to the reliability of the services; people don't factor in their mental models, in this case, the secondary processes during an outage (this is my *assumption*). From my experience in the industry, we don't test the incident procedures (whatever the type of incident); we still have a road to learn from other industries, where they mature the practices to decrease the risks during an outage. I felt into this trap and saw my peers do the same (this is the start of my *reflection*). I call it the **reliability trap**.

### How to escape from the reliability trap?

The reliability trap is common in our industry. I describe the reliability trap when people, teams and organisations take IT systems and processes as granted, leading to simplified versions of their mental models. It is common when organisations have outstanding engineering practices, and the IT systems are highly reliability (Amazon example) or when the IT systems and processes didn't suffer from a diversity of use cases (increase in the load or people using those for other porpuses that are not the initial intent).

During my years as an engineer, architect, consultant and CTO, I "developed" ladders to get out of the trap and increased my awareness of it. My goal is to avoid falling into the reliability trap again. I will summarise my learnings and why I use it.

First and foremost, I use [Wardley Maps](https://medium.com/wardleymaps) to model the components that underpin the company's scope, which I work with; It helps me to develop an awareness of the landscape, and I can generate different options for the various components (think about what-if type of scenarios). Next to it, and because we operate in sociotechnical systems, I practice and use sense-making, which I borrowed from [Cynefin](https://hbr.org/2007/11/a-leaders-framework-for-decision-making). Rather than drawing my own conclusions, based on my mental models (which are highly influenced by my bias and assumptions), I use the sense-making practices and tools to generate insights. Having those two practices and steps together helped me reason how people perceive their roles and their processes.

To verify the potential consequences of the options generated, I practice [Chaos Engineering](https://principlesofchaos.org/). Although Chaos Engineering bornt at the technical level, I also use it at **processes** and **organisational levels**. The principles are the same, but we don't have the same tools available. We are humans, and we can leverage our creativity to design experiments to verify our assumptions at a broader scope. The goal is to verify how the sociotechnical system behaves, how people and teams engage, and if the processes are followed or are outdated. You can find more details in a [previous post](https://joaorosa.io/2020/10/21/chaos-engineering-as-management-practice/). It is helpful because it provides a safe space to verify the assumptions and mental models; if there are reliable systems, and people got used to it, it will uncover potential risks in a real-life scenario (a real outage). Having these insights and experiences firsthand, people can challenge their mental models, and the organisation can provide support to mitigate the risks (think about training programs and adjust processes that are not useful, that only generate hindrance).

In the aftermath of the chaos experiments, and as part of the retrospectives, I tend to use the [Maturity Mapping](https://maturitymapping.com/), a variant of Wardley Maps that blends *Meaning*, *Material* and *Competence* (more on the concepts and the why [here](https://maturitymapping.com/2020/02/17/why-mapping-maturity/)). Enhancing the initial Wardley Maps with the result of the chaos experiments allows people to discuss the delta; as delta, I'm referring to the landscape's mental models and the result of the chaos experiments. Having the delta in a map, namely a Maturity Map, captures the different perspectives in a sociotechnical system, and has the benefit to discuss the agency of teams and purpose of teams, on top of the different mental models. As a CTO, I can support the organisation with the proper training, facilitation, coaching and mentoring, since we have a common ground. People can also challenge me to improve since my own behaviour and mental models influence the sociotechnical system; I can look for training, coaching, and mentoring to close the gap.

### In summary

Today, in a world that moves faster than we ever experienced, where we are not fully aware of all the connections (it is a complex challenge, beyond our ability to have accurate mental models), it is paramount that organisations are empowered to keep their options open. Also, before executing a strategy, we have a body of knowledge that allows us to test and verify the strategy's direction, minimise the impact, and avoid sunken costs fallacies, that can have disastrous results (in the extreme, a company can fall).

I used these practices, and I'm still learning :) For the challenges that I faced, those practices were able to deliver the expected results. However, there is a big world out there, and I'm interested in your experiences in this field. How do you recover and avoid the reliability trap?
