---
layout: post
title: Abstract from your CI. Use Cake!
date: 2017-10-18 08:43:38.000000000 +02:00
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
- ".NET"
- ".NET Core"
- Applications
- AppVeyor
- Cake
- Continuous Improvement
- Continuous Innovation
- DevOps
- Docker
- Jenkins
- Linux
- TravisCI
- Windows
meta:
  _wpcom_is_markdown: '1'
  _rest_api_published: '1'
  _rest_api_client_id: "-1"
  _publicize_job_id: '10449975814'
  publicize_google_plus_url: https://plus.google.com/105879670784970671735/posts/eacqRYCL518
  _publicize_done_15567246: '1'
  _wpas_done_15420870: '1'
  _publicize_done_external: a:1:{s:7:"twitter";a:1:{i:15487188;s:56:"https://twitter.com/joaoasrosa/status/920540881828155392";}}
  _publicize_done_15638091: '1'
  _wpas_done_15487188: '1'
  publicize_twitter_user: joaoasrosa
  publicize_linkedin_url: https://www.linkedin.com/updates?discuss=&scope=27794317&stype=M&topic=6326306575438876672&type=U&a=YlCS
  _publicize_done_15638097: '1'
  _wpas_done_15487191: '1'
author:
  login: joaoasrosa
  email: joaoasrosa@gmail.com
  display_name: João Rosa
  first_name: ''
  last_name: ''
permalink: "/2017/10/18/abstract-from-your-ci-use-cake/"
comments: true
---
Here at [Coolblue](https://www.coolblue.nl), we can choose our tools from a range of technologies. A while ago, our team started moving from Microsoft MSTest to xUnit.

Although the code change was fairly simple, the build pipeline was tied with the MSTest framework, ignoring the xUnit tests. Between the requests to the deployment team to alter the team's deployment pipelines, [Nathan](https://nathanjohnstone.wordpress.com/) challenged us to use Cake.

[](#what-is-cake)What is Cake?
------------------------------

![The Cake](/images/assets/68747470733a2f2f63646e2d696d6167652e6d79726563697065732e636f6d2f73697465732f64656661756c742f66696c65732f7265642d76656c7665742d63616b652d636f636f6e75742d637265616d2d6368656573652d66726f7374696e672d63726f702d736c2e6a7067)] 

{:.image-caption}
*Red Velvet cake; Photo: Jim Franco; Styling: Lydia Degaris Pursell; Original URL: [http://www.myrecipes.com/recipe/red-velvet-cake-1](http://www.myrecipes.com/recipe/red-velvet-cake-1)*

Although I'm a cake monster, "Cake (C# Make) is a cross-platform build automation system with a C# DSL to do things like compiling code, copy files/folders, running unit tests, compress files and build NuGet packages _(source)_."

Great, this is the tool that was missing, allowing us to abstract from our CI server, speeding our development (at the end that is Agile)!

[](#the-roller-coast)The roller-coaster
---------------------------------------

Cake allow us to build our project in many different ways with a syntax that is our bread and butter (C#). The platform is open-source, meaning that we can fix any bug, or [contribute](https://cakebuild.net/docs/contributing/contribution-guidelines) with a module to increase the ecosystem.

During my spare time, I started playing around with Cake in a [pet project](https://github.com/joaoasrosa/pullrequests-viewer). The pet project is built using .NET Core 2.0, and the ultimate goal was to build the project in [AppVeyor](https://www.appveyor.com/) and [TravisCI](https://travis-ci.org/). The build steps were:

1.  Ensure the non-solution folders exists (for example, artifacts folder)
2.  Clean the solution
3.  Restore the NuGet packages
4.  Apply the [Semantic Versioning](http://semver.org/)
5.  Build the solution
6.  Run the tests

As a bonus it should be able to:

1.  Package and push a NuGet package
2.  Create and push a Docker container

Cake offers support to all these steps, either out-of-the-box feature or as a module offered by the community.

The development was simplified since the operations to build & test my project was the same that the build server would execute. It avoids the old developer excuse "it works on my machine", _**since**_ the developer machine has the same software as the build server (during the development I face this problem with AppVeyor. The solution was published [here](https://anotherlookontech.wordpress.com/2017/08/10/build-a-net-core-2-0-application-in-appveyor/)).

[](#a-plethora-of-opportunities)A plethora of opportunities
-----------------------------------------------------------

![Opportunities everywhere!](/images/assets/68747470733a2f2f6d656469612e6d616b65616d656d652e6f72672f637265617465642f4f50504f5254554e49544945532d4f50504f5254554e49544945532d455645525957484552452d316b657575732e6a7067)]

{:.image-caption}
*Opportunities everywhere!*

This approach decreased the time to configure two different CI servers since it supports the executing of the scripts in Windows, Linux, and MacOS.

However, the opportunities are endless. In an enterprise environment, the software is a complex web of services and other moving parts; a team needs to be able to add a feature, test & ship it quickly; at the same time ensuring the business is working as expected, and more important, it doesn't introduce any regression bugs.

Using Cake, we can setup the script to deploy the necessary components on our development machines, running the tests to assure that everything works before we push our changes. This level of automation and abstraction also enables the developers to focus on delivering value (coding a new feature), rather than spending time configuring and deploying (manually) all the components to run the tests. Raise your hand who was in this situation. Yeah, every developer. 😉

[](#the-final-result)The final result
-------------------------------------

After a few hours around the script, both AppVeyor and TravisCI can execute it, predictably, as I do in my development environment. You can view a sample of the build logs [here](https://ci.appveyor.com/project/joaoasrosa/pullrequests-viewer) and [here](https://travis-ci.org/joaoasrosa/pullrequests-viewer).

Within our team, we started to move towards this direction. All the new projects are bootstrapped with a basic Cake script (Clean, Restore, Build, Test and Create NuGet package), but the team iteratively adapts it to our development needs. In the end, a development team should be proud of the software delivered, because it improves the business, but also the team has to be able to use its time in an effective way.

[](#and-for-other-languagesframeworks)And for other languages/frameworks?
-------------------------------------------------------------------------

The same concept exists in other languages/frameworks. As short list we can:

*   [CMake](https://cmake.org/)
*   [Gradle](https://gradle.org/)
*   [Fake](https://fake.build/)
*   [PSake](https://github.com/psake/psake)
*   [Rake](https://ruby.github.io/rake/)

Be aware that this is a _short list_. Out there exists other build platforms that allow you to abstract from your CI server.
