---
layout: post
title: How to solve Magento 2 upgrade errors
date: 2018-03-11 12:54:21.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Continuous Deployment
- Continuous Integration
- Magento 2
- OSS
tags:
- Linux
- Magento2
meta:
  _wpcom_is_markdown: '1'
  _rest_api_published: '1'
  _rest_api_client_id: "-1"
  _publicize_job_id: '15609200966'
  timeline_notification: '1520769261'
  publicize_google_plus_url: https://plus.google.com/105879670784970671735/posts/8btbv89ZeT7
  _publicize_done_15567246: '1'
  _wpas_done_15420870: '1'
  _publicize_done_external: a:1:{s:7:"twitter";a:1:{i:15487188;s:56:"https://twitter.com/joaoasrosa/status/972802946042867713";}}
  _publicize_done_15638091: '1'
  _wpas_done_15487188: '1'
  publicize_twitter_user: joaoasrosa
  publicize_linkedin_url: https://www.linkedin.com/updates?discuss=&scope=27794317&stype=M&topic=6378568641138421760&type=U&a=71My
  _publicize_done_15638097: '1'
  _wpas_done_15487191: '1'
  _oembed_a2fb2f0e69076690c87567fab3364dd7: '<div class="embed-twitter"><blockquote
    class="twitter-tweet" data-width="500" data-dnt="true"><p lang="en" dir="ltr">If
    you want to tweet or blog about how serverless actually runs on servers, let me
    save you some time: Nobody thinks that serverless doesn&#39;t run on servers.
    Nobody. You&#39;re just taking cheap shots at a catchy name.</p>&mdash; Mathias
    Verraes (@mathiasverraes) <a href="https://twitter.com/mathiasverraes/status/995317295072382976?ref_src=twsrc%5Etfw">May
    12, 2018</a></blockquote><script async src="https://platform.twitter.com/widgets.js"
    charset="utf-8"></script></div>'
  _oembed_time_a2fb2f0e69076690c87567fab3364dd7: '1526479963'
author:
  login: joaoasrosa
  email: joaoasrosa@gmail.com
  display_name: João Rosa
  first_name: ''
  last_name: ''
permalink: "/2018/03/11/how-to-solve-magento-2-upgrade-errors/"
---
Magento 2 is the leading Open Source Software for e-commerce, with a vibrant community and proper product documentation.

The development team releases bug fixes and new features in a regular cadence, given support to security threats, market trends, amongst others.

Environment
-----------

The environment is [deployed in AWS](https://anotherlookontech.wordpress.com/2018/01/14/migrate-magento-from-on-premises-to-the-cloud/), using an immutable infrastructure. It allows us to deploy several development/testing environments where we can develop the scripts to automate the upgrade process for our CI/CD pipeline. Also, it is our workbench for testing UI changes, new plugins, amongst others.

Upgrading
---------

However, trying to upgrade to the latest version (at the moment of writing this post is 2.2.3), using the [official documentation](http://devdocs.magento.com/guides/v2.2/comp-mgr/cli/cli-upgrade.html), we receive the following error:

![magento2_upgrade_004](/images/assets/magento2_upgrade_004.png)

{:.image-caption}
*Magento 2 upgrade command - failed to open stream error*

This is annoying. So far, we had reliable platform upgrades. Using my developer hat, we followed the error. A file was missing in the `magento 2 installation path\setup\` folder.

Doing a quick search with the `ls` command, we had the folder structure:

![magento2_upgrade_003](/images/assets/magento2_upgrade_003.png)

{:.image-caption}
*Magento 2 root folder - after the ls command*

The code never lies. The `setup`/ folder doesn't exist. It intrigued us, getting us to investigate why the folder wasn't there. We verified:

*   The [official GitHub repo](https://github.com/magento/magento2/tree/2.2). The `setup/` folder exists, and it has content
*   Download the official [Magento 2 Full Release](https://magento.com/tech-resources/download), inspecting the contents. Again, the `setup/` folder exists, and it has content
*   Deploy a new AWS development environment with the current infrastructure, inspecting the folder structure. The `setup/` folder **exists** in the current installation

![magento2_upgrade_001](/images/assets/magento2_upgrade_001.png)

{:.image-caption}
*Magento 2 root folder - current installation*

Given the information from our investigation, it seemed to point out to the PHP Composer, which doesn't deploy the `setup/` folder during the upgrade process. To prove it, we tried to upgrade the environment again, using the same commands:

![magento2_upgrade_002](/images/assets/magento2_upgrade_002.png)

{:.image-caption}
*Magento 2 composer - update command*

And we were able to reproduce the initial error. At least it is reproducible and supports our theory. :)

The (temporary) solution
------------------------

Since the PHP Composer package should contain (apart from the metadata file) the same files as  the downloadable Magento 2 installation package, we've tried to:

*   Follow the upgrade steps from the official guide **until step 6** (_Update the database schema and data_)
*   Download the Magento 2 installation package
*   Extract the `setup/` folder to the Magento 2 installation folder
*   Resume the Magento 2 upgrade process

And voilá, it finished the Magento 2 upgrade to the version 2.2.3. Happy days, we can do our testing on the new version of the shop, before promoting it to production.

This error had been reported to the Magento development team, however, they can't reproduce it. Nevertheless, we can use this workaround to upgrade our (your) shop.
