---
layout: post
title: Migrate Magento from on-premises to the cloud
date: 2018-01-14 19:56:42.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Cloud Computing
tags:
- AWS
- Magento
- Magento2
meta:
  _publicize_job_id: '13594271913'
  _rest_api_client_id: "-1"
  _rest_api_published: '1'
  timeline_notification: '1515956206'
  publicize_google_plus_url: https://plus.google.com/105879670784970671735/posts/R29dWKBD4Dq
  _publicize_done_external: a:1:{s:7:"twitter";a:1:{i:15487188;s:56:"https://twitter.com/joaoasrosa/status/952615509987680256";}}
  _wpcom_is_markdown: '1'
  _publicize_done_15567246: '1'
  _wpas_done_15420870: '1'
  _publicize_done_15638091: '1'
  _wpas_done_15487188: '1'
  publicize_twitter_user: joaoasrosa
  publicize_linkedin_url: https://www.linkedin.com/updates?discuss=&scope=27794317&stype=M&topic=6358381204122714112&type=U&a=XIJz
  _publicize_done_15638097: '1'
  _wpas_done_15487191: '1'
author:
  login: joaoasrosa
  email: joaoasrosa@gmail.com
  display_name: João Rosa
  first_name: ''
  last_name: ''
permalink: "/2018/01/14/migrate-magento-from-on-premises-to-the-cloud/"
comments: true
---
Last summer a good friend of mine challenged me to help him move his Magento webshop from an on-premises server to the cloud. Also, to upgrade the webshop to the newest version (Magento 2).

The starting point
------------------

The webshop is the online spot for a small streetwear Portuguese shop. The crew supporting the shop is 3 persons, and the online channel is extremely important to the growth.

Select a cloud provider
-----------------------

![Clouds. Clouds everywhere!](/images/assets/gettyimages-482252-001-570a81d93df78c7d9edc0d78.jpg)

{:.image-caption}
*Ryan Beyer, The Image Bank, Getty Images*

The cloud provider offer is huge. We've put some effort into the investigation of the right cloud provider for us. The key points are:

*   Maturity. We need a mature cloud platform, and at this moment there are a few providers ticking this box
*   The range of services. The plan is to grow, and with that, we need a cloud provider with a variety of services that will allow the platform expansion
*   Quality of service. Given today we are used to the Google speed, and Apple minimalistic design, everyone expects the same level of service. We need a cloud provider with a proven record regarding the quality of service, allowing us to serve the audience with the quality they deserve
*   Price. A good bang for the buck, providing Return on Investment quickly
*   Community. Today we are interconnected, and we tend to share our ideas and engage in discussions. We need a cloud provider with an engaged community, whereby we can Q&A our ideas

We chose AWS, since it ticks all the boxes, having a good offer for the price tag. The community support is excellent, and we can find useful open source resources from the AWS folks (one of them is described in the next section).

Also, AWS offers a range of services that allow the webshop to grow sustainably. An example is the AWS Simple Email Service (SES), where it can be used as e-mail service to support the marketing campaigns.

Create a playground
-------------------

![Create a playground](/images/assets/5612_product_detail.jpeg)

{:.image-caption}
*Playmobil Playground*

In order to do a smooth migration, we've created a playground in AWS. We used the [Magento 2 Quick Start](https://docs.aws.amazon.com/quickstart/latest/magento/welcome.html) provided by AWS, to build the Magento 2 infrastructure. It allows us to reduce the time to market, and we were able to focus on the webshop content, rather than the infrastructure.

In our playground, we tested all the variations, namely themes, modules, and integrations. To name a few:

*   Composer. It is the PHP package manager, and most of the Magento 2 modules are distributed using it
*   Theme. We tested several themes, testing the variations in all the devices
*   Performance. We developed our own performance test suite. Given the data from the on-premises usage, we extrapolate the data tenfold and execute the performance tests to discover the resources needed to operate the webshop

Migration Plan
--------------

![Testing code in Production!](/images/assets/0hsfnsw.jpg)

{:.image-caption}
*Testing code in Production*

We created a migration plan, to mitigate potential issues when we triggered the migration. We planned to do a hot migration, e. g., put the old webshop in read-only mode until all traffic is redirected to the new webshop.

To develop this migration plan we read the [official documentation](http://devdocs.magento.com/guides/v2.0/migration/migration-plan.html), where Magento states the steps to migrate a webshop. Our migration plan was based on the official documentation, adding the possibility to recover the old webshop from backups, minimizing the data loss. We did the dry run 3 times before the final move, testing the backup recovering strategy. We wanted to be sure that we covered all the bases, and we were able to recover from backups.

Lessons learned
---------------

![Phil McKinney Blog](/images/assets/adobestock_87364193-760x507.jpeg)

{:.image-caption}
*Cycle to reach success: try, fail, try again, success*

From the migration we learned a few good lessons:

*   Create a playground. It is essential to test the webshop in a safe environment. We tested the UI, backup strategy, migration amongst others
*   Contribute to the Open Source Community. We used the Magento 2 Quick Start offered by AWS. It is available on [GitHub](https://github.com/aws-quickstart/quickstart-magento), and we made small contributions based on the tweaks that we did in our playground area
*   Test, test & test! We tested as much as we could, ranging from the UI, the UX, the modules to the performance. We based our testing targets on assumptions, but the assumptions were generated from data collected over the years
*   Create the migration plan. The Magento documentation is in a good shape and provides a solid direction. We used it to our migration plan
*   Rehearsal the migration. To mitigate the risks we rehearsal the migration several times, learning the pitfalls and potential issues after the data is migrated to the new platform
*   Have a backup plan. We had a plan B if the migration failed. We were able to revert to the old webshop if we needed to, having the capability to inspect and analyze the problem with the migration

This was the start of our journey. In the upcoming weeks we will post more implementation details, such as monitoring & logging, security measures, build & deployment pipelines, amongst others.
