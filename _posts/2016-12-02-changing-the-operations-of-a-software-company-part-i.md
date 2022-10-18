---
layout: post
title: Changing the operations of a Software Company - Part I
date: 2016-12-02 14:23:08.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Continuous Deployment
- Continuous Integration
tags:
- ".NET"
- Deployment
- DevOps
- Jenkins
- nant
- Octopus
- PowerShell
- Testing
permalink: "/2016/12/02/changing-the-operations-of-a-software-company-part-i/"
comments: true
---
Agile is great... and sometimes painful. Do not get me wrong, I love an Agile work environment when everyone is keen to "Try, Fail, Fix, Learn and Move On". For those ones that work in the software development space, we have more tasks than develop software.

One of the tasks, usually in Operations space. In the recent years we assist to the DevOps movement, however, most of the companies call themselves DevOps, "forgetting" the Ops bit, e. g., they continue to do Operations in an old fashion. Old fashion can be translated into doing manual deployments, minimal change control management, cumbersome release management, documentation everywhere, among others.

Due to the nature of a Distributed and Enterprise Software Application, the deployment of services and applications can be... well, complicated! Moreover when the software is metadata driven and allows multiple configurations that influence the product behaviour. On top of that, the software is deployed on customer premises, where the company do not have control over the deployment process, apart from (the obvious) installation notes.

Today we will focus on the first part of the problem: How can we improve the development process?

Let's put things in context: we already have a build automation using Jenkins, and using NAnt scripts the solution shell is built (the base web applications and services, with the default configuration). However, this is not enough, since it involves manual (and repetitive) tasks, such as overriding the configuration, or do the manual deployment. All this work, in an average case, can take up to a day for an experienced developer familiar with the operations.

Personally, I automate the tasks if I need to repeat it. And this scenario just bugs me... It's needed to be sorted out, ASAP!  After a bit of investigation, and given the technological constraints (Microsoft Stack, and Jenkins as CI), we decided to give a try to [Octopus Deploy](https://octopus.com/). Octopus Deploy is an Automated deployment tool for .NET, develop from a good crowd in Australia!

To test if Octopus was viable, we decide to apply to a new project, decreasing the risk involved in the implementation of a new tool. The goal of the project was to create a new component that will be part of the product core, and the development team has multiple environments and wants to build a fair number of automated testing around the component. To speed up the development we need to cut the deployment time (and manual tasks by the way).

In the inception of the project, we identify the environments, the development workflow and the required configurations. We set up an Octopus project to address and fulfil the requirements, and we start the project development. As any technology adoption, we did some mistakes during the configuration of the tool, but we are in an Agile environment where the turnover is quick. After a couple of sprints, we start to see (and fell) the benefits. :) They were:

*   End-to-end integration, since the commit to the source control, to the software deployment and automated testing
*   Quick and dirty testing in the environments, without the fear of broke something. Since the configurations are centralised in Octopus, the team can test different configuration variants to tune the component, and even break the environment.  If this happened it just redeploy the solution again
*   Promotion between environments with one click
*   Change management tracking, where all the configuration changes are logged
*   Increase the resilience of the release management process, where within an application it is possible to improve the process
*   Environment changes can be accommodated easily since it is a configuration, such as adding or removing machines from it

The test was a success, and it shown to other teams how we can optimise the development process without a huge disruption of the work environment. Currently, the process as been rollout to other projects, and everyone is happy with the new process. It requires upfront configuration and agreement on the workflow, but down the line, the team will save time with the repetitive and "trivial" tasks (how many times we arrive on morning and someone has broken the test environment?).

This experiment lead the company to address the second part of the problem: How can we bring the automation to our client installer?

The answer to the question will be answered in the next blog post. Stay tune!
