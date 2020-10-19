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
permalink: "/2016/09/14/update-project-json-version-number-in-appveyor/"
comments: true
excerpt: Today was a debut using GitHub Gist. In one of my GitHub projects, I need a close integration between the Continuous Integration tool (in this case AppVeyor) and my .NET Core project, specifically in how to update the version of the DLL based on the version in AppVeyor?
---
Today was a debut using [GitHub Gist](https://help.github.com/articles/about-gists/). In one of my GitHub projects, I need a close integration between the Continuous Integration tool (in this case [AppVeyor](https://www.appveyor.com/)) and my .NET Core project, specifically in how to update the version of the DLL based on the version in AppVeyor?

To sort out this, I use my Powershell ninja skills to write the script:

https://gist.github.com/joaoasrosa/8b3a9681c6153f9abed94af7089b222a

And integrate it with the appveyor.yml before_build event! Simple and do the job!
