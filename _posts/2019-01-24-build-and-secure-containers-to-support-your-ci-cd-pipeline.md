---
layout: post
title: Build and secure containers to support your CI/CD pipeline
date: 2019-01-24 21:18:56.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Continuous Deployment
- Continuous Integration
- OSS
- Security
tags:
- CI/CD
- Docker
- Google Container Structure Tests
- Snyk
- Testing
meta:
  _wpcom_is_markdown: '1'
  _wpas_skip_15487188: '1'
  _wpas_skip_15487191: '1'
  _publicize_job_id: '26892149487'
  timeline_notification: '1548361141'
  publicize_google_plus_url: https://plus.google.com/105879670784970671735/posts/CYvb2rcQeNN
  _publicize_done_15567246: '1'
  _wpas_done_15420870: '1'
author:
  email: joaoasrosa@gmail.com
  display_name: João Rosa
  first_name: ''
  last_name: ''
permalink: "/2019/01/24/build-and-secure-containers-to-support-your-ci-cd-pipeline/"
---
There are 2 systems in any company that are critical: the payroll system, and the CI/CD system. Why? You may ask...  
If the payroll system doesn't work, people will leave the company and the company (may) face legal problems; the CI/CD system is the gateway to production. If it is down and there is a bug in production, it will affect your business; loss of revenue, loss of customers, loss of money, just to name a few.

Usually, I find these problems regarding the CI/CD tooling:

*   Poor Software Lifecycle Management, with outdated software, containing critical vulnerabilities
*   Ancient capabilities in the build agents. In extreme cases, frameworks and tools that are no longer supported by the vendors
*   Drifting agents. It means that teams had to do some sorcery to get the software build
*   Lack of proper isolation between different builds. It means that a build could access to another build files
*   Lead teams to upgrade or install a new framework
*   Outdated and strict rules mandated by a operations team. Usually from people that outdated heuristics on how software should be developed

To tackle these problems, I usually suggest the use of a SaaS solution where they shift the responsibility of maintaining and securing the tool to the vendor; also, I recommend to select a tool which supports containers where the software is built. It can address several of the issues, such as providing isolation and decreasing the lead time to provide new capabilities. Also, it allows teams to create their own containers, shifting the responsibilities of the platform team to the development teams. Using containers as computing unit, it allows for granular capabilities (comparing to the typical full flagged machine), having a cleaner environment based on specific needs.

As an added benefit, the platform team is no longer a constraint, since the development teams do not need to request new capabilities for the build/deploy agents. The platform team is responsible for a service provided to the organisation, and the service needs to be stable and secure. It is a paradigm and mindset shift for the typical operations team, which can become a platform team, offering outstanding services to the developers.

All boxes ticked! Or not...
---------------------------

The pivotal change is shifting the responsibilities of the platform team to the development teams. Well, this calls for a great life lesson from Ben Parker:

> "With great power, comes great responsibilities!

{:.image-caption}
*Ben Parker, Spider-Man*

Allowing the teams to build their own containers, who guarantees the security of the containers? Although it ticks some boxes, new challenges arose...

It's 0's and 1's
----------------

The platform team, who offers the service, is in the perfect spot to implement (dogfooding) a pipeline where the containers are tested and scanned for vulnerabilities. When everything passes, the container image is stored in the container registry, and it is continuously monitored. As CVE’s can be disclosed at any moment these images are constantly monitored. Using this approach, the platform team is in control of the CI/CD environment, and it is flexible enough for the development teams to deliver value quickly.

In the end, it's 0's and 1's. Also known as Infrastructure as Code, and like any piece of code, it should be built, tested, stored in a central artifact store and deployed.

Recapping (or the one image that explains it all)
-------------------------------------------------

![](/images/assets/recapping.png)  

{:.image-caption}
*Explaining the world in one image*

Putting all together, the pipeline can be described by the previous image. The code is in a git repository and a build agent uses an image from the container registry to kick the pipeline. Once the pipeline starts, it builds the code (another container image in this case), testing and scanning it. Finally, if all is sound and safe, it pushes the new image to the container registry. All of this using the typical [Trunk Based Development](https://trunkbaseddevelopment.com/), with Pull Requests to enforce the 4-eyes principle (traceability for audit purposes).

Amazing, another architecture diagram... And the implementation?
----------------------------------------------------------------

A possible implementation can be founded on this [open source project](https://github.com/joaoasrosa/packer-goss-docker). It uses free tools for open source projects, but there are other alternatives.

The implementation is simple and uses the following tools:

*   [GitHub](https://github.com) as the git repository
*   [Azure DevOps](https://azure.microsoft.com/en-us/services/devops/) as CI/CD server
*   [Dockerfile](https://docs.docker.com/engine/reference/builder/) describing the steps to create the container image
*   [Google Container Structure Tests](https://github.com/GoogleContainerTools/container-structure-test) as the test framework
*   [Snyk](https://snyk.io/) as the scanning and monitoring tool

The decisions behind the tooling were:

*   Use a testing framework that is language agnostic. Today, some testing frameworks use YAML to describe the expectations of the artifact, and it makes easy to learn when compared to a language-based testing framework. It is important for organisations where there are multiple programming languages
*   A scanning tool that can also monitor the artifacts. Given the nature of the disclosure of the CVE's, it is important to have a tool that automates and reports any new findings

Taking a closer look at the implementation you can see it in action:

*   Tests failing, TDD all the way (commit b6b0a6c): [https://dev.azure.com/joaoasrosa/joaoasrosa/_build/results?buildId=50](https://dev.azure.com/joaoasrosa/joaoasrosa/_build/results?buildId=50)
*   Scan failing (commit b92b058): [https://dev.azure.com/joaoasrosa/joaoasrosa/_build/results?buildId=51](https://dev.azure.com/joaoasrosa/joaoasrosa/_build/results?buildId=51)
*   Monitoring in place:

![](/images/assets/image-1.png)  

{:.image-caption}
*Report monitoring from 2019/01/24*

In conclusion...
----------------

The implementation empowers the development teams to create their own containers to be used in the build environments, without interfering with other teams. It also enables the platform team to be in control without constraint the development teams, and dictate the "holy rules" of "the platform". However, provides the correct level of security controls, since everything is automated, PR's are enforced, and it is possible to know exactly what and when it was used. It makes the auditors lives easier, and creates a safer environment!

If you have alternative implementations or ideas, feel free to shout! This implementation uses some tooling, and perhaps you have better alternatives. I will love to discuss it!
