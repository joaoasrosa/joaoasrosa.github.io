---
title: "Mental models: reflection on AWS outage"
date: 2021-01-09 00:00:00.000000000 +02:00
type: post
parent_id: '0'
published: false
password: ''
status: draft
permalink: "/2021/01/09/mental-models-reflection-on-aws-outage/"
comments: true
categories:
- Sociotechnical systems
tags:
- Autonomy
- Agency
- Team
- Chaos Engineering
- Management
excerpt: My reflection on the recent AWS outage (November 2020). Rather than focus on the technical aspects, and how technical dependencies can be managed, I will deep dive into social aspects; namely the mental models, and how they play in a sociotechnical system that is under stress. I will share my experiences in how to escape from the reliability trap
---

In November 2020 AWS had a major outage, which started with their Kinesis service, having a cascading failure over several services. There are several analysis of the outage, including the [official note](https://aws.amazon.com/message/11201/) from AWS. This blog post is a refletion on the outage, but rather focus on the technical aspects, I will deep dive into the social ones, namely mental models.

### Pre-refection, what is a mental model?

I will borrow two definitions for the mental models; the first one from Kenneth Craik:

> If the organism carries a "small-scale model" of external reality and of its own possible actions within its head, it is able to try out various alternatives, conclude which is the best of them, react to future situations before they arise, utilise the knowledge of past events in dealing with the present and future, and in every way to react in a much fuller, safer, and more competent manner to the emergencies which face it.

And the second one from Jay Wright Forrester, where he defines general mental models:

> The image of the world around us, which we carry in our head, is just a model. Nobody in his head imagines all the world, government or country. He has only selected concepts, and relationships between them, and uses those to represent the real system.

I can say that a *mental model* is a representation of concepts and their relationships, which help us to reason about a problem/challenge/whatever needs meantl capacity. It is influenced by our bias, past experiences, knwonledge and information. We use theses models to try to anticipate future events, and it shapes our behaviour. Our mental moels are not static, they evolve, although most of the times we are not aware of it. Note that I'm not a specialist in behavioral or cognitive sciense, and there is more behind it, but for now we can stick with these definitions and my own spin.

### My reflection

On the [AWS official note](https://aws.amazon.com/message/11201/), towards the end of the message, it states:

> Outside of the service issues, we experienced some delays in communicating service status to customers during the early part of this event. We have two ways of communicating during operational events – the Service Health Dashboard, which is our public dashboard to alert all customers of broad operational issues, and the Personal Health Dashboard, which we use to communicate directly with impacted customers. With an event such as this one, we typically post to the Service Health Dashboard. During the early part of this event, we were unable to update the Service Health Dashboard because the tool we use to post these updates itself uses Cognito, which was impacted by this event. We have a back-up means of updating the Service Health Dashboard that has minimal service dependencies. While this worked as expected, we encountered several delays during the earlier part of the event in posting to the Service Health Dashboard with this tool, as it is a more manual and less familiar tool for our support operators. To ensure customers were getting timely updates, the support team used the Personal Health Dashboard to notify impacted customers if they were impacted by the service issues. We also posted a global banner summary on the Service Health Dashboard to ensure customers had broad visibility into the event. During the remainder of event, we continued using a combination of the Service Health Dashboard, both with global banner summaries and service specific details, while also continuing to update impacted customers via Personal Health Dashboard. Going forward, we have changed our support training to ensure that our support engineers are regularly trained on the backup tool for posting to the Service Health Dashboard.

I was draw to this paragraph, and it is the reason for this blog post; mental models and the ripple effects on a sociotechnical system. As stated in the paragraph, AWS service operators have a backup procedure, where they can update the Service Health Dashboard. I notice the delays, where the public available information was reporting that everything was fine, but services running on top of the AWS cloud where down. And the well known [DownDetector](https://downdetector.com/) was reporting the outage.

My assumption is that the AWS are stable (actual top of the line, and it is a *fact*), and people got used to the reliability, that they don't factor in their mental models the secondary processes during an outage (this is my *assumption*). From my experience in our industry, we don't test the incident procedures (whatever the type of incident); we still have a road to learn from other industries, where they mature the practices to decrease the risks during an outage. I felt into this trap, and saw my peers do the same (this is the start of my *reflection*).

### How to escape of the reliability trap?