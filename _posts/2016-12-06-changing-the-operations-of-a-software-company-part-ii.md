---
layout: post
title: Changing the operations of a Software Company – Part II
date: 2016-12-06 17:09:19.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Continuous Deployment
- Continuous Integration
tags:
- Deployment
- DevOps
- Octopus
permalink: "/2016/12/06/changing-the-operations-of-a-software-company-part-ii/"
comments: true
excerpt: In the previous post, I wrote about my experience changing the operations of a Software Company, improving the development process.
---
In the previous [post](https://joaorosa.io/2016/12/02/changing-the-operations-of-a-software-company-part-i/), I wrote about my experience changing the operations of a Software Company, improving the development process.

After we tackle this problem, we move to the next one: How can we bring the automation to our client installer?

To give some context, the software is installed on client premises, thus we have deployed a fair number of network, tiers and security configurations to met the customer requirements. When the software is metadata driven and has a Service Oriented Architecture (SOA), it's crucial to do the installation in the right way. Since it based on installation notes (sometimes with a dozen of pages), the operator will miss a step (we are all humans, and we get tired). And we know what that means... Everything will fall apart, a rollback needs to be applied to the environment, time is wasted, and ultimately the customer will be unhappy. Our first priority is the customer (as any business should focus), and we want to make sure that all the processes can run smoothly.

Using our experience with [Octopus Deploy](https://octopus.com/), we started to explore the [Offline Package Drop](http://docs.octopusdeploy.com/display/OD/Offline+Package+Drop) feature whereby the target environment doesn't need an agent installed, which is the perfect scenario for a deployment in client premises (since the client will operate using isolated networks, and we can't access to them for security reasons).

After the initial experiments, the stakeholders decided to support the project, and we design and implement a client installer on top of an Octopus Process. This allows:

*   Usage of the same internal process
*   More control over the installation steps, thus removing the human factor of the equation
*   Guarantee the steps run of the right order at the right time
*   The deployment process  is smooth since the customer only needs to start the installer application and follow the steps
*   Security is paramount since the customer will not share passwords with us (as an example). The application requires the customer to input the parameters that can't be shared, and the application leverages the [Calamari API](http://docs.octopusdeploy.com/display/OD/Calamari) (it's open source we can contribute to it) to replace it in the Octopus Project settings files
*   Reduce the installation time, since it is done in an automated fashion

Currently, we are rolling out the project internally, with one of the customers facing teams. Until now it had been a success, gathering feedback for further iterations (a software component is not static). Sooner it will be applied by the customer in a UAT environment and we will collect more metric statistics and feedback.

Happy customers, happy days! :)
