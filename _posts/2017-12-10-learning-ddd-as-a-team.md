---
layout: post
title: Learning DDD as a team
date: 2017-12-10 22:04:09.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Domain Driven Design
tags:
- Agile
- Continuous Improvement
- DDD
- Team
meta:
  _wpas_skip_15487191: '1'
  _publicize_job_id: '13639328010'
  _wpas_skip_15487188: '1'
  _wpas_skip_15420870: '1'
  _rest_api_published: '1'
  _rest_api_client_id: "-1"
  timeline_notification: '1516050341'
  _wpcom_is_markdown: '1'
author:
  login: joaoasrosa
  email: joaoasrosa@gmail.com
  display_name: João Rosa
  first_name: ''
  last_name: ''
permalink: "/2017/12/10/learning-ddd-as-a-team/"
comments: true
featured_image: /images/left-panel/blog.webp
---
A few sprints ago my team and I decided to invest heavily in Domain Driven Desing. We already started to develop the new microservices in a DDD fashion, with our domain as the central component. However, we wanted to formalize it and move the old microservices to this new paradigm.

During this period we used several tools and techniques, to aid us to figure out what was the best approach for us. And we are Agile; _**probe, experiment and evaluate**_. If it doesn’t work, learn from it and move on!

Activities as a development team
--------------------------------

### Whiteboard sessions

As a developer, one of the best tools is a pen and paper. As a development team, nothing better than a whiteboard and markers. Before or during the development of a component we gather the team around our whiteboard, and we scatch potential solutions for the problems in hand. It helped the team to focus, and reach a common understanding, making the software implementation easier.

### Coffee & lunch breaks

We have around 150 software developers, it’s common to take a coffee or have lunch together. Most of the times, during our chats, it drifts to the problems that we are facing. It’s a great informal platform to share our ideas, struggles, and solutions for the problems. As [Kevin Boles](https://twitter.com/thesqlguru) once [wrote](https://www.google.nl/url?sa=t&rct=j&q=&esrc=s&source=web&cd=4&ved=0ahUKEwiH_62F8v_XAhVRIewKHZk9Cb4QFgg5MAM&url=http%3A%2F%2Fwww.pass.org%2FDownloadFile.aspx%3FFile%3D76767a5e&usg=AOvVaw1sgE1vPjWc_tr5BVetjiYB): “Smart people learn from their mistakes. Wise peoples learn from other people mistakes”.

### Craftsmanship sessions

Here at Coolblue, we host private craftsmanship sessions. During the meetings, we have the opportunity to work on a particular problem, sharing our thoughts and discuss possible solutions. It’s more formalized than the coffee & lunch breaks.

### EventStorming sessions

Another activity used by our team is Event Storming sessions. We use this activity to help us to match the new business requirements and all the technical debt that we need to catch. This is an opportunity to optimize the work to be carried, minimizing the creative tension between the developers and the business. It also raises the business awareness for software risks, since our domain has goals to help the company grown; to achieve the goals, we need to minimize the risks or acknowledge them. Transparency is the keyword!

Lessons Learned
---------------

### Language definition

One of the challenges is to set the correct language, terms, and definitions. Although we are developing software, we are doing it to achieve a business goal, and given that, the software should be read like a book. Also, the software naming should match the business terms, making everyone lives easier. Please raise the hand, who never found variables names that **_don’t_** match the business terms?

It’s paramount for the development team to speak the same domain language; it will pay the dividends in the future once, for instance, a refactor is needed, or even when the software goes into maintenance mode.

### Boundaries

Any good resource in this space points to the bounded context as the central pattern for the DDD. When we are building software for a new domain, discovering the bounded context is the first challenge that a development team faces.

However, in my experience, in a growing company, the development team needs to be actively looking for _**changes**_ in the bounded context, since the software should serve the business, not in the other way around. This is a massive challenge, not only requires the ability to have useful metrics in place (especially business KPIs) but also to keep asking if the software continues to have the same positive effect within the user base.

Value to the Business
---------------------

### Close the gap between development and business

It’s important to keep the development teams as close as possible to the business. Applying DDD techniques, it helps the development team to bring the domain concepts to the center of the software development, closing the gap between the development and the business.

### Use of the same language

Once the developers start to use the same domain language as the business, it decreases the time in the discussions between the business and development, since it is not needed to translate technical terms to business terms.

### Helps the Product Owner to make informed decisions

All these activities end with valuable insights to the Product Owner. She/He can prioritize the work, based on the team’s feedback and the business necessities. It also reduces the creative tension between the developers, trying to improve the speed of the features delivery.

Value to the Development Team
-----------------------------

### Long-term sustainability

Software long-term sustainability is essential. In other words, creating and deliver software at a high pace, minimizing the technical debt. During my career, I found the DDD concepts and techniques more useful to increase the long-term sustainability of the software, since it uses the _**same domain language**_ as the business. It helps the development teams to add new features to an existent component since it matches the business processes.

### Vision and goals

The activities carried by the development team help to state the vision and goals for the upcoming period. Although its impossible to create a roadmap six-months ahead, due to quick company growth, it empowers the team to help the business to achieve our (domain) goals.

### Removes ambiguity

Sometimes we (developers) make assumptions that turn out wrong. Even in an Agile environment, whereby the feedback cycle is the centerpiece, and we work in an iterative process, we prefer to get it right since the beginning. Since we start to focus on DDD, I observed, the team began to remove the ambiguity during the software development process, thus increasing the _**speed and quality**_ of the deliveries.

### Clear dependencies & Visibility

We work in one of the biggest e-commerce companies in the Benelux area, and it’s near impossible for a team to _**own all the software**_ to cover a business process. During this time we started to improve our documentation, focusing on the boundaries of the software that my team is responsible. It created a clear image of the upstream and downstream dependencies. It helped in the discussions with our peers accountable for the upstream dependencies, whereby we presented documentation in the same (technical) language. Using these artifacts, we are able to discuss the importance of the upstream dependencies, since it raises visibility and awareness for the inter-dependencies between the teams (and software systems).

It also raises the visibility since we hanged in our glass walls the software diagrams of our system. As a learning opportunity, we choose to document our software using the [C4 model](https://c4model.com/) from [Simon Brown](https://twitter.com/simonbrown).
