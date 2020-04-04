---
layout: post
title: Code development improvement with JetBrains UpSource (configuration and first
  impressions)
date: 2017-01-03 14:45:55.000000000 +01:00
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
- CentOS 7
- Continuous Improvement
- Continuous Innovation
- JetBrains
- Linux
- UpSource
- VCS
- Visual Studio
meta:
  publicize_google_plus_url: https://plus.google.com/105879670784970671735/posts/hXtFuYtRYmG
  _rest_api_published: '1'
  _rest_api_client_id: "-1"
  _publicize_job_id: '359848196'
  _publicize_done_15567246: '1'
  _wpas_done_15420870: '1'
  _publicize_done_external: a:2:{s:7:"twitter";a:1:{i:15487188;s:56:"https://twitter.com/joaoasrosa/status/816294538348298240";}s:8:"facebook";a:1:{i:15487197;s:38:"https://facebook.com/10155122486288287";}}
  _publicize_done_15638091: '1'
  _wpas_done_15487188: '1'
  publicize_twitter_user: joaoasrosa
  publicize_linkedin_url: https://www.linkedin.com/updates?discuss=&scope=27794317&stype=M&topic=6222060230943997952&type=U&a=mlMF
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
permalink: "/2017/01/03/code-development-improvement-with-jetbrains-upsource-configuration-and-first-impressions/"
comments: true
---
We should seek excellence in our jobs, doesn't matter our line of work. As professionals, we should always aim to improve the quality of our outputs, either it is customer satisfaction, code quality or just faster builds and deployments.

As any developer knows, working with a Version Control System (VCS) is great, but it has some pain points. As an example, if you are working in a product framework and you have lots of branches, it's complicated to do cross-branch searches with parameters like commit comments, authors and time. Plus we have a strict rule of code reviews (what we call the 4 eyes rule) to assess the code standards and the implementation itself. The code review comments are on our ticket system, disconnected from the VCS (I know there are integrated systems, but for business reasons the products do not interact as we like).

To close this gap, improving the developers' performance, we did research for useful tools that can help us. The frontrunner was [UpSource](https://www.jetbrains.com/upsource/) from JetBrains. UpSource supports most of the VCS, giving some cool visualisations, allowing us to do the code reviews and last but not the least provide us with a full range of searches over the code branches.

Before buying the license, we set up the free version of UpSource, and using Continuous Improvements techniques we start an experiment with of our development teams.

To configure UpSource (version 3.5.3597) we:

*   Read the [pre-requisites](https://www.jetbrains.com/help/upsource/3.5/prerequisites.html)
*   Spin up a VM with CentOS 7
*   Install CentOS 7

In the bash command line for the VM we:

*   Update all packages  
    `yum -y update`
*   Install net-tools  
    `yum install net-tools`
*   Install wget  
    `yum install wget`
*   Install unzip  
    `yum install unzip`
*   Download UpSource  
    `wget https://download.jetbrains.com/upsource/upsource-3.5.3597.zip`
*   Unzip it  
    `unzip upsource-3.5.3597.zip -d /usr/local`
*   Set the Linux configuration per [UpSource recommendations](https://www.jetbrains.com/help/upsource/3.5/things-to-configure-before-starting-upsource.html) (using vi in my case)
*   Restart the machine to enforce the changes  
    `shutdown -r now`
*   Set up the machine name to access it using the FQDN  
    `hostnameclt set-hostname my_machine_name`
*   Open the firewall port 8080  
    `firewall-cmd --zone=public --add-port=8080/tcp --permanent`  
    `firewall-cmd --reload`
*   Start UpSource  
    `/usr/local/upsource-3.5.3597/bin/upsource.sh start`

Using a browser we:

*   Navigate to http://my\_machine\_name:8080
*   Login as admin
*   Change the settings to use our Active Directory Domain as authentication provider
    *   Navigate to the Hub
    *   Under the Access Management, navigate to Auth Modules
    *   Click in Add Module and select Active Directory
    *   Fill all the input fields with the Active Directory Domain information
    *   Click in Create Module
*   Configure the e-mail provider
    *   Navigate to the Hub
    *   Under the Server Settings, navigate to System Settings
    *   Enable the Email notifications and fill all the input fields for the e-mail settings
    *   Test an email to make sure the configuration is correct
*   Configure the UpSource project to analyse our branches

And at this point, we hit a roadblock... The certificate use by the VCS is self-signed. To fix it, we applied the following recipe:

*   Get the self-signed certificate
*   Upload it to the UpSource machine
*   Following the [instructions](https://upsource-support.jetbrains.com/hc/en-us/articles/206545609-Using-a-self-signed-certificate-to-connect-to-a-VCS-server) provided by JetBrains support

And UpSource started to get all the information of the configured branches. :)

As a security measure, we enabled HTTPS following these [instructions](https://www.jetbrains.com/help/upsource/2.0/proxy_configuration.html). We close the shop, go home, take a good rest and start using it in the next day, using the rules agreed between the teams' technical leads.

After a week of usage, we start to see the benefits. We can search the code and the reviews in a faster way, leveraging the index system of UpSource. Plus we have visualisations that help us to identify what are the commits without reviews. In one particular situation, we found one optimisation broke our verifications in one of the plugins. Due to the search and comparison capabilities of UpSource, we cross-reference between different branches, identifying the bug and fixing it in a matter of minutes. If we use the tools provided by the VCS it will take a couple of hours to do the same job.

Our plan is to keep the experience with the team, refining the development process, since we change the way of doing code reviews. So far, we like the tool, and we are looking for the integration with [Visual Studio](https://youtrack.jetbrains.com/issue/UP-4138). After we agree and settle on the process, we will roll out to all the development teams within the company.
