---
layout: post
title: When Cake meets NDepend
date: 2017-12-31 18:36:27.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Code Development
- Continuous Integration
- OSS
tags:
- ".NET"
- Agile
- Applications
- Cake
- Continuous Improvement
- Deployment
- Linux
- NDepend
- Windows
meta:
  _wpcom_is_markdown: '1'
  _wpas_skip_15487188: '1'
  _rest_api_published: '1'
  _rest_api_client_id: "-1"
  _publicize_job_id: '13069378625'
  publicize_google_plus_url: https://plus.google.com/105879670784970671735/posts/fDHYkxdSRqw
  _publicize_done_15567246: '1'
  _wpas_done_15420870: '1'
  publicize_linkedin_url: https://www.linkedin.com/updates?discuss=&scope=27794317&stype=M&topic=6353287575322521601&type=U&a=Hc-y
  _publicize_done_15638097: '1'
  _wpas_done_15487191: '1'
author:
  login: joaoasrosa
  email: joaoasrosa@gmail.com
  display_name: João Rosa
  first_name: ''
  last_name: ''
permalink: "/2017/12/31/when-cake-meets-ndepend/"
---
As a developer, I'm a big fan of automation. I can't create software where I need to push buttons and run manual scripts, to test & deploy it. To help me automate my software development tasks, I use [Cake](https://anotherlookontech.wordpress.com/2017/10/18/abstract-from-your-ci-use-cake/), "a cross platform build automation system with a C# DSL".

Working as a team, there are specific tasks to be carried, such as code reviews. A code review can be focused on architectural principles, naming conventions, test coverage, among others. To aid the code reviews, static code analyzers can be used, helping with the code analysis. Personally, I prefer [NDepend](https://anotherlookontech.wordpress.com/2017/10/01/ndepend-first-impressions-on-a-static-code-analyser/), because of the wide range of reports and insights about the codebase.

Joining the best of both worlds
-------------------------------

After a bit of research, I couldn't find a Cake Addin that interfaces NDepend. Given Cake is Open Source Software, why not create one?

![This-is-open-source](/images/assets/this-is-open-source.jpg)

{:.image-caption}
*This is open-source*

From this thought was created the [Cake NDepend Addin](https://github.com/joaoasrosa/cake-ndepend). It is a regular Cake Addin based on NDepend Console. Although NDepend offers integration with the major CI servers, the usage of Cake allows a layer of abstraction, avoiding the "works on my machine" principle. :)

A live example
--------------

[Eat your own dog food](https://en.wikipedia.org/wiki/Eating_your_own_dog_food). That's it, the Cake NDepend Addin uses itself to create a build artifact in each commit to GitHub. Inception?

![inception](/images/assets/inception.jpg)

{:.image-caption}
*Inception*

I want to report on every commit to my git repo. AppVeyor is instrumented to configure NDepend (the way to configure external software on each CI server is different) and uses the Cake NDepend Addin through the Cake script, producing the reports as artifacts. You can inspect an example [here](https://ci.appveyor.com/project/joaoasrosa/cake-ndepend/build/artifacts).

After download and uncompress the reports artifacts, it is something similar to this:

![Screen Shot 2017-12-31 at 17.45.02](/images/assets/screen-shot-2017-12-31-at-17-45-02.png)

{:.image-caption}
*An example*

The Holy Graal
--------------

The Holy Graal would be the integration of the report's metrics with a Pull Request. It would give visibility to the reviewers about the code quality trends, enabling the developers to be proactive to maintain the quality standards, rather than reactive.
