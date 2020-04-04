---
layout: post
title: Why Integration Tests won't save you... or your software
date: 2019-08-13 14:05:44.000000000 +02:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Code Development
- Continuous Deployment
- Continuous Integration
tags:
- CI/CD
- Contract Testing
- Health Testing
- Integration Testing
- Quality
meta:
  _wpcom_is_markdown: '1'
  _thumbnail_id: '1930'
  _publicize_done_external: a:1:{s:7:"twitter";a:1:{i:15487188;s:57:"https://twitter.com/joaoasrosa/status/1161643751011422210";}}
  _publicize_job_id: '34076424460'
  timeline_notification: '1565792425'
  _publicize_done_15638091: '1'
  _wpas_done_15487188: '1'
  publicize_twitter_user: joaoasrosa
author:
  login: joaoasrosa
  email: joaoasrosa@gmail.com
  display_name: João Rosa
  first_name: ''
  last_name: ''
permalink: "/2019/08/13/why-integration-tests-wont-save-you-or-your-software/"
excerpt: Did the title tease you? Great, job is done! Today I will tell you my story about Integration Tests; it came after another knowledge share lunch with my pal Kenny.
comments: true
---
Did the title tease you? Great, job is done! Today I will tell you my story about Integration Tests; it came after another knowledge share lunch with my pal [Kenny](https://twitter.com/kenny_baas).

By [this](https://en.m.wikipedia.org/wiki/Integration_testing) definition an Integration Test is

> "(...) the phase in software testing in which individual software modules are combined and tested as a group. Integration testing is conducted to evaluate the compliance of a system or component with specified functional requirements. It occurs after unit testing and before validation testing. Integration testing takes as its input modules  that have been unit tested, groups them in larger aggregates, applies tests defined in an integration test plan to those aggregates, and delivers as its output the integrated system ready for system testing.

Sounds pretty waterfall, right? It is! also, the implementation approaches that I observed creates huge dependencies between teams, coupling the software release process.

![Two different fluids integrating in each other](/images/assets/adrien-ledoux-mbhuekka5wm-unsplash.jpg)  

{:.image-caption}
*Photo by [Adrien Ledoux](https://unsplash.com/@adrienl?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/integration-tests?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)*

Everything coupled, a tale of Integration Tests
-----------------------------------------------

A sound CI/CD pipeline has several steps; which includes validating, build, test, pack and release the software. I won't go into details, given the necessary steps will vary, given languages, frameworks, platforms and release strategies.

However (always a but), more often than I would like, teams use Integration Tests to (1) assert if the dependencies of software are up and running (software dependencies), and (2) verify if user journeys that crossed multiple domain boundaries (cross-team dependencies).

From these reasons, I observed coupling between different systems, teams and domains. Moreover, it is painful to watch the development and release process… The time and effort put in the process and the blurred line between the automated process and manual coordination…

So, what is the alternative do deliver quality software?
--------------------------------------------------------

Integration Tests are a _symptom_, not the _cause_ of the systems and teams coupling! Moreover, before going wild and delete all the Integration Tests from your codebase, I will present **my alternative** to it.

The first testing technique that I use is Contract Testing. Contract Testing is

> "(...) a way to ensure that services (such as an API provider and a client) can communicate with each other.

This definition is provided by [Pact](https://docs.pact.io/), a Contract Testing tool for HTTP based APIs. **Disclaimer**: Contract Testing can be applied to any API, and this blog post is not focused on a (this) tool. I just like their definition! :)

The contract tests run before deploying to an environment, and they are validated against a broker. It means that I will verify if all my assumptions about the contracts with my direct dependencies are correct. If not, I will stop the CI/CD process.

However, this doesn't solve all the problems. Contract Testing does not provide an answer to the question: Are my dependencies up and running?

To answer to that question, I implement a second technique, Health Testing. Health Testing is

> "a way of providing feedback about the direct dependencies of an application in realtime.

This definition is mine. It means that an application can report (via push or pull mechanisms) the status and metrics of the direct dependencies. When aggregated at the application level, it can have a traffic light pattern, with Green, Yellow and Red. Combined with a proper monitoring tool, we can have realtime visibility of the status of the dependencies.

This second technique solves an important trap of Integration Tests. Integration Tests provide dependencies feedback at **one point in time**. Health Testing (if properly implemented) **continuously** provide the necessary feedback.

Combining these two techniques has some interesting side effects. First of all, it reduces the executing time of the CI/CD pipeline when compared to the executing times of Integration Tests, given that fewer components are involved. Secondly, Integration Tests tend to be brittle, and it can reduce the number of false positives, increasing team productivity.  
Last but not least, it pushes teams to discuss the boundaries of their systems and their domains. It increases awareness of the context were teams operate, and leads to mean full conversations between everyone involved in the software development process (yes, I'm saying IT and Business).

### And what are your thoughts?

Share with me, in the comments session or via [Twitter](https://twitter.com/joaoasrosa) (DM messages are open).
