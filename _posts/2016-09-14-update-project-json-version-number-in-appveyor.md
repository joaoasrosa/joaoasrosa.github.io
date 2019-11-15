---
layout: post
title: Update project.json version number in AppVeyor
date: 2016-09-14 13:34:40.000000000 +02:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Continuous Integration
- OSS
tags:
- AppVeyor
- Gist
- GitHub
- PowerShell
meta:
  publicize_google_plus_url: https://plus.google.com/105879670784970671735/posts/LCszMFq8xq1
  _rest_api_published: '1'
  _rest_api_client_id: "-1"
  _publicize_job_id: '26817621406'
  _publicize_done_15567246: '1'
  _wpas_done_15420870: '1'
  _publicize_done_external: a:2:{s:7:"twitter";a:1:{i:15487188;s:56:"https://twitter.com/joaoasrosa/status/776051553715105794";}s:8:"facebook";a:1:{i:15487197;s:38:"https://facebook.com/10154730599578287";}}
  _publicize_done_15638091: '1'
  _wpas_done_15487188: '1'
  publicize_twitter_user: joaoasrosa
  publicize_linkedin_url: https://www.linkedin.com/updates?discuss=&scope=27794317&stype=M&topic=6181817245799325696&type=U&a=n_Id
  _publicize_done_15638097: '1'
  _wpas_done_15487191: '1'
  _publicize_done_15638104: '1'
  _wpas_done_15487197: '1'
author:
  login: joaoasrosa
  email: joaoasrosa@gmail.com
  display_name: João Rosa
  first_name: ''
  last_name: ''
permalink: "/2016/09/14/update-project-json-version-number-in-appveyor/"
---
Today was a debut using [GitHub Gist](https://help.github.com/articles/about-gists/). In one of my GitHub projects, I need a close integration between the Continuous Integration tool (in this case [AppVeyor](https://www.appveyor.com/)) and my .NET Core project, specifically in how to update the version of the DLL based on the version in AppVeyor?

To sort out this, I use my Powershell ninja skills to write the script:

https://gist.github.com/joaoasrosa/8b3a9681c6153f9abed94af7089b222a

And integrate it with the appveyor.yml before_build event! Simple and do the job!
